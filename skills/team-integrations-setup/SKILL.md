---
name: team-integrations-setup
description: >-
  First-run setup for the CipherHealth team MCP plugin (Salesforce, ZoomInfo,
  Google Calendar, Gmail, Google Drive, Seismic, Looker). Use when any bundled
  MCP is missing, errored, needs auth, or the user asks how to connect trial
  integrations in Cursor.
---

# CipherHealth team MCP setup

This plugin bundles **seven MCP servers** in one `mcp.json`. Most use **OAuth on connect** — no env vars. Only Salesforce needs a Consumer Key before launch.

## 1. Salesforce env var (before opening Cursor)

```bash
launchctl setenv SF_CLIENT_ID "YOUR_CONSUMER_KEY"
```

Fully quit Cursor (**Cmd+Q**) and reopen.

**OAuth only (no env vars):** Google Calendar, Gmail, Google Drive, ZoomInfo, Seismic, Looker.

## 2. Connect each server

**Settings → Tools & MCP** — click **Connect** for every server:

| Server | Auth |
|--------|------|
| **Salesforce** | `SF_CLIENT_ID` env + OAuth |
| **zoominfo** | OAuth |
| **Google Calendar** | OAuth (Google account) |
| **Gmail** | OAuth (Google account) |
| **Google Drive** | OAuth (Google account) |
| **Seismic** | OAuth (cipherhealth.com tenant) |
| **looker-toolbox** | OAuth (Looker instance) |

Toggle servers on if disabled.

## 3. Verify

- **Salesforce:** `getUserInfo` or `SELECT Id, Name FROM Account LIMIT 1`
- **Google Calendar:** `list_calendars`
- **Gmail / Drive / ZoomInfo / Seismic / Looker:** tools appear after Connect

## Common failures

| Symptom | Fix |
|---------|-----|
| No MCP servers from plugin | Check team marketplace **Required** install |
| Salesforce 404 | URL must end in `sobject-reads` |
| Google / Looker OAuth fails | Connect via **Settings → Tools & MCP**, not chat |
| Seismic fails | User needs access to cipherhealth.com tenant |
| Salesforce empty auth | Set `SF_CLIENT_ID` before Cursor starts |

See **salesforce-setup** for Salesforce admin checklist.
