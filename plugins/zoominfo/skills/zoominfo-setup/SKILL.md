---
name: zoominfo-setup
description: >-
  First-run setup for the CipherHealth ZoomInfo MCP plugin. Use when ZoomInfo MCP
  is missing, errored, needs authentication, or the user asks how to connect
  ZoomInfo in Cursor.
---

# CipherHealth ZoomInfo MCP setup

This plugin uses the **`mcp-remote` bridge** — Cursor's native HTTP OAuth often fails for ZoomInfo's server.

## 1. Prerequisites

- **Node.js** installed (`node` and `npx` on your PATH). Install via [nodejs.org](https://nodejs.org) or `brew install node`.
- A ZoomInfo account with MCP/API access.

## 2. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **zoominfo** (from the CipherHealth ZoomInfo plugin)
3. Toggle on if disabled
4. Click **Connect** — a browser window opens for ZoomInfo sign-in
5. Approve permissions

On first connect, `npx` downloads `mcp-remote` automatically.

## 3. Verify

After Connect, ZoomInfo tools should appear. Try: "Find Acme Health in ZoomInfo."

## Common failures

| Symptom | Fix |
|---------|-----|
| Server errored immediately | Install Node.js, then restart Cursor |
| `npx: command not found` | Add Node to PATH or reinstall Node.js |
| OAuth fails | Use personal ZoomInfo credentials with MCP access |
| Connect loop | Toggle server off/on; delete `~/.cursor/plugins/cache/` entries and retry |

See the [ZoomInfo MCP plugin](https://github.com/Zoominfo/zoominfo-mcp-plugin) for upstream docs.
