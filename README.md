# ANAF Claude Plugins

Claude Code plugins for Romanian ANAF e-Factura invoicing.

## Add this marketplace

```bash
/plugin marketplace add florin-szilagyi/anaf-claude-plugins
```

## Available plugins

### anaf-mcp

ANAF e-Factura MCP server — create, validate, upload and manage Romanian e-invoices directly from Claude Code.

**Install:**
```bash
/plugin install anaf-mcp@anaf-claude-plugins
```

**What you get:**
- 10 MCP tools: authenticate, lookup companies, build UBL XML, validate, upload, check status, download, list messages
- 3 skills: `anaf-setup`, `anaf-invoice`, `anaf-messages`
- Auto-configured `npx @florinszilagyi/anaf-mcp` MCP server

**Quick start:**
1. Get ANAF OAuth credentials from the ANAF developer portal
2. Install the plugin and set `ANAF_CLIENT_ID`, `ANAF_CLIENT_SECRET`, `ANAF_REDIRECT_URI` in MCP env
3. Ask Claude: "Set up ANAF for company CUI 12345678"
4. Ask Claude: "Create an invoice for client XYZ for 1000 RON consulting services"

See the [anaf-setup skill](plugins/anaf-mcp/skills/anaf-setup.md) for detailed configuration.
