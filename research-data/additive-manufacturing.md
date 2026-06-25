---
title: "🖨️ Additive manufacturing"
description: Find companies that are engaged in additive manufacturing.
cover: ../.gitbook/assets/iStock-638869954.jpg
coverY: 20
---

<AccordionGroup>
<Accordion title="What do we measure?">
The webAI Additive Manufacturing Agent (3D Printing) was trained by ISTARI.AI to derive companies’ know-how in the field of additive manufacturing from their websites and to map it as an individual Additive Manufacturing Score. By knowhow in this context, we mean products and services in additive manufacturing or personnel with skills in additive manufacturing. This numerical indicator reflects how central the topic of additive manufacturing is communicated by the company on its own website and presented as essential for its own business model.

In addition, webAI also derives an Additive Manufacturing Information Intensity Score for each company. This reflects how intensively the company communicates about the topic of additive manufacturing without having its own products and services with integrated additive manufacturing or specially trained personnel.

Companies that are active in the field of additive manufacturing, have business areas geared to it, or offer products and services with a direct link, usually communicate this fact. The more central this topic is for the company, the more significant it is for the company’s external communication. For example, a startup for “rapid prototyping” communicates almost exclusively on the topic of additive manufacturing, while a consulting company that offers “additive manufacturing consulting” among many other topics communicates only to a limited extent on additive manufacturing. WebAI distinguishes “information” communication in addition to this “knowhow” communication (it offers its own additive manufacturing products and services). An example of this would be a regional newspaper’s website reporting that a regional incubator for additive manufacturing startups has recently opened.
</Accordion>

<Accordion title="How do we measure?">
Our webAI reads the website of the company under investigation and searches it for text sections (paragraphs) that deal with the topic of additive manufacturing. For this purpose, webAI first searches for keywords related to additive manufacturing, then analyzes the identified paragraphs and determines whether the company reports on its own additive manufacturing know-how or only communicates information about additive manufacturing. If webAI has assigned a corresponding paragraph to the category “Knowhow” or “Information”, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website, or the particularly relevant “top-level” sub-webpages in the case of very extensive websites with hundreds of sub-webpages (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).\
WebAI thus finds a certain number of paragraphs per company website that deal with the topic of additive manufacturing. WebAI classifies these paragraphs into “knowhow” and “information” and then relates the number to the total amount of text content read on the website. Thus, webAI determine an Additive Manufacturing Knowhow Intensity and an Additive Manufacturing Information Intensity for the company.
</Accordion>

<Accordion title="How do you interpret the data?">
The intensities determined in this way would be 0.0 for a company with no additive manufacturing-related texts. For the example of a consulting company described above, on the other hand, the value for Additive Manufacturing Knowhow could be 0.25 and the value for Additive Manufacturing Information 0.21. The startup that is particularly focused on additive manufacturing could have an Additive Manufacturing Knowhow Intensity of 3.8 and an Additive Manufacturing Information Intensity of 0.9. The regional newspaper, on the other hand, would have an Additive Manufacturing Knowhow Intensity of 0.0 and an Additive Manufacturing Information Intensity of 0.05.&#x20;

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

So, unlike simpler, binary classifications (“additive manufacturing YES/NO”), webAI outputs two continuous scores at the company level. This allows to distinguish between companies where additive manufacturing is only a marginal topic and those where it plays a central role. In addition, companies with products and services based on or related to additive manufacturing can be distinguished from those that merely provide information on the topic. Users of webAI data can thus easily determine for themselves how and to what extent a company should focus on additive manufacturing so that it is relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland) it can be said that 0.9% of the investigated companies have an Additive Manufacturing Knowhow Intensity of greater than 0.0 and thus communicate knowhow in the area of additive manufacturing in some form. The average Knowhow Intensity score for companies with knowhow is 0.44, with half of the companies having a score lower than 0.17. The maximum score achieved is 4.0, with only 15.8% achieving a score of 1.0 or higher.
</Accordion>

<Accordion title="How do we ensure the data quality?">
Like all our webAI agents, the webAI Additive Manufacturing Agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then generates expert-level results. For this agent, ISTARI.AI collaborated with the Technical University of Munich.&#x20;

The validation of the Additive Manufacturing Intensity Scores was also carried out in the study [Technology Mapping Using WebAI: The Case of 3D Printing](https://doi.org/10.48550/arXiv.2201.01125), which was conducted by researchers from the University of Mannheim, University of Giessen, University of Salzburg and the Technical University of Munich.
</Accordion>
</AccordionGroup>
