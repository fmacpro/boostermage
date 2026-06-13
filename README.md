# Boostermage

**UK MTG Sealed Product Price Comparison**

Boostermage tracks sealed Magic: The Gathering product prices across UK retailers, helping buyers find the best deals on booster boxes, packs, bundles, decks, and more.

## Features

- **Price comparison** — Compare prices across 54 UK retailers for 383 tracked products
- **Price history** — Track price trends over time (up to 2 years of data)
- **Deals & price drops** — Automatically detected products priced below market average
- **Restock alerts** — Products that recently came back in stock
- **Upcoming releases** — MTG release schedule with confirmed dates
- **Product catalog** — Official descriptions, contents, and features for every product

## Access Methods

### 🌐 Website

**https://boostermage.com**

The main website provides a browser-based interface for browsing products, comparing prices, and viewing set information.

### 📡 REST API

**Base URL:** `https://api.boostermage.com`

A read-only REST API for programmatic access to pricing data.

**Documentation:** [API Reference](./api.md)

**Quick start:**

```bash
# Health check
curl https://api.boostermage.com/api/v1/health

# Search products
curl "https://api.boostermage.com/api/v1/products?q=aetherdrift&limit=5"

# Best price for a product
curl https://api.boostermage.com/api/v1/products/aetherdrift-play-booster/best-price

# Current deals (10%+ off market average)
curl "https://api.boostermage.com/api/v1/products/deals/list?min_discount=10&limit=5"

# Price drops in last 24 hours
curl "https://api.boostermage.com/api/v1/products/price-drops/list?hours=24&limit=5"
```

**Rate limits:** 100 req/min (anonymous), 1000 req/min (with API key)

API listing links use Boostermage product URLs with an optional `retailer`
selector. Retailer destination and affiliate URLs are not exposed.

### 🤖 MCP Server

**Endpoint:** `https://mcp.boostermage.com/mcp`

A Model Context Protocol (MCP) server for AI agents to query pricing data directly. Compatible with Claude, Cursor, GitHub Copilot, and any MCP-compatible client.

**Documentation:** [MCP Server Reference](./mcp.md)

**Quick start (VS Code `mcp.json`):**

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

**Quick start (Codex CLI):**

```bash
codex mcp add boostermage --url https://mcp.boostermage.com/mcp
```

### 📊 Static Data Files

Publicly accessible JSON data files are available at `https://boostermage.com/data/`.

**Documentation:** [Data Feeds](./data-feeds.md)

## Registry

Boostermage is published on the [MCP Registry](https://registry.modelcontextprotocol.io) as `com.boostermage/mtg-prices`.

## Repository

This documentation is maintained at **https://github.com/fmacpro/boostermage**.

---

_Boostermage is an independent UK MTG sealed product price comparison site. Not affiliated with Wizards of the Coast or any retailer._
