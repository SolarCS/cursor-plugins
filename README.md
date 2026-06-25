# CipherHealth Cursor Plugins

Private team marketplace for the CipherHealth trial. Four plugins — **Salesforce**, **ZoomInfo**, **Seismic**, and **Google Marketplace** — each with its own MCP server and setup skill.

**Repo:** [github.com/SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins)

## Plugins

| Plugin | MCP server | Auth |
|--------|------------|------|
| **CipherHealth Salesforce** | `platform/sobject-reads` (read-only CRM) | OAuth on connect (Consumer Key bundled) |
| **CipherHealth ZoomInfo** | `mcp.zoominfo.com` via `mcp-remote` | OAuth on connect (requires **Node.js**) |
| **CipherHealth Seismic** | `mcp.seismic.com/.../cipherhealth.com` | Seismic MCP app **Client ID** + OAuth |
| **CipherHealth Google Marketplace** | `cipher-mcp-365212235619.us-central1.run.app/mcp` | OAuth on connect |

Salesforce has the Consumer Key bundled. Seismic requires env vars from a Seismic App Registry MCP app. ZoomInfo requires Node.js for the OAuth bridge. Google uses the CipherHealth marketplace proxy — connect via OAuth in Cursor.

## Admin: publish to team marketplace

1. Push to `SolarCS/cursor-plugins`.
2. **Cursor Dashboard → Settings → Plugins → Team Marketplaces**
3. **Import from Repo** (or **Refresh** if already imported) → `https://github.com/SolarCS/cursor-plugins`
4. Grant the **Cursor GitHub App** read access to this repo.
5. Cursor reads `.cursor-plugin/marketplace.json` and discovers all four plugins.
6. Set **Marketplace Access** to **All Members**.
7. Mark each plugin **Required** (or **Optional** per role) → **Save**.

After this restructure, re-import or refresh the marketplace so the old **CipherHealth Integrations** bundle is replaced by the three individual plugins.

See [TEAM-TROUBLESHOOTING.md](./TEAM-TROUBLESHOOTING.md) if plugins work for admins but not teammates.

## Trial user: first run

1. Plugins auto-install (if **Required**).
2. **Settings → Tools & MCP → Connect** for **Salesforce**, **zoominfo**, **Seismic**, and **google**.
3. Test in chat.

## Skills included

| Plugin | Skills |
|--------|--------|
| Salesforce | `salesforce-setup`, `salesforce-queries` |
| ZoomInfo | `zoominfo-setup` |
| Seismic | `seismic-setup` |
| Google Marketplace | `google-marketplace-setup` |

## Repository structure

```
.cursor-plugin/
  marketplace.json
plugins/
  salesforce/
    .cursor-plugin/plugin.json
    mcp.json
    skills/
  zoominfo/
    .cursor-plugin/plugin.json
    mcp.json
    skills/
  seismic/
    .cursor-plugin/plugin.json
    mcp.json
    skills/
  google/
    .cursor-plugin/plugin.json
    mcp.json
    skills/
```

## Maintainers

- Bump `version` in each plugin's `.cursor-plugin/plugin.json` when changing that plugin's `mcp.json` or skills.
- Bump `metadata.version` in `.cursor-plugin/marketplace.json` when changing marketplace-level config.
- Enable **Auto Refresh** on the team marketplace for pushes to `main`.

Internal use only — CipherHealth / SolarCS.
