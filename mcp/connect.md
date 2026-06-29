---
title: "Connect"
description: Connect GOI MCP to Claude, ChatGPT, Cursor, and other MCP clients.
---

GOI MCP uses your ISTARI account at [index.istari.ai](https://index.istari.ai). The same account works for the GOI dashboard, the GOI API, and GOI MCP.

<Note>
GOI MCP is not yet listed in connector directories for Claude or ChatGPT. Request access, then add it manually as a **custom connector** using the credentials we email you. Once store approval is complete, we will update this page with one-click install instructions.
</Note>

## Request access

1. Sign up or sign in at [index.istari.ai](https://index.istari.ai).
2. Submit the [GOI MCP access request](https://index.istari.ai/goi-mcp-access).
3. After we enable your account, you receive an email titled **Your GOI MCP credentials** with everything you need to connect:

| Field | Example | Notes |
| --- | --- | --- |
| **Name** | `istari-goi` | Use this as the server or connector name in your MCP client. |
| **MCP URL** | `https://mcp.goi.istari.ai/mcp` | The remote MCP endpoint. |
| **Client ID** | *(in your email)* | OAuth client ID for your account. |
| **Secret** | *(in your email)* | OAuth client secret. Treat it like a password. |

Keep your **Client ID** and **Secret** private. Do not commit them to git or share them in chat logs. Use environment variables or your client's secure credential storage where supported.

## Add as a custom connector

Use the **Name**, **MCP URL**, **Client ID**, and **Secret** from your email in the steps below. When a client asks you to sign in, use the same `index.istari.ai` account you used to request access.

### Claude

#### Claude on the web (claude.ai)

1. Go to **Settings → Connectors** on [claude.ai](https://claude.ai). Team and Enterprise admins can add org-wide connectors under **Admin settings → Connectors**.
2. Click **Add custom connector**.
3. Enter the **MCP URL** from your email: `https://mcp.goi.istari.ai/mcp`.
4. Under **Advanced settings**, enter your **Client ID** and **Secret** from the email.
5. Click **Add**, then sign in with your `index.istari.ai` account when prompted.


#### Claude Code

From a terminal:

```bash
claude mcp add --transport http \
  --client-id YOUR_CLIENT_ID \
  --client-secret \
  istari-goi https://mcp.goi.istari.ai/mcp
```

Replace `YOUR_CLIENT_ID` with the **Client ID** from your email. The `--client-secret` flag prompts for your **Secret** with masked input.

Alternatively, add via JSON:

```bash
claude mcp add-json istari-goi \
  '{"type":"http","url":"https://mcp.goi.istari.ai/mcp","oauth":{"clientId":"YOUR_CLIENT_ID","callbackPort":8080}}' \
  --client-secret
```

Run `/mcp` inside Claude Code to confirm the server is connected and complete OAuth if prompted.

### ChatGPT

ChatGPT connects to remote MCP servers over HTTPS with OAuth. Custom connectors require **Developer mode**, available on ChatGPT Pro, Team, Enterprise, and Edu plans.

1. Click your avatar → **Settings → Connectors**.
2. Under **Advanced**, turn on **Developer mode** and accept the warning.
3. Click **Add custom connector**.
4. Enter a name (use **istari-goi** or **ISTARI GOI** from your email), an optional description, and the **MCP URL**: `https://mcp.goi.istari.ai/mcp`.
5. Set **Authentication** to **OAuth**.
6. If the form exposes OAuth client fields, enter your **Client ID** and **Secret** from the email.
7. Check **I trust this application**, then click **Create**.
8. Sign in with your `index.istari.ai` account when ChatGPT redirects you through OAuth.

In a chat, enable the connector from the **Tools** menu before asking the agent to search organizations.

### Cursor

#### Cursor (IDE)

For local Agent and Chat sessions:

1. Open **Cursor Settings** (Cmd + Shift + J on Mac, Ctrl + Shift + J on Windows/Linux) → **Tools & MCP**.
2. Click **Add new MCP server**, or add an entry to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "istari-goi": {
      "url": "https://mcp.goi.istari.ai/mcp",
      "auth": {
        "CLIENT_ID": "YOUR_CLIENT_ID",
        "CLIENT_SECRET": "YOUR_CLIENT_SECRET"
      }
    }
  }
}
```

Replace `YOUR_CLIENT_ID` and `YOUR_CLIENT_SECRET` with the values from your email. Prefer environment variables instead of hardcoding secrets:

```json
{
  "mcpServers": {
    "istari-goi": {
      "url": "https://mcp.goi.istari.ai/mcp",
      "auth": {
        "CLIENT_ID": "${env:GOI_MCP_CLIENT_ID}",
        "CLIENT_SECRET": "${env:GOI_MCP_CLIENT_SECRET}"
      }
    }
  }
}
```

3. Restart Cursor if prompted, then complete OAuth when asked to sign in.

#### Cursor Cloud Agents

Cloud Agents do **not** read your local `~/.cursor/mcp.json`. Configure GOI MCP in the Cloud Agents dashboard instead.

1. Open [cursor.com/agents](https://cursor.com/agents).
2. Open the **MCP** dropdown and add a custom **HTTP** server.
3. Enter the **MCP URL**: `https://mcp.goi.istari.ai/mcp`.
4. Enter your **Client ID** and **Secret** from the email if the form provides OAuth fields.
5. Enable the server for your session and complete OAuth when prompted.

On Team plans, admins can configure shared MCP servers under **Settings → Integrations & MCP** in the [Cursor dashboard](https://cursor.com/dashboard). OAuth is per user, including for team-shared servers.

Cloud Agents support HTTP (recommended) and stdio transport. SSE and `mcp-remote` are not supported.

### Other MCP clients

Any client that supports remote MCP over HTTP with OAuth can connect using the **MCP URL**, **Client ID**, and **Secret** from your email. After connecting, verify access by asking the agent to run a simple `search_organizations` query or check the GOI MCP health endpoint described in the [overview](/mcp/overview).

## Verify the connection

Ask the agent to search for organizations or call `search_organizations` with a simple query. A successful connection returns GOI results scoped to your account plan.

## Plan access

New accounts start on the **Standard** plan. See [Standard plan quotas](/mcp/overview#standard-plan-quotas) on the overview page for monthly limits.

For higher quotas, see [GOI access plans](https://www.istari.ai/en/technology) on the ISTARI technology page.

## Troubleshooting

- **`Monthly request quota exceeded`**: quotas reset on the first of the month (UTC). To raise limits, see [GOI access plans](https://www.istari.ai/en/technology).
- **Authentication errors**: confirm you are signed in at [index.istari.ai](https://index.istari.ai/) with the same account used to request access, and that your **Client ID** and **Secret** match the values in your credentials email.
- **No credentials email**: confirm you submitted the [access request](https://index.istari.ai/goi-mcp-access) with the same email you use at `index.istari.ai`. Contact [support@istari.ai](mailto:support@istari.ai) if it has been more than a few business days.
- **ChatGPT cannot connect**: confirm Developer mode is on, the URL ends with `/mcp`, and OAuth is selected as the authentication method.
- **Cloud Agent cannot see GOI MCP**: confirm the server is added and enabled in [cursor.com/agents](https://cursor.com/agents), not only in local IDE settings.
- **Still stuck?** Contact [support@istari.ai](mailto:support@istari.ai).

## See also

- [Overview](/mcp/overview): what GOI MCP provides and quota tables.
- [Tools](/mcp/tools): tool reference and when to use each one.
- [Privacy](/mcp/privacy): logging and data retention.
