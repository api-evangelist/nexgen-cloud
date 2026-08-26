---
name: nexgen-cloud-control-gpu-spend
description: Read and control what a Hyperstack account is spending - query the pricebook before provisioning, read usage and last-day cost, and choose correctly between stop, hibernate and delete (they do not cost the same).
api: Hyperstack API
base_url: https://infrahub-api.nexgencloud.com/v1
auth: api_key header
generated: '2026-08-26'
method: generated
source: >-
  openapi/nexgen-cloud-hyperstack-openapi.json,
  https://docs.hyperstack.cloud/docs/billing/states-and-billing,
  https://docs.hyperstack.cloud/docs/virtual-machines/hibernation
operations:
  - Get_pricebook
  - Calculate_resource_billing_rate
  - Get_user_credit
  - Get_usage
  - Get_last_day_cost
  - List_Vms
  - Stop_VM
  - Start_VM
  - Hibernate_VM
  - Restore_VM_from_hibernation
  - Create_Snapshot_for_VM
  - Restore_snapshot
  - Delete_VM
---

# Control what a Hyperstack account is spending

## The one thing to get right

`SHUTOFF` still bills. This is the single most expensive misconception about this platform,
and it is stated plainly in the provider's own docs: when a VM is stopped its CPUs, GPUs,
RAM and local storage remain reserved for it, so **billing continues at the full rate**.
Stopping a GPU VM saves nothing.

| Action | Operation | What stops billing | What survives |
|---|---|---|---|
| Stop | `Stop_VM` (`GET /core/virtual-machines/{vm_id}/stop`) | nothing | everything |
| Hibernate | `Hibernate_VM` (`GET /core/virtual-machines/{vm_id}/hibernate`) | CPU, GPU, RAM, ephemeral storage | root disk (still billed), config |
| Delete | `Delete_VM` (`DELETE /core/virtual-machines/{vm_id}`) | everything | nothing |

Hibernate is the cost lever. Delete is the irreversible one.

## Price something before you buy it

- `Get_pricebook` (`GET /pricebook`) — resource pricing by flavor and region, straight from
  the API rather than the marketing page.
- `Calculate_resource_billing_rate`
  (`GET /pricebook/calculate/resource/{resource_type}/{id}`) — the hourly rate for one
  specific resource. Call this before `Create_Vms` and you can budget a run before you
  start it.

## Read what is being spent

- `Get_user_credit` (`GET /billing/user-credit/credit`) — current credit balance and the
  low-balance notification threshold.
- `Get_last_day_cost` (`GET /billing/billing/last-day-cost`) — previous day's cost breakdown.
- `Get_usage` (`GET /billing/billing/usage`) — usage records, filterable by environment and
  including deleted resources.
- `List_Vms` (`GET /core/virtual-machines`) — what is actually running. Anything in `ACTIVE`
  or `SHUTOFF` is costing money right now.

Billing endpoints page with `per_page`, not `pageSize`.

## Hibernating safely

`Hibernate_VM` deallocates the hardware and preserves the root disk. Two things bite:

1. **Ephemeral disk data is lost.** Copy anything you need to a Shared Storage Volume first.
2. **The public IP is released by default** and a *different* IP is assigned on restore.
   Pass `retain_ip=true` if the address matters. (Postpaid/premium accounts managing their
   own subnets are enrolled in an IP-retention policy by the Hyperstack team.)

Restore with `Restore_VM_from_hibernation`
(`GET /core/virtual-machines/{vm_id}/hibernate-restore`). The VM must be `HIBERNATED`, not
`HIBERNATING`. The provider states no expiry on a hibernated VM — but it also states no
guarantee, so do not treat "indefinite" as a commitment.

## Before deleting anything

`Delete_VM`, `Delete_volume`, `Delete_cluster` and `Delete_snapshot` are all permanent. No
undelete operation exists, there is no soft-delete state, and no retention window is
published anywhere. If you might want it back:

1. `Create_Snapshot_for_VM` (`POST /core/virtual-machines/{vm_id}/snapshots`). The VM is
   temporarily `SHUTOFF` during the snapshot and restarted afterwards. Max 100 GB, one at a
   time per VM, unsupported for cluster VMs and bootable-volume VMs.
2. Later, `Restore_snapshot` (`POST /core/snapshots/{id}/restore`).

Snapshots are themselves billed at Cloud-SSD rates, and no retention guarantee is published
for them either.

## Payments have no reverse

`Initiate_Payment` has no refund, void or reverse counterpart in the API. Treat it as final.
