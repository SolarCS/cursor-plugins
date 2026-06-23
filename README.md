# CipherHealth Cursor Plugins

Private team marketplace for the CipherHealth trial. Three plugins — **Salesforce**, **ZoomInfo**, and **Seismic** — each with its own MCP server and setup skill.

**Repo:** [github.com/SolarCS/cursor-plugins](https://github.com/SolarCS/cursor-plugins)

## Plugins

| Plugin | MCP server | Auth |
|--------|------------|------|
| **CipherHealth Salesforce** | `platform/sobject-reads` (read-only CRM) | OAuth on connect (Consumer Key bundled) |
| **CipherHealth ZoomInfo** | `mcp.zoominfo.com` | OAuth on connect |
| **CipherHealth Seismic** | `mcp.seismic.com/.../cipherhealth.com` | OAuth on connect |

No env vars required. Each user connects via **Settings → Tools & MCP → Connect**.

## Admin: publish to team marketplace

1. Push to `SolarCS/cursor-plugins`.
2. **Cursor Dashboard → Settings → Plugins → Team Marketplaces**
3. **Import from Repo** (or **Refresh** if already imported) → `https://github.com/SolarCS/cursor-plugins`
4. Grant the **Cursor GitHub App** read access to this repo.
5. Cursor reads `.cursor-plugin/marketplace.json` and discovers all three plugins.
6. Set **Marketplace Access** to **All Members**.
7. Mark each plugin **Required** (or **Optional** per role) → **Save**.

After this restructure, re-import or refresh the marketplace so the old **CipherHealth Integrations** bundle is replaced by the three individual plugins.

See [TEAM-TROUBLESHOOTING.md](./TEAM-TROUBLESHOOTING.md) if plugins work for admins but not teammates.

## Trial user: first run

1. Plugins auto-install (if **Required**).
2. **Settings → Tools & MCP → Connect** for **Salesforce**, **zoominfo**, and **Seismic**.
3. Test in chat.

## Skills included

| Plugin | Skills |
|--------|--------|
| Salesforce | `salesforce-setup`, `salesforce-queries` |
| ZoomInfo | `zoominfo-setup` |
| Seismic | `seismic-setup` |

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
```

## Maintainers

- Bump `version` in each plugin's `.cursor-plugin/plugin.json` when changing that plugin's `mcp.json` or skills.
- Bump `metadata.version` in `.cursor-plugin/marketplace.json` when changing marketplace-level config.
- Enable **Auto Refresh** on the team marketplace for pushes to `main`.

Internal use only — CipherHealth / SolarCS.
