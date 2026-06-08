# Boostermage Static Data Feeds

Publicly accessible JSON data files are available at `https://boostermage.com/data/`. These are generated periodically and served via Cloudflare Pages.

## Available Files

### `prices.latest.json`

The most recent price snapshot across all tracked products and retailers.

**URL:** `https://boostermage.com/data/prices.latest.json`

```json
{
  "generatedAt": "2026-06-08T01:05:00.000Z",
  "sourceRetailers": ["zatu", "magic-madhouse", ...],
  "results": [
    {
      "product": {
        "id": "aetherdrift-play-booster-display",
        "name": "Aetherdrift Play Booster Display",
        "setName": "Aetherdrift",
        "category": "booster-box",
        "imageUrl": "/cache/wpn/..."
      },
      "listings": [
        {
          "retailerId": "zatu",
          "retailerName": "Zatu Games",
          "title": "Aetherdrift Play Booster Display",
          "url": "https://...",
          "priceGbp": 129.95,
          "availability": "in-stock"
        }
      ],
      "bestPrice": {
        "priceGbp": 125.00,
        "availability": "in-stock"
      }
    }
  ],
  "scrapeMeta": { ... }
}
```

### `catalog.generated.json`

The official product catalog with descriptions, contents, and features.

**URL:** `https://boostermage.com/data/catalog.generated.json`

### `future-sets.generated.json`

Upcoming MTG release schedule with confirmed dates and source attribution.

**URL:** `https://boostermage.com/data/future-sets.generated.json`

### `sets.generated.json`

All known MTG sets with metadata.

**URL:** `https://boostermage.com/data/sets.generated.json`

## Usage Notes

- All files are updated multiple times daily
- Prices are in GBP (£)
- `availability` values: `in-stock`, `out-of-stock`, `pre-order`
- Data is for informational purposes — always verify prices with retailers before purchasing
