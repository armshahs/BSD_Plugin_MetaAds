# BSD Meta Ads

Blue Sense Digital plugin for Claude. It reviews Meta ads performance and creates or updates paused campaigns and ad sets. The MCP server is not in this repository. Tool calls go to the BSD Meta Ads MCP after the user signs in.

## Add the marketplace

On claude.ai or in Claude Desktop, open Customize, then Plugins, then Add, then Add marketplace, then Add from a repository. Enter one of these and select Sync:

- `https://github.com/armshahs/BSD_Plugin_MetaAds`
- `armshahs/BSD_Plugin_MetaAds`

The repository is public, so this step does not need the Claude GitHub App. Turn on Sync automatically so each push to `main` reaches accounts that added this marketplace.

After Sync finishes, open the plugin and select Add if it is not already on the account. Then open its Connectors tab, select Add, and connect it. The skills load before that connection. The Meta tools stay unreachable until the connector shows Connected.

A BSD account is required. A person without a BSD account cannot call the ads tools.

On a Team or Enterprise plan, an Owner controls whether members can add their own marketplaces, and an Owner adds the connector for the organization when a member cannot add it.

## What is in this repository

The marketplace catalog is `.claude-plugin/marketplace.json`. The plugin itself is in `plugin/`. A developer can load a local checkout for one session with `claude --plugin-dir ./plugin`.

This repository is not listed in Anthropic's directory. Each person adds the same GitHub URL.
