---
name: seismic-setup
description: >-
  First-run setup for the CipherHealth Seismic MCP plugin. Use when Seismic MCP
  is missing, errored, needs authentication, or the user asks how to connect
  Seismic in Cursor.
---

# CipherHealth Seismic MCP setup

## 1. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **Seismic** (from the CipherHealth Seismic plugin)
3. Toggle on if disabled
4. Click **Connect** and sign in with your **cipherhealth.com** Seismic account

No API keys or env vars are required.

## 2. Verify

After Connect, Seismic tools should appear. Try searching for a deck or enablement asset in chat.

## Common failures

| Symptom | Fix |
|---------|-----|
| Server errored | Connect via **Settings → Tools & MCP**, not chat |
| Auth fails | User must have access to the **cipherhealth.com** Seismic tenant |
| Tools missing | Plugin not installed — check team marketplace **Required** setting |
