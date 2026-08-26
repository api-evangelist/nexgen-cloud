---
name: nexgen-cloud-ai-studio-inference
description: Run inference on Hyperstack AI Studio - OpenAI-compatible chat completions, image generation, and grounding answers in a knowledge base. Covers the different base URL, the different error envelope, and what was removed in August 2026.
api: Hyperstack AI Studio API
base_url: https://console.hyperstack.cloud/ai/api/v1
auth: api_key header
generated: '2026-08-26'
method: generated
source: >-
  openapi/nexgen-cloud-ai-studio-openapi.json,
  https://docs.hyperstack.cloud/docs/ai-studio-api-reference/inference,
  https://docs.hyperstack.cloud/docs/release-notes
operations:
  - getBaseModels
  - getBaseModelPricing
  - getModels
  - chatCompletions
  - sendMessage
  - getConversations
  - getConversationMessages
  - listSystemPrompts
  - createSystemPrompt
  - generateImageFromText
  - generateImageFromImage
  - getImageResult
  - listKnowledgeBases
  - createKnowledgeBase
  - getKbFileUploadUrl
  - ingestKbFiles
  - getKnowledgeBaseStatus
---

# Run inference on Hyperstack AI Studio

## Two things that are different from the rest of Hyperstack

1. **Different base URL.** `https://console.hyperstack.cloud/ai/api/v1` — not
   `infrahub-api.nexgencloud.com`. Same API key, same `api_key` header.
2. **Different error envelope.** AI Studio returns `{code, message, status}` where `status`
   is a **string**. The Hyperstack Core API returns `{status, message, error_reason}` where
   `status` is a **boolean**. A shared error handler across the two APIs will misread every
   AI Studio failure. `422` is the dominant failure status here, not `400`.

## What changed on 2026-08-25 — read this before writing code

Fine-tuning and Hyperstack-hosted base models were **removed from the console and the API**.
Gone with them: LoRA adapter training and import, model deployment, model aliases, model
evaluations, training metrics and logs, datasets, and data synthesis. Four base models were
retired: `openai/gpt-oss-120b`, `mistralai/Mistral-Small-24B-Instruct-2501`,
`meta-llama/Llama-3.3-70B-Instruct`, `meta-llama/Llama-3.1-8B-Instruct`.

AI Studio is now **inference-only, over third-party hosted models**. Inference, the
playground, knowledge bases, system prompts and conversations were unaffected. There was no
notice period and no `Sunset` header — the change landed the day it was announced. Assume
the same is possible again: check `getBaseModels` at runtime rather than hardcoding a model
name.

## Chat completions (OpenAI-compatible)

1. `getModels` (`GET /models`) — returns models in OpenAI-compatible format. Use a model's
   `id` as the `model` value.
2. `getBaseModelPricing` (`GET /base_models/pricing`) — per-model pricing before you spend.
3. `chatCompletions` (`POST /chat/completions`) — the OpenAI shape. An existing OpenAI
   client needs a base URL change and a key change, nothing else.

## Stateful conversations

`sendMessage` (`POST /conversations/send_message`) keeps server-side history, unlike
`chatCompletions`. Read it back with `getConversationMessages`
(`GET /conversations/{conversation_id}/messages`), list with `getConversations`, and attach
images with `uploadImage`. `deleteConversation` is permanent.

## Grounding answers in your own content

1. `createKnowledgeBase` (`POST /knowledge-bases`).
2. `getKbFileUploadUrl` (`GET /knowledge-bases/{kb_id}/files/upload-url`) then
   `ingestKbFiles` (`POST /knowledge-bases/{kb_id}/files/ingest`). Text and Markdown files.
3. Poll `getKnowledgeBaseStatus` (`GET /knowledge-bases/{kb_id}/status`) while indexing runs.
   `cancelKnowledgeBaseIngestion` stops it mid-flight.
4. Pass the knowledge base to `sendMessage` to ground a reply. Grounded replies carry
   numbered citation markers naming the source file and passage.

`deleteKnowledgeBase` is irreversible — there is no restore, and the indexed files go with it.

## Image generation is asynchronous

`generateImageFromText` (`POST /images/generations`) and `generateImageFromImage`
(`POST /images/edits`) return a `job_id`. Poll `getImageResult`
(`GET /images/tasks/{job_id}`) for the result. Do not block on the first call.

## Reusable system prompts

`createSystemPrompt` / `listSystemPrompts` / `updateSystemPrompt` / `deleteSystemPrompt`
under `/system-prompts` — server-side prompt templates you can reference instead of
resending the same preamble.

## Limits

AI Studio publishes **no** rate limits of its own. Whether the Hyperstack Core 500/min
per-source-IP ceiling applies here is not stated. There is no idempotency key: a retried
`chatCompletions` or `generateImageFromText` is a second billable inference.
