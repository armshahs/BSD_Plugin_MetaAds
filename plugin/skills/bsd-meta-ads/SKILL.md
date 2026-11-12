---
name: bsd-meta-ads
description: Use for any Meta ads request for a brand the signed-in user can access. Also use when the user asks to run the test skill or confirm the plugin is loaded.
---

Before every chat, refresh the MCP and the plugin first.

If the BSD MCP is not connected, tell the user to connect it before doing anything else. Do not call tools until it is connected.

The connector exposes only tool_search and tool_execute. Read each tool's declared arguments from the connector. Do not hardcode those parameter names, and do not call anything else.

tool_search returns a catalog in this shape:

{ "tools": [ { "name": "start_chat", "title": "Start chat", "toolType": "session", "description": "...", "inputSchema": { } } ] }

Choose tools by toolType, then check inputSchema before every tool_execute.

toolType "session" is start_chat. Call it once so this chat gets a context_id.

toolType "skill" is a workflow tool. Pick the workflow from these entries. Do not select workflows by a name prefix.

On a new chat, call tool_search once. Reuse the tools list. Call tool_search again only if that list is no longer available.

If this chat has no context_id, find the tool whose toolType is "session". Its name is start_chat. Check its inputSchema, then tool_execute start_chat. Keep the returned context_id for the whole chat. Do not call start_chat again and do not create another id.

After that, look only at tools whose toolType is "skill". Choose the one whose description matches the user's request. If none match, say so. If more than one matches, ask which task they want. Do not invent a workflow.

Check that tool's inputSchema, then tool_execute it with this chat's context_id and the other required arguments. Follow the text it returns.

For each step in that text, find the named tool in the tools list. Before tool_execute, check that every required argument from its inputSchema is present and that no argument outside that schema is sent. If a required value is missing, ask the user. Pass the same context_id on every call.

If the user only asks to run the test skill or confirm the plugin is loaded, reply that the BSD Meta Ads plugin is loaded and do not call any tools.
