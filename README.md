# CipherHealth Cursor Plugins

Private team marketplace plugin for the CipherHealth trial. One plugin, **multiple MCP servers** — auto-installed when marked **Required** for your trial group.

**Repo:** [github.com/SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins)

## Bundled MCP servers

| Server | Endpoint | Auth |
|--------|----------|------|
| **Salesforce** | `platform/sobject-reads` (read-only CRM) | `SF_CLIENT_ID` env + OAuth |
| **ZoomInfo** | `mcp.zoominfo.com` | OAuth on connect |
| **Google Calendar** | Google Calendar MCP | `GOOGLE_CALENDAR_*` env + OAuth |

Add more servers by editing `mcp.json` — no need for a separate plugin per integration.

## Admin: publish to team marketplace

1. Push this repo to `SolarCS/cursor-plugins` (private org repo).
2. **Cursor Dashboard → Settings → Plugins → Team Marketplaces → Add Marketplace**
3. **Import from Repo** → `https://github.com/SolarCS/cursor-plugins`
4. Grant the **Cursor GitHub App** read access on the repo.
5. Add plugin **CipherHealth Integrations** to the marketplace.
6. Set **Team Access** to your trial distribution group.
7. Set install mode to **Required** (auto-installs MCP config for all participants).
8. Save.

### Optional: zero env-var friction (private repo only)

Replace `${env:SF_CLIENT_ID}` in `mcp.json` with the literal Consumer Key. Acceptable in a private org repo; the key is not the client secret.

## Trial user: first run

1. Plugin auto-installs (if Required) — or install from the marketplace panel.
2. Set env vars (see `.env.example`), then **Cmd+Q** and reopen Cursor.
3. **Settings → Tools & MCP** → **Connect** for Salesforce, ZoomInfo, and Google Calendar.
4. Test in chat (e.g. *"What's on my calendar tomorrow?"* or *"Brief me on UCI Health from Salesforce"*).

## Skills included

| Skill | Purpose |
|-------|---------|
| `team-integrations-setup` | Connect all bundled MCPs |
| `salesforce-queries` | Account briefs and SOQL patterns |
| `salesforce-setup` | Salesforce-specific troubleshooting |

## Why this instead of Team MCP dashboard?

[Team MCP Not Syncing](https://forum.cursor.com/t/team-mcp-not-syncing/160512) — dashboard saves config but IDE sync is still rolling out. **Team marketplace plugins** are Cursor's recommended workaround.

## Local testing (before pushing)

```bash
mkdir -p ~/.cursor/plugins/local
ln -sf "$(pwd)" ~/.cursor/plugins/local/cipherhealth-integrations
launchctl setenv SF_CLIENT_ID "YOUR_KEY"
# restart Cursor
```

## Maintainers

- Bump `version` in `.cursor-plugin/plugin.json` when changing `mcp.json` or skills.
- Enable **Auto Refresh** on the team marketplace to pick up pushes to `main`.

Internal use only — CipherHealth / SolarCS.
