---
name: anaf-setup
description: First-time setup guide for the ANAF e-Factura MCP — walks through obtaining OAuth credentials, configuring env vars in Claude Code, and authenticating for a company. Use when the user wants to set up ANAF invoicing, says "set up ANAF", "configure ANAF", or gets auth errors from ANAF tools.
---

# ANAF MCP First-Time Setup

## Prerequisites

You need an ANAF OAuth application. If you don't have one, get it at the ANAF developer portal (logincert.anaf.ro). You need:
- `ANAF_CLIENT_ID` — your OAuth app client ID
- `ANAF_CLIENT_SECRET` — your OAuth app secret
- `ANAF_REDIRECT_URI` — must be `https://localhost:9002/callback` (or another HTTPS localhost port)

## Step 1 — Configure env vars in Claude Code

Run this to open MCP settings:

```
/mcp
```

Or add directly to your `~/.claude.json` project config (find the `anaf` entry under `mcpServers`) and set:

```json
"env": {
  "ANAF_CLIENT_ID": "your-client-id",
  "ANAF_CLIENT_SECRET": "your-client-secret",
  "ANAF_REDIRECT_URI": "https://localhost:9002/callback",
  "ANAF_ENV": "prod"
}
```

After saving, restart the MCP server (type `/mcp` and reconnect).

## Step 2 — Authenticate for your company

Tell Claude:

> "Authenticate me for ANAF company CUI 12345678"

Claude will call `anaf_auth_login`, return a URL, ask you to open it in your browser, and then call `anaf_auth_complete` to finish.

After this, all ANAF tools work automatically. Tokens are stored at `~/.local/share/anaf-cli/tokens/_default.json`.

## Step 3 — Verify it works

> "Look up company CUI 30498862"

Claude calls `anaf_lookup_company` (no auth needed) and returns company details. If that works, you're all set.

## Switching companies

> "Switch my active ANAF company to CUI 87654321"

Claude calls `anaf_switch_company`. No re-authentication needed — the token is shared across companies you've previously authenticated.

## Troubleshooting

| Error | Fix |
|---|---|
| `BAD_CONFIG: Missing ANAF_CLIENT_ID` | Set env vars and restart MCP |
| `NO_PENDING_AUTH` | Call anaf_auth_login first |
| `CLIENT_SECRET_MISSING` | Set ANAF_CLIENT_SECRET in env |
| `AUTH_FAILED` | Re-run anaf_auth_login, ensure ANAF_REDIRECT_URI matches your app |
