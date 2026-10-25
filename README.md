# Lucra plugin

Run creator marketing from Claude, ChatGPT and Codex. The plugin connects your Lucra account through Lucra's MCP server and adds skills for the jobs brands and agencies do every day: reviewing creator work, reading ad results by creator, launching programs, paying creators and working across client brands. Answers come back as Lucra's own cards and charts where the host shows UI.

## What's inside

```
plugins/lucra/
├── .claude-plugin/plugin.json   Claude Code / Claude plugin manifest
├── .mcp.json                    Claude: Lucra's MCP server
├── plugin.json                  ChatGPT and Codex (Agent Plugins) manifest
├── mcp.json                     ChatGPT and Codex: Lucra's MCP server
├── skills/                      shared by every host
└── assets/                      logos
.claude-plugin/marketplace.json  Claude marketplace for this repo
.agents/plugins/marketplace.json Codex marketplace for this repo
```

**MCP server:** `https://api.onlucra.com/api/mcp` (streamable HTTP, OAuth 2.1 with dynamic client registration). Tools:

| Tool | What it does |
| --- | --- |
| `lucra_endpoints` | Lists Lucra's API paths, filtered by a few words |
| `describe_endpoint` | The exact query and body an endpoint takes |
| `read_lucra` | Reads any Lucra record or list, shown as Lucra cards |
| `change_lucra` | Creates or updates a record (needs a read-and-write connection) |
| `tally_lucra` | Counts, sums and ranks across every page of a list |
| `chart` | Draws a bar, line or donut chart from numbers already read |
| `lucra_docs` | Searches and reads Lucra's help docs |

**Skills:** `get-started`, `review-creator-work`, `ad-performance`, `launch-program`, `pay-creators`, `partner-clients`.

## Install

- **Claude Code:** `/plugin marketplace add on-lucra/lucra-plugin`, then `/plugin install lucra@lucra`.
- **Codex:** `codex plugin marketplace add on-lucra/lucra-plugin`, then install Lucra from the Plugins Directory.
- **Claude.ai and ChatGPT:** add Lucra from the connector or plugin directory.

On first use, sign in to Lucra and pick the brand or partner workspace to connect. Choose read-only if you only want answers.

## Data and permissions

The plugin acts as the Lucra member who connected it, with their role, and only in the workspaces they can reach. Lucra's tools read and change data in that Lucra account; nothing else on your computer is read. Anything that spends or moves money, launches ads, or ends, archives or removes something asks you to confirm first. Credentials such as new API keys are shown to you in the card and are never sent to the model.

Privacy policy: https://www.onlucra.com/privacy · Terms: https://www.onlucra.com/terms · Support: https://www.onlucra.com/docs/mcp

## License

MIT
