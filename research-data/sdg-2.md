---
title: "🍞 SDG 2"
description: >-
  Find companies that are engaged in the Sustainable Development Goal 2 - "Zero
  Hunger"
cover: ../.gitbook/assets/food_security.jpg
coverY: -9
---

<AccordionGroup>
<Accordion title="What do we measure?">
The webAI SDG 2 Agent was trained by ISTARI.AI to derive companies’ commitment to Sustainable Development Goal 2 (Zero Hunger) from their websites and to display it as an individual SDG 2 Intensity Score. This numerical indicator reflects how centrally the topic of Sustainable Development Goal 2 is communicated by the company on its own website and presented as essential for its own business model.&#x20;

SDG 2 is to be understood as a broad concept. This includes services and products that are used directly to combat hunger and ensure food security (e.g., agricultural technology companies or food distribution organizations), but also, for example, suppliers of sustainable farming equipment, and companies involved in food preservation and waste reduction. Thus, among others, players from the agriculture, food production, distribution, and technology sectors are considered.&#x20;

However, WebAI also finds, for example, companies that specialize in developing innovative food solutions, such as alternative protein sources, organizations that focus on agricultural education and research, or businesses that create efficient supply chain solutions to reduce food loss and improve access to nutritious food.
</Accordion>

<Accordion title="How do we measure?">
Our webAI reads the website of the company under investigation and searches for text sections (paragraphs) that deal with the topic of SDG 2. To do this, webAI first searches for keywords that are potentially related to SDG 2, analyzes the paragraphs identified in this way, and determines whether or not they are actually relevant texts. If webAI has assigned a corresponding paragraph to the topic of SDG 2 with a high probability, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website or the particularly relevant “top-level” sub-pages if it is a very extensive website with hundreds of sub-pages.

In this way, webAI finds a certain number of paragraphs per company website that deal with the topic of SDG 2. WebAI then puts this number in relation to the total amount of text content read on the website. In this way, webAI determines a SDG 2 intensity for each company.
</Accordion>

<Accordion title="How do you interpret the data?">
The SDG 2 Intensity Score calculated in this way would be 0.0 for a company with no SDG 2-related texts. For a consulting company, for example, the value could be 0.18, and for a startup that is particularly focused on SDG 2-related topics, it could be 3.05. The SDG 2 Intensity Score has no upper limit.

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

Unlike simpler, binary classifications (“SDG 2 YES/NO”), webAI therefore outputs a continuous score at company level. This makes it possible to distinguish between companies for which SDG 2-related topics are only a marginal issue and those for which they play a central role. Users of webAI data can thus easily determine for themselves how strongly a company should focus on SDG 2 in order for it to be relevant to them.
</Accordion>

<Accordion title="How do we ensure the data quality?">
Like all our webAI agents, the webAI SDG2 Agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then delivers expert-level results. The SDG2 Intensity Scores are currently also being validated in a not yet published study.
</Accordion>
</AccordionGroup>
