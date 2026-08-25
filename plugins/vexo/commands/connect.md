---
description: Connect to Vexo and show what you can ask about your app analytics
---

You are helping the user get started with the **Vexo MCP server**, which exposes
their Vexo React Native analytics and session-replay data as read-only tools.

Do the following:

1. Check whether the `vexo` MCP server is connected and authenticated. If any
   `vexo` MCP tools are available (for example `list_apps`), it is connected.
   - If the tools are **not** available or calls return an authentication error,
     tell the user to run `/mcp`, select **vexo**, and choose **Authenticate** to
     sign in through the browser. (On Claude Desktop or Cursor, point them to the
     README for adding a token.)
2. Once connected, call `list_apps` to show the user their apps and ids.
3. Briefly explain what they can ask, with concrete examples:
   - "How many users did <app> have in the last 7 days?" (get_stats)
   - "Top 10 screens by errors last week for <app>" (query_events)
   - "Daily active users for <app> this month" (query_events)
4. Remind them everything is **read-only** and scoped to their own apps.

Keep it short and action-oriented. If the user already asked a question, answer
it using the appropriate Vexo tool instead of just explaining.
