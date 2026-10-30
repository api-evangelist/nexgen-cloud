# NexGen Cloud

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

NexGen Cloud Limited is a UK-headquartered AI cloud and GPU infrastructure provider. Its on-demand platform, Hyperstack, sells NVIDIA GPU and CPU virtual machines, managed Kubernetes clusters, block storage volumes, S3-compatible object storage and high-speed networking across three regions (CANADA-1, NORWAY-1, US-1), billed per minute. A second product, Hyperstack AI Studio, provides an OpenAI-compatible inference API over a catalog of third-party hosted text and image models, with playgrounds, system prompts, conversations and knowledge bases. The company also sells Secure Private Cloud, a single-tenant sovereign supercluster offering. Everything Hyperstack does in the console is available through a documented REST API at infrahub-api.nexgencloud.com, with official Python, Go, JavaScript and TypeScript SDKs, a Terraform provider, a Kubernetes CSI driver, a hosted read-only documentation MCP server and a self-hosted API MCP server.

**Areas:** Company · Cloud · GPU · Artificial Intelligence · Machine Learning · Infrastructure · Compute · Kubernetes · Storage · Inference · Virtual Machines · Sovereign AI

## NexGen Cloud on APIs.io

Everything profiled for NexGen Cloud is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/nexgen-cloud/](https://apis.io/providers/nexgen-cloud/)** — or go straight to one of the APIs or properties below.

### APIs (64)

- [NexGen Cloud Access Keys API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-access-keys-api/) — Access keys authenticate S3-compatible object storage operations. Each key has an access ID and a secret. Generate access keys via this API or in the…
- [NexGen Cloud Alive API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-alive-api/) — Service liveness check for the billing API. Use to confirm the billing service is reachable.
- [NexGen Cloud API Key API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-api-key-api/) — API keys authenticate requests to the Hyperstack API. Generate keys in the console; each key is server-side and scoped to a specific environment. Rotate…
- [NexGen Cloud Assigning Member Role API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-assigning-member-role-api/) — Bulk role assignments for organization members.
- [NexGen Cloud Auth API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-auth-api/) — Auth endpoints manage organization tokens, including changing the active organization on the current token. Use these endpoints when an account spans…
- [NexGen Cloud Auto Topup API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-auto-topup-api/) — The auto-topup API from NexGen Cloud — 2 operation(s) for auto-topup.
- [NexGen Cloud Base Models API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-base-models-api/) — Pre-trained foundation models available in AI Studio. These endpoints let you list available models, retrieve pricing, and fetch details for a specific base…
- [NexGen Cloud beta access API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-beta-access-api/) — Beta Access APIs
- [NexGen Cloud Billing API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-billing-api/) — Billing endpoints expose your account's billing history, current credit balance, payment history, and usage costs. Use these to reconcile spend, build…
- [NexGen Cloud Buckets API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-buckets-api/) — A bucket is an S3-compatible object storage container. Buckets are region-scoped and accessed via standard S3 SDKs once you have access keys. Use these…
- [NexGen Cloud Calculate API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-calculate-api/) — Calculate endpoints return billing-rate breakdowns for specific resources. Provide a resource type and ID to retrieve its hourly cost, including pre- and…
- [NexGen Cloud Callbacks API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-callbacks-api/) — Webhook callback registrations on virtual machines and volumes for state-change notifications.
- [NexGen Cloud cluster events API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-cluster-events-api/) — Cluster Event APIs
- [NexGen Cloud Clusters API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-clusters-api/) — A cluster is a managed Kubernetes cluster on Hyperstack, control plane + worker nodes preconfigured for GPU workloads. Clusters are region-scoped and can…
- [NexGen Cloud Compliance API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-compliance-api/) — Compliance APIs
- [NexGen Cloud Conversations API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-conversations-api/) — Conversation threads and message history for AI Studio chat sessions. These endpoints let you create conversations, send messages, retrieve message history,…
- [NexGen Cloud Credit API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-credit-api/) — Credit endpoints retrieve your account's current credit balance. Credits are consumed by resource usage and replenished via payments or vouchers.
- [NexGen Cloud Customer Contract API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-customer-contract-api/) — Customer contract endpoints retrieve negotiated pricing terms applied to your account. Contracts override standard pricebook rates for the resources they cover.
- [NexGen Cloud Dashboard API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-dashboard-api/) — Aggregate account-level metrics for the calling user, VM and resource counts, recent activity.
- [NexGen Cloud Deployment API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-deployment-api/) — Deployment endpoints manage scripts that run during virtual machine boot to install dependencies, configure services, or prepare GPU workloads. Attach a…
- [NexGen Cloud Email Opt In Out API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-email-opt-in-out-api/) — User email preference management
- [NexGen Cloud Environment API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-environment-api/) — An environment is a logical container for resources within a region. Use environments to separate development, staging, and production resources, or to…
- [NexGen Cloud FIP Exclusions API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-fip-exclusions-api/) — FIP exclusion endpoints manage which virtual machines are exempt from automatic floating-IP detachment policies.
- [NexGen Cloud Firewall Attachment API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-firewall-attachment-api/) — Firewall Attachments APIs
- [NexGen Cloud Firewalls API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-firewalls-api/) — A firewall is a set of inbound and outbound rules scoped to an environment. Attach a firewall to one or more virtual machines or Kubernetes clusters to…
- [NexGen Cloud Flavor API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-flavor-api/) — A flavor is a machine type, its CPU count, memory, and GPU configuration. Flavors are region-specific. List flavors before deploying a virtual machine to…
- [NexGen Cloud Floating IP API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-floating-ip-api/) — A floating IP is a static public IPv4 address that can be assigned to a virtual machine. Floating IPs persist across VM lifecycle events, detach from one VM…
- [NexGen Cloud GPU API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-gpu-api/) — GPU model availability and stock per region.
- [NexGen Cloud Health API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-health-api/) — Service liveness check for object storage. Use to confirm the object-storage service is reachable.
- [NexGen Cloud Image API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-image-api/) — An image is the operating system disk a virtual machine boots from. Images include Ubuntu, Rocky Linux, and other distributions, with optional pre-installed…
- [NexGen Cloud Image Generation API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-image-generation-api/) — Text-to-image and image-to-image generation. Submit a generation or edit request, then poll the task endpoint to retrieve the resulting image. Use a…
- [NexGen Cloud Inference API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-inference-api/) — OpenAI-compatible chat completions endpoint for running inference against deployed models. Use this endpoint to send prompts and receive generated responses.
- [NexGen Cloud Invite API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-invite-api/) — Invite endpoints add and manage users within an organization. Invite a user by email; they accept the invitation and gain access to the organization with…
- [NexGen Cloud Knowledge Bases API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-knowledge-bases-api/) — Collections of your own documents that models can search at inference time.
- [NexGen Cloud Models API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-models-api/) — User-deployed models and model aliases. These endpoints let you deploy and undeploy models, list available models, manage model aliases, and retrieve…
- [NexGen Cloud Organization API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-organization-api/) — Organization endpoints manage organization-level metadata: name, members, and configuration. Most users belong to a single organization; multi-organization…
- [NexGen Cloud Overview API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-overview-api/) — Organization-level summary and resource usage metrics for the AI Studio account.
- [NexGen Cloud Partner Config API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-partner-config-api/) — Partner config fetch endpoint
- [NexGen Cloud Payment API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-payment-api/) — Payment endpoints initiate and retrieve payments. Use these to add funds to your account programmatically or to fetch receipts for reconciliation.
- [NexGen Cloud Permission API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-permission-api/) — Permission endpoints list the granular permissions defined by Hyperstack. Permissions compose into RBAC roles, which are assigned to organization members.…
- [NexGen Cloud Policy API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-policy-api/) — Authorization policies that bind permissions to roles.
- [NexGen Cloud Pricebook API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-pricebook-api/) — Pricebook endpoints expose Hyperstack's pricing for compute, storage, and networking resources. Use these to estimate costs before deploying or to surface…
- [NexGen Cloud Profile API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-profile-api/) — Saved virtual-machine deployment configurations that can be reused across new VMs.
- [NexGen Cloud RBAC Role API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-rbac-role-api/) — RBAC role endpoints create, list, update, and delete custom roles. A role is a named bundle of permissions that you can assign to organization members.…
- [NexGen Cloud Region API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-region-api/) — A region is a geographic location where Hyperstack hosts compute and storage. Resources are region-scoped, virtual machines, volumes, snapshots, and…
- [NexGen Cloud Regions API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-regions-api/) — Regions where object storage is available.
- [NexGen Cloud Security Rules API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-security-rules-api/) — Security Rule APIs
- [NexGen Cloud snapshot events API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-snapshot-events-api/) — Snapshot Events APIs
- [NexGen Cloud Snapshots API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-snapshots-api/) — A snapshot is a point-in-time copy of a virtual machine or volume. Snapshots are stored in the same region as the source resource and can be used to clone,…
- [NexGen Cloud Stock API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-stock-api/) — GPU and CPU stock availability per flavor and region. Use before deployment to confirm capacity.
- [NexGen Cloud System Prompts API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-system-prompts-api/) — Reusable system prompt templates for AI Studio deployments. These endpoints let you create, retrieve, update, and delete system prompts that can be applied…
- [NexGen Cloud Template API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-template-api/) — A template is a saved virtual machine configuration that you can reuse to deploy identical VMs without re-specifying every parameter. Templates capture…
- [NexGen Cloud User API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-user-api/) — Account-level user information and billing identity.
- [NexGen Cloud User Consent API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-user-consent-api/) — User Consent endpoints record each user's grant or revoke decision for a given consent type (e.g. marketing communications, data-sharing terms). Use these…
- [NexGen Cloud User Consent Events API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-user-consent-events-api/) — User Consent management
- [NexGen Cloud User Detail Choice API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-user-detail-choice-api/) — User-specific configuration choices (profile preferences, defaults).
- [NexGen Cloud User Permission API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-user-permission-api/) — Permissions assigned to specific users in the calling organization.
- [NexGen Cloud Virtual Machine API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-virtual-machine-api/) — A virtual machine on Hyperstack is a single-tenant compute instance backed by dedicated GPU and CPU resources. Each VM runs in a region, attaches a root…
- [NexGen Cloud virtual machine events API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-virtual-machine-events-api/) — Virtual Machine Event APIs
- [NexGen Cloud VNC URL API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-vnc-url-api/) — Console-access URLs for connecting to a virtual machine over VNC.
- [NexGen Cloud Volume API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-volume-api/) — A volume is persistent block storage that attaches to a virtual machine. Volumes are region-scoped and can be detached and reattached to other VMs in the…
- [NexGen Cloud Volume Attachment API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-volume-attachment-api/) — Volume attachment endpoints manage the binding between a volume and a virtual machine. A volume can be attached to one VM at a time. Detach a volume before…
- [NexGen Cloud Vouchers API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-vouchers-api/) — Voucher endpoints redeem promotional codes to add credit to your account. Vouchers are single-use.
- [NexGen Cloud Key Pair API](https://apis.io/apis/nexgen-cloud/nexgen-cloud-key-pair-api/) — Keypair APIs

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Nexgen Cloud Webhooks](https://apis.io/asyncapis/nexgen-cloud/nexgen-cloud-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [nexgen-cloud-mcp.yml](https://apis.io/servers/nexgen-cloud/nexgen-cloud-mcp-yml/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Nexgen Cloud Ai Studio Overlay](https://apis.io/overlays/nexgen-cloud/nexgen-cloud-ai-studio-overlay/)
- [Nexgen Cloud Hyperstack Overlay](https://apis.io/overlays/nexgen-cloud/nexgen-cloud-hyperstack-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Nexgen Cloud Authentication](https://apis.io/security/nexgen-cloud/nexgen-cloud-authentication/)
- [Nexgen Cloud Domain Security](https://apis.io/security/nexgen-cloud/nexgen-cloud-domain-security/)
- [Nexgen Cloud Trust Center](https://apis.io/security/nexgen-cloud/nexgen-cloud-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Nexgen Cloud Plans Pricing](https://apis.io/plans/nexgen-cloud/nexgen-cloud-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Nexgen Cloud Rate Limits](https://apis.io/rate-limits/nexgen-cloud/nexgen-cloud-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.nexgencloud.com/)
- [Documentation](https://docs.hyperstack.cloud/docs/intro)
- [Getting started](https://docs.hyperstack.cloud/docs/getting-started)
- [API reference](https://docs.hyperstack.cloud/docs/api-reference/)
- [Pricing](https://www.hyperstack.cloud/gpu-pricing)
- [Sign up](https://console.hyperstack.cloud/login)
- [Support](https://docs.hyperstack.cloud/docs/support)
- [Changelog](https://docs.hyperstack.cloud/docs/release-notes)
- [Blog](https://www.nexgencloud.com/blog)
- [Terms of service](https://www.hyperstack.cloud/terms-and-conditions)
- [Privacy policy](https://www.hyperstack.cloud/privacy-policy)
- [GitHub](https://github.com/NexGenCloud)
- [Status](https://status.hyperstack.cloud/)

## API Evangelist rating

**Kin Score 66.5** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 61.3 |
| Contract governance | 18.2 |
| Operational transparency | 63.2 |
| Developer ergonomics | 66.1 |
| Access clarity | 92.1 |

**Agent readiness 43.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 27.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/nexgen-cloud/](https://apis.io/providers/nexgen-cloud/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for NexGen Cloud: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/nexgen-cloud/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
