---
name: nexgen-cloud-discover-hyperstack-machine-readable
description: Discover everything Hyperstack publishes for machines from a single request - the RFC 8288 Link header and RFC 9727 api-catalog give you both OpenAPI documents, the llms.txt index and the anonymous docs MCP endpoint without knowing any path in advance.
api: Hyperstack API
base_url: https://docs.hyperstack.cloud
auth: none
generated: '2026-08-26'
method: generated
source: >-
  probed Link header and /.well-known/api-catalog on docs.hyperstack.cloud;
  https://docs.hyperstack.cloud/docs/libraries/agent-docs
operations: []
---

# Discover Hyperstack's machine-readable surface

Hyperstack does the discovery work properly, which is rare enough to be worth a skill of its
own. You do not need to guess a spec path.

## One HEAD request gives you everything

```
HEAD https://docs.hyperstack.cloud/docs/api-reference/introduction
```

The response carries an RFC 8288 `Link` header:

```
link: </docs/api-reference/introduction/>; rel="service-doc",
      </openapi/hyperstack.json>; rel="service-desc",
      </openapi/ai-studio.json>; rel="service-desc",
      </llms.txt>; rel="llms-txt",
      </mcp>; rel="mcp-server",
      </.well-known/api-catalog>; rel="api-catalog"
```

Six relations, resolved against `https://docs.hyperstack.cloud`.

## Or the RFC 9727 catalog

```
GET https://docs.hyperstack.cloud/.well-known/api-catalog
```

Returns `application/linkset+json` naming both APIs and binding each to its `service-desc`
(OpenAPI JSON) and `service-doc` (HTML reference):

- **Hyperstack API** → `/openapi/hyperstack.json` — 209 operations, 323 schemas, OpenAPI 3.0.1
- **AI Studio API** → `/openapi/ai-studio.json` — 33 operations, OpenAPI 3.1.0

A third document, the raw generator source, is served at
`https://infrahub-api-doc.nexgencloud.com/api.json`. It carries 225 operations against
hyperstack.json's 209, but with far thinner descriptions — it is the SDK build input, not
the documentation contract. Prefer `hyperstack.json`.

## Pages as Markdown

Append `.txt` to any docs path — `https://docs.hyperstack.cloud/docs/api-reference/errors.txt`
— or send an `Accept` header for Markdown. Every `.txt` page opens with a pointer to
`/llms.txt` and `/mcp`.

## The anonymous MCP server

`https://docs.hyperstack.cloud/mcp`, Streamable HTTP, **no authentication**. Five read-only
tools:

- `search_docs(query, resource_type, limit)` — natural-language search; set
  `resource_type` to `api` or `ai_studio_api` to search reference pages only
- `get_page(path, section)` — a full page as Markdown
- `list_sections(filter)` — table of contents by product area
- `lookup_error(error_message, context)` — resolve an HTTP status, `error_reason` or raw
  message to cause and fix
- `get_flavor_info(query, gpu_model)` — GPU flavor specifications

Add it with `claude mcp add --transport http hyperstack-docs https://docs.hyperstack.cloud/mcp`
or `npx add-mcp https://docs.hyperstack.cloud/mcp --name hyperstack-docs`.

## What is NOT there

- No `/.well-known/security.txt` on any host (404 on all six probed).
- No `/.well-known/agent-card.json` or `/.well-known/agent.json` — no A2A agent card.
- No OAuth or OIDC discovery documents.
- No AsyncAPI, despite a documented 32-event webhook catalog.
- `www.hyperstack.cloud/llms.txt` and `www.nexgencloud.com/llms.txt` return **200 with an
  HTML page**, not an llms.txt. Only `docs.hyperstack.cloud/llms.txt` is real.

## The second MCP server, which is not this one

`https://docs.hyperstack.cloud/mcp` is read-only over documentation. The **Hyperstack API
MCP Server** is a different product: a Docker image
(`ghcr.io/nexgencloud/hyperstack-mcp-server:latest`) that you run yourself with your own API
key, and it creates, modifies and deletes real billable infrastructure. See
`mcp/nexgen-cloud-mcp.yml` and `mcp/nexgen-cloud-tool-crosswalk.yml`.
