# RealUptime MCP server

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for
[RealUptime](https://realuptime.io): status pages, multi-region uptime
monitoring, error tracking, and free "Is X down?" pages.

There is nothing to install. Point any MCP client at one of the two
endpoints below (Streamable HTTP).

| Endpoint | Auth | What it does |
| --- | --- | --- |
| `https://mcp.realuptime.io/public` | none | Read-only outage tools over RealUptime's own multi-region check readings of popular services |
| `https://mcp.realuptime.io/mcp` | API key | Everything above, plus your own monitors, incidents, status pages and error issues |

API keys work on every plan, including Free (no card). Create one at
<https://dashboard.realuptime.io/account/api-keys> and send it as
`Authorization: Bearer <key>`.

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
- `get_stack`: a "my stack" page, every member service's status in one roll-up
- `internet_weather`: response-time percentiles per check region against a 7-day baseline
- `is_the_internet_down`: whether a shared-infrastructure incident (CDN, cloud region, DNS) is under way

With an API key (`/mcp`):

- Monitors: `get_check_status`, `list_heartbeat_runs`, `create_check`,
  `update_check_regions`, `update_check_assertions`, `delete_check`
- Status pages and incidents: `list_status_pages`, `list_incidents`,
  `create_incident`, `add_incident_update`, `get_active_maintenance_window`,
  `create_maintenance_window`, `end_maintenance_window`
- Errors: `list_error_projects`, `create_error_project`, `set_error_issue_status`

## Listings

- Official MCP registry: `io.realuptime/mcp`
- Smithery: <https://smithery.ai/servers/realuptime/mcp>

## Support

<https://realuptime.io/support> or support@realuptime.io.

This repository holds the connection documentation only; the server itself
is operated by RealUptime.
