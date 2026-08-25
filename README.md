# Vexo MCP

Query your [Vexo](https://www.vexo.co) React Native analytics and session-replay
data from your AI coding tools. The Vexo MCP server exposes a small set of
**read-only** tools, scoped to your own apps:

- `list_apps` — list the apps you have access to (id and name).
- `query_events` — ask a plain-language analytics question about one app
  (for example, "top 10 screens by errors last week"). Returns rows plus the
  generated SQL.
- `get_stats` — headline metrics for one app over a time window: total events,
  distinct users, distinct sessions.

The server lives at `https://api.vexo.co/mcp` and speaks the Model Context
Protocol over HTTP (protocol version `2025-06-18`).

## Install in Claude Code

Add this marketplace, then install the plugin:

```
/plugin marketplace add vexotech/vexo-mcp-plugin
/plugin install vexo@vexo
```

The plugin registers the `vexo` MCP server automatically. To sign in, run:

```
/mcp
```

Select **vexo** and choose **Authenticate** — a browser window opens for you to
log in to Vexo. After that, just ask questions in natural language, or run
`/vexo:connect` to see your apps and example prompts.

## Install in Claude Desktop or Cursor

These clients connect via a static config entry. Add the following to your MCP
config (`claude_desktop_config.json` for Claude Desktop, or your Cursor MCP
settings), replacing the token with one from your Vexo dashboard:

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

## Authentication

- **Claude Code:** browser sign-in via `/mcp` → **Authenticate** (OAuth). No token
  handling required.
- **Claude Desktop / Cursor:** paste a Vexo token into the `Authorization` header,
  as shown above.

All tools are read-only and return only data from apps your account can access.

## Support

- Docs: https://docs.vexo.co
- Website: https://www.vexo.co

## License

MIT — see [LICENSE](./LICENSE).
