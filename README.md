# Houzz Professionals Directory MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-houzz-professionals/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-houzz-professionals) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-houzz-professionals%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-houzz-professionals&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-houzz-professionals)](https://www.npmjs.com/package/@mambalabsdev/mcp-houzz-professionals) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-houzz-professionals)](https://www.npmjs.com/package/@mambalabsdev/mcp-houzz-professionals) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-houzz-professionals)](https://github.com/mambalabsdev/mcp-houzz-professionals/blob/main/LICENSE)

An MCP server for the Mamba Labs Houzz Professionals Directory actor on Apify. Houzz home services pros as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes Houzz categories and US or Canadian cities, or Houzz directory URLs, and returns one row per professional listed, with phone, address, rating, review count, and typical job cost.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-houzz-professionals": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-houzz-professionals"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_houzz_professionals` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 30 general contractors in Denver, CO on Houzz with their phone numbers."
- "List kitchen remodelers in Austin, TX on Houzz rated 4.5 or higher."

## Tool

`find_houzz_professionals`. One tool. Example arguments:

```json
{
  "categories": [
    "general contractor"
  ],
  "locations": [
    "Denver, CO"
  ],
  "max_results_per_search": 15
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `categories` | array | no | Houzz professional categories, such as general contractor, plumber, roofer, interior designer, kitchen remodelers, or a Houzz category slug such as general-contractor. One search per category per place. Houzz has 64 categories; a name Houzz does not know returns a free summary row. |
| `locations` | array | no | US or Canadian cities as City, ST, for example Denver, CO or Toronto, ON. Put each place on its own line. A place Houzz does not recognize, or resolves to a different city, returns a free summary row. |
| `start_urls` | array | no | Optional. Houzz directory pages, for example https://www.houzz.com/professionals/general-contractor/c/Denver--CO. Profile pages are not read. |
| `max_results_per_search` | number | no | Professional rows to return for each category and place, or each URL, counting sponsored cards when they are included. Houzz lists 15 organic professionals a page. Default 15, maximum 1500. |
| `include_sponsored` | boolean | no | yes (default) returns the paid placements Houzz mixes into the results, labeled sponsored and without a rank. no returns organic results only. |
| `dedupe` | boolean | no | yes (default) returns each professional once per run, so a professional found by two searches, or shown again as a sponsored card on a later page, is charged once. no returns it again each time, charged each time. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `pro-row`, one professional | $0.002 | $0.0019 | $0.0018 | $0.0017 |
| `apify-actor-start`, per run start | $0.004 | $0.004 | $0.004 | $0.004 |

Summary rows and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/houzz-professionals](https://apify.com/mambalabs/houzz-professionals)

## License

MIT. See [LICENSE](LICENSE).
