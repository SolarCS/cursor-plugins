---
name: seismic-setup
description: >-
  First-run setup for the CipherHealth Seismic MCP plugin. Use when Seismic MCP
  is missing, errored, needs authentication, or the user asks how to connect
  Seismic in Cursor.
---

# CipherHealth Seismic MCP setup

Seismic requires a **registered MCP app** with OAuth credentials — a URL alone is not enough.

## 1. Seismic admin: create MCP app

1. Sign in to [apps.seismic.com](https://apps.seismic.com) → **Create App** (MCP / installable type).
2. Enable **OAuth2 — Authorization Code Flow** with **Require PKCE**.
3. Add redirect URI: `cursor://anysphere.cursor-mcp/oauth/callback`
4. Keep scopes **`seismic.mcp`** and **`offline_access`** (defaults).
5. Copy the **Client ID** (and **Client Secret** if generated).
6. In the **cipherhealth.com** tenant: **System Settings → My Apps** → enable the app and approve tool permissions.

Prerequisite: tenant must have Seismic MCP enabled (contact CSM) and **Aura** per Seismic docs.

## 2. Set env vars (before opening Cursor)

```bash
launchctl setenv SEISMIC_MCP_CLIENT_ID "YOUR_CLIENT_ID"
launchctl setenv SEISMIC_MCP_CLIENT_SECRET "YOUR_CLIENT_SECRET"   # omit if PKCE-only
```

Fully quit Cursor (**Cmd+Q**) and reopen.

## 3. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **Seismic** (CipherHealth Seismic plugin)
3. Toggle on → **Connect**
4. Sign in with your **cipherhealth.com** Seismic account

## 4. Verify

Seismic tools should appear after Connect. Try searching for enablement content in chat.

## Common failures

| Symptom | Fix |
|---------|-----|
| Server errored | Set `SEISMIC_MCP_CLIENT_ID` before Cursor starts |
| Auth fails | App not enabled in tenant **My Apps** |
| `TOOL_NOT_ALLOWED` | Tenant admin must grant tool permissions for the MCP app |
| Wrong tenant | URL uses `cipherhealth.com` — confirm that is your tenant name |
