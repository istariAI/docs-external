---
title: "Tools"
description: The eight read-only MCP tools exposed by GOI MCP, search, similarity, filter, fetch, aggregate, and metadata helpers.
---

The MCP server exposes eight tools. All eight are read-only. When a client connects, it discovers them automatically via MCP's `tools/list`, there is no separate REST surface to learn.

The same server also exposes this documentation as MCP **resources**. A client can list them via `resources/list` and fetch the raw Markdown via `resources/read`, with URIs like `https://mcp.goi.istari.ai/docs/tools.md`. Pick whichever discovery path your client supports.

A successful tool call returns a Markdown-formatted response. On errors, the response is a string beginning with `Error:` followed by a human-readable explanation. Every successful response (above an 80% quota threshold) gets a footer disclosing your active scope and remaining monthly budget.

## search\_organizations

Search the GOI corpus with auto-detected mode:

* `query` alone → **semantic** (embedding) search.
* `keywords_*` alone → **BM25** full-text search.
* `query` + `keywords_*` → **hybrid** with Reciprocal Rank Fusion.

Add filters (country, state, NACE sector, organization size / type, register attributes, summary keyword tags) to narrow the scope. Results are deduplicated by name and paginated with an opaque `search_after` cursor.

Use this for "find me organizations that …" and exploratory market research questions.

## find\_similar\_organizations

Find organizations similar to up to three reference domains via embedding similarity. Optional `keywords_must_all` / `keywords_must_not` are applied as post-filters.

If a reference domain is not already in GOI, the public site is fetched and embedded on demand. The resulting embedding is cached across users, see [Privacy](/mcp/privacy#scraping-and-the-embedding-cache).

Use for "organizations like X", competitive benchmarking, supplier discovery, peer-group analysis.

## find\_similar\_with\_steering

Same as `find_similar_organizations` but with **embedding arithmetic** to steer the search:

* `boost`: up to five terms whose averaged embedding is _added_ to the reference vector. Pulls the search toward a concept.
* `penalize`: up to five terms whose embedding is _subtracted_. Pushes the search away.
* `repel_domains`: up to five domains whose embeddings are subtracted. Pushes the search away from a specific organization.
* `weight`: `weak` (0.5), `normal` (1.0), or `strong` (2.0) to scale every adjustment.

Use this when a plain similarity search returns too much of the wrong thing, for example _"organizations like Stripe, but enterprise-focused"_ maps to `domains=["stripe.com"], boost=["enterprise"]`.

## filter\_organizations

Enumerate organizations matching structured criteria, with no relevance scoring. Supports the same filter dimensions as `search_organizations`, plus optional keyword filters that trigger a BM25 query. Useful when you know exactly what you want and don't need ranking.

## get\_organization\_details

Fetch full organization profiles by exact domain. Up to 20 domains per call. Returns identity, location, classification (NACE, type, size), description, keywords, and registry filings for each.

Use this after a search to drill into specific organizations, or when you already have a list of domains to look up.

## aggregate\_organizations

Count organizations grouped by one or two dimensions, optionally with a date bucket. Supports the full set of filterable dimensions plus `continent`, `country_code`, `state_code`, `region_code`, `district_code`, `municipality_code`, `employee_class`, `revenue_class`, `source`, `summary_keywords`, `company_register_date`, and `created_at`.

Use for _"how many"_, _"share of"_, _"distribution of"_, and _"trend of"_ questions. Returns a table the caller can chart directly.

## describe\_filters

Returns valid values for the enumerable filter columns (`organization_size`, `organization_type`, `nace_code`, `company_register_court`), plus a documentation block describing the date-filter parameters and how to resolve location names.

Call this once at the start of a session to ground filter-string choices, instead of guessing.

## resolve\_location

Fuzzy-match a free-text place name to the canonical GADM administrative entry. Returns ranked candidates with their admin level (country / state / region / district / municipality) and a suggested filter object to drop into the next call.

Place names follow GADM's native official spelling, _Bayern_ not _Bavaria_, _München_ not _Munich_, _Île-de-France_ not _Ile de France_. The fuzzy match catches anglicizations and minor misspellings, but the value returned to filters is the canonical form.

## Filter dimensions

All filter-accepting tools (`search_organizations`, `find_similar_*`, `filter_organizations`, `aggregate_organizations`) share the same filter parameter set:

| Group | Fields |
| --- | --- |
| Geographic | `country`, `state`, `region`, `district`, `municipality` |
| Classification | `nace_code`, `organization_size`, `organization_type` |
| Tags | `summary_keywords` |
| Registry | `company_register_court`, `register_date_from`, `register_date_to` |

Values within a single field combine with **OR**. Different fields combine with **AND**. See the [GOI dashboard docs](/goi/advanced-search-filters) for the same filters as they appear in the web UI.

### A note on commercial-register data

The registry fields (`company_register_court`, `register_date_*`) are populated **only for German, Austrian, and Swiss organizations** today, and only for entries appearing in the commercial register from January 2026 onwards. Organizations outside that scope have null register attributes and are excluded from any filter on those fields. The rest of the dataset (~20M organizations across 232 countries) is unaffected.

This isn't an API restriction, it's the current state of the underlying source data. Coverage expands over time.

## Pagination

Search and filter tools return up to 500 results per call, default 20. The response includes an opaque `search_after` cursor; pass it verbatim on the next call to get the next page.

## Errors

Tool errors are returned as plain text in the format:

```
Error [<CODE>]: <human-readable message>
```

The bracketed code is stable across releases and lets a client (or LLM) route on a single identifier instead of parsing prose. The message body explains what specifically went wrong and what to do.

| Code | When it fires | Caller action |
| --- | --- | --- |
| `INVALID_INPUT` | A required argument is missing, a value is malformed, or a cross-field rule is violated (e.g. `must_not` without any positive terms) | Adjust the inputs and retry |
| `INVALID_AGGREGATION_COLUMN` | `aggregate_organizations` was called with an unknown `group_by` / `group_by_secondary`, or with the secondary set without a primary, or with the two equal | Pick a value from the message's `Allowed: [...]` list |
| `INVALID_FILTER_COLUMN` | `describe_filters` was called with a column that is not an enumerable filter | Pass one of the `Allowed:` values, or omit `column` to see all |
| `INVALID_DATE_TRUNC` | `date_trunc` not in `year` / `month` / `week` | Pass a valid value |
| `OUT_OF_SCOPE` | A filter value is outside your account's allowed scope (region or commercial-register court) | Use one of the `Allowed values:` in the message; this only fires for accounts with a configured scope |
| `RATE_LIMITED_REQUESTS` | Monthly request budget for this bucket exceeded | Wait until the start of next month, or upgrade: see [Connect](/mcp/connect#standard-plan-quotas) |
| `RATE_LIMITED_RESULTS` | Monthly result budget for this bucket exceeded | Same |
| `ROUTE_BLOCKED` | This tool is gated and not available on your plan | Upgrade plan: see [GOI access plans](https://www.istari.ai/en/technology) |
| `REFERENCE_DOMAIN_UNAVAILABLE` | `find_similar_*` got a reference domain that is not in GOI and whose website could not be fetched | Try a different reference domain, or remove the unreachable one |
| `INTERNAL` | An unexpected server-side error. The message contains a short **reference ID** (8 hex characters): quote it when contacting support so we can correlate to logs | Retry once; if the same ID class repeats, contact `support@istari.ai` with the reference ID |

`INTERNAL` errors are the only ones whose detail is intentionally opaque, full traceback goes to our server logs, not to you.
