# Boostermage MCP Server

**Endpoint:** `https://mcp.boostermage.com/mcp`

A Model Context Protocol (MCP) server providing live MTG sealed product pricing data. Supports Streamable HTTP (recommended) and SSE transports.

## Transport

### Streamable HTTP (Recommended)

```
URL: https://mcp.boostermage.com/mcp
Type: streamable-http
```

### SSE (Legacy)

```
URL: https://mcp.boostermage.com/sse
Messages: https://mcp.boostermage.com/messages
Type: sse
```

## Tools

The server provides 15 tools for querying MTG pricing data:

### Product Lookup

| Tool                  | Description                                      | Parameters                               |
| --------------------- | ------------------------------------------------ | ---------------------------------------- |
| `search_products`     | Search MTG products by name, set, or category    | `query`, `set_slug`, `category`, `limit` |
| `get_product_details` | Get official description, contents, and features | `product_id`                             |
| `get_set_products`    | Get all products in a set with current prices    | `set_slug`, `limit`                      |

### Pricing

| Tool                | Description                                            | Parameters                          |
| ------------------- | ------------------------------------------------------ | ----------------------------------- |
| `find_best_price`   | Find the cheapest in-stock or pre-order price           | `product_id`                        |
| `compare_prices`    | Compare a product's current price across all retailers | `product_id`                        |
| `get_price_history` | Get compact daily history and recorded range            | `product_id`, `retailer_id`, `days` |
| `get_price_range`   | Get lowest, highest, and average recorded price        | `product_id`, `days`                |

### Deals & Discovery

| Tool                      | Description                                | Parameters                          |
| ------------------------- | ------------------------------------------ | ----------------------------------- |
| `find_deals`              | Products priced below average market price | `min_discount`, `limit`             |
| `find_overpriced`         | Products priced above average market price | `limit`, `min_overpriced`           |
| `get_price_drops`         | Products that dropped in price recently    | `hours`, `limit`, `min_drop`        |
| `find_recently_restocked` | Products that recently became available    | `hours`, `limit`, `availability`    |
| `find_in_stock`           | Products currently in stock or pre-order   | `availability`, `category`, `limit` |

### Retailers & Releases

| Tool                    | Description                               | Parameters             |
| ----------------------- | ----------------------------------------- | ---------------------- |
| `get_retailer_list`     | List all tracked UK retailers             | —                      |
| `get_retailer_products` | Products available at a specific retailer | `retailer_id`, `limit` |
| `get_upcoming_releases` | Upcoming MTG release schedule             | `limit`                |

## Output Schemas

All tools include `outputSchema` declarations and return `structuredContent` for typed responses. The MCP server wraps the public REST API's safe `boostermage_url` fields rather than constructing or exposing retailer destinations. Retailer and affiliate destination URLs are deliberately omitted at the API source.

## Annotations

All tools are annotated as:

- `readOnlyHint: true` — No write operations
- `destructiveHint: false` — Not destructive
- `openWorldHint: false` — Reads from internal database, not the open web

## Authentication

The MCP server does not require authentication for basic access. For higher rate limits, pass an API key to the underlying REST API (the MCP server forwards it automatically).

## Registry

Published on the [MCP Registry](https://registry.modelcontextprotocol.io) as `com.boostermage/mtg-prices`.

## Client Configuration

### VS Code (`mcp.json`)

```json
{
  "servers": {
    "boostermage": {
      "type": "http",
      "url": "https://mcp.boostermage.com/mcp"
    }
  }
}
```

### Codex CLI

```bash
codex mcp add boostermage --url https://mcp.boostermage.com/mcp
```

### Claude Desktop

```json
{
  "mcpServers": {
    "boostermage": {
      "type": "http",
      "url": "https://mcp.boostermage.com/mcp"
    }
  }
}
```

### Cursor

```
Settings → Features → MCP Servers → Add new MCP server
URL: https://mcp.boostermage.com/mcp
Type: streamable-http
```
