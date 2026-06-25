---
title: "Privacy"
description: Data handling for GOI MCP, what we log, where it lives, retention, embedding cache, and GDPR rights.
---

This page covers data handling specific to GOI MCP. For istari.ai's full privacy policy and legal notices, see the [imprint](https://www.istari.ai/en/imprint#privacypolicy).

## Data controller

**istari.ai GmbH**\
Julius-Hatry-Straße 1\
68163 Mannheim, Germany

Data Protection Officer: Dr. Sebastian Schmidt. Contact: [support@istari.ai](mailto:support@istari.ai).

## Where data lives

Application data is processed and stored in **Google Cloud `europe-west3` (Frankfurt)**. The Postgres database, application servers, and audit logs are all in-region.

## What we log

Every MCP tool call produces one row in our `request_log` table. Each row stores:

* Your istari.ai user ID and tier.
* The tool name (e.g. `search_organizations`).
* The structured arguments you passed: for example, your search query text, the domain list you asked us to fetch, the filter values you applied. We log these so we can enforce monthly quotas, debug failures, and improve relevance.
* The result count returned and the wall-clock duration.
* HTTP status and error code (if any).

We **do not log**: your full conversation with the AI client, the text the AI client generated around the tool call, your IP address, or your user-agent string.

## How long we keep it

* **Server / HTTP access logs**: retained for at most **7 days**, per the istari.ai [privacy policy](https://www.istari.ai/en/imprint#privacypolicy).
* **Application request log** (the `request_log` table described above): retained for **24 months**, then deleted.
* **Embedding cache**: embeddings of submitted reference domains are retained indefinitely. They are derived numerical features, not personal data.

## Cross-tenant isolation

* Your queries and results are never visible to other users.
* Your queries are **not** used to train AI models.
* Your queries are **not** sold or shared with third parties beyond the sub-processors listed in the [istari.ai privacy policy](https://www.istari.ai/en/imprint#privacypolicy) (Google Cloud for hosting, Clerk for authentication, Azure OpenAI for embedding generation).

## Scraping and the embedding cache

When you pass a reference domain to `find_similar_organizations` or `find_similar_with_steering`, GOI MCP tries to look up that domain in our database first. If the domain is **not** already indexed, the server fetches the public website and generates an embedding from it on demand.

* The fetched URLs are **public web pages**: the same content anyone with a browser can see.
* We cache the resulting **embedding** (a numerical vector), not the raw page content. The cache is **shared across the user base** so that the same domain isn't re-fetched repeatedly. This is purely a performance optimization.
* Subsequent requests for the same domain: from you or from any other user, re-use the cached embedding and trigger no further HTTP fetch.

The crawler respects standard `robots.txt` directives.

## Authentication and tokens

Authentication uses **OAuth 2.1 with Dynamic Client Registration**, backed by [Clerk](https://clerk.com/). Access tokens are issued to your AI client (not stored on istari.ai side beyond verification caches), are short-lived, and are refreshed automatically by the client.

We verify JWTs against Clerk's JWKS and fetch your profile metadata (tier, scope) via Clerk's userinfo endpoint with a five-minute in-memory cache. We do not see your password.

## GDPR rights

If you are an EU resident, you have the right to access, rectify, erase, restrict, and port your personal data, and to object to processing. To exercise any of these rights, email [support@istari.ai](mailto:support@istari.ai). Standard response window is 30 days.

## Updates to this page

Material changes to data handling will be reflected here and in the changelog of new GOI MCP revisions. For binding policy language, the [istari.ai privacy policy](https://www.istari.ai/en/imprint#privacypolicy) is authoritative.
