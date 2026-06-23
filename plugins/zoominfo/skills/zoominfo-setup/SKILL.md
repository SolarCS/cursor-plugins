---
name: zoominfo-setup
description: >-
  First-run setup for the CipherHealth ZoomInfo MCP plugin. Use when ZoomInfo MCP
  is missing, errored, needs authentication, or the user asks how to connect
  ZoomInfo in Cursor.
---

# CipherHealth ZoomInfo MCP setup

## 1. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **zoominfo** (from the CipherHealth ZoomInfo plugin)
3. Toggle on if disabled
4. Click **Connect** and sign in with your ZoomInfo account in the browser

No API keys or env vars are required.

## 2. Verify

After Connect, ZoomInfo tools should appear. Try a simple lookup in chat, e.g. "Find Acme Health in ZoomInfo."

## Common failures

| Symptom | Fix |
|---------|-----|
| Server errored | Connect via **Settings → Tools & MCP**, not chat |
| OAuth fails | Use your personal ZoomInfo credentials with MCP/API access |
| Tools missing | Plugin not installed — check team marketplace **Required** setting |
| Connect loop | Toggle server off/on to re-trigger OAuth |

If native OAuth fails, see the [ZoomInfo MCP plugin README](https://github.com/Zoominfo/zoominfo-mcp-plugin) for the `mcp-remote` bridge fallback (requires Node.js).
