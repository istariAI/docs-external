---
description: >-
  Retrieve Precise Company Data by Domain, Location, or Keyword with Full Column
  Customization.
---

# Column Information

> This page refers to **`fetch-market`** and columns on the **legacy ISTARI HTTP API (v1)** (`https://api.istari.ai/v1/...`). For GOI column selection on `/v2/search` and `/v2/fetch`, see [Reference: columns and filters](../goi-reference.md).

## **Endpoint: `fetch-market`**

Fetches market data for the exact domains you specify in the `domains` parameter—no fuzzy matching or similar-company lookups.\
Use the optional `columns` parameter to list the fields you want returned, so you can tailor and enrich your dataset with only the data you need.

**Available Columns**

Below are some commonly used columns. For the complete list with detailed descriptions, data types, and possible values, please refer to the Dataset Codebook.

* **Contact & Communications**
  * `all_mails`
  * `all_phones`
  * `main_contact_mail`
  * `main_contact_number`
  * `links`
  * `address`
* **Domain Information**
  * `domain`
  * `domain_alias`
  * `domain_provider_true`
  * `domain_redirect`
* **Business Details**
  * `title`
  * `description`
  * `keywords`
  * `name`
  * `summary`
  * `summary_keywords`
  * `new_register_entry`
  * `type`
  * `b2x`
  * `techstack`
* **Location Data**
  * `continent`
  * `country` / `country_code`
  * `region` / `region_code`
  * `state` / `state_code`
  * `district` / `district_code`
  * `municipality` / `municipality_code`
  * `geolocation` _(includes `lat`, `lon`)_
* **Scores & Categories**
  * `cultural_score` / `cultural_score_category`
  * `leisure_score` / `leisure_score_category`
  * `recreational_score` / `recreational_score_category`
  * `transport_score` / `transport_score_category`
* **Probabilities & Classes**
  * `innoprob` / `innoprob_innovator_probability`
  * `social_innoprob` / `social_innoprob_innovator_probability`
  * `news_probability`
  * `retailer_probability`
  * `employee_class`
  * `revenue_class`
* **Intensity Metrics**
  * **AI**
    * `ai_intensity` / `ai_intensity_level`
    * `ai_keywords` / `ai_keywords_hits` / `ai_total_hits`
  * **Energy**
    * `energy_intensity` / `energy_intensity_level`
    * `energy_keywords` / `energy_keywords_hits` / `energy_total_hits`
  * **Sustainability**
    * `sustainability_intensity` / `sustainability_intensity_level`
    * `sustainability_keywords` / `sustainability_keywords_hits` / `sustainability_total_hits`
  * **Digital Health**
    * `digital_health_intensity` / `digital_health_intensity_level`
    * `digital_health_keywords` / `digital_health_keywords_hits` / `digital_health_total_hits`
  * **Mobility**
    * `mobility_intensity` / `mobility_intensity_level`
    * `mobility_keywords` / `mobility_keywords_hits` / `mobility_total_hits`
  * **Blockchain**
    * `blockchain_intensity` / `blockchain_intensity_level`
    * `blockchain_keywords` / `blockchain_keywords_hits` / `blockchain_total_hits`
  * **Additive Manufacturing**
    * `additive_manufacturing_intensity` / `additive_manufacturing_intensity_level`
    * `additive_manufacturing_keywords` / `additive_manufacturing_keywords_hits` / `additive_manufacturing_total_hits`
  * **SDG Metrics**
    * `sdg1_intensity` / `sdg1_intensity_level` / `sdg1_keywords` / `sdg1_keywords_hits` / `sdg1_total_hits`
    * `sdg2_intensity` / `sdg2_intensity_level` / `sdg2_keywords` / `sdg2_keywords_hits` / `sdg2_total_hits`
    * `sdg3_intensity` / `sdg3_intensity_level` / `sdg3_keywords` / `sdg3_keywords_hits` / `sdg3_total_hits`
* **Complex Structures**
  * `products` (contains: `name`, `type`, `pricing`, `main_features`)
  * `team` (contains: `name`, `position`, `contact`, `cv`)
  * `structure` (contains: `name`, `type`, `description`, `location`, `contact`)
  * `partnerships` (contains: `entity_name`, `relationship_type`)

```python
import requests

api_url = 'https://api.istari.ai/v1/fetch-market' # this is the endpoint for the API Gateway
headers = {
    'x-api-key': 'sk_api_key', # api-key generated from AWS API Gateway, each company has their own api-key in the future
    'Content-Type': 'application/json'
}

payload = {
    "domains": ["peterconradconstruction.com", "istari.ai"], # this is the list of domains that you are looking for in the database (it must be a list of strings even for a single domain!!)
    "columns": [ # this is the list of columns that you are looking for in the database
      "domain",
      "country",
      "state",
      "title",
      "description",
      "keywords"
    ],
    "index": "webai*" # this is the index that you are looking for in the database (it must be a string)
}

response = requests.post(api_url, headers=headers, json=payload)
print(response.json())
```

The API returns a JSON object with two primary sections:

1. **`data`**\
   Contains an array of records—one per requested domain—each including exactly the fields you asked for via the `columns` parameter:
   * `domain`: The queried domain name.
   * `country`: Registered/operating country.
   * `state`: State or region.
   * `title`: Content of the HTML `<title>` tag.
   * `description`: Content of the HTML `<meta name="description">` tag (or a snippet).
   * `keywords`: Content of the HTML `<meta name="keywords">` tag (empty string if absent).
2. **`metadata`**\
   Echoes your input parameters and provides execution details:
   * **`domains_requested`** (int): Number of domains in your payload.
   * **`domains_found`** (int): How many of those domains were found in the index.
   * **`missing_domains`** (array): Any domains you requested but weren’t found.
   * **`columns`** (array): The exact list of columns you specified in the request.
   * **`index`** (string): The index or index pattern queried (e.g. `"webai*"`).
   * **`total_fetched`** (int): Total records returned (should equal `domains_found`).
   * **`timestamp`** (string): Server-side timestamp when the query executed (`YYYY-MM-DD HH:MM:SS`).

**Summary:**

* **`data`** holds exactly the information you requested in the `columns` array.
* **`metadata`** captures your original input (domains, columns, index) and when the API processed your request.

## **Endpoint: `sublocations`**

Retrieves all child locations (“sublocations”) for a given parent level and value.

**Parameters**

* `parent_level` (string) – Geographic hierarchy to drill into:
  * `all` – return every level of sublocation
  * `country` – states/regions within a country
  * `state` – regions/districts within a state
  * `region` – districts/municipalities within a region
  * `district` – municipalities within a district
  * `municipality` – localities within a municipality
* `parent_value` (string) – The name of the parent location (e.g. `"Germany"`).
* `index` (string) – The data index or pattern to query (e.g. `"webai*"`).

```python
import requests

api_url = 'https://api.istari.ai/v1/sublocations'

headers = {
    'x-api-key': 'sk_api_key',
    'Content-Type': 'application/json'
}

payload = {
    "parent_level": "country", # this is the level of the parent location (it must be a string!!)
    "parent_value": "Germany", # this is the value of the parent location (it must be a string!!)
    "index": "webai*" # this is the index that you are looking for in the database (it must be a string!!)
}

response = requests.post(api_url, headers=headers, json=payload)
print(response.json())
```

The `sublocations` returns the immediate geographic subdivisions for a given parent level and value.

**Response Fields**

| Field         | Description                                                              |
| ------------- | ------------------------------------------------------------------------ |
| `locations`   | Array of sublocation names (e.g., Germany’s 16 states)                   |
| `level`       | Granularity of returned locations (`"state"` when drilling into country) |
| `total_count` | Number of items in the `locations` array                                 |

**Example**\
Based on above provided payload, the return result will be:

```json
{
    "locations": ["Nordrhein-Westfalen", "Bayern", "Baden-Württemberg", "Niedersachsen", "Hessen", "Berlin", "Rheinland-Pfalz", "Sachsen", "Schleswig-Holstein", "Thüringen", "Hamburg", "Brandenburg", "Sachsen-Anhalt", "Mecklenburg-Vorpommern", "Saarland", "Bremen"], 
    "level": "state", 
    "total_count": 16
}
```

## **Endpoint: `search`**

**Description**\
Fetches company records from the search backend in two modes:

* **Similarity (KNN) Search** when you supply `domains`.
* **Keyword Search** when `domains` is empty, using `keywords`, `locations`, and `custom_filters`.
* **Semantic (KNN) Search :** when you apply `semantic_input`.

**Request Parameters**

| Name             | Type       | Description                                                                      |
| ---------------- | ---------- | -------------------------------------------------------------------------------- |
| `search_id`      | `string`   | UUID to uniquely identify this search.                                           |
| `domains`        | `string[]` | _(Optional)_ Seed domains for embedding-based similarity search.                 |
| `excludes`       | `string[]` | _(Optional)_ Domains to omit from results.                                       |
| `keywords`       | `object`   | Term filters (`must_one`, `must_all`, `must_not`).                               |
| `locations`      | `object`   | Geographic filters (`country`, `state`, `region`, etc.).                         |
| `custom_filters` | `object`   | Field-level filters (must match allowed filter columns).                         |
| `index`          | `string`   | Data index or pattern (default: `"webai*"`).                            |
| `size`           | `integer`  | Number of results (1–100, default: 25).                                          |
| `columns`        | `string[]` | Fields to return (defaults to the core output columns).                          |
| `pit_id`         | `string`   | _(Optional)_ Point-in-time ID for consistent pagination.                         |
| `search_after`   | `any[]`    | _(Optional)_ Cursor token from previous response for efficient, deep pagination. |
| `semantic_input` | `string`   | _(Optional)_ The semantic input (as the user query) .                            |

**Response Structure**

* `data`: Array of company objects containing the requested `columns`.
* `metadata`: Echoes your inputs (including `domains`, `keywords`, `locations`, `columns`), plus query details and timestamps.

> For the full list of **Available Columns** and their descriptions, please refer to the Dataset Codebook. The codebook provides detailed information about all available variables, their data types, possible values, and descriptions. It also includes information about which fields can be used in `custom_filters` parameter.

**Important Note:** The domains and semantic\_input can only one of them are having value else it will trigger an error.

```python
# code for similarity search when you have a list of domains
import requests

api_url = 'https://api.istari.ai/v1/search'
headers = {
    'x-api-key': 'sk_api_key',
    'Content-Type': 'application/json'
}

payload = {
        "search_id": [], # this is the search id (it must be a string as uuid!!)
        "domains": [],  # this is the list of domains that you are looking for in the database (it must be a list of strings!! or None)
        "excludes": [],                                                                             # this is the list of domains that you want to exclude from the search (it must be a list of strings!!)
        "keywords": {"must_one": ["packaging"], "must_all": [], "must_not": []},
        "locations": {"country": ["United Kingdom"], "state": [], "region": []},
        "custom_filters": {"b2x": ["B2C", "B2B"]},  # apply extra field-level constraints (e.g. `country`, `team.name`, `products.type`). Each key must be an allowed column, and its list of values becomes filter clauses to precisely include or exclude documents.
        "index": "webai*",
        "size": 1,
        "semantic_input": None,                                                                     # this is the semantic input that you are looking for in the database (it must be a string!!), if not using it please set it to None
        "columns": [
            "domain",
            "country",
            "state",
            "title",
            "description",
            "keywords",
            "region_code"
        ],
        "pit_id": None,
        "search_after": [],                                                                         # cursor-based paging: use the last hit’s sort values to fetch the next batch. It’s more efficient and consistent than deep offsets.
    }

response = requests.post(api_url, headers=headers, json=payload)
print(response.json())
```

The `search` endpoint return those similar company based on inserted keywords and locations

* **Data**
  * Returns one company record matching your criteria:
    * `domain`: The website queried (`ledburytownfc.co.uk`)
    * `country` / `state`: Geographic info (`United Kingdom`, `England`)
    * `title`, `description`, `keywords`: Metadata scraped from the site (empty here)
    * `region_code`: Internal code for the region
* **Metadata**
  * **`total_hits`**: \~2.48 million matches in the index
  * **`search_id`**: Your unique search identifier
  * **`search_input`**: Echoes your request parameters (filters, size = 1, requested columns)
  * **`query`**: The boolean query built from your filters
  * **`pit_id`** & **`search_after`**: Cursor tokens for efficient pagination
  * **`start_time`** / **`end_time`**: When the query ran

> In short: you asked for one UK-based domain, and the API returned its basic fields plus metadata about how the search was executed and how to page further.

***

## **Endpoint: `api-usage`**

**Description**\
Check API Usage of the user.

**Behavior**

* Return the user API usage that recorded in the database as how much requests they sent.

```python
import requests

api_url = 'https://api.istari.ai/v1/api-usage'
headers = {
    'x-api-key': 'sk_api_key',
    'Content-Type': 'application/json'
}
response = requests.get(api_url, headers=headers)
print(response.json())
```

If needed to use the API, please contact us at `support@istari.ai` for requesting your own API Key and pricing details. Then you can to access the API with our enriched dataset.
