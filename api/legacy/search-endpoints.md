---
description: Query, Filter, and Download Company Data with Flexible Access Options.
---
# Search Endpoints

> This page documents the **legacy WebAI search HTTP API (v1)** at `https://api.istari.ai/v1/...`. For the current GOI Public API (v2), see [Search](../goi-search.md) and [Overview](../api_start_page.md).

This document provides comprehensive documentation for the WebAI Search API, which allows users to search and retrieve company data from the legacy search backend.

### Table of Contents

* API Endpoints
* Authentication
* Search Endpoint
* Sublocations Endpoint
* Fetch Market Endpoint
* Download Endpoint
* Close PIT Endpoint
* Data Models
* Error Handling

### API Endpoints

All endpoints are prefixed with `/v1`.

| Endpoint        | Method | Description                                                          |
| --------------- | ------ | -------------------------------------------------------------------- |
| `/search`       | POST   | Execute a search operation                                           |
| `/sublocations` | POST   | Get all unique locations at the child level within a parent location |
| `/fetch-market` | POST   | Fetch data for a list of domains representing a market               |
| `/download`     | POST   | Download search results in various formats                           |
| `/close_pit`    | DELETE | Close a point-in-time (PIT) search context                           |

### Authentication

The API supports two authentication methods:

1.  **API Key Authentication**: Include an API key in the request header. (for API-Key user)

    ```
    x-api-key: your-api-key
    ```
2.  **Cognito Authentication**: Use AWS Cognito for user authentication. (for Dashboard user)

    ```
    Authorization: Bearer your-jwt-token
    ```

All endpoints require authentication using one of these methods.

### Search Endpoint

#### Endpoint

```
POST /v1/search
```

#### Description

Execute a search operation using various parameters including keywords, locations, and custom filters.

#### Request Body

```json
{
  "search_id": "unique-search-id",
  "domains": ["example.com", "example.org"],
  "excludes": ["exclude-domain.com"],
  "keywords": {
    "must_one": ["keyword1", "keyword2"],
    "must_all": ["requiredKeyword"],
    "must_not": ["excludedKeyword"]
  },
  "locations": {
    "country": ["Germany"],
    "state": ["Bavaria"],
    "region": [],
    "district": [],
    "municipality": []
  },
  "custom_filters": None,
  "index": "webai*",
  "size": 25,
  "columns": ["domain", "country", "description", "main_contact_mail"],
  "pit_id": None,
  "search_after": None,
  "semantic_input": None
}
```

#### Tool to generate UUIDs

You can use this free tool to generate UUIDs for your search requests: [https://www.guidgenerator.com/](https://www.guidgenerator.com/)

> _**Recommendation**: while you can use one UUID for multiple requests, we would recommend using separate ones to keep your searches clean and well organised._&#x20;

#### Parameters

| Parameter        | Type    | Required | Description                                        |
| ---------------- | ------- | -------- | -------------------------------------------------- |
| `search_id`      | string  | Yes      | Unique identifier for the search (UUID)            |
| `domains`        | array   | No       | List of domains for similarity search              |
| `excludes`       | array   | No       | List of domains to exclude from results            |
| `keywords`       | object  | No       | Keyword search parameters                          |
| `locations`      | object  | No       | Location filters                                   |
| `custom_filters` | object  | No       | Additional filters for specific fields             |
| `index`          | string  | No       | Data index to search (default: "webai\*") |
| `size`           | integer | No       | Number of results to return (default: 25)          |
| `columns`        | array   | No       | Columns to include in the output                   |
| `pit_id`         | string  | No       | Point in Time ID for pagination                    |
| `search_after`   | array   | No       | Search after parameter for pagination              |
| `semantic_input` | string  | No       | Text input for semantic search                     |

#### Response

```json
{
  "data": [
    {
      "domain": "example.com",
      "country": "Germany",
      "description": "Example company description",
      "main_contact_mail": "contact@example.com"
    }
  ],
  "metadata": {
    "search_id": "unique-search-id",
    "index": "webai*",
    "size": 25,
    "columns": ["domain", "country", "description", "main_contact_mail"],
    "query": "your inserted query"
    "total_hits": 100,
    "total_fetched": 25,
    "query_type": "keyword",
    "pit_id": "pit_id_for_pagination",
    "search_after": ["value_for_next_page"]
  }
}
```

### Sublocations Endpoint

#### Endpoint

```
POST /v1/sublocations
```

#### Description

Get all unique locations at the child level within a parent location. For example, get all states in Germany or all districts in Bavaria.

#### Request Body

```json
{
  "parent_level": "country",
  "parent_value": "Germany",
  "index": "webai*"
}
```

#### Parameters

| Parameter      | Type   | Required | Description                                                                              |
| -------------- | ------ | -------- | ---------------------------------------------------------------------------------------- |
| `parent_level` | string | Yes      | The geographic level of the parent (all, country, state, region, district, municipality) |
| `parent_value` | string | Yes      | The value of the parent location                                                         |
| `index`        | string | No       | Data index to search (default: "webai\*")                                       |

#### Response

```json
{
  "locations": ["Bavaria", "Berlin", "Hamburg"],
  "level": "state",
  "total_count": 3
}
```

### Fetch Market Endpoint

#### Endpoint

```
POST /v1/fetch-market
```

#### Description

Fetch data for a list of domains representing a market. This is useful for getting information about a specific set of companies.

#### Request Body

```json
{
  "index": "webai*",
  "columns": ["domain", "country", "description", "employee_class"],
  "domains": ["example.com", "example.org", "example.net"]
}
```

#### Parameters

| Parameter | Type   | Required | Description                                        |
| --------- | ------ | -------- | -------------------------------------------------- |
| `index`   | string | No       | Data index to search (default: "webai\*") |
| `columns` | array  | No       | Columns to include in the output                   |
| `domains` | array  | Yes      | List of domains to fetch data for                  |

#### Response

```json
{
  "data": [
    {
      "domain": "example.com",
      "country": "Germany",
      "description": "Example company description",
      "employee_class": "10-49"
    }
  ],
  "metadata": {
    "total_fetched": 1,
    "index": "webai*",
    "columns": ["domain", "country", "description", "employee_class"],
    "domains_requested": 3,
    "domains_found": 1,
    "missing_domains": ["example.org", "example.net"],
    "timestamp": "2023-01-01 12:00:00"
  }
}
```

### Download Endpoint

#### Endpoint

```
POST /v1/download
```

#### Description

Download search results in various formats (TSV, Excel, Parquet). This endpoint supports text queries, KNN queries, and market queries.

#### Request Body

```json
{
  "download_id": "unique-download-id",
  "index": "webai*",
  "size": 10,
  "columns": ["domain", "country", "description"],
  "search_info": {
    "search_id": "unique-search-id",
    "query": {
      "match": {
        "description": "AI company"
      }
    }
  },
  "download_format": "xlsx"
}
```

Alternatively, for market-based downloads:

```json
{
  "download_id": "unique-download-id",
  "index": "webai*",
  "size": 10,
  "columns": ["domain", "country", "description"],
  "market_info": {
    "market_id": "unique-market-id",
    "market": ["example.com", "example.org"]
  },
  "download_format": "tsv"
}
```

#### Parameters

| Parameter         | Type    | Required | Description                                                       |
| ----------------- | ------- | -------- | ----------------------------------------------------------------- |
| `download_id`     | string  | No       | Unique identifier for the download (default: auto-generated UUID) |
| `index`           | string  | No       | Data index to search (default: "webai\*")                |
| `size`            | integer | No       | Number of results to download (default: 10, max: 10)              |
| `columns`         | array   | No       | Columns to include in the output                                  |
| `search_info`     | object  | No       | Search information for text or KNN queries                        |
| `market_info`     | object  | No       | Market information for market-based downloads                     |
| `download_format` | string  | No       | Format of the downloaded file (tsv, xlsx, parquet) (default: tsv) |

#### Response

```json
{
  "download_url": "https://presigned-s3-url-for-download",
  "metadata": {
    "download_id": "unique-download-id",
    "user_id": "user-id",
    "file_path": "s3://bucket-name/path/to/file",
    "total_hits": 100,
    "total_fetched": 10,
    "index": "webai*",
    "timestamp": "2023-01-01T12:00:00",
    "download_format": "xlsx",
    "query_type": "text"
  }
}
```

### Close PIT Endpoint

#### Endpoint

```
DELETE /v1/close_pit
```

#### Description

Close a point-in-time (PIT) search context to free up resources.

#### Parameters

| Parameter | Type   | Required | Description                   |
| --------- | ------ | -------- | ----------------------------- |
| `pit_id`  | string | Yes      | The point-in-time ID to close |

#### Response

```json
{
  "succeeded": true
}
```

### Data Models

#### Allowed Columns

The API supports a wide range of columns for filtering and output. Here are some of the commonly used columns:

* `domain`: The website domain
* `country`: Country where the company is located
* `description`: Company description
* `main_contact_mail`: Primary contact email
* `main_contact_number`: Primary contact phone number
* `employee_class`: Company size by employee count
* `revenue_class`: Company size by revenue
* `lat`, `lon`: Geolocation coordinates

For a complete list of allowed columns, refer to the `ALLOWED_COLUMNS` constant in the API code.

#### Geography Hierarchy

The API supports a hierarchical structure for geographic locations:

1. `country`: Country level (e.g., Germany)
2. `state`: State/province level (e.g., Bavaria)
3. `region`: Region level (e.g., Upper Bavaria)
4. `district`: District level (e.g., Munich District)
5. `municipality`: Municipality level (e.g., Munich City)

### Error Handling

The API returns standard HTTP status codes to indicate success or failure:

* `200 OK`: Request was successful
* `400 Bad Request`: Invalid request parameters
* `403 Forbidden`: Authentication or authorization failure
* `500 Internal Server Error`: Server-side error

Error responses include a detail message explaining the issue:

```json
{
  "detail": "Error message explaining the issue"
}
```

Common error scenarios:

1. Unauthorized access: Missing or invalid API key
2. Invalid query parameters: Malformed request body
3. Resource limitations: Attempting to fetch more than allowed records
4. Search backend errors: Issues with the underlying search service
