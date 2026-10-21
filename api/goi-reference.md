---
title: "Reference"
description: GOI API, selectable columns, filters, tiers, rate limits, and HTTP errors.
---

## Selectable columns

Default for **`POST …/v2/search`** and **`POST …/v2/fetch`**: `["domain", "name", "country"]`.

Request a subset via `columns`. **`domain` is always included** in each row. Unknown column names return `422`.

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
| `nace_code` | Industry (NACE section) |
| `continent`, `country`, `country_code` | Geography |
| `state`, `state_code`, `region`, `region_code` | Subnational hierarchy |
| `district`, `district_code`, `municipality`, `municipality_code` | Finer admin units |
| `lat`, `lon` | Coordinates (may be `null`) |
| `source` | Data provenance bucket |
| `company_register_date`, `company_register_id`, `company_register_court` | Register metadata |
| `registries` | List of the organization's register entries, one object per registration: `{"court", "date", "id"}`, e.g. `{"court": "München", "date": "2026-02-12", "id": "HRB 291002"}`. An organization can have several. |
| `created_at` | Row creation time |

**Never returned:** raw long text used only for indexing, embedding vectors, and internal flags such as `has_embedding`.

### Commercial-register coverage

Register fields (`company_register_*`, `registries`) are populated for organizations in **Germany, Austria, Switzerland, France, the United Kingdom, and Spain**, for entries appearing in the commercial register from **January 2026** onwards. Other organizations have `null` register fields.

---

## Filters object

All keys are optional. Different fields combine with **AND**. For most list fields, multiple values mean **“match any of these values”** (OR inside the field). The exception is `summary_keywords`, where an organization must have **all** listed keywords.

| Field | Matches |
| ----- | ------- |
| `country`, `state`, `region`, `district`, `municipality` | Exact string on the corresponding column. Use [`/locations`](/api/goi-fetch-stats#locations) to find the exact name. |
| `organization_type` | e.g. `Company`, `Startup`, `Public`, `Academic`, `Other` |
| `organization_size` | e.g. `Micro (0-9)`, `Small (10-49)`, `Medium-sized (50-249)`, `Large enterprise (250+)` |
| `nace_code` | Exact NACE section string, e.g. `"NACE C: Manufacturing"`. See [NACE values](#nace-values). |
| `source` | Data provenance bucket |
| `company_register_court` | Court / register name |
| `register_date_from`, `register_date_to` | Inclusive ISO dates (`YYYY-MM-DD`) on registration dates |
| `summary_keywords` | Exact match on the keyword array. **All** listed keywords must be present. |
| `text_keywords` | Same object shape as top-level `keywords`: BM25 sub-filter on text. Not supported in `/stats`. |
| `$or` | Object of ordinary column filters whose conditions are **OR**-combined instead of AND. Nested `$or` and `text_keywords` are not supported inside it. |

Example: organizations in Bayern **or** in the manufacturing sector, limited to Germany:

```json
{
  "filters": {
    "country": ["Germany"],
    "$or": {
      "state": ["Bayern"],
      "nace_code": ["NACE C: Manufacturing"]
    }
  }
}
```

Use **`GET …/v2/filters/options`** for the live list of values your key may actually use.

### NACE values

`nace_code` matches the full section string exactly. A bare letter (`C`) or a detailed code (`62.01`) returns no results.

* `NACE A: Agriculture, forestry and fishing`
* `NACE B: Mining and quarrying`
* `NACE C: Manufacturing`
* `NACE D: Electricity, gas, steam and air conditioning supply`
* `NACE E: Water supply; sewerage, waste management and remediation activities`
* `NACE F: Construction`
* `NACE G: Wholesale and retail trade`
* `NACE H: Transportation and storage`
* `NACE I: Accommodation and food service activities`
* `NACE J: Publishing, broadcasting, and content production and distribution activities`
* `NACE K: Telecommunication, computer programming, consulting, computing infrastructure and other information service activities`
* `NACE L: Financial and insurance activities`
* `NACE M: Real estate activities`
* `NACE N: Professional, scientific and technical activities`
* `NACE O: Administrative and support service activities`
* `NACE P: Public administration and defence; compulsory social security`
* `NACE Q: Education`
* `NACE R: Human health and social work activities`
* `NACE S: Arts, sports and recreation`
* `NACE T: Other service activities`
* `NACE U: Activities of households as employers and undifferentiated goods- and service-producing activities of households for own use`
* `NACE V: Activities of extraterritorial organisations and bodies`

---

## Rate limits and tiers

Every key has an API tier. New keys get **`tier_1`**. **`tier_2`** is assigned by ISTARI on request: contact [support@istari.ai](mailto:support@istari.ai).

### Monthly quotas

Quotas are per key, per route, per calendar month. They reset at the start of each month (UTC), and only successful responses (status below `400`) count. **Results** are organization rows returned.

| API tier | `POST /search` | `POST /fetch` | `POST /stats` |
| ---- | ---- | ---- | ---- |
| `tier_1` (default) | 1,000 requests / 5,000 results | 1,000 requests / 5,000 results | 500 requests |
| `tier_2` (on request) | 10,000 requests / 250,000 results | 30,000 requests / 250,000 results | 5,000 requests |

### Throughput

The gateway also throttles each key:

| API tier | Steady rate | Burst |
| ---- | ---- | ---- |
| `tier_1` | 0.5 requests/second | 5 |
| `tier_2` | 1 request/second | 10 |

A per-IP safety limit of **60 requests/minute** also applies on all GOI endpoints. It is enforced by the load balancer in front of the API, separately from the per-key throttle above.

### Rate-limit headers

Responses include your remaining monthly budget for the route. Example values:

```http
X-RateLimit-Requests-Limit: 1000
X-RateLimit-Requests-Remaining: 843
X-RateLimit-Results-Limit: 5000
X-RateLimit-Results-Remaining: 4231
X-RateLimit-Reset: 1209600
```

* `X-RateLimit-Reset` is the number of **seconds** until the quota resets at the end of the month.
* On routes without a limit, `X-RateLimit-Requests-Limit` is `unlimited`.

When a monthly quota is used up, the API returns **`429 Too Many Requests`** with a `Retry-After` header (seconds) and the code `RATE_LIMITED_REQUESTS` or `RATE_LIMITED_RESULTS`. If a route isn't available on your tier at all, the API returns **`403`** with `ROUTE_BLOCKED`.

---

## HTTP errors

| Status | `code` | When |
| ------ | ------ | ---- |
| `400` | `LOCATION_QUERY_EMPTY`, `LOCATION_LOOKUP_INVALID` | Invalid input to `/locations` or `/locations/search` |
| `401` | `NO_API_KEY` | No `x-api-key` header |
| `403` | `KEY_DISABLED` | Key revoked or suspended |
| `403` | `INVALID_PLAN` | The key's usage plan is not recognized |
| `403` | `ROUTE_BLOCKED` | Route not available on your tier |
| `422` | none | Request body fails validation, for example an unknown column or an invalid filter value |
| `429` | `RATE_LIMITED_REQUESTS`, `RATE_LIMITED_RESULTS` | Monthly quota used up |
| `500` | `INTERNAL_ERROR` | Unexpected server error |
| `503` | `AUTH_UNAVAILABLE` | Key lookup temporarily unavailable. Retry. |

Error bodies come in two shapes:

* Authentication, rate-limit, and location errors: `{"error": "...", "code": "..."}`.
* Validation errors (`422`): `{"detail": [...]}`, one entry per invalid field, or `{"detail": "message"}` (for example, an unknown column). They have no `code` field.

### Errors from the load balancer

The per-IP safety limit and a web application firewall sit in front of the API. When they reject a request, you get a `429` (more than 60 requests/minute from your IP) or a `403` (request content blocked by the firewall) **without** a JSON `code` field and without `X-RateLimit-*` headers.

A `429` or `403` with no `code` means: slow down, or check the request content. It is not a monthly quota issue.

---

## Related

* [Overview & endpoint list](/api/api_start_page)  
* [Search behaviour](/api/goi-search)  
* [Fetch and stats](/api/goi-fetch-stats)  
