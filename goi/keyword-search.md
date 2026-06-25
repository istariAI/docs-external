---
title: "Keyword search"
---

Keyword Search is one of the [three ways to search](/goi/dashboard#three-ways-to-search) in GOI. Use this method when you want **exact term matching** over organization profiles, with full control over which words define a hit — no semantic interpretation, no reference company.

## How it works

* Switch to **Advanced** mode and pick **Use keywords** from the search-type dropdown in the search panel.
* Type a keyword into the search bar and press **Enter**. The keyword becomes a pill.
* Repeat for as many keywords as you need — each press of **Enter** adds another pill. Remove a pill with its **×** button, or press **Backspace** in the empty input to remove the last one.
* Run the search. GOI performs a full-text (BM25) search over organization profiles and returns matches, ranked by how well the keywords match each profile.

Keyword Search is ideal when:

* You know the exact terminology your target organizations use.
* Semantic paraphrasing is a risk (e.g. niche technical terms, brand names, standards).
* You want to sanity-check a semantic search by comparing against a strict keyword-only variant.

## Combine with filters

Keyword Search can be combined with any of the usual filters to narrow the scope further:

* [**Location Filters**](/goi/location-filters) — restrict to a country, state, district, or city.
* [**Organizational Filters**](/goi/organizational-filters) — restrict by organization size, type, or NACE sector.
* [**Keyword refinement filters**](/goi/advanced-search-filters) — layered *Must Include (Any / All)* and *Must Not Include* filters on top of the main keyword query, for even more precise control.

## See also

* [Semantic Search](/goi/semantic-search) — natural-language search when you don't have exact keywords.
* [Similarity Search](/goi/similarity-search) — find companies similar to a reference website.
