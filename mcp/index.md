---
description: GOI over the Model Context Protocol — search, similarity, and analytics across ~20M verified organizations, exposed to AI agents.
---

# GOI MCP Connector

Search, similarity, and analytics across **approximately 20 million active, verified organizations across 232 countries and territories** — exposed to AI agents via the [Model Context Protocol](https://modelcontextprotocol.io).

The Global Organization Index (GOI) is ISTARI's curated, organization-level dataset, built through a multi-step validation pipeline that prioritizes quality over volume. See the [GOI product documentation](/goi/goi_start_page) for dataset methodology, schema, and coverage statistics.

## What this connector gives you

A single MCP endpoint that lets an AI agent run the same queries a GOI dashboard user would run, with all results scoped to that user's account and plan:

* **Search** companies by natural-language description, exact keywords, or a hybrid of both.
* **Find lookalikes** to one or more reference companies via embedding similarity, optionally steered with boost / penalize terms.
* **Filter and list** by country, state, region, district, municipality, NACE sector, organization type, size, and commercial-register attributes.
* **Aggregate** counts and distributions across any combination of those dimensions (one- or two-dimensional breakdowns, with optional time bucketing).
* **Look up** full company profiles by exact domain.
* **Resolve** free-text place names to canonical filter values.

## Setup for Claude

1. Sign up at [index.istari.ai](https://index.istari.ai/). The same account works for the GOI dashboard, the API, and this MCP connector.
2. In Claude, go to Connectors > Browse Connectors > ISTARI GOI. And simply add it.
3. Sign in when prompted. If you don't have an account at index.istari.ai yet, you can just create one during the sign-in process.


## Plan access

New accounts start on the **Standard** plan — most functionality with monthly limits (see [Connect](/mcp/connect#standard-plan-quotas)). For higher quotas, see [GOI access plans](https://www.istari.ai/en/technology) on the ISTARI technology page.

## Standard plan quotas

All new accounts start on the **Standard** plan. Quotas reset on the first of each month (UTC).

| Capability | Tool group | Monthly limit |
| --- | --- | ---: |
| Search | `search_organizations`, `find_similar_organizations`, `find_similar_with_steering`, `filter_organizations` | 100 requests / 1,000 results |
| Fetch | `get_organization_details` | 100 requests / 1,000 results |
| Aggregate | `aggregate_organizations` | unlimited |
| Metadata | `describe_filters`, `resolve_location` | unlimited |

When a call would exceed the limit, the tool returns an error string beginning with `Error:`. A short consumption indicator appears in the response footer once you cross 80% of any limit.

To raise your quotas, see the [GOI access plans on the istari.ai technology page](https://www.istari.ai/en/technology).

A server-level burst cap (60 requests / minute per IP via Cloud Armor) also applies, independent of the monthly plan quota.

## Troubleshooting

* **`Monthly request quota exceeded`** — quotas reset on the first of the month (UTC). To raise your limits, see [GOI access plans](https://www.istari.ai/en/technology).
* **`/health`** returns `200 OK` with `{"healthy": true, "service": "goi-mcp"}` whenever the service is reachable.

For everything else: [support@istari.ai](mailto:support@istari.ai).



## Learn more

* [Tools](/mcp/tools) — what each tool does and when to use it.
* [Privacy](/mcp/privacy) — what we log, where it lives, how long we keep it.
* [GOI product docs](/goi/goi_start_page) — dataset, schema, dashboard features.
* [GOI API docs](/api/api_start_page) — the underlying HTTP API this connector wraps.
