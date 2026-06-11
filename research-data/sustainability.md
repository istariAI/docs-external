---
description: Find companies that are engaged in sustainability.
cover: ../.gitbook/assets/sustainability.jpg
coverY: -7
---

# 🌳 Sustainability

<details>

<summary>What do we measure?</summary>

The webAI Sustainability Agent was trained by ISTARI.AI to derive from the websites of companies their commitment in the area of sustainability and to depict it as an individual Sustainability Intensity Score. This numerical indicator reflects how centrally the topic of sustainability is communicated by the company on its own website and presented as essential for its own business model.&#x20;

In this sense, sustainability is to be understood as “ecological sustainability”. This therefore refers to concepts such as circular economy, the energy transition, ecological agriculture, regenerative energy, efficient use of resources, reduction of emissions or recycling.

Companies that are active in these or related subject areas, have business fields geared to them, or offer products and services with a direct connection, usually communicate this on their websites. The more central this topic is for the company, the more significant it is for the company’s external communications. For example, a startup for compostable ballpoint pens communicates almost exclusively on the topic of sustainability, while a consulting company that offers “ESG consulting” among many other topics does so only to a limited extent.

</details>

<details>

<summary>How do we measure?</summary>

Our webAI reads the website of the company under investigation and searches it for text sections (paragraphs) that deal with the topic of sustainability. To do this, webAI first searches for keywords potentially related to sustainability, analyzes the paragraphs identified in this way, and in doing so determines whether or not they are actually sustainability-related texts. If webAI has assigned a corresponding paragraph to the topic of sustainability with a high probability, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website, or the particularly relevant “top-level” sub-webpages if it is a very extensive website with hundreds of sub-webpages (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://link.springer.com/article/10.1007/s11192-020-03726-9)).

WebAI thus finds a certain number of paragraphs per company website that deal with the topic of sustainability. WebAI then relates this number to the total amount of text content read on the website. In this way, webAI determines a Sustainability Intensity for each company.

</details>

<details>

<summary>How do you interpret the data?</summary>

The Sustainability Intensity Score calculated in this way would be 0.0 for a company with no sustainability-related texts. For the example of a consulting company described above, on the other hand, the value could be 0.25, and for the startup that is particularly focused on sustainability, it could be 2.37. The Sustainability Intensity Score has no upper limit.

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

Unlike simpler, binary classifications (“sustainable YES/NO”), webAI therefore outputs a continuous score at company level. This makes it possible to distinguish between companies for which sustainability is only a marginal issue and those for which it plays a central role. Users of webAI data can thus easily determine for themselves how strongly a company should focus on sustainability in order for it to be relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland), it can be said that 17.5% of the companies examined have a Sustainability Intensity Score of greater than 0.0 and thus communicate the topic of sustainability in some form on their websites. The average Sustainability Intensity Score of these companies is 0.53 and half of the companies have a score smaller than 0.28. The maximum score achieved is 6.94, with only 2.88% achieving a score of 1.0 or higher.

</details>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI Sustainability Agent has been developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then generates expert-level results. For this agent, ISTARI.AI collaborated with the OECD’s Centre for Entrepreneurship, SMEs, Regions & Cities. The OECD is an international organization with 38 member states and nearly sixty years of experience in analyzing political, economic and social developments.&#x20;

Our Sustainability Intensity Scores were also validated in a study on “[Greenwashing in the U.S. Metals Industry](https://www.sciencedirect.com/science/article/pii/S0048969722026080)” published by researchers from the University of Salzburg, University of Heidelberg, Harvard University and the University of Giessen in the prestigious journal Science of The Total Environment.

</details>
