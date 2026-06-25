---
description: POST /v2/search — modes, keywords, semantic and similarity queries, filters, pagination.
---

# GOI Public API — Search (`POST …/v2/search`)

Search returns a JSON object with a `data` array of organisation rows and a `metadata` object (total hits, mode, timing, pagination cursor, filters applied, optional explain plan).

## Requirements

You must supply **at least one** of:

* `filters` — column filters only (browse / filter mode)  
* `keywords` — BM25 text search  
* `describe` — natural-language description → embedding search (**cannot** be combined with `similar_to`)  
* `similar_to` — similarity to one or more reference domains (**cannot** be combined with `describe`)

`similar_to` and `describe` are **mutually exclusive**.

## Search mode (automatic)

You do **not** send a mode name. The API infers it from your inputs:

| `metadata.mode` value | When it runs |
| --------------------- | ------------ |
| `filter` | Only `filters` (no `keywords`, `describe`, or `similar_to`) |
| `fulltext` | `keywords` only (no `describe`, no `similar_to`) |
| `semantic` | `describe` only |
| `vector_similarity` | `similar_to` only |
| `hybrid` | `keywords` together with `similar_to` **or** with `describe` |

Hybrid queries blend BM25 and vector ranking (reciprocal rank fusion). Use `search_balance` from `0.0` (BM25-heavy) to `1.0` (vector-heavy); default `0.5`.

## Request body (overview)

```json
{
  "similar_to": ["stripe.com"],
  "describe": null,
  "keywords": { "must_all": [], "must_any": [], "must_not": [] },
  "filters": { },
  "excludes": [],
  "columns": ["domain", "name", "country"],
  "size": 100,
  "min_score": null,
  "search_balance": 0.5,
  "search_after": null,
  "explain": false,
  "dedup": false
}
```

| Field | Notes |
| ----- | ----- |
| `columns` | Subset of allowed columns; `domain` is always returned. Default `["domain", "name", "country"]`. See [Reference](/api/goi-reference#selectable-columns). |
| `size` | Page size, default `100`, maximum `500`. |
| `min_score` | Optional `0.0`–`1.0` cosine similarity floor for vector / semantic / hybrid modes. |
| `search_after` | Opaque cursor from the previous response’s `metadata.search_after` for pagination. |
| `dedup` | If `true`, collapse rows that share the same company `name`, keeping the best match until `size` rows. |
| `explain` | If `true`, includes PostgreSQL `EXPLAIN ANALYZE` lines in metadata — **tier_3 only**. |

## Keywords (`keywords`)

Drives BM25 search on name and description (and participates in hybrid):

```json
{
  "must_all": ["payments", "B2B"],
  "must_any": ["SaaS", "cloud"],
  "must_not": ["crypto"]
}
```

All parts are optional, but **`must_not` alone is invalid** — you need at least one of `must_all` or `must_any` whenever `must_not` is present.

## Similar companies (`similar_to`)

Pass up to **three** domains as strings, or as objects for **steering** (boost / penalize terms, repel domains, weight):

```json
{
  "similar_to": [
    {
      "domain": "stripe.com",
      "boost": ["enterprise", "B2B"],
      "penalize": ["consumer"],
      "repel_domains": ["paypal.com"],
      "weight": 1.0
    }
  ]
}
```

* `boost`, `penalize`, `repel_domains` — up to **5** entries each.  
* `weight` — number from **0.0** to **2.0**, or the strings **`weak`**, **`normal`**, **`strong`** (mapped to internal numeric weights). Default **1.0**.

## Semantic description (`describe`)

Free-text description of the kind of companies you want; embedded and searched like a vector query. Cannot be used together with `similar_to`.

## Filters (`filters`)

Optional on any mode. Multiple values in a list are OR-combined for that field. Full field list and semantics: [Reference — filters](/api/goi-reference#filters-object).

Inside `filters`, `text_keywords` uses the same shape as top-level `keywords` but acts as a **strict BM25 filter** on text (slower than `summary_keywords` for exact keyword-array matches).

## Excludes

`excludes` is a list of domains that must not appear in results, regardless of score.

## Pagination

* First page: omit `search_after` or send `null`.  
* Next page: copy `metadata.search_after` from the previous response into the next request.

Scored modes use an offset-style cursor with a **maximum depth of 10,000** rows. **Filter-only** mode uses keyset pagination by domain and has **no** depth cap. When `metadata.search_after` is `null`, there is no further page.

## Example requests

**Filter-only browse (Germany):**

```json
{
  "filters": { "country": ["Germany"] },
  "size": 50
}
```

**Keyword search with geography:**

```json
{
  "keywords": { "must_any": ["renewable energy", "solar"] },
  "filters": { "country": ["Germany", "Austria"] }
}
```

**Similar to a reference company:**

```json
{
  "similar_to": ["stripe.com"],
  "filters": { "country": ["Ireland", "Germany"] },
  "columns": ["domain", "name", "country", "nace_code"]
}
```

**Hybrid (keywords + description):**

```json
{
  "keywords": { "must_all": ["HR", "software"] },
  "describe": "payroll automation for SMEs",
  "search_balance": 0.6,
  "size": 20
}
```

## Response shape

```json
{
  "data": [
    { "domain": "example.com", "name": "Example GmbH", "country": "Germany" }
  ],
  "metadata": {
    "total_hits": 142,
    "returned": 25,
    "mode": "hybrid",
    "elapsed_ms": 312,
    "search_after": [25],
    "filters_applied": { "country": ["Germany"] },
    "explain_plan": null
  }
}
```

`total_hits` may be `null` in some filter paths. See [Errors](/api/goi-reference#http-errors) for failure responses.
