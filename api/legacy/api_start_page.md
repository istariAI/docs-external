# Welcome to the ISTARI API (legacy)

> This material describes the **previous ISTARI HTTP API (v1)** at `https://api.istari.ai/v1/...`. It remains here for existing integrations that still use those paths.

> **Current product:** use the [GOI Public API (v2)](../api_start_page.md) at **`https://api.istari.ai/v2/`** for the ISTARI Global Organization Index.

The **ISTARI API** offers a powerful suite of endpoints for querying, filtering, and retrieving company data from a large, searchable company dataset. Whether you're targeting specific domains using the `fetch-market` endpoint, conducting broad discovery via keyword and semantic search with `search`, or drilling into geographic structures, the API provides full control over what data you retrieve and how you retrieve it. With hundreds of customizable fields spanning contact details, company structure, technology adoption, innovation intensity, and sustainability metrics, ISTARI API helps you build targeted, enriched datasets to fit your exact use case—whether for market research, lead generation, analytics, or integration.

### Getting started

The base URL for legacy v1 requests is **`https://api.istari.ai/v1/`** (paths such as `/v1/search` as documented below).

A sample curl POST request to search would look like this:

```sh
curl --location 'https://api.istari.ai/v1/search' \
--header 'Accept: application/json' \
--header 'x-api-key: your-api-key' \
--header 'Content-Type: application/json' \
--data '{
        "search_id: [],
        "domains": [],
        "excludes": [],
        "keywords": {"must_one": [], "must_all": [], "must_not": []},
        "locations": {"country": [], "state": [], "region": []},
        "custom_filters": {},
        "index": "webai*",
        "size": 100,
        "semantic_input": "social",
        "columns": [
            "domain"
        ],
        "pit_id": null,
        "search_after": []
    }'

```

