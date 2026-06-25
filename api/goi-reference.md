---
title: "Reference"
description: GOI Public API — selectable columns, filters, tiers, rate limits, and HTTP errors.
---

## Selectable columns

Default for **`POST …/v2/search`** and **`POST …/v2/fetch`**: `["domain", "name", "country"]`.

Request a subset via `columns`. **`domain` is always included** in each row.

Allowed column names:

| Column | Typical use |
| ------ | ----------- |
| `domain` | Primary identifier (hostname) |
| `name` | Legal or trade name |
| `summary` | Short text description |
| `summary_keywords` | Extracted keyword tags |
| `address` | Street address |
| `organization_type` | e.g. Company, Startup |
| `organization_size` | Size band |
| `employee_class` | Employee count bracket |
| `revenue_class` | Revenue bracket |
| `nace_code` | Industry (NACE) |
| `continent`, `country`, `country_code` | Geography |
| `state`, `state_code`, `region`, `region_code` | Subnational hierarchy |
| `district`, `district_code`, `municipality`, `municipality_code` | Finer admin units |
| `lat`, `lon` | Coordinates (may be `null`) |
| `new_register_entry` | Recently registered flag |
| `company_register_date`, `company_register_id` | Register metadata |
| `created_at` | Row creation time |

**Never returned:** raw long text used only for indexing, embedding vectors, and internal flags such as `has_embedding`.

---

## Filters object

All keys are optional. Lists mean **“match any of these values”** for that field (OR inside the field).

| Field | Matches |
| ----- | ------- |
| `country`, `state`, `region`, `district`, `municipality` | Exact string on the corresponding column |
| `organization_type` | e.g. `Company`, `Startup`, `Public`, `Academic`, `Other` |
| `organization_size` | e.g. `Micro (0-9)`, `Small (10-49)`, `Medium-sized (50-249)`, `Large enterprise (250+)` |
| `nace_code` | Section letter (e.g. `K`) or detailed code (e.g. `62.01`) |
| `source` | Data provenance bucket |
| `company_register_court` | Court / register name |
| `register_date_from`, `register_date_to` | Inclusive ISO dates (`YYYY-MM-DD`) on registration dates |
| `summary_keywords` | Fast exact match on keyword array |
| `text_keywords` | Same object shape as top-level `keywords` — BM25 sub-filter on text |

Use **`GET …/v2/filters/options`** for values your key may actually use.

---

## Rate limits and tiers

Throughput and monthly quotas depend on your key’s tier (enforced at the gateway and in service middleware).

Typical **public** tier profile:

| Tier | Approx. steady RPS | Burst | Monthly request quota |
| ---- | ------------------ | ----- | ------------------------ |
| `tier_1` | 2 | 5 | 10,000 |
| `tier_2` | 5 | 10 | 50,000 |
| `tier_3` | 10 | 20 | Unlimited (subject to fair use) |

Result rows also count against monthly **result** quotas where configured.

Responses may include rate-limit headers, for example:

```http
X-RateLimit-Requests-Limit: 10000
X-RateLimit-Requests-Remaining: 9843
X-RateLimit-Results-Limit: 500000
X-RateLimit-Results-Remaining: 498231
X-RateLimit-Reset: 2026-04-01T00:00:00Z
```

When limits are exceeded, the API returns **`429 Too Many Requests`**.

---

## HTTP errors

| Status | Meaning |
| ------ | ------- |
| `400` | Malformed or inconsistent input |
| `401` | Missing or invalid API key |
| `403` | Authenticated but action not allowed for this tier (e.g. `explain`, `/stats`, `/test`) |
| `422` | Validation error (body fails schema or business rules) |
| `429` | Rate or quota exceeded |
| `500` | Unexpected server error |

Error bodies are usually JSON with a `detail` or `error` field you can log.

---

## Related

* [Overview & endpoint list](/api/api_start_page)  
* [Search behaviour](/api/goi-search)  
* [Fetch and stats](/api/goi-fetch-stats)  
