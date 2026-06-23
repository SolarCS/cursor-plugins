---
name: salesforce-setup
description: >-
  First-run setup for the CipherHealth Salesforce MCP plugin. Use when Salesforce
  MCP is missing, errored, needs authentication, or the user asks how to connect
  Salesforce in Cursor.
---

# CipherHealth Salesforce MCP setup

## 1. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **Salesforce** (from the CipherHealth Salesforce plugin)
3. Toggle on if disabled
4. Click **Connect** and complete Salesforce OAuth in the browser

The Consumer Key is bundled in the plugin — no env vars required.

## 2. Verify

Ask the agent to run `getUserInfo` or a test query:

```sql
SELECT Id, Name FROM Account LIMIT 1
```

## Common failures

| Symptom | Fix |
|---------|-----|
| `Server definition not found` | URL must be `.../platform/sobject-reads` (with **s**) |
| Server errored / 405 | Complete OAuth via Settings → Connect (not just chat) |
| Tools missing | Plugin not installed — check team marketplace or install locally |

## Salesforce admin checklist

- Enable `platform/sobject-reads` in **Setup → API Catalog → MCP Servers**
- External Client App with scopes: `mcp_api`, `refresh_token`
- Callback URLs (register both if unsure):
  - `cursor://anysphere.cursor-mcp/oauth/callback`
  - `https://www.cursor.com/agents/mcp/oauth/callback`
- **Do not** enable "Require Secret for Web Server Flow" unless you distribute `SF_CLIENT_SECRET` to all trial users
