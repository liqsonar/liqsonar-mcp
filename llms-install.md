# Installing the LiqSonar MCP server

LiqSonar is a hosted (remote) MCP server. Nothing needs to be installed or built.

1. Add a remote MCP server with the URL `https://liqsonar.com/mcp` and the Streamable HTTP transport.
2. Authentication, pick one:
   - OAuth: leave headers empty. The client gets a 401 with `resource_metadata`, registers itself and opens the LiqSonar sign-in page. The user signs in to a LiqSonar Pro account.
   - API key: send `Authorization: Bearer lsk_...` with a Pro API key from https://liqsonar.com/api-docs.
3. Example config for clients that read `mcpServers`:

```json
{
  "mcpServers": {
    "liqsonar": {
      "type": "http",
      "url": "https://liqsonar.com/mcp"
    }
  }
}
```

With an API key instead of OAuth:

```json
{
  "mcpServers": {
    "liqsonar": {
      "type": "http",
      "url": "https://liqsonar.com/mcp",
      "headers": { "Authorization": "Bearer lsk_YOUR_KEY" }
    }
  }
}
```

4. Check the connection by asking for `get_signals` or `get_verdict` with `symbol: "BTCUSDT"`.
