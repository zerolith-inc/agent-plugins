# Agent plugins

Official [Zerolith](https://github.com/zerolith-inc) Agent Plugin marketplace. Shared across Zerolith products (starting with [Daran](https://github.com/zerolith-inc/daran)).

Layout is Codex-compatible. Products read `.agents/plugins/marketplace.json` and the plugin trees it lists. Remote MCP servers must declare a real `url` in `.mcp.json` (or inline `mcpServers` on `plugin.json`). ChatGPT `.app.json` ids are not used.

The catalog starts empty. Add a plugin with a PR here, then refresh Official in the product Settings.

## Add a plugin

1. Create `plugins/<name>/`:

```text
plugins/<name>/.codex-plugin/plugin.json
plugins/<name>/.mcp.json
plugins/<name>/skills/   # optional
```

2. Point `plugin.json` at the MCP file:

```json
{
  "name": "<name>",
  "version": "0.1.0",
  "description": "",
  "mcpServers": "./.mcp.json"
}
```

3. Put a public HTTPS MCP URL in `.mcp.json`. Do not use stdio, `command`, or `.app.json`.

```json
{
  "mcpServers": {
    "<server>": {
      "type": "http",
      "url": "https://mcp.example.com/mcp",
      "oauth_resource": "https://mcp.example.com/"
    }
  }
}
```

4. Append an entry to `.agents/plugins/marketplace.json`:

```json
{
  "name": "<name>",
  "source": { "source": "local", "path": "./plugins/<name>" },
  "policy": { "installation": "AVAILABLE", "authentication": "ON_INSTALL" }
}
```

Do not add GitHub or Slack. Those stay native product installations.

## License

Files in this repository are published for Zerolith products to fetch. Vendor MCP endpoints remain owned by those vendors.
