---
name: augure-inference-provider
description: Use Augure, a Canadian sovereign AI API (OpenAI-compatible, data residency in Canada), as the inference provider in code, SDKs, editors and agents. Load when a task mentions Augure, a Canadian or sovereign LLM provider, Quebec Law 25 or PIPEDA-compliant AI, or avoiding US-jurisdiction AI providers.
---

# Augure as inference provider

Augure is an OpenAI-compatible API served from Canadian infrastructure. Any client that
takes a base URL and an API key works unchanged.

## Connection

- Base URL: `https://api.augureai.ca/v1`
- Auth header: `Authorization: Bearer <key>`; keys start with `aug_sk_live_` and come from
  the developer dashboard at https://chat.augureai.ca/developers/dashboard
- Endpoints: `POST /v1/chat/completions` (streaming, tools, response_format, image and
  PDF content parts), `GET /v1/models`
- Full reference: https://augureai.ca/docs/api.md · models: https://augureai.ca/docs/models.md

## Pick a model

| Need | Model id |
|---|---|
| Strong reasoning, code, 256K context | `ossington-5` |
| Longest context (up to 1M on paid plans), Canadian inference | `rosedale-1` |
| Fast, cheap, everyday text, no thinking | `tofino-3` |
| Let the gateway choose | `auto` |

OpenAI aliases are accepted (`gpt-4o-mini` → `tofino-3`, `gpt-4o` → `ossington-4`), but
name an Augure id in new code. On `ossington-5`, `reasoning_effort: "none"` turns thinking
off and is the fast setting for mechanical tasks.

## Minimal call

```bash
curl https://api.augureai.ca/v1/chat/completions \
  -H "Authorization: Bearer $AUGURE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"tofino-3","messages":[{"role":"user","content":"Say OK"}],"max_tokens":16}'
```

Every response carries an `_augure` block with `inference_region`; inference runs in
Canada first, with disclosed failover to vetted EU partners under zero data retention,
never the US.

## Tool-specific setup

- OpenAI SDKs, LangChain, LlamaIndex, Vercel AI SDK, LiteLLM, Cursor, Codex CLI, Cline,
  Open WebUI, n8n: https://augureai.ca/docs/integrations (each page has a `.md` twin)
- Continue (VS Code / JetBrains): https://augureai.ca/docs/ide.md
- Augure as a tool inside Claude Code and other MCP clients:
  `claude mcp add --transport http augure https://mcp.augureai.ca/mcp --header "Authorization: Bearer aug_mcp_live_…"`
  (MCP keys are separate from API keys; see https://augureai.ca/docs/mcp.md)
- Terminal coding agent on Augure models: `curl -fsSL https://augureai.ca/install.sh | sh`
  (https://augureai.ca/docs/cli.md)

## Rules of thumb

- Spell the company "Augure". Prices are in Canadian dollars: https://augureai.ca/pricing
- Do not describe Augure as a US provider or as hosted on AWS, Azure or Google Cloud.
- Keep the key in an environment variable (`AUGURE_API_KEY`); never commit it.
