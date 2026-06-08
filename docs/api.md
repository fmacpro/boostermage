# Boostermage REST API Reference

**Base URL:** `https://api.boostermage.com`

A read-only REST API serving MTG sealed product pricing data. All endpoints return JSON. Authentication is optional (provides higher rate limits).

## Authentication

Include an API key via the `Authorization` header:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.boostermage.com/api/v1/products
```

Without a key, requests are rate-limited to 100 req/min. With a key, 1000 req/min.

## Rate Limiting

Rate limit information is returned in response headers:

| Header                  | Description                           |
| ----------------------- | ------------------------------------- |
| `X-RateLimit-Limit`     | Max requests per minute               |
| `X-RateLimit-Remaining` | Requests remaining in current window  |
| `X-RateLimit-Reset`     | Unix timestamp when the window resets |
| `X-Auth-Status`         | `anonymous` or `bot`                  |

## Endpoints

### Health

```
GET /api/v1/health
```

Returns server status and database connectivity.

### Products

#### Search Products

```
GET /api/v1/products
```

| Param      | Type   | Default | Description                        |
| ---------- | ------ | ------- | ---------------------------------- |
| `q`        | string | —       | Search query (matches name and ID) |
| `set`      | string | —       | Filter by set slug                 |
| `category` | string | —       | Filter by category                 |
| `limit`    | number | 50      | Max results (max 200)              |

#### Product Details

```
GET /api/v1/products/:id/details
```

Returns rich product information from the official catalog, including description, contents, and features.

#### Price History

```
GET /api/v1/products/:id/history
```

| Param      | Type   | Default | Description               |
| ---------- | ------ | ------- | ------------------------- |
| `retailer` | string | —       | Filter by retailer ID     |
| `days`     | number | 90      | Lookback period (max 730) |

Returns time-series price observations for a product.

#### Best Price

```
GET /api/v1/products/:id/best-price
```

Returns the cheapest in-stock price across all retailers.

#### Price Range

```
GET /api/v1/products/:id/price-range
```

| Param  | Type   | Default | Description               |
| ------ | ------ | ------- | ------------------------- |
| `days` | number | 365     | Lookback period (max 730) |

Returns lowest, highest, and average recorded prices.

#### Deals (Below Market Average)

```
GET /api/v1/products/deals/list
```

| Param          | Type   | Default | Description                 |
| -------------- | ------ | ------- | --------------------------- |
| `min_discount` | number | 5       | Minimum discount percentage |
| `limit`        | number | 20      | Max results (max 100)       |

Products currently priced below their market average.

#### Price Drops

```
GET /api/v1/products/price-drops/list
```

| Param      | Type   | Default | Description               |
| ---------- | ------ | ------- | ------------------------- |
| `hours`    | number | 24      | Lookback window (max 168) |
| `limit`    | number | 20      | Max results (max 100)     |
| `min_drop` | number | 0       | Minimum drop percentage   |

Products where the current best price dropped below the historical average.

#### Recently Restocked

```
GET /api/v1/products/recently-restocked/list
```

| Param          | Type   | Default    | Description               |
| -------------- | ------ | ---------- | ------------------------- |
| `hours`        | number | 24         | Lookback window (max 168) |
| `limit`        | number | 20         | Max results (max 100)     |
| `availability` | string | `in-stock` | `in-stock` or `pre-order` |

Products that recently transitioned from out-of-stock to available.

#### Overpriced

```
GET /api/v1/products/overpriced/list
```

| Param            | Type   | Default | Description                             |
| ---------------- | ------ | ------- | --------------------------------------- |
| `limit`          | number | 20      | Max results (max 100)                   |
| `min_overpriced` | number | 10      | Minimum overpriced percentage (max 500) |

Products priced above their market average.

#### In Stock

```
GET /api/v1/products/in-stock/list
```

| Param          | Type   | Default              | Description                |
| -------------- | ------ | -------------------- | -------------------------- |
| `availability` | string | `in-stock,pre-order` | Comma-separated list       |
| `category`     | string | —                    | Filter by product category |
| `limit`        | number | 30                   | Max results (max 100)      |

#### By Set

```
GET /api/v1/products/by-set/:slug
```

| Param   | Type   | Default | Description           |
| ------- | ------ | ------- | --------------------- |
| `limit` | number | 50      | Max results (max 200) |

All products in a specific set with current prices.

### Retailers

#### List Retailers

```
GET /api/v1/retailers
```

Returns all tracked UK retailers.

#### Retailer Products

```
GET /api/v1/retailers/:id/products
```

| Param   | Type   | Default | Description           |
| ------- | ------ | ------- | --------------------- |
| `limit` | number | 50      | Max results (max 200) |

Products available at a specific retailer.

### Prices

#### Latest Prices

```
GET /api/v1/prices/latest
```

| Param   | Type   | Default | Description           |
| ------- | ------ | ------- | --------------------- |
| `limit` | number | 100     | Max results (max 500) |

Most recent price snapshot across all products and retailers.

#### Best Prices

```
GET /api/v1/prices/best
```

| Param   | Type   | Default | Description           |
| ------- | ------ | ------- | --------------------- |
| `limit` | number | 100     | Max results (max 500) |

Cheapest in-stock price per product, sorted ascending.

### Releases

#### Upcoming Releases

```
GET /api/v1/releases/upcoming
```

| Param   | Type   | Default | Description          |
| ------- | ------ | ------- | -------------------- |
| `limit` | number | 20      | Max results (max 50) |

Upcoming MTG release schedule with confirmed dates.

## OpenAPI Spec

An OpenAPI 3.1 specification is available at:
**https://boostermage.com/openapi.json**
