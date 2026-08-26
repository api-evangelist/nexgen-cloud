---
name: nexgen-cloud-provision-kubernetes-cluster
description: Provision a GPU Kubernetes cluster on Hyperstack via the API - pick a supported version and master flavor, create the cluster, add node groups, and manage nodes. Includes the constraints that are not obvious from the contract.
api: Hyperstack API
base_url: https://infrahub-api.nexgencloud.com/v1
auth: api_key header
generated: '2026-08-26'
method: generated
source: >-
  openapi/nexgen-cloud-hyperstack-openapi.json,
  https://docs.hyperstack.cloud/docs/kubernetes/kubernetes-guide
operations:
  - Get_Cluster_Versions
  - Get_Cluster_Master_Flavors
  - Fetch_cluster_name_availability
  - List_environments
  - Create_Cluster
  - Getting_Cluster_Detail
  - List_Clusters
  - List_cluster_events
  - Create_Node_Group
  - List_Node_Groups
  - Update_Node_Group
  - Delete_Node_Group
  - Create_Node
  - Get_Cluster_Nodes
  - Delete_Cluster_Node
  - Delete_Cluster_Nodes
  - Reconcile_cluster
  - Delete_cluster
---

# Provision a GPU Kubernetes cluster on Hyperstack

`api_key: <key>` header on every request. Base `https://infrahub-api.nexgencloud.com/v1`.

## Steps

1. **Check supported versions.** `Get_Cluster_Versions` (`GET /core/clusters/versions`).
   Supported versions change — the release notes have updated them more than once in 2026.
   **There are no in-place upgrades**; migrating versions means standing up a fresh cluster
   and moving workloads.
2. **Pick a master flavor.** `Get_Cluster_Master_Flavors`
   (`GET /core/clusters/master-flavors`). The master node is free; you pay for worker nodes.
3. **Reserve the name.** `Fetch_cluster_name_availability`
   (`GET /core/clusters/name-availability/{name}`). Skipping this is how you get
   `409 already_exist` — and, with no idempotency key on this API, an ambiguous retry.
4. **Pick the environment.** `List_environments` (`GET /core/environments`). The cluster is
   bound to that environment's region.
5. **Create.** `Create_Cluster` (`POST /core/clusters`). Returns immediately.
6. **Poll.** `Getting_Cluster_Detail` (`GET /core/clusters/{id}`) until it reports ready.
   `List_cluster_events` (`GET /core/clusters/{cluster_id}/events`) is the diagnostic path
   when it does not. **There are no callbacks for clusters** — only VMs and volumes emit
   webhook events, so polling is the only option here.
7. **Add worker capacity.** `Create_Node_Group`
   (`POST /core/clusters/{cluster_id}/node-groups`), then `Create_Node`
   (`POST /core/clusters/{cluster_id}/nodes`) or scale the group with `Update_Node_Group`
   (`PATCH /core/clusters/{cluster_id}/node-groups/{node_group_id}`).
8. **Inspect nodes.** `Get_Cluster_Nodes` (`GET /core/clusters/{cluster_id}/nodes`). Each
   node is backed by a real VM instance.
9. **Repair drift.** `Reconcile_cluster` (`POST /core/clusters/{cluster_id}/reconcile`).

## Constraints worth knowing before you build

- **Snapshots do not work on cluster VMs.** A VM that is part of a Kubernetes cluster cannot
  be snapshotted. Your backup strategy has to be workload-level, not machine-level.
- **Firewall rules are required for node communication.** See
  https://docs.hyperstack.cloud/docs/kubernetes/firewall-rules-k8s.
- **Persistent volumes need the CSI driver.** NexGen Cloud publishes an official CSI driver
  at github.com/NexGenCloud/csi-hyperstack, installed by Helm chart.
- **Deletion is permanent.** `Delete_cluster` (`DELETE /core/clusters/{id}`) has no reversal.
  The provider's own MCP tool for this requires explicit confirmation before firing.

## Rate limits and errors

500 req/min per source IP across all endpoints; `429` with no `Retry-After` and no
`RateLimit-*` headers. Back off exponentially from 1 second, 5 attempts maximum. Error
envelope is `{status, message, error_reason}`. Cluster IDs are region-scoped, so a wrong-region
read returns `404 not_found`.
