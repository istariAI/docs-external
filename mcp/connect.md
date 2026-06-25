---
title: "Connect"
description: Connect GOI MCP to Claude, Cursor, and other MCP clients.
---

GOI MCP uses your ISTARI account at [index.istari.ai](https://index.istari.ai). The same account works for the GOI dashboard, the GOI API, and GOI MCP.

<Note>
GOI MCP is undergoing review for publication in connector stores, including Claude and ChatGPT. Until it is listed there, [request beta access](https://index.istari.ai/goi-mcp-access) with your ISTARI account.
</Note>

## Request beta access

1. Sign up or sign in at [index.istari.ai](https://index.istari.ai).
2. Submit the [beta access request](https://index.istari.ai/goi-mcp-access). We enable approved accounts for early use.

## Connect after approval

### Claude

1. In Claude, go to **Connectors → Browse Connectors → ISTARI GOI** and add GOI MCP.
2. Sign in when prompted. You can create an account during sign-in if you do not have one yet.

### Cursor

1. Open **Cursor Settings → MCP** and add the ISTARI GOI server from the MCP directory, or configure it manually if provided by your admin.
2. Authenticate when prompted.

### Other MCP clients

Any client that supports remote MCP connectors with OAuth can use GOI MCP. After connecting, verify access by asking the agent to run a simple `search_organizations` query or check the GOI MCP health endpoint described in the [overview](/mcp/overview).

## Plan access

New accounts start on the **Standard** plan. See [Standard plan quotas](/mcp/overview#standard-plan-quotas) on the overview page for monthly limits.

For higher quotas, see [GOI access plans](https://www.istari.ai/en/technology) on the ISTARI technology page.

## Troubleshooting

- **`Monthly request quota exceeded`**: quotas reset on the first of the month (UTC). To raise limits, see [GOI access plans](https://www.istari.ai/en/technology).
- **Authentication errors**: confirm you are signed in at [index.istari.ai](https://index.istari.ai/) with the same account used for GOI MCP.
- **Still stuck?** Contact [support@istari.ai](mailto:support@istari.ai).

## See also

- [Overview](/mcp/overview): what GOI MCP provides and quota tables.
- [Tools](/mcp/tools): tool reference and when to use each one.
- [Privacy](/mcp/privacy): logging and data retention.
