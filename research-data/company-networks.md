---
description: Explore company networks.
cover: ../.gitbook/assets/network.jpg
coverY: -31
---

# 🎆 Company networks

<details>

<summary>What do we measure?</summary>

The webAI Company Networks Agent captures hyperlinks between companies’ websites to map their interconnectedness. Companies link to the websites of other economic actors for various reasons. For example, companies often name reference customers on their websites and then usually also set up a hyperlink to their website. With webAI we quantify these linkages by identifying hyperlink connections between companies.

</details>

<details>

<summary>How do we measure?</summary>



Our webAI reads the website of the examined company and searches it for hyperlinks that target other websites (domains). Thus, webAI searches the entire corporate website, or the particularly relevant “top-level” sub-webpages, if very extensive websites with hundreds of sub-webpages are involved (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).&#x20;

WebAI thus finds a certain number of hyperlinks per company website that point to external websites. Then, webAI merges this information with content from all other corporate websites that were also searched. Thus, webAI identifies not only “outbound” hyperlinks, i.e., those pointing from Company A to Companies B, C, and D, but also “inbound” hyperlinks, i.e., hyperlinks from Companies B, E, and F pointing to Company A. From this information, webAI calculates the following variables that provide information about the interconnectedness of the company:

1. Incoming links: The destination domains of all outbound hyperlinks from a company’s website.
2. Incoming links count: The total number of target domains of all outgoing hyperlinks from a company’s website.
3. Outgoing Links: The origin domains of all incoming hyperlinks pointing to a company’s website.
4. Outgoing links count: The total number of origin domains of all inbound hyperlinks pointing to a company’s website.
5. Links: Variable (1)and (3) combined.
6. Links Count: The number of domains from (5).

</details>

<details>

<summary>How do you interpret the data?</summary>

The data collected with webAI Company Networks maps the hyperlink connections between the examined company websites. This relational data can be examined for more complex analysis using specialized software for network analysis. For example, centrality measures or cluster detection algorithms can be applied. However, the data provided also allows valuable insights into the networking of individual companies without further analysis.&#x20;

For example, a glance at the “Links Count” column reveals how many other companies the company under consideration is connected to via a hyperlink. This variable combines both all outgoing links from the company under consideration and all incoming links from other companies. As an example for the DACH region (Germany, Austria, Switzerland), it can be said that companies have an average “Links Count” of 13.1 (median 6.0), with 9.4% of companies having no hyperlinks to other companies at all. The maximum achieved value for “Links Count” is 559,203, which is google.com. Depending on the nature of the question, it is recommended to remove such outliers from the data.&#x20;

</details>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI Comapny Networks was developed and validated together with independent subject matter experts. This way, we ensure that the results of the webAI agents are validated in the context of external studies at a high scientific level. For the development of this agent ISTARI.AI collaborated with ZEW – Leibniz Centre for European Economic Research in Mannheim, the University of Salzburg and the Technical University of Berlin. In addition, the results of the agent have been used in scientific studies, including by researchers at the University of Groningen in the Netherlands and in a joint study with researchers at ETH Zurich. The latter study was awarded the Best Paper Award at the renowned “R\&D Management Conference 2022”.

</details>
