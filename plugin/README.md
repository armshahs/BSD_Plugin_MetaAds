# BSD Meta Ads

BSD Meta Ads is a Blue Sense Digital plugin for Claude. It runs Meta ads tasks for a brand the signed-in user can access. Tool calls go to the BSD Meta Ads MCP after you sign in with a BSD account. A person without a BSD account cannot call the ads tools.

The plugin includes one skill, `bsd-meta-ads`. That skill calls `tool_search` and `tool_execute` on the MCP server. `tool_search` returns the tool catalog. `tool_execute` runs one tool from that catalog. The connector exposes only those two tools.

On a new chat, the skill calls `tool_search`, then runs `start_chat` once. `start_chat` is the tool whose `toolType` is `session`. That call returns a `context_id`. The same chat keeps that id. A later request reuses it and calls `start_chat` only when the chat has none.

Workflow tools have `toolType` `skill`. The skill picks the one whose description matches the request and follows the text that tool returns. The workflow steps are stored on the server. They are not written in the skill file. Adding or changing a workflow does not require a plugin release.

Connect the plugin connector before asking Claude to run the skill. The skill loads before that connection. The Meta tools stay unreachable until the connector shows Connected.

Asking to run the test skill, or to confirm the plugin is loaded, gets one reply: The BSD Meta Ads plugin is loaded. That check calls no tools.
