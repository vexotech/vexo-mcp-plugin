# Vexo MCP

Ask your AI coding tools about your [Vexo](https://www.vexo.co) analytics, session replays, and errors. The Vexo MCP
server is at `https://api.vexo.co/mcp` and speaks the Model Context Protocol over HTTP (protocol version
`2025-06-18`). Every tool works only on the apps your account can access: the apps you own and the apps a team shares
with you.

## Tools

Read tools work with every connection:

| Tool | What it does |
| --- | --- |
| `list_apps` | Lists the apps you can access, with the id every other tool takes as `app_id`. |
| `query_events` | Answers a plain-language analytics question about one app, for example "top 10 screens by errors last week". Returns rows and the SQL it ran. |
| `get_stats` | Returns an app's total events, distinct users, and distinct sessions in a time window. |
| `list_replays` | Lists session replays, newest or longest first, with filters for errors, rage taps, user, screen, app version, and OS. |
| `get_session_timeline` | Reads one session's events in time order: screens, taps, custom events, network requests, logs, and errors. |
| `list_error_groups` | Lists deduplicated errors with counts, app versions, triage status, and assignee. |
| `get_error_group` | Returns one error's newest occurrence with its stack trace, and the sessions that hit it with their replays. |
| `list_dashboards` | Lists dashboards and the saved insights (trends and funnels) on each. |
| `get_insight` | Runs a saved insight over a time window and returns the numbers the dashboard shows. |
| `get_funnel` | Returns a saved funnel's conversion per step, optionally broken down by OS, app version, country, or an event property. |
| `list_cohorts` | Lists saved cohorts and their definitions. |
| `count_cohort` | Counts the users in a saved cohort over a time window. |
| `list_heatmap_screens` | Lists heatmap screens with their tap counts. |

Write tools need the `mcp:write` scope (see [Allow changes](#allow-changes)):

| Tool | What it does |
| --- | --- |
| `set_error_group_status` | Sets an error group to `OPEN`, `RESOLVED`, or `IGNORED`. Needs write access to the app. |
| `add_session_comment` | Adds a comment to a session, optionally pinned to a playback position. |

Tools that read events take a time window as `from` and `to` in milliseconds since the Unix epoch. It defaults to the
last 28 days and can span at most 366 days. For every parameter, see the
[MCP tool reference](https://docs.vexo.co/settings/mcp-server#tool-reference).

## Install in Claude Code

Add this marketplace, then install the plugin:

```
/plugin marketplace add vexotech/vexo-mcp-plugin
/plugin install vexo@vexo
```

The plugin registers the `vexo` MCP server. To sign in:

1. Run `/mcp`.
2. Select **vexo**, and choose **Authenticate**. A browser window opens.
3. Sign in to Vexo, and on **Authorize access**, click **Approve**.

Then ask questions in plain language, or run `/vexo:connect` to see your apps and example prompts.

The plugin's connection is read-only. To let Claude Code change data, see [Allow changes](#allow-changes).

## Allow changes

The write tools need an OAuth token with the `mcp:write` scope. Claude Code asks for the scopes in a server's
`oauth.scopes` setting, so add a second, write-enabled server for your user:

```
claude mcp add-json --scope user vexo-write '{"type":"http","url":"https://api.vexo.co/mcp","oauth":{"scopes":"mcp mcp:write"}}'
```

Then run `/mcp`, select **vexo-write**, and choose **Authenticate**. The **Authorize access** screen says that the
connection can make changes. Without the scope, a write tool returns an error that names `mcp:write`.

## Install in Claude Desktop or Cursor

These clients connect with a static config entry. Create a
[personal access token](https://docs.vexo.co/settings/api-tokens) in the Vexo dashboard, then add the server to your
MCP config (`claude_desktop_config.json` for Claude Desktop, or your Cursor MCP settings), and replace
`YOUR_VEXO_TOKEN` with your token:

```json
{
  "mcpServers": {
    "vexo": {
      "type": "http",
      "url": "https://api.vexo.co/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_VEXO_TOKEN"
      }
    }
  }
}
```

A personal access token is read-only: it can call every read tool but no write tool.

## Support

- Docs: [MCP server](https://docs.vexo.co/settings/mcp-server)
- Website: https://www.vexo.co

## License

MIT. See [LICENSE](./LICENSE).
