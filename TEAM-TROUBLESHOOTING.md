# Team marketplace troubleshooting

Use this guide when **CipherHealth Integrations** works for admins but not for other trial users.

## Two different permission systems

| System | What it controls |
|--------|------------------|
| **GitHub repo access** | Lets the Cursor GitHub App read the repo for the admin dashboard |
| **Cursor Marketplace Access** | Controls which Cursor team members can see and receive plugins from this marketplace |

Granting GitHub access to all org members does **not** install the plugin. Admins must configure **Marketplace Access** in the Cursor dashboard.

## Admin checklist

1. **Cursor Dashboard → Settings → Plugins → Team Marketplaces**
2. Confirm all plugins are listed: **CipherHealth Salesforce**, **CipherHealth ZoomInfo**, **CipherHealth Seismic**, **CipherHealth Google Marketplace**.
3. Set **Marketplace Access** to **All Members** (or a group that includes every trial user).
4. Set the plugin to **Required** (auto-install) or **Optional** (user installs from Customize).
5. Click **Save** — changes are not live until saved.
6. If using a specific group (not All Members), confirm teammates are in that group under **Dashboard → Members**.

After saving, ask teammates to fully quit Cursor (**Cmd+Q**) and reopen.

## Teammate checklist

1. Open **Customize** in the sidebar (not only Settings → Plugins).
2. Look for **CipherHealth Integrations** under your team marketplace.
3. If the plugin is **Optional**, click **Install**.
4. Restart Cursor after install.

## Private repo download issue (common)

For private GitHub repos, Cursor downloads plugin files by running `git clone` on **each user's machine**. Dashboard GitHub App access does not carry over to that step.

**Symptoms:** Plugin name appears in Customize, but skills/MCP/rules never load. `/salesforce-queries` or other skills are not recognized.

**Diagnose on the teammate's machine:**

```bash
# Can they clone the repo?
git clone https://github.com/SolarCS/cursor-plugins.git /tmp/cursor-plugins-test

# Is Cursor's plugin cache empty?
ls -la ~/.cursor/plugins/cache/solarcs-cursor-plugins/
```

If clone fails → fix GitHub auth (`gh auth login` or a PAT with repo read access).

If cache folder exists but has no plugin files → known Cursor bug with private repos. Workarounds:

1. **Recommended for trials:** Make the repo public (no secrets in this repo; credentials are env vars only).
2. **Per-user fix:** Set up git auth, delete empty cache, reinstall:
   ```bash
   rm -rf ~/.cursor/plugins/cache/solarcs-cursor-plugins/
   rm -rf ~/.cursor/plugins/marketplaces/
   ```
   Then reinstall from **Customize** and restart Cursor.
3. **Manual fallback:** Copy the repo into `~/.cursor/plugins/local/cipherhealth-integrations/` (must contain `.cursor-plugin/plugin.json` at the root) and restart Cursor.

## Developer console errors

If issues persist, open **Developer Tools** (Cmd+Shift+I) → **Console** and search for:

- `getTeamRepos`
- `ConnectError`
- `pollRepoBlocklist`

Share those errors with your admin or Cursor support.

## Still stuck?

Contact your Cursor team admin with:

- Your Cursor account email
- Whether you see the plugin in **Customize**
- Output of the clone and cache checks above
- Any console errors
