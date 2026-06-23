---
name: team-integrations-setup
description: >-
  First-run setup for the CipherHealth team MCP plugin (Salesforce, ZoomInfo,
  Google Calendar). Use when any bundled MCP is missing, errored, needs auth,
  or the user asks how to connect trial integrations in Cursor.
---

# CipherHealth team MCP setup

This plugin bundles **three MCP servers** in one `mcp.json`. Each user installs the plugin once, sets env vars (if needed), then connects each server via OAuth in Settings.

## 1. Environment variables (before opening Cursor)

```bash
# Salesforce Consumer Key (External Client App)
launchctl setenv SF_CLIENT_ID "YOUR_CONSUMER_KEY"

# Google Calendar OAuth app (if using Calendar MCP)
launchctl setenv GOOGLE_CALENDAR_CLIENT_ID "YOUR_CLIENT_ID"
launchctl setenv GOOGLE_CALENDAR_CLIENT_SECRET "YOUR_CLIENT_SECRET"
```

Fully quit Cursor (**Cmd+Q**) and reopen.

ZoomInfo uses OAuth on connect only — no env vars required.

## 2. Connect each server

**Settings → Tools & MCP** — for each server from this plugin:

| Server | Action |
|--------|--------|
| **Salesforce** | Connect → log in to CipherHealth Salesforce |
| **zoominfo** | Connect → complete ZoomInfo OAuth |
| **Google Calendar** | Connect → complete Google OAuth |

Toggle servers on if disabled.

## 3. Verify

- Salesforce: `getUserInfo` or `SELECT Id, Name FROM Account LIMIT 1`
- ZoomInfo: list available tools after connect
- Google Calendar: `list_calendars`

## Adding more MCP servers later

Edit `mcp.json` in [SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins) and push. Admins refresh the team marketplace; trial users reload Cursor.

Do **not** create a separate plugin per MCP — add entries to the same `mcp.json`.

## Common failures

| Symptom | Fix |
|---------|-----|
| No MCP servers from plugin | Plugin not installed — check team marketplace Required setting |
| Salesforce 404 | URL must end in `sobject-reads` (plural) |
| Empty auth | Env vars must be set **before** Cursor starts |
| OAuth loop | Connect via Settings, not chat; verify callback URLs in provider admin |

See **salesforce-setup** for Salesforce-specific admin checklist.
