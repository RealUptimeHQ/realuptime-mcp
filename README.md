# RealUptime MCP server

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for
[RealUptime](https://realuptime.io).

RealUptime is two products on one plan: RealUptime Monitoring (uptime checks, server monitoring and public status pages) and RealUptime Errors (application error tracking), with Outages, a free public "Is X down?" tracker, as a free tool beside them. The MCP server covers all of it: the keyless tools answer from Outages, and the keyed tools work on your uptime checks and heartbeats, status pages and incidents, and error issues.

There is nothing to install. Point any MCP client at one of the two
endpoints below (Streamable HTTP).

| Endpoint | Auth | What it does |
| --- | --- | --- |
| `https://mcp.realuptime.io/public` | none | Read-only outage tools over RealUptime's own check readings of the services it tracks (https://realuptime.io/outages) |
| `https://mcp.realuptime.io/mcp` | API key | Everything above, plus your own monitors, incidents, status pages and error issues |

API keys work on every plan, including Free (no card). Create one at
<https://dashboard.realuptime.io/account/api-keys> and send it as
`Authorization: Bearer <key>`.

MCP clients that support OAuth can sign in with it instead.

Full documentation: <https://docs.realuptime.io/mcp>

## Connect

**Claude Code**

```bash
claude mcp add --transport http realuptime https://mcp.realuptime.io/public
```

**Cline, Cursor, VS Code and other clients that read `mcpServers` JSON**

Keyless:

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

With an API key:

```json
{
  "mcpServers": {
    "realuptime": {
      "type": "streamableHttp",
      "url": "https://mcp.realuptime.io/mcp",
      "headers": { "Authorization": "Bearer YOUR_REALUPTIME_API_KEY" }
    }
  }
}
```

## Tools

Keyless (`/public`, also available on `/mcp`):

- `is_service_down`: do our own checks of a third-party service fail right now, region by region
- `get_regional_readings`: every current per-region reading for one service, with latency and freshness
- `get_report_volume`: how many people report problems with a service right now, beside our own reading
- `list_recent_incidents`: past probe events for one service

With an API key (`/mcp`):

28 more tools over your own account: monitors and heartbeats, status pages and
incidents, maintenance windows, notification channels and error issues. Full
list: https://docs.realuptime.io/mcp

## Listings

- Official MCP registry: `io.realuptime/mcp`

## Support

<https://realuptime.io/support> or support@realuptime.io.

This repository holds the connection documentation only; the server itself
is operated by RealUptime.
