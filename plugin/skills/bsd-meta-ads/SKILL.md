---
name: bsd-meta-ads
description: Use for any Meta ads request for a brand the signed-in user can access. Also use when the user asks to run the test skill or confirm the plugin is loaded.
---

# BSD Meta Ads

## Before every chat

Refresh the MCP and the plugin first.

If the BSD MCP is not connected, tell the user to connect it before doing anything else. Do not call tools until it is connected.

If the user only asks to run the test skill or confirm the plugin is loaded, check and then reply accordingly if the BSD Meta Ads plugin is loaded or not and do not call any tools.

## Tools you can call

The connector exposes only `tool_search` and `tool_execute`. Read each tool's declared arguments from the connector. Do not hardcode those parameter names, and do not call anything else.

## Catalog

`tool_search` returns a catalog in this shape:

```json
{ "tools": [ { "name": "start_chat", "title": "Start chat", "toolType": "session", "description": "...", "inputSchema": { } } ] }
```

Choose tools by `toolType`, then check `inputSchema` before every `tool_execute`.

- `toolType` `"session"` is `start_chat`. Call it once so this chat gets a `context_id`.
- `toolType` `"skill"` is a workflow tool. Pick the workflow from these entries. Do not select workflows by a name prefix.

On a new chat, call `tool_search` once. Reuse the tools list. Call `tool_search` again only if that list is no longer available.

## Start the chat

If this chat has no `context_id`, find the tool whose `toolType` is `"session"`. Its name is `start_chat`. Check its `inputSchema`, then `tool_execute` `start_chat`. Keep the returned `context_id` for the whole chat. Do not call `start_chat` again and do not create another id. Also, the `chat_instructions` field will give the steps to follow.

## Choose the workflow

Refer to the the `chat_instructions` field obtained from the `start_chat` tool. That will give all the steps. Follow it.
