---
name: xquik
status: published
description: Use Xquik to search public X data, monitor activity, publish from connected accounts, and automate workflows through REST API, webhooks, and MCP.
---

# Xquik

Xquik is an independent third-party service. Not affiliated with X Corp. "Twitter" and "X" are trademarks of X Corp.

Use Xquik to search public X data, monitor activity, publish from connected accounts, and automate workflows.

## Connect Through MCP

1. Add the Streamable HTTP endpoint: https://xquik.com/mcp
2. Complete the OAuth 2.1 flow opened by your MCP client.
3. Call `explore` to find the smallest relevant API operation.
4. Call `xquik` to run authenticated operations.

Current SDKs negotiate MCP 2026-07-28 through `server/discover`.
They attach required headers and per-request `_meta` automatically.
Do not call `initialize` or manage sessions for modern connections.
Xquik also accepts stateless 2025-era clients at the same endpoint.

MCP clients discover authorization metadata automatically. API-key fallback is client-specific. ChatGPT custom apps require OAuth and cannot present custom API keys.

### Codex OAuth fallback

If Codex reports `Authorization server response missing required issuer: expected https://xquik.com`, the Codex client discarded Xquik's RFC 9207 `iss` response parameter. Xquik already returned the issuer. Track the client fix at https://github.com/openai/codex/issues/31573.

Store an Xquik API key in `XQUIK_API_KEY`, then configure Codex:

```toml
[mcp_servers.xquik]
url = "https://xquik.com/mcp"
bearer_token_env_var = "XQUIK_API_KEY"
```

Do not run `codex mcp login xquik` while using this fallback. See https://docs.xquik.com/guides/troubleshooting#codex-oauth-issuer-validation-error.

Affected Goose releases can report the same issuer error. Use Goose's documented environment-backed bearer header until its callback adapter preserves `iss`. Roo Code is archived and API-key-only. Pi has no native MCP support.

## Use the REST API

- Read the API guide: https://docs.xquik.com/api-reference/overview
- Read the OpenAPI schema: https://xquik.com/openapi.json
- Send an Xquik API key through the `x-api-key` header.
- Send `xquik-api-contract: 2026-04-29` for normalized snake_case responses.
- Follow `has_more` and `next_cursor` for paginated reads.
- Respect structured errors and `retry_after` values.

## Discovery

- MCP guide: https://docs.xquik.com/mcp/overview
- OAuth guide: https://docs.xquik.com/oauth/overview
- Authentication instructions: https://xquik.com/auth.md
- MCP manifest: https://xquik.com/.well-known/mcp.json
- Agent index: https://xquik.com/.well-known/agent-index.json
