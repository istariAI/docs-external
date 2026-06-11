---
description: Find companies that are engaged in the mobility sector.
cover: ../.gitbook/assets/mobility.jpg
coverY: 4
---

# 🚗 Mobility

<details>

<summary>What do we measure?</summary>

The webAI Mobility Agent was trained by ISTARI.AI to derive companies’ commitment to mobility from their websites and to display it as an individual Mobility Intensity Score. This numerical indicator reflects how centrally the topic of mobility is communicated by the company on its own website and presented as essential for its own business model.

Mobility is to be understood as a broad concept. This includes services and products that are used directly as a means of transport (e.g. manufacturers of e-bikes or automobiles), but also, for example, suppliers of components and software for the production of means of transport or mobility service providers such as public transport. Thus, among others, players from the automotive industry, railroad, aerospace, shipping, logistics, telematics (e.g. intelligent transport systems), e-mobility or fuel cell technology are considered. However, WebAI also finds, for example, companies that specialize in the construction of underground garages, electricians who install wallboxes, or chemical manufacturers who produce lubricants for the automotive industry.

Companies that are active in these mobility-related areas, have business fields geared to them, or offer products and services with a direct connection, usually communicate this on their websites. The more central the topic is for the company, the more significant it is for the company’s external communication. For example, a startup for bicycle helmets communicates almost exclusively on the topic of mobility, while a chemical company, which among many other products also offers specific soaps for automotive workshops, does so only to a limited extent.

</details>

<details>

<summary>How do we measure?</summary>

Our webAI reads the website of the company under investigation and searches for text sections (paragraphs) that deal with the topic of mobility. To do this, webAI first searches for keywords that are potentially related to mobility, analyzes the paragraphs identified in this way, and determines whether or not they are actually mobility-related texts. If webAI has assigned a corresponding paragraph to the topic of mobility with a high probability, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website or the particularly relevant “top-level” sub-pages if it is a very extensive website with hundreds of sub-pages (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).

In this way, webAI finds a certain number of paragraphs per company website that deal with the topic of mobility. WebAI then puts this number in relation to the total amount of text content read on the website. In this way, webAI determines a mobility intensity for each company.

</details>

<details>

<summary>How do you interpret the data?</summary>

The Mobility Intensity Score calculated in this way would be 0.0 for a company with no mobility-related texts. For the example of a chemical company described above, on the other hand, the value could be 0.15, and 3.97 for the startup that is particularly focused on mobility. The Mobility Intensity Score has no upper limit. In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the chemical company would be classified as “low” intensity and the startup as “very high” intensity.

In contrast to simpler, binary classifications (“Mobility YES/NO”), webAI outputs a continuous score at the company level. This makes it possible to distinguish between companies for which mobility is only a peripheral issue and those for which it plays a central role. Users of the webAI data can thus easily determine for themselves how strongly a company should adopt mobility for it to be relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland), it can be said that 20.5% of the companies studied have a Mobility Intensity Score of greater than 0.0 and thus communicate the topic of mobility in some form on their websites. The average Mobility Intensity Score of these companies is 0.61 and half of the companies have a score lower than 0.30. The maximum score achieved is 6.93, with 21.63% achieving a score of 1.0 or higher.

</details>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI Mobility Agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then delivers expert-level results. For this agent ISTARI.AI has collaborated with researchers from the [University of Salzburg](https://www.plus.ac.at/?lang=en). The Mobility Intensity Scores are currently also being validated in a not yet published study.

</details>
