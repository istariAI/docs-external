---
title: "Research workflows"
description: "Multi-step recipes that chain GOI tools together — size a market, map it, and drill into individual companies in one flow."
---

A single tool call answers a single question. Real research chains them: resolve a place, size the sector, pull the players, then drill into one. These workflows are validated end-to-end against the live index.

## Workflow 1 — Size & map a niche market in a region

**Goal:** "How big is the battery-manufacturing scene in Bavaria, and who are the players?"

```python
# 1. Resolve the place to a canonical filter (NATIVE name — see note)
resolve_location(query="Bayern")
#   → state "Bayern" · filter {"state": ["Bayern"]} · 324,463 orgs

# 2. Size the sector in that region (exact, deterministic)
aggregate_organizations(
    country=["Germany"], state=["Bayern"],
    nace_code=["NACE C: Manufacturing"], group_by="organization_size",
)
#   → Small 14,462 · Micro 12,457 · Medium 2,932 · Large 1,692  (~31.5k manufacturers)

# 3. Pull the actual players (niche-finder pattern, scoped to the region)
search_organizations(
    query="manufacturer of battery cells, modules and packs for EVs and energy storage",
    keywords_must_all=["battery"], state=["Bayern"],
    nace_code=["NACE C: Manufacturing"], size=10,
)
#   → Smart Battery Solutions, LION Smart, A² Battery Solutions, CATL (Bavaria), BMZ Group

# 4. Drill into one for a full profile
get_organization_details(domains=["lionsmart.com"])
#   → LION Smart GmbH · Garching b. München · NACE C · battery/BMS/e-mobility keywords
```

<Warning>
  **Use native place names with `resolve_location`.** `resolve_location("Bavaria")` returns junk (it fuzzy-matched *Bagnaria, Italy*). `resolve_location("Bayern")` returns the real state. Resolve first, then pass the returned filter object verbatim.
</Warning>

## Workflow 2 — Competitive landscape from a seed company

**Goal:** "Map the competitors of a company I know, then profile the top ones."

```python
# 1. Find lookalikes by embedding similarity
find_similar_organizations(
    domains=["celonis.com"], exclude_domains=["celonis.com", "celonis.de"],
    min_score=0.6, size=15,
)
#   → Mimica, mindzie, iGrafx, ARIS, Wang Fan Xin … (the process-mining cluster)

# 2. (optional) Size the cluster by geography or scope it
#    aggregate_organizations(nace_code=[...], group_by="country")

# 3. Hydrate the shortlist for outreach / analysis
get_organization_details(domains=["mimica.ai", "mindzie.com", "igrafx.com"])
```

## Why chain instead of one big query

- **Different tools answer different questions.** `aggregate` gives exact counts but ignores keywords; `search` ranks but its `Total` is unreliable. Use each for what it's good at.
- **Resolve → filter → search → hydrate** keeps every step deterministic and reproducible.
- For the per-step parameter discipline, see the [Cookbooks](/cookbooks/overview); to make an agent do this automatically, install the [Agent skill](/mcp/agent-skill).
