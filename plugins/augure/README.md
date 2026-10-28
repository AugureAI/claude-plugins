# Augure plugins for Claude Code

Augure is a Canadian sovereign AI platform: an OpenAI-compatible API at `https://api.augureai.ca/v1`, customer data stored in Canada, inference on Canadian infrastructure and vetted EU partners under zero data retention, never US providers, priced in Canadian dollars.

## Install

```
/plugin marketplace add AugureAI/claude-plugins
/plugin install augure@augure
```

The plugin bundles:

- the `augure-inference-provider` skill, which tells Claude Code how to configure Augure in any SDK, editor or agent, which model to pick, and what not to claim;
- the Augure MCP server (`https://mcp.augureai.ca/mcp`), which needs an MCP key in `AUGURE_MCP_KEY`. Create one in the developer dashboard: https://augureai.ca/docs/mcp

Docs: https://augureai.ca/docs/agents · API reference: https://augureai.ca/docs/api · Models and prices: https://augureai.ca/docs/models

## Licence

MIT. Augure is a trademark of The Altercation Company Inc.
