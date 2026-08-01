---
generated: '2026-08-01'
method: declared
publisher: Xquik
name: Use Xquik
description: Use Xquik through its REST API, webhooks, SDKs, and hosted MCP server.
api: https://xquik.com/openapi.json
source: https://xquik.com/.well-known/agent-skills/xquik/SKILL.md
---

# Use Xquik

Xquik is an independent third-party service. Not affiliated with X Corp. "Twitter" and "X" are trademarks of X Corp.

## Connect Through MCP

1. Add `https://xquik.com/mcp` as a Streamable HTTP endpoint.
2. Complete the OAuth 2.1 flow.
3. Call `explore` to find the smallest relevant operation.
4. Call `xquik` to run authenticated operations.

Use `https://xquik.com/.well-known/mcp.json` for discovery.

## Use the REST API

- Read `https://docs.xquik.com/api-reference/overview`.
- Load `https://xquik.com/openapi.json`.
- Send an API key through the `x-api-key` header.
- Send `xquik-api-contract: 2026-04-29` for normalized responses.
- Follow `has_more` and `next_cursor` for paginated reads.
- Respect structured errors and `retry_after` values.
- Send a unique `Idempotency-Key` when the contract requires one.
- Request `dry_run=true` before starting an extraction when appropriate.

## Discovery

- MCP guide: https://docs.xquik.com/mcp/overview
- OAuth guide: https://docs.xquik.com/oauth/overview
- Authentication: https://xquik.com/auth.md
- Agent index: https://xquik.com/.well-known/agent-index.json
- Agent card: https://xquik.com/.well-known/agent-card.json
