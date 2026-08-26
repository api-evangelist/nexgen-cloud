---
name: nexgen-cloud-deploy-gpu-vm
description: Deploy a GPU virtual machine on Hyperstack from scratch - pick a region and flavor with stock, create an environment, import an SSH key, create the VM, and poll it to ACTIVE.
api: Hyperstack API
base_url: https://infrahub-api.nexgencloud.com/v1
auth: api_key header
generated: '2026-08-26'
method: generated
source: openapi/nexgen-cloud-hyperstack-openapi.json + https://docs.hyperstack.cloud/docs/api-reference/quickstart
operations:
  - List_Regions
  - Get_GPU_stock
  - List_Flavors
  - List_Images
  - List_environments
  - Create_environment
  - List_key_pairs
  - Import_key_pair
  - Check_VM_name_availability
  - Calculate_resource_billing_rate
  - Create_Vms
  - Get_VM
  - Attach_callback_to_VM
---

# Deploy a GPU virtual machine on Hyperstack

Every request carries `api_key: <key>` as a header. No prefix, no Bearer. If the header is
missing or the key is revoked you get `401 unauthorized`.

## Before you start — this operation spends money

`Create_Vms` provisions billable hardware immediately, billed per minute. There is **no
idempotency key on this API**, so a request that times out and is retried can create a
second VM you are also billed for. Two mitigations, both real:

1. Call `Calculate_resource_billing_rate`
   (`GET /pricebook/calculate/resource/{resource_type}/{id}`) first to get the hourly rate
   for the flavor you are about to provision. That is the closest thing to a dry run.
2. Call `Check_VM_name_availability` (`GET /core/virtual-machines/name-availability/{name}`)
   and use a unique name. If a retry comes back `409 already_exist`, that is evidence the
   first call **succeeded** — go look it up with `List_Vms` before creating anything else.

## Steps

1. **Pick a region.** `List_Regions` (`GET /core/regions`). Values are `CANADA-1`,
   `NORWAY-1`, `US-1`. Everything below is region-scoped: an ID from one region returns
   `404 not_found` — not `403` — when read with a key working in another.
2. **Check stock before choosing hardware.** `Get_GPU_stock` (`GET /core/stocks`) returns
   real-time GPU availability per model and region. Choosing a flavor with no stock is the
   most common way this flow fails late instead of early.
3. **Choose a flavor.** `List_Flavors` (`GET /core/flavors`) for the GPU/CPU configurations
   available in that region.
4. **Choose an image.** `List_Images` (`GET /core/images`). Note this endpoint pages with
   `per_page`, not `pageSize` — see the pagination note below.
5. **Get or create an environment.** `List_environments` (`GET /core/environments`), and
   `Create_environment` (`POST /core/environments`) if none fits. An environment is bound
   to a region and is the container every VM, volume, firewall and keypair belongs to.
6. **Get or import an SSH key.** `List_key_pairs` (`GET /core/keypairs`); if you need a new
   one, `Import_key_pair` (`POST /core/keypairs`). Key material is validated server-side.
7. **Create the VM.** `Create_Vms` (`POST /core/virtual-machines`) with the environment,
   flavor, image and keypair. Returns immediately with the VM in `CREATING`.
8. **Poll to ACTIVE.** `Get_VM` (`GET /core/virtual-machines/{vm_id}`) until status is
   `ACTIVE`. The state sequence is `CREATING` → `BUILD` → `ACTIVE`, or `ERROR` on failure.
9. **Optional — stop polling.** `Attach_callback_to_VM`
   (`POST /core/virtual-machines/{vm_id}/attach-callback`) with `{"url": "https://..."}`
   and Hyperstack posts `InstanceCreationSuccess` / `InstanceCreationFailed` to you instead.
   Callbacks are per-resource, unsigned and not retried — see
   `asyncapi/nexgen-cloud-webhooks.yml` before you depend on them.

## Pagination, if you list anything

Three page-size parameter names on one API. `pageSize` for core resources
(`/core/virtual-machines`, `/core/volumes`, `/core/environments`), `per_page` for billing,
pricebook and `/core/images`, `page_size` for `/object-storage/*`. `page` starts at 1.
Read response fields by name, never by position — metadata precedes the data array on some
Core endpoints and follows it on others.

## Errors

Envelope is `{"status": false, "message": "...", "error_reason": "..."}`. `error_reason` is
occasionally absent (legacy 5xx, some pre-validation 400s) — treat missing as
`bad_request`. Full table in `errors/nexgen-cloud-problem-types.yml`, and Hyperstack also
runs an anonymous MCP server with a `lookup_error` tool at `https://docs.hyperstack.cloud/mcp`
that resolves a status code, `error_reason` or raw message to cause and fix at runtime.

## Rate limits

500 requests per minute **per source IP**, across all endpoints. Not per key, not per
account — every process behind one egress IP shares the budget. On exhaustion you get `429`
for the rest of the minute. **No `RateLimit-*` or `Retry-After` headers are returned**, so
pace yourself: exponential backoff from 1 second, doubling, stop after 5 attempts.

## Cleaning up

`Delete_VM` is permanent — no undelete, no retention window, and ephemeral disk data is
gone. If the state matters, `Create_Snapshot_for_VM` first. To stop paying without losing
the machine, hibernate rather than stop: see `nexgen-cloud-control-gpu-spend.md`.
