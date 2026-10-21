---
title: "Overview"
description: GOI over the Model Context Protocol, search, similarity, and analytics across ~20M verified organizations, exposed to AI agents.
---

Search, similarity, and analytics across **approximately 20 million active, verified organizations across 232 countries and territories**: exposed to AI agents via the [Model Context Protocol](https://modelcontextprotocol.io).

The Global Organization Index (GOI) is ISTARI's curated, organization-level dataset, built through a multi-step validation pipeline that prioritizes quality over volume. See the [GOI product documentation](/goi/goi_start_page) for dataset methodology, schema, and coverage statistics.

## What GOI MCP gives you

A single MCP endpoint that lets an AI agent run the same queries a GOI user would run, with all results scoped to that user's account and plan:

* **Search** organizations by natural-language description, exact keywords, or a hybrid of both.
* **Find lookalikes** to one or more reference organizations via embedding similarity, optionally steered with boost / penalize terms.
* **Filter and list** by country, state, region, district, municipality, NACE sector, organization type, size, and commercial-register attributes.
* **Aggregate** counts and distributions across any combination of those dimensions (one- or two-dimensional breakdowns, with optional time bucketing).
* **Look up** full organization profiles by exact domain.
* **Resolve** free-text place names to canonical filter values.

<Note>
GOI MCP is not yet listed in connector directories for Claude or ChatGPT. Add it as a custom connector — see [Connect](/mcp/connect). Once store approval is complete, we will update the docs with one-click install instructions.
</Note>

## Get access

1. Sign up or sign in at [index.istari.ai](https://index.istari.ai). The same account works for the GOI dashboard, the API, and GOI MCP.
2. Submit the [GOI MCP access request](https://index.istari.ai/goi-mcp-access). No approval is needed: we email you the **Client ID**, **Secret**, and connection details.
3. Follow [Connect](/mcp/connect) to add GOI MCP as a custom connector in Claude, ChatGPT, Cursor, or another MCP client.

## Plan access

New accounts start on the **Standard** plan, most functionality with monthly limits (see [Standard plan quotas](#standard-plan-quotas)). For higher quotas, [book a demo](https://calendar.istari.ai/team/istari-sales-team/exploration?source=external-docs) to talk about Premium.

## Standard plan quotas

All new accounts start on the **Standard** plan. Quotas reset on the first of each month (UTC).

| Capability | Tool group | Monthly limit |
| --- | --- | ---: |
| Search | `search_organizations`, `find_similar_organizations`, `find_similar_with_steering`, `filter_organizations` | 500 requests / 5,000 results |
| Fetch | `get_organization_details` | 500 requests / 5,000 results |
| Aggregate | `aggregate_organizations` | 500 requests |
| Metadata | `describe_filters`, `resolve_location` | unlimited |

When a call would exceed the limit, the tool returns an error in the format `Error [CODE]: message`, for example `Error [RATE_LIMITED_REQUESTS]: ...`. A short consumption indicator appears in the response footer once you cross 80% of any limit.

For full quota tables across dashboard, MCP, and API, see [Pricing and limits](/docs/pricing). For higher quotas on a commercial plan, [book a demo](https://calendar.istari.ai/team/istari-sales-team/exploration?source=external-docs) or contact [support@istari.ai](mailto:support@istari.ai).

A per-IP safety limit of 60 requests/minute also applies on all GOI endpoints, independent of the monthly plan quota.

## Troubleshooting

* **`Monthly request quota exceeded`**: quotas reset on the first of the month (UTC). To raise your limits, [book a demo](https://calendar.istari.ai/team/istari-sales-team/exploration?source=external-docs).
* **`/health`** returns `200 OK` with `{"healthy": true, "service": "goi-mcp"}` whenever the service is reachable.

For everything else: [support@istari.ai](mailto:support@istari.ai).



## Learn more

* [Tools](/mcp/tools): what each tool does and when to use it.
* [Privacy](/mcp/privacy): what we log, where it lives, how long we keep it.
* [GOI product docs](/goi/goi_start_page): dataset, schema, GOI dashboard features.
* [GOI API docs](/api/api_start_page): the underlying API GOI MCP wraps.
