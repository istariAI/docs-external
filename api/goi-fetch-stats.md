---
title: "Fetch & statistics"
description: v2 /fetch bulk lookup, /stats aggregations, /filters/options, /locations, and health.
---

Base URL prefix: **`https://api.istari.ai/v2`**.

## `POST /fetch` : bulk domain lookup

Returns current GOI rows for domains you already know. There is **no** relevance ranking.

### Request

```json
{
  "domains": ["stripe.com", "adyen.com", "unknown.example"],
  "columns": ["domain", "name", "country", "nace_code"]
}
```

* **domains**: required, non-empty list, **maximum 5,000** domains per request.  
* **columns**: same rules as search; default `["domain", "name", "country"]`. See [Reference: columns](/api/goi-reference#selectable-columns).

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

## `POST /stats` : aggregations

Returns `COUNT(*)` buckets over the filtered population. No text or vector scoring, plain SQL grouping.

Available on all customer API tiers. Monthly **request** quotas apply by tier (see [Reference: rate limits](/api/goi-reference#rate-limits-and-tiers)).

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
  "limit": 100
}
```

| Field | Description |
| ----- | ----------- |
| `group_by` | Optional. Primary dimension to bucket by. Omit for a **single total** count. |
| `group_by_derived` | Optional. Custom buckets you define with filters, used instead of `group_by`. See [Derived groups](#derived-groups). |
| `group_by_secondary` | Optional second dimension (2D breakdown). Requires `group_by` or `group_by_derived`. Must differ from `group_by`. |
| `date_trunc` | `year`, `month`, or `week`: used when a grouping column is a **date** (`company_register_date`, `created_at`). |
| `filters` | Same column filters as `/search`, including `$or`. **`text_keywords` is not supported** in stats. |
| `date_range` | Optional bounds on `company_register_date`, `created_at`, or `updated_at`. |
| `limit` | Max buckets returned (default `100`, max `500`). Ordered by count descending, except date dimensions (chronological ascending). |

### Allowed `group_by` / `group_by_secondary` columns

Geographic: `continent`, `country`, `country_code`, `state`, `state_code`, `region`, `region_code`, `district`, `district_code`, `municipality`, `municipality_code`.

Classification: `nace_code`, `organization_type`, `organization_size`, `employee_class`, `revenue_class`.

Source / registry: `source`, `company_register_court`.

Registration columns (`company_register_court`, `company_register_date`) count **one row per registration**, so an organization with several register entries is counted once per entry.

Array (exploded per value): `summary_keywords`.

Date (use with `date_trunc`): `company_register_date`, `created_at`.

### Derived groups

`group_by_derived` lets you define your own buckets. Each key in `groups` is an output label, and each value is a filters object, like the top-level `filters`. Up to **25** groups.

```json
{
  "filters": { "country": ["Germany"] },
  "group_by_derived": {
    "groups": {
      "Manufacturing": { "nace_code": ["NACE C: Manufacturing"] },
      "Trade": { "nace_code": ["NACE G: Wholesale and retail trade"] }
    },
    "include_unmatched": true
  },
  "group_by_secondary": "organization_size"
}
```

| Field | Description |
| ----- | ----------- |
| `groups` | Required. Ordered mapping of label → filters, 1 to 25 entries. |
| `multi_label` | Label for rows that match more than one group. Default `"Multiple"`. |
| `include_unmatched` | Include rows that match no group. Default `false`. |
| `unmatched_label` | Label for those rows. Default `"Unmatched"`. |

`group_by_derived` and `group_by` are mutually exclusive. `group_by_derived` requires top-level `filters` (they bound the scan); without them the request is rejected with `422`.

### Response

Each bucket in `data` includes the grouping column value(s) and a `count`. Top-level `elapsed_ms` and `metadata` echo timings, filters, and bucket counts.

---

## `GET /filters/options`

Returns JSON suitable for building filter UIs: allowed categorical values, **scoped to your API key’s data access**. No request body.

---

## Locations

Use these endpoints to find the exact place name that geographic filters (`country`, `state`, `region`, `district`, `municipality`) expect. Names follow [GADM](https://gadm.org) native spellings: `Bayern`, not `Bavaria`.

| Method | Path | Description |
| ------ | ---- | ----------- |
| `GET` | [`/locations`](/api-reference/locations/list-or-look-up-locations) | Browse the administrative tree (root, children, or an exact entry). Default `limit` 100. |
| `GET` | [`/locations/search?q=...`](/api-reference/locations/search-locations-by-name) | Fuzzy-search place names. `q` is required. Default `limit` 50. |

The maximum `limit` on both endpoints is 10,000. Follow the links above to the API Playground for every parameter.

---

## Large exports (on request)

For exports larger than search and fetch allow, ISTARI can enable asynchronous SQL exports to Parquet on your key. Contact [support@istari.ai](mailto:support@istari.ai) to request access.

---

## `GET /health`

Lightweight check that the service can reach the database. Response shape:

```json
{ "healthy": true }
```

or, on failure, `healthy: false` with an `error` message.

---

## Minimal `curl` : fetch

```bash
curl -sS 'https://api.istari.ai/v2/fetch' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: YOUR_KEY' \
  -d '{"domains":["istari.ai"],"columns":["domain","name","country"]}'
```
