# Lucra plugin

Run creator marketing from Claude, ChatGPT and Codex. The plugin connects your Lucra account through Lucra's MCP server and adds skills for the jobs brands and agencies do every day: reviewing creator work, reading ad results by creator, launching programs, paying creators and working across client brands.

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

**MCP server:** `https://api.onlucra.com/api/mcp` (streamable HTTP, OAuth 2.1 with dynamic client registration). Each kind of record has a find tool (`programs_find`, `submissions_find`…: pass `id` for one, or filters to list), each change is its own tool (`programs_create`, `campaigns_update`, `payments_create`…), and `ad_results` reads performance, plus:

| Tool | What it does |
| --- | --- |
| `tally` | Counts, sums and ranks across every page of a list tool |
| `lucra_docs` | Searches and reads Lucra's help docs |

A read-only connection gets only the read tools.

**Skills:** `get-started`, `review-creator-work`, `ad-performance`, `launch-program`, `pay-creators`, `partner-clients`, and for creators connected as themselves, `creator-work`.

## Install

- **Claude Code:** `/plugin marketplace add on-lucra/lucra-plugin`, then `/plugin install lucra@lucra`.
- **Codex:** `codex plugin marketplace add on-lucra/lucra-plugin`, then install Lucra from the Plugins Directory.
- **Claude.ai and ChatGPT:** add Lucra from the connector or plugin directory.

On first use, sign in to Lucra and pick the brand or partner workspace to connect. Choose read-only if you only want answers.

## Data and permissions

The plugin acts as the Lucra member who connected it, with their role, and only in the workspaces they can reach. Lucra's tools read and change data in that Lucra account; nothing else on your computer is read. Anything that spends or moves money, launches ads, or ends, archives or removes something asks you to confirm first. Credentials such as new secrets are never sent to the model; you copy them in Lucra.

Privacy policy: https://www.onlucra.com/privacy · Terms: https://www.onlucra.com/terms · Support: https://www.onlucra.com/docs/mcp

## License

MIT
