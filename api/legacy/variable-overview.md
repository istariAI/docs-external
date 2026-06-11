
# Variable Overview

> This reference describes variables on the **legacy company dataset** exposed by `api.istari.ai`. For GOI organisation fields, see [Reference: columns and filters](../goi-reference.md).

### Company Identification <a href="#company-identification" id="company-identification"></a>

| `name`                 | String  | Real-value                                                                 | Company or organization name                                                                       |
| ---------------------- | ------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `type`                 | String  | Company type                                                               | Classification of the organization type                                                            |
| `domain`               | String  | Real-value                                                                 | Primary web domain of the company                                                                  |
| `domain_alias`         | String  | Real-value                                                                 | Alternative or secondary domain names                                                              |
| `domain_provider_true` | Boolean | 0, 1                                                                       | Indicates if the domain provider information is verified                                           |
| `domain_redirect`      | Boolean | 0, 1                                                                       | Indicates if the domain redirects to another URL                                                   |
| `b2x`                  | String  | B2B, B2C, B2G                                                              | Business model classification (Business-to-Business, Business-to-Consumer, Business-to-Government) |
| `employee_class`       | String  | 0-10 employees, 11-50 employees, 51-250 employees, 250+ employees, unknown | Company size classification based on number of employees                                           |
| `new_register_entry`   | Boolean | true, false                                                                | Indicates if this is a newly registered entry in the database                                      |

### Geographic Information <a href="#geographic-information" id="geographic-information"></a>

| `continent`         | String | Asia, Africa, North America, South America, Antarctica, Europe, Australia | Continental location                 |
| ------------------- | ------ | ------------------------------------------------------------------------- | ------------------------------------ |
| `country`           | String | Real-value                                                                | Country name                         |
| `country_code`      | String | Real-value                                                                | ISO country code                     |
| `state`             | String | Real-value                                                                | State or province name               |
| `state_code`        | String | Real-value                                                                | State or province code               |
| `region`            | String | Real-value                                                                | Regional administrative division     |
| `region_code`       | String | Real-value                                                                | Regional code identifier             |
| `district`          | String | Real-value                                                                | District administrative division     |
| `district_code`     | String | Real-value                                                                | District code identifier             |
| `municipality`      | String | Real-value                                                                | Municipal administrative division    |
| `municipality_code` | String | Real-value                                                                | Municipal code identifier            |
| `address`           | String | Real-value                                                                | Physical address of the organization |

## Technology Intensity Measures

### Artificial Intelligence

| Variable             | Data Type | Values                                 | Description                                             |
| -------------------- | --------- | -------------------------------------- | ------------------------------------------------------- |
| `ai_intensity`       | Double    | Real-value                             | Numerical measure of AI technology adoption/focus       |
| `ai_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of AI intensity              |
| `ai_keywords`        | String    | Real-value                             | Keywords related to AI technologies used by the company |

### Additive Manufacturing (3D Printing)

| Variable                                 | Data Type | Values                                 | Description                                                    |
| ---------------------------------------- | --------- | -------------------------------------- | -------------------------------------------------------------- |
| `additive_manufacturing_intensity`       | Double    | Real-value                             | Numerical measure of additive manufacturing adoption           |
| `additive_manufacturing_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of additive manufacturing intensity |
| `additive_manufacturing_keywords`        | String    | Real-value                             | Keywords related to additive manufacturing technologies        |

### Blockchain Technology

| Variable                     | Data Type | Values                                 | Description                                         |
| ---------------------------- | --------- | -------------------------------------- | --------------------------------------------------- |
| `blockchain_intensity`       | Double    | Real-value                             | Numerical measure of blockchain technology adoption |
| `blockchain_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of blockchain intensity  |
| `blockchain_keywords`        | String    | Real-value                             | Keywords related to blockchain technologies         |

### Digital Health

| Variable                         | Data Type | Values                                 | Description                                            |
| -------------------------------- | --------- | -------------------------------------- | ------------------------------------------------------ |
| `digital_health_intensity`       | Double    | Real-value                             | Numerical measure of digital health technology focus   |
| `digital_health_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of digital health intensity |
| `digital_health_keywords`        | String    | Real-value                             | Keywords related to digital health technologies        |

### Energy Technology

| Variable                 | Data Type | Values                                 | Description                                               |
| ------------------------ | --------- | -------------------------------------- | --------------------------------------------------------- |
| `energy_intensity`       | Double    | Real-value                             | Numerical measure of energy technology focus              |
| `energy_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of energy technology intensity |
| `energy_keywords`        | String    | Real-value                             | Keywords related to energy technologies                   |

### Mobility Technology

| Variable                   | Data Type | Values                                 | Description                                                 |
| -------------------------- | --------- | -------------------------------------- | ----------------------------------------------------------- |
| `mobility_intensity`       | Double    | Real-value                             | Numerical measure of mobility technology focus              |
| `mobility_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of mobility technology intensity |
| `mobility_keywords`        | String    | Real-value                             | Keywords related to mobility technologies                   |

### Sustainability

| Variable                         | Data Type | Values                                 | Description                                            |
| -------------------------------- | --------- | -------------------------------------- | ------------------------------------------------------ |
| `sustainability_intensity`       | Double    | Real-value                             | Numerical measure of sustainability focus              |
| `sustainability_intensity_level` | String    | very low, low, medium, high, very high | Categorical classification of sustainability intensity |
| `sustainability_keywords`        | String    | Real-value                             | Keywords related to sustainability practices           |

***

### Sustainable Development Goals (SDG)

| Variable               | Data Type | Values                                 | Description                                           |
| ---------------------- | --------- | -------------------------------------- | ----------------------------------------------------- |
| `sdg1_intensity`       | Double    | Real-value                             | Intensity score for SDG 1: No Poverty                 |
| `sdg1_intensity_level` | String    | very low, low, medium, high, very high | Categorical level for SDG 1 focus                     |
| `sdg1_keywords`        | String    | Real-value                             | Keywords related to poverty reduction efforts         |
| `sdg2_intensity`       | Double    | Real-value                             | Intensity score for SDG 2: Zero Hunger                |
| `sdg2_intensity_level` | String    | very low, low, medium, high, very high | Categorical level for SDG 2 focus                     |
| `sdg2_keywords`        | String    | Real-value                             | Keywords related to hunger and food security          |
| `sdg3_intensity`       | Double    | Real-value                             | Intensity score for SDG 3: Good Health and Well-being |
| `sdg3_intensity_level` | String    | very low, low, medium, high, very high | Categorical level for SDG 3 focus                     |
| `sdg3_keywords`        | String    | Real-value                             | Keywords related to health and well-being initiatives |

***

### Scoring and Probability Measures

| Variable                                | Data Type | Values                                                                                             | Description                                             |
| --------------------------------------- | --------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `cultural_score`                        | Integer   | Real-value                                                                                         | Numerical score measuring cultural aspects              |
| `cultural_score_category`               | String    | very low, low, medium, high, very high                                                             | Categorical classification of cultural score            |
| `leisure_score`                         | Integer   | Real-value                                                                                         | Numerical score related to leisure industry involvement |
| `leisure_score_category`                | String    | very low, low, medium, high, very high                                                             | Categorical classification of leisure score             |
| `recreational_score`                    | Double    | Real-value                                                                                         | Numerical score for recreational activities/services    |
| `recreational_score_category`           | String    | very low, low, medium, high, very high                                                             | Categorical classification of recreational score        |
| `transport_score_category`              | String    | very low, low, medium, high, very high                                                             | Categorical score for transportation-related activities |
| `innoprob_innovator_probability`        | String    | very low, low, medium, high, very high                                                             | Probability assessment of being an innovator            |
| `social_innoprob_innovator_probability` | String    | very low, low, medium, high, very high                                                             | Probability of being a social innovator                 |
| `news_probability`                      | String    | very low probability, low probability, medium probability, high probability, very high probability | Likelihood of appearing in news/media                   |
| `retailer_probability`                  | String    | very low probability, low probability, medium probability, high probability, very high probability | Probability of being classified as a retailer           |

## Company Structure and Team

### Structure Information

| Variable                | Data Type | Values     | Description                                 |
| ----------------------- | --------- | ---------- | ------------------------------------------- |
| `structure.name`        | String    | Real-value | Name of organizational structure/division   |
| `structure.type`        | String    | Real-value | Type of organizational structure            |
| `structure.description` | String    | Real-value | Description of the organizational structure |
| `structure.location`    | String    | Real-value | Location of the structure/division          |
| `structure.contact`     | String    | Real-value | Contact information for the structure       |

### Team Information

| Variable        | Data Type | Values     | Description                             |
| --------------- | --------- | ---------- | --------------------------------------- |
| `team.name`     | String    | Real-value | Team member name                        |
| `team.position` | String    | Real-value | Position/role of team member            |
| `team.contact`  | String    | Real-value | Contact information for team member     |
| `team.cv`       | String    | Real-value | Curriculum vitae or profile information |

## Products and Services

| Variable                 | Data Type | Values                                                                                    | Description                                    |
| ------------------------ | --------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------- |
| `products.name`          | String    | Real-value                                                                                | Name of product or service                     |
| `products.type`          | String    | Service, Product, Software, Subscription, Book, Event, Course, Program, Food, Game, Other | Classification of product/service type         |
| `products.main_features` | String    | Real-value                                                                                | Key features or characteristics of the product |
| `products.pricing`       | String    | Free, and others (real-value)                                                             | Pricing information for the product/service    |

## Partnerships

| Variable                         | Data Type | Values                                                                                                | Description                   |
| -------------------------------- | --------- | ----------------------------------------------------------------------------------------------------- | ----------------------------- |
| `partnerships.entity_name`       | String    | Real-value                                                                                            | Name of partner organization  |
| `partnerships.relationship_type` | String    | Cooperation, Customer, Supplier, Affiliate, Investor, Regulator, Other, Sponsor, Partner, Distributor | Type of business relationship |

## Contact Information

| Variable              | Data Type | Values     | Description                    |
| --------------------- | --------- | ---------- | ------------------------------ |
| `main_contact_mail`   | String    | Real-value | Primary email address          |
| `main_contact_number` | String    | Real-value | Primary phone number           |
| `all_mails`           | String    | Real-value | All associated email addresses |
| `all_phones`          | String    | Real-value | All associated phone numbers   |

## Technical and Content Data

| Variable           | Data Type | Values     | Description                                   |
| ------------------ | --------- | ---------- | --------------------------------------------- |
| `techstack`        | String    | Real-value | Technology stack used by the company          |
| `description`      | String    | Real-value | General description of the company            |
| `summary`          | String    | Real-value | Executive summary of the organization         |
| `summary_keywords` | String    | Real-value | Keywords extracted from the summary           |
| `keywords`         | String    | Real-value | General keywords associated with the company  |
| `text`             | String    | Real-value | Full text content related to the organization |
| `title`            | String    | Real-value | Title or headline associated with the entry   |
| `links`            | String    | Real-value | Web links associated with the company         |

## Data Quality Notes

* **Real-value**: Indicates that the field can contain any text or numerical value within the data type constraints
* **Boolean fields**: Use 0/1 or true/false depending on the specific variable
* **Intensity measures**: Higher numerical values typically indicate greater intensity or involvement
* **Categorical levels**: Five-point scale from "very low" to "very high" for most categorical variables
* **Probability measures**: Express likelihood using standardized probability categories

## Usage Guidelines

1. **Missing Values**: Fields marked as "Real-value" may contain empty or null values
2. **Data Validation**: Boolean fields should be validated for proper 0/1 or true/false values
3. **Geographic Hierarchy**: Geographic variables follow administrative hierarchy from continent to municipality
4. **Technology Intensity**: Both numerical and categorical versions are provided for flexibility in analysis
5. **Nested Fields**: Variables with dots (e.g., `team.name`) represent nested or structured data fields
