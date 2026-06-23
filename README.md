# CipherHealth Cursor Plugins

Private team marketplace plugin for the CipherHealth trial. One plugin, **multiple MCP servers** — auto-installed when marked **Required** for your trial group.

**Repo:** [github.com/SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins)

## Bundled MCP servers

| Server | Endpoint | Auth |
|--------|----------|------|
| **Salesforce** | `platform/sobject-reads` (read-only CRM) | `SF_CLIENT_ID` + OAuth |
| **ZoomInfo** | `mcp.zoominfo.com` | OAuth on connect |
| **Google Calendar** | `calendarmcp.googleapis.com/mcp/v1` | OAuth on connect |
| **Gmail** | `gmailmcp.googleapis.com/mcp/v1` | OAuth on connect |
| **Google Drive** | `drivemcp.googleapis.com/mcp/v1` | OAuth on connect |
| **Seismic** | `mcp.seismic.com/.../cipherhealth.com` | OAuth on connect |
| **looker-toolbox** | `qaloadcipherhealth.cloud.looker.com/mcp` | OAuth on connect |

Only **Salesforce** requires an env var (`SF_CLIENT_ID`). All other servers authenticate when each user clicks **Connect** in Settings → Tools & MCP.

Add more servers by editing `mcp.json` — no separate plugin per integration.

## Admin: publish to team marketplace

1. Push to `SolarCS/cursor-plugins`.
2. **Cursor Dashboard → Settings → Plugins → Team Marketplaces → Add Marketplace**
3. **Import from Repo** → `https://github.com/SolarCS/cursor-plugins`
4. Grant the **Cursor GitHub App** read access.
5. Add **CipherHealth Integrations** to the marketplace.
6. Set **Team Access** to your trial group → **Required** → Save.

### Optional: reduce env-var setup (private repo)

Hardcode `SF_CLIENT_ID` in `mcp.json` (Consumer Key only) so trial users only need OAuth connects.

## Trial user: first run

1. Plugin auto-installs (if **Required**).
2. Set `SF_CLIENT_ID` (Salesforce only), **Cmd+Q** Cursor, reopen.
3. **Settings → Tools & MCP → Connect** for each server (7 total).
4. Test in chat.

```bash
launchctl setenv SF_CLIENT_ID "..."
```

## Skills included

| Skill | Purpose |
|-------|---------|
| `team-integrations-setup` | Connect all bundled MCPs |
| `salesforce-queries` | Account briefs and SOQL patterns |
| `salesforce-setup` | Salesforce troubleshooting |

## Why plugins instead of Team MCP dashboard?

[Team MCP Not Syncing](https://forum.cursor.com/t/team-mcp-not-syncing/160512) — use team marketplace plugins as Cursor's recommended workaround.

## Maintainers

- Bump `version` in `.cursor-plugin/plugin.json` when changing `mcp.json`.
- Enable **Auto Refresh** on the team marketplace for pushes to `main`.

Internal use only — CipherHealth / SolarCS.
