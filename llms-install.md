# Installing the RealUptime MCP server

RealUptime's MCP server is hosted. Do not clone, build or run anything.

1. Add a remote (Streamable HTTP) server named `realuptime` with URL
   `https://mcp.realuptime.io/public`. No authentication is needed.
2. If the user wants their own monitors, incidents, status pages or error
   issues, ask them for a RealUptime API key (created at
   https://dashboard.realuptime.io/account/api-keys, free plan included),
   then use URL `https://mcp.realuptime.io/mcp` instead and send the header
   `Authorization: Bearer <key>`.
3. Verify by calling `is_service_down` with `service: "github"`.

Cline settings example:

```json
{
  "mcpServers": {
    "realuptime": {
      "type": "streamableHttp",
      "url": "https://mcp.realuptime.io/public"
    }
  }
}
```
