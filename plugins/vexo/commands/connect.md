---
description: Connect to Vexo and show what you can ask about your app analytics, replays, and errors
---

You are helping the user get started with the **Vexo MCP server**, which exposes their Vexo analytics, session
replays, and errors as tools.

Do the following:

1. Check whether the `vexo` MCP server is connected and authenticated. If any `vexo` MCP tools are available (for
   example `list_apps`), it is connected.
   - If the tools are **not** available or calls return an authentication error, tell the user to run `/mcp`, select
     **vexo**, and choose **Authenticate** to sign in through the browser. (On Claude Desktop or Cursor, point them to
     the README for adding a personal access token.)
2. Once connected, call `list_apps` to show the user their apps and ids.
3. Briefly explain what they can ask, with concrete examples:
   - "How many users did <app> have in the last 7 days?" (get_stats)
   - "Top 10 screens by errors last week for <app>" (query_events)
   - "Show me last week's replays with rage taps, and walk me through the longest one" (list_replays,
     get_session_timeline)
   - "What are the newest open errors, and what led up to the top one?" (list_error_groups, get_error_group,
     get_session_timeline)
   - "How is the signup funnel converting by app version?" (list_dashboards, get_funnel)
4. Mention that reads are always allowed. Resolving or ignoring an error (set_error_group_status) and commenting on a
   session (add_session_comment) need a connection with the `mcp:write` scope; the README's "Allow changes" section
   shows how to add one.

Keep it short and action-oriented. If the user already asked a question, answer it using the appropriate Vexo tool
instead of just explaining.
