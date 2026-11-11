# BSD Meta Ads

BSD Meta Ads is a Blue Sense Digital plugin for Claude. It reviews Meta ads performance and creates or updates paused campaigns and ad sets. Tool calls go to the BSD Meta Ads MCP after you sign in with a BSD account. A person without a BSD account cannot call the ads tools.

The plugin includes six skills:

- `review-meta-performance` reviews ROAS, spend, and the metrics table.
- `create-paused-campaign` creates one paused Meta campaign.
- `update-paused-campaign` updates one paused Meta campaign.
- `create-paused-ad-set` creates one paused Meta ad set under an existing campaign.
- `update-paused-ad-set` updates one paused Meta ad set.
- `test-skill` confirms the plugin is loaded and calls no tools.

Each skill calls its workflow tool on the MCP server and follows the text that tool returns. The workflow steps are stored on the server. They are not written in these skill files. Changing those steps does not require a plugin release.

Connect the plugin connector before asking Claude to run a skill. The skills load before that connection. The Meta tools stay unreachable until the connector shows Connected. The same chat keeps one context id. A later skill reuses that id and calls start chat only when the chat has none.
