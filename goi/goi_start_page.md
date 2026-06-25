# Welcome to the ISTARI Global Organization Index

The Global Organization Index (GOI) is our curated, organization-level dataset containing **approximately 20 million active organizations** across **232 countries and territories**. It serves as the canonical source for firmographic data at ISTARI, covering organization identity, location, industry classification, size, and more.

<Frame>
  <img src="/images/goi_example_query.png" alt="" />
</Frame>

## Data Pipeline & Methodology

GOI is built through a multi-step validation pipeline designed to prioritize quality over volume:

1. **Registry Collection** — We systematically query national registers worldwide — including organization, commercial, and association registers. This primary data source is then enriched with additional open data sources, giving us an initial pool of approximately **400 million organizations**.
2. **Domain Attribution** — We determine which of these organizations can be attributed to a clearly identifiable web domain. This results in roughly **10%** of the total — about **40 million organizations**. The remainder are either no longer active, were never truly operational (e.g., pure holding structures), or simply never maintained a web presence.
3. **Activity Verification** — We verify which of those 40 million domains are still actively operated. This validation step brings the dataset down to approximately **20 million organizations** that are demonstrably active.

This process ensures that every record in GOI is web domain-verified and confirmed active.

### Quality vs. Volume

Our final dataset is smaller than comparable, traditional databases. However, in contrast, our dataset contains exclusively verified and active organizations — no inactive records or dormant entities. The key differentiator is not size, but data timliness, operational relevance, and verification depth.

### Data Sources

| Source Type | Role | Examples |
|---|---|---|
| National registers | Primary source | Company registers, commercial registers, association registers |
| Open data sources | Enrichment | Government databases, administrative statistics data, structured open datasets |
| Web presence | Verification | Organisation websites, active domain validation |


## Schema

### Key Definitions

- **NACE Code** — The EU's standard statistical classification of economic activities. Used as GOI's primary industry taxonomy. [Learn more](https://ec.europa.eu/eurostat/web/nace)
- **Organization Type** — Categorized as Company, Startup, Academic, Public, or Other based on registry data and web content analysis.
- **Organization Size** — Derived from employee and revenue signals, bucketed into Micro, Small, Medium-sized, and Large enterprise per EU SME definitions.

### Core Fields

| Column | Type | Description |
|---|---|---|
| `name` | STRING | Organization name |
| `domain` | STRING | Organisation website domain |
| `summary` | STRING | AI-generated summary of the organization |
| `keywords` | LIST | Descriptive keywords |
| `employee_class` | STRING | Employee count bracket |
| `country` | STRING | Country name |
| `country_code` | STRING | ISO country code |
| `state` / `state_code` | STRING | State or province |
| `region` / `region_code` | STRING | Region |
| `district` / `district_code` | STRING | District |
| `municipality` / `municipality_code` | STRING | Municipality |
| `address` | STRING | Full address |
| `latitude` | FLOAT64 | Latitude coordinate |
| `longitude` | FLOAT64 | Longitude coordinate |

### Classification Fields

| Column | Type | Description |
|---|---|---|
| `nace_code` | STRING | NACE industry classification code |
| `nace_reasoning` (optional) | STRING | Reasoning behind the assigned NACE code |
| `organization_type` | STRING | Type of organization (Company, Public, Academic, Startup, Other) |
| `organization_type_reasoning` (optional) | STRING | Reasoning behind the assigned type |
| `organization_size` | STRING | Size bracket (Micro, Small, Medium-sized, Large enterprise) |
| `organization_size_reasoning` (optional) | STRING | Reasoning behind the assigned size |

**Note:** Reasoning fields are not published in the standard dataset.

## Coverage Statistics

### At a Glance

| Metric | Value |
|---|---|
| Total organizations | ~20,000,000 |
| Countries & territories | 232 |
| Industry sectors (NACE) | 22 |
| Last updated | February 2026 |

### Top 20 Countries by Volume

| Country | Organizations |
|---|---|
| United States | 3,626,794 |
| Germany | 1,828,181 |
| United Kingdom | 1,013,026 |
| Netherlands | 778,416 |
| Italy | 625,754 |
| Australia | 601,797 |
| France | 571,895 |
| Japan | 461,640 |
| Brazil | 421,034 |
| Canada | 366,258 |
| Poland | 339,745 |
| Czechia | 268,404 |
| Spain | 250,467 |
| Belgium | 233,349 |
| Switzerland | 219,274 |
| Sweden | 199,470 |
| India | 186,750 |
| Russia | 182,112 |
| Austria | 158,644 |
| Denmark | 140,840 |

### Organization Size Distribution

| Size | Employee Range | Count | Share |
|---|---|---|---|
| Micro | 0–9 | 7,341,838 | 42.78% |
| Small | 10–49 | 7,494,409 | 43.67% |
| Medium-sized | 50–249 | 1,501,655 | 8.75% |
| Large enterprise | 250+ | 824,126 | 4.80% |

### Top 10 Industries (NACE)

| NACE Code | Industry | Count | Share |
|---|---|---|---|
| N | Professional, scientific & technical activities | 3,093,879 | 18.03% |
| G | Wholesale & retail trade | 2,240,191 | 13.05% |
| C | Manufacturing | 2,006,435 | 11.69% |
| R | Human health & social work | 1,440,340 | 8.39% |
| K | Telecom, IT & computing | 1,269,131 | 7.39% |
| F | Construction | 1,173,226 | 6.84% |
| I | Accommodation & food service | 1,126,594 | 6.56% |
| S | Arts, sports & recreation | 1,101,592 | 6.42% |
| Q | Education | 584,430 | 3.41% |
| J | Publishing, broadcasting & content | 554,985 | 3.23% |

### Notes on Geographic Data

Approximately 2.7 million organizations in the dataset do not have a standardized administrative region.

These organizations are **intentionally retained** in the dataset. While they cannot be filtered by geographic region, they remain valuable for non-geographic analyses (e.g., industry, size, domain-level insights).

When an organization appears multiple times (e.g., the same domain linked to different addresses), we deduplicate by domain and retain the record with the highest employee count, treating it as the organization's headquarters.

### Delivery

- **Formats:** CSV, Excel, API, web app, parquet or any other requested file format for big data.
- **Delivery type:** One-time dataset delivery or ongoing updates (discuss with the team)
- **Filters available:** By country, industry (NACE), size, organization type, keyword filter, similarity filter, or any combination