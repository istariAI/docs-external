---
description: Connect the GOI MCP connector to Claude, Cursor, and other MCP clients.
---

# Connect

The GOI MCP connector uses your ISTARI account at [index.istari.ai](https://index.istari.ai). The same account works for the GOI dashboard, the HTTP API, and this MCP connector.

## Claude

1. Sign up or sign in at [index.istari.ai](https://index.istari.ai/).
2. In Claude, go to **Connectors → Browse Connectors → ISTARI GOI** and add the connector.
3. Sign in when prompted. You can create an account during sign-in if you do not have one yet.

## Cursor

1. Sign up or sign in at [index.istari.ai](https://index.istari.ai/).
2. Open **Cursor Settings → MCP** and add the ISTARI GOI server from the MCP directory, or configure it manually if provided by your admin.
3. Authenticate when prompted.

## Other MCP clients

Any client that supports remote MCP connectors with OAuth can use the GOI connector. After connecting, verify access by asking the agent to run a simple `search_organizations` query or check the connector health endpoint described in the [overview](index).

## Plan access

New accounts start on the **Standard** plan. See [Standard plan quotas](index#standard-plan-quotas) on the overview page for monthly limits.

For higher quotas, see [GOI access plans](https://www.istari.ai/en/technology) on the ISTARI technology page.

## Troubleshooting

- **`Monthly request quota exceeded`** — quotas reset on the first of the month (UTC). To raise limits, see [GOI access plans](https://www.istari.ai/en/technology).
- **Authentication errors** — confirm you are signed in at [index.istari.ai](https://index.istari.ai/) with the same account used for the connector.
- **Still stuck?** Contact [support@istari.ai](mailto:support@istari.ai).

## See also

- [Overview](index) — what the connector provides and quota tables.
- [Tools](tools) — tool reference and when to use each one.
- [Privacy](privacy) — logging and data retention.
