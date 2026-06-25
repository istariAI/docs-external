---
description: v2 /fetch bulk lookup, /stats aggregations, /filters/options, health and test.
---

# GOI Public API — Fetch, stats & utilities

Base URL prefix: **`https://api.istari.ai/v2`**.

## `POST /fetch` — bulk domain lookup

Returns current GOI rows for domains you already know. There is **no** relevance ranking.

### Request

```json
{
  "domains": ["stripe.com", "adyen.com", "unknown.example"],
  "columns": ["domain", "name", "country", "nace_code"]
}
```

* **domains** — required, non-empty list, **maximum 5,000** domains per request.  
* **columns** — same rules as search; default `["domain", "name", "country"]`. See [Reference — columns](/api/goi-reference#selectable-columns).

Domains your key is not allowed to see are treated like missing and appear in `metadata.missing`.

### Response

```json
{
  "data": [ … ],
  "metadata": {
    "requested": 3,
    "found": 2,
    "missing": ["unknown.example"]
  }
}
```

---

## `POST /stats` — aggregations (**tier_3**)

Returns `COUNT(*)` buckets over the filtered population. No text or vector scoring — plain SQL grouping.

**Requires tier_3.** Other tiers receive `403`.

### Request (shape)

```json
{
  "group_by": "nace_code",
  "group_by_secondary": "organization_size",
  "date_trunc": "month",
  "filters": { "country": ["Germany"] },
  "date_range": {
    "field": "company_register_date",
    "from_date": "2020-01-01",
    "to_date": "2024-12-31"
  },
  "limit": 100,
  "explain": false
}
```

| Field | Description |
| ----- | ----------- |
| `group_by` | Optional. Primary dimension to bucket by. Omit for a **single total** count. |
| `group_by_secondary` | Optional second dimension (2D breakdown). Requires `group_by`. Must differ from `group_by`. |
| `date_trunc` | `year`, `month`, or `week` — used when a grouping column is a **date** (`company_register_date`, `created_at`). |
| `filters` | Same column filters as `/search`. **`text_keywords` is not supported** in stats. |
| `date_range` | Optional bounds on `company_register_date`, `created_at`, or `updated_at`. |
| `limit` | Max buckets returned (default `100`, max `500`). Ordered by count descending, except date dimensions (chronological ascending). |
| `explain` | `EXPLAIN ANALYZE` in metadata — **tier_3**; uses a longer statement timeout. |

### Allowed `group_by` / `group_by_secondary` columns

Geographic: `continent`, `country`, `country_code`, `state`, `state_code`, `region`, `region_code`, `district`, `district_code`, `municipality`, `municipality_code`.

Classification: `nace_code`, `organization_type`, `organization_size`, `employee_class`, `revenue_class`.

Source / registry: `source`, `company_register_court`.

Array (exploded per value): `summary_keywords`.

Date (use with `date_trunc`): `company_register_date`, `created_at`.

### Response

Each bucket in `data` includes the grouping column value(s) and a `count`. Top-level `elapsed_ms` and `metadata` echo timings, filters, and bucket counts. When `explain` is true, `metadata.explain_plan` contains plan lines.

---

## `GET /filters/options`

Returns JSON suitable for building filter UIs: allowed categorical values, **scoped to your API key’s data access**. No request body.

---

## `GET /health`

Lightweight check that the service can reach the database. Response shape:

```json
{ "healthy": true }
```

or, on failure, `healthy: false` with an `error` message.

---

## `GET /test` (**tier_3**)

Runs an internal parallel smoke suite against search paths. Intended for operators / support, not for application monitoring. Query parameter `explain=true` adds extra diagnostics.

---

## Minimal `curl` — fetch

```bash
curl -sS 'https://api.istari.ai/v2/fetch' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: YOUR_KEY' \
  -d '{"domains":["istari.ai"],"columns":["domain","name","country"]}'
```
