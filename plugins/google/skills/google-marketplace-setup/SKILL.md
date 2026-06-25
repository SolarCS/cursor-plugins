---
name: google-marketplace-setup
description: >-
  First-run setup for the CipherHealth Google Marketplace MCP plugin. Use when
  Google MCP is missing, errored, needs authentication, or the user asks how to
  connect Google Workspace tools (Calendar, Gmail, Drive) in Cursor.
---

# CipherHealth Google Marketplace MCP setup

This plugin connects to the CipherHealth-hosted Google Marketplace MCP proxy.

## 1. Connect in Cursor

1. **Settings → Tools & MCP**
2. Find **google** (from the CipherHealth Google Marketplace plugin)
3. Toggle on if disabled
4. Click **Connect** and sign in with your Google account when prompted

## 2. Verify

After Connect, Google MCP tools should appear. Try a simple request in chat, e.g. "List my calendars" or "Search my recent Gmail."

## Common failures

| Symptom | Fix |
|---------|-----|
| Server errored | Connect via **Settings → Tools & MCP**, not chat |
| OAuth fails | Use a Google account authorized for your org's marketplace app |
| Tools missing | Plugin not installed — check team marketplace **Required** setting |
| Connect loop | Toggle server off/on to re-trigger OAuth |
