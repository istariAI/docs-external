---
title: "⛓️ Blockchain"
description: Find companies that are engaged in blockchain.
cover: ../.gitbook/assets/blockchain.jpg
coverY: 0
---

<AccordionGroup>
<Accordion title="What do we measure?">
The webAI Blockchain Agent was trained by ISTARI.AI to derive companies’ Blockchain know-how from their websites and to map it as an individual Blockchain Intensity Score. Blockchain know-how in this context is products and services with integrated Blockchain or personnel with Blockchain skills. This numerical indicator reflects how central the topic of Blockchain is communicated by the company on its own website and presented as essential for its own business model.&#x20;

Companies that are active in the area of Blockchain, have business fields geared to it or offer products and services with a direct connection usually communicate this fact. The more central this topic is for the company, the more significant it is for the company’s external communication. For example, a startup for integrating blockchain into the supply chain communicates almost exclusively on the topic of blockchain, while a consulting company that offers “blockchain consulting” among many other topics communicates only to a limited extent about this technology. WebAI distinguishes “information” communication in addition to this “know-how” communication (it offers its own products and services with integrated Blockchain). An example of this would be the website of a regional newspaper reporting that a regional incubator for Blockchain startups has recently opened.
</Accordion>

<Accordion title="How do we measure?">
Our webAI reads the website of the company under investigation and searches it for text sections (paragraphs) that deal with the topic of blockchain. For this purpose, webAI first searches for keywords related to blockchain, then analyzes the paragraphs identified in this way and determines whether the company reports on its own blockchain know-how or merely communicates information on the topic of blockchain. If webAI has assigned a corresponding paragraph to the category “Know-how”, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website, or the particularly relevant “top-level” sub-webpages, if very extensive websites with hundreds of sub-webpages are involved (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).&#x20;

WebAI thus finds a certain number of paragraphs per corporate website that deal with the topic of blockchain. WebAI classifies identifies “know-how” paragraphs and then relates their number to the total amount of text content read on the website. Thus, webAI determine a Blockchain Intensity for the company.
</Accordion>

<Accordion title="How do you interpret the data?">
The intensity determined in this way would be 0.0 for a company with no Blockchain-related texts. For the example of a consulting company described above, on the other hand, the value for Blockchain Intensity could be 0.25. The startup that is particularly focused on Blockchain could have a Blockchain Intensity of 3.8. The regional newspaper, on the other hand, would have a Blockchain Intensity of 0.0.&#x20;

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

So, unlike simpler binary classifications (“Blockchain YES/NO”), webAI outputs two continuous scores at the company level. This allows us to distinguish between companies where Blockchain is only a marginal topic and those where it plays a central role. Users of webAI data can thus easily determine for themselves how and to what extent a company should focus on Blockchain so that it is relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland), it can be said that 0.5% of the companies surveyed have a Blockchain Intensity greater than 0.0 and thus communicate Blockchain know-how in some form. The average Intensity Score for those companies is 0.45, with half of the companies having a score greater than 0.18. The maximum score achieved is 4.2, with 14.0% achieving a score of 1.0 or higher.
</Accordion>

<Accordion title="How do we ensure the data quality?">
Like all our webAI agents, the webAI Blockchain Agent has been developed and validated together with independent domain experts. This ensures that we train the webAI agent with real expert knowledge and that it then generates expert-level results. For this agent, ISTARI.AI collaborated with the Technical University of Munich.&#x20;

The validation of the Blockchain Intensity Scores is also currently being carried out in a study with the working title “Blockchain Technology Diffusion and Use Cases in the European Industry”, which is being conducted by researchers from the University of Mannheim, University of Giessen and the Technical University of Munich.
</Accordion>
</AccordionGroup>
