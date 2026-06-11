---
description: >-
  The starting point for most workflows on the webAI Platform. Allows you to
  compile custom company lists for further processing.
---

# 📄 Company List Creator

The Company List Creator can be used to compile individual company lists using a mixture of keyword-based searches, geography filters and webAI indicators. When you first open the creator, you see a minimalist view in which most of the available filters are hidden for a better overview.

<figure><img src="../.gitbook/assets/15_company_list_creator.png" alt=""><figcaption><p>Company List Creator interface with hidden filters.</p></figcaption></figure>

In order to start searching for companies, you can, for example, enter a keyword in the search bar that matches the companies you are looking for. This could be, for example, a specific technology mentioned by the companies on their websites. Press enter on your keyboard or use the arrow to confirm your input.

<figure><img src="../.gitbook/assets/16_kw_search.png" alt=""><figcaption><p>Keyword search bar with exemplary keyword entered.</p></figcaption></figure>

Alternatively, you can also click on one of the popular keywords that are suggested to you.

<figure><img src="../.gitbook/assets/17_popular_keywords.png" alt=""><figcaption><p>Suggested popular keyword searches.</p></figcaption></figure>

Another option is to activate the keyword generator to automatically generate suitable keywords and keyword combinations based on your own entries. Please note that this function consumes the displayed credits each time it is activated.

As soon as a filter is active, this is displayed as shown below.

<figure><img src="../.gitbook/assets/18_active_filters.png" alt=""><figcaption><p>Active filter "Keyword" with 1 active keyword.</p></figcaption></figure>

## Results view

If any filters are active and at least one company has been found based on these filters, the results view appears. The number of companies found is displayed at the top. In the `Dataframe` view, which is activated by default, you will also see a map on the left with the locations of the companies found. On the right, you can see the results in tabular form, whereby each company found corresponds to a row.

<figure><img src="../.gitbook/assets/19_results_view_table.png" alt=""><figcaption></figcaption></figure>

Please note that the results view only shows a small selection of the companies actually found (preview). For the complete data set, you must use the [Company List Downloader](broken-reference) module, which will be explained later.

The columns displayed within the table can be customized using the "Select Columns" drop-down menu. Please note that different columns ([indicators](indicators-overview.md)) may be available to you depending on your active subscription.

<figure><img src="../.gitbook/assets/21_column_selection.png" alt=""><figcaption><p>Select columns drop-down menu with three active columns.</p></figcaption></figure>

As an alternative result view, the card view can opened by clicking on `Companies`, in which a selection of the companies found is displayed. Click on the individual cards to open a detailed view of the company in question.

<figure><img src="../.gitbook/assets/20_results_view_cards.png" alt=""><figcaption><p>Search results in the card view.</p></figcaption></figure>

## Filters

Click on `Show Filters` to open the filter detail view.

<figure><img src="../.gitbook/assets/22_filters (1).png" alt=""><figcaption><p>Detailed filters view.</p></figcaption></figure>

### Keyword filters

On the left-hand side you can see the three available keyword filters:

* Optional: At least 1 of the keywords listed here must be named.
* Mandatory: All keywords listed here must be specified.
* Blacklist: None of the keywords listed here may be mentioned.

In the example below, we are looking for all companies that mention "packaging machine" and at least one additional keyword from "producer" and "manufacturing". We also use a \* wildcard as a blacklist keyword. This wildcard in "consult\*" allows us to filter words such as "consulting" or "consultants" with just one keyword.



<figure><img src="../.gitbook/assets/23_keyword_filters (1).png" alt=""><figcaption><p>Exemplary advanced keyword search.</p></figcaption></figure>

You can remove keywords individually by activating the x next to the keyword. Each change in the filters immediately updates the hits displayed.

Please note that the keyword search is language-specific. For example, you must enter the German word "Verpackungsmaschine" if you want to search for it, as "packaging machine" will probably not return the desired results for company websites in German.

Alternatively, you can also activate the slider for "webAI Multilingual Search", which automatically translates your keywords into over 20 relevant languages in the background and uses them for the search. Please note that the multilingual search is a function for which the displayed webAI credits must be used. The multilingual search also takes a little longer.

### Geo filters

On the right-hand side of the detailed filter view, at the top, you find the filters with which companies can be filtered according to their location. With the `All Locations` search bar, you can search for specific regions and use them as filters. After clicking on `Set Locations`, the selected locations are applied as filters.

<figure><img src="../.gitbook/assets/25_set_location.png" alt=""><figcaption><p>Exemplary georaphic filters for the regions of Mannheim and Paris.</p></figcaption></figure>

Under the `All Locations` filter you will find the filters for the [administrative units](../tools/administrative-units.md). Select the different administrative levels one after the other to use one or more regions as a filter. In the screenshot below, for example, "United States of America" has been selected as the `Country` filter, which activates the US states in the `State` drop-down menu, which in turn can be selected as further filters.

<figure><img src="../.gitbook/assets/26_region_select.png" alt=""><figcaption><p>Administrative units as geo filters.</p></figcaption></figure>

### Other filters

Under the geo filters you can find a number of other filters with which you can, for example, exclude all companies for which no contact information is available, which are retailers or pure news providers.

<figure><img src="../.gitbook/assets/27_other_filters.png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Retailer</summary>

In addition to using our [TechStack ](../indicators-research-data/website-techstack.md)indicator to filter companies with online shops, we build an additional indicator to discard retailers. We indicate the probability of a company website to belong to a retailer from low probability to high probability. Each class can be `Include` or `Exclude` and you may reset the filters just as with the geography filters described above.

</details>

<details>

<summary>News provider</summary>

Additional filter to discard news providers (i.e. news outlets like newspapers, online magazines, academic journals, blogs). Functionality is identical to the drop-down menus described above. In some searches it can be advantageous to exclude such websites. For example, if you are looking for an emerging technology, you may only want to find manufacturing companies that already mention this technology on their website, but not media companies that report on this technology on their websites. We indicate the probability of a company website to belong be a news provider from low probability to high probability.&#x20;

</details>

<details>

<summary>Domain provider</summary>

Additional filter to discard domain providers. Functionality is identical to the drop-down menus described above. When companies shut down business and their domains (i.e. website addresses) are up for sale, the domain vendors (i.e. domain provider) shows ads when accessing these domains. In order to filter such cases you may `Exclude` the `1` values using this drop-down menu.

</details>

### TechStack

You can use the TechStack filter to find companies that have integrated certain website technologies on their websites. It is best to take a look at the[ exact description of the indicator](company-list-creator.md#techstack). This filter works just like a keyword filter and you can simply enter the names of the relevant technologies and the results will be updated to show that the companies found must have integrated at least one of the specified technologies.

<figure><img src="../.gitbook/assets/28_TechStack.png" alt=""><figcaption><p>Exemplary TechStack search for HubSpot website technologies.</p></figcaption></figure>

### Advanced filters

A click on `Show Advanced Filters` reveals another set of filters that are only available to users of certain webAI plans. Here, companies can be searched for specifically using advanced webAI indicators. In the example below, only companies with a link to the istari.ai website, an [AI Intensity Level](../indicators-research-data/artificial-intelligence.md) of "high" or "very high" and a [Sustainability Intensity](../indicators-research-data/sustainability.md) of "low" or "very low" are displayed as hits.

<figure><img src="../.gitbook/assets/29_advanced_filters.png" alt=""><figcaption><p>Advanced filters.</p></figcaption></figure>

## Save, load and clear filters

You can save the filters you have set and the company list you have created (companies that match your filters) by entering a name that has not yet been used and clicking `Save Company List`. Saved lists can be selected via the drop-down menu next to `Load Company List` and loaded using the same button. Be careful, the currently set filters will be overwritten.

Click on `Clear Filters` to reset all filters and search results.

<figure><img src="../.gitbook/assets/30_save_load_clear_filters.png" alt=""><figcaption><p>Save, load and clear filters.</p></figcaption></figure>
