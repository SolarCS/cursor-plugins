---
name: team-integrations-setup
description: >-
  First-run setup for the CipherHealth team MCP plugin (Salesforce, ZoomInfo,
  Google Calendar, Gmail, Google Drive, Seismic, Looker). Use when any bundled
  MCP is missing, errored, needs auth, or the user asks how to connect trial
  integrations in Cursor.
---

# CipherHealth team MCP setup

This plugin bundles **seven MCP servers** in one `mcp.json`. Install the plugin once, set env vars (if needed), then connect each server via OAuth in Settings.

## 1. Environment variables (before opening Cursor)

```bash
# Salesforce Consumer Key (External Client App)
launchctl setenv SF_CLIENT_ID "YOUR_CONSUMER_KEY"

# Google OAuth app — shared by Calendar, Gmail, and Drive MCP
launchctl setenv GOOGLE_MCP_CLIENT_ID "YOUR_CLIENT_ID"
launchctl setenv GOOGLE_MCP_CLIENT_SECRET "YOUR_CLIENT_SECRET"
```

Fully quit Cursor (**Cmd+Q**) and reopen.

**No env vars needed:** ZoomInfo, Seismic (OAuth on connect), Looker (`CLIENT_ID` is in `mcp.json`).

## 2. Connect each server

**Settings → Tools & MCP** — connect every server from this plugin:

| Server | Auth |
|--------|------|
| **Salesforce** | OAuth → CipherHealth Salesforce |
| **zoominfo** | OAuth |
| **Google Calendar** | OAuth (Google account) |
| **Gmail** | OAuth (Google account) |
| **Google Drive** | OAuth (Google account) |
| **Seismic** | OAuth (Seismic / cipherhealth.com tenant) |
| **looker-toolbox** | OAuth (Looker instance) |

Toggle servers on if disabled.

## 3. Verify

- **Salesforce:** `getUserInfo` or `SELECT Id, Name FROM Account LIMIT 1`
- **Google Calendar:** `list_calendars`
- **Gmail / Drive:** list tools after connect; try a read-only action
- **ZoomInfo / Seismic / Looker:** confirm tools appear after Connect

## Adding more MCP servers

Edit `mcp.json` in [SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins) and push. Do **not** create a separate plugin per MCP.

## Common failures

| Symptom | Fix |
|---------|-----|
| No MCP servers from plugin | Plugin not installed — check team marketplace **Required** |
| Salesforce 404 | URL must end in `sobject-reads` (plural) |
| Google MCP auth fails | Same OAuth app must allow Calendar/Gmail/Drive MCP redirect URLs |
| Looker fails | Confirm `cursor_mcp` client is registered on Looker instance |
| Seismic fails | User must have access to `cipherhealth.com` Seismic tenant |
| Empty auth | Env vars must be set **before** Cursor starts |

See **salesforce-setup** for Salesforce admin checklist.
