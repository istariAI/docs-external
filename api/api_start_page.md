---
description: Programmatic access to the ISTARI Global Organization Index (GOI) via API key — API v2.
---

# GOI Public API (v2)

The **GOI Public API** is the supported HTTP API for querying the **ISTARI Global Organization Index (GOI)**: tens of millions of organisation records across Europe, backed by PostgreSQL with vector (DiskANN) and full-text (BM25) search.

Use it to **discover** companies (keyword, semantic description, similarity to known domains, or filters alone), **look up** known domains in bulk, and (on eligible keys) run **aggregations** and read **filter option** lists.

!!! tip "Interactive reference"
    When exposed for your environment, OpenAPI / Swagger is typically at **`https://api.istari.ai/v2/docs`**.

## Base URL (v2)

All GOI v2 paths are under:

```text
https://api.istari.ai/v2/
```

Examples:

- `POST https://api.istari.ai/v2/search`
- `POST https://api.istari.ai/v2/fetch`

## Authentication

Every request must include your API key:

```http
x-api-key: <your-api-key>
```

Keys are issued for GOI access tiers (`tier_1`, `tier_2`, `tier_3`). Some routes and features require **tier_3** (see linked pages).

## Quick example — search

```bash
curl --location 'https://api.istari.ai/v2/search' \
  --header 'Accept: application/json' \
  --header 'x-api-key: your-api-key' \
  --header 'Content-Type: application/json' \
  --data '{
    "describe": "SaaS companies in the US",
    "keywords": {
      "must_all": [],
      "must_any": [],
      "must_not": []
    },
    "filters": {
      "country": ["United States"],
      "state": [],
      "region": [],
      "organization_type": [],
      "organization_size": [],
      "nace_code": []
    },
    "excludes": [],
    "columns": ["domain"],
    "size": 50
  }'
```

## Endpoints at a glance

Paths are relative to **`https://api.istari.ai/v2`**.

| Method | Path | Purpose |
| ------ | ---- | ------- |
| `POST` | `/search` | Search and rank organisations (modes described in [Search](goi-search.md)) |
| `POST` | `/fetch` | Bulk lookup by domain list — no scoring ([Fetch, stats & utilities](goi-fetch-stats.md)) |
| `POST` | `/stats` | Aggregations (`COUNT` by dimension); **tier_3 only** |
| `GET` | `/filters/options` | Allowed values for categorical filters (scoped to your key) |
| `GET` | `/health` | Liveness / database check |
| `GET` | `/test` | Internal smoke suite — **tier_3 only** |

## Documentation map

* [Search](goi-search.md) — request body, auto-detected modes, keywords, `similar_to`, `describe`, filters, pagination, deduplication  
* [Fetch, stats & utilities](goi-fetch-stats.md) — `/fetch`, `/stats`, `/filters/options`, health and test  
* [Reference: columns, filters, limits & errors](goi-reference.md) — response fields, quotas, HTTP errors  

## Previous ISTARI HTTP API (v1)

If your integration still uses **`https://api.istari.ai/v1/...`** (older search and `fetch-market`-style paths), see **[Legacy API documentation](legacy/api_start_page.md)**. New work should use **GOI v2** at **`https://api.istari.ai/v2/`** (this section).
