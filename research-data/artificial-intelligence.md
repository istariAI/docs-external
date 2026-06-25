---
title: "🤖 Artificial intelligence"
description: Find companies that are engaged in artificial intelligence.
cover: ../.gitbook/assets/artifical_intelligence.jpg
coverY: 64.49257425742574
---

<AccordionGroup>
<Accordion title="What do we measure?">
The webAI AI Agent was trained by ISTARI.AI to derive companies’ artificial intelligence (AI) know-how from their websites and to map it as an individual AI Intensity Score. By AI know-how, in this context, we mean products and services with integrated AI or personnel with AI skills. The resulting numerical indicator reflects how centrally the topic of artificial intelligence is communicated on the company’s website and presented as essential for its own business model.&#x20;

Companies that are active in the field of artificial intelligence, have business areas geared to it, or offer products and services with a direct link, usually communicate this. The more central this topic is for the company, the more significant it is for the company’s external communications. For example, a machine translation startup communicates almost exclusively on the topic of artificial intelligence, while a consulting company that offers “AI consulting” among many other topics communicates only to a limited extent on artificial intelligence. An example of a company that only communicates about AI would be a regional newspaper’s website reporting that a regional incubator for AI startups has recently opened.
</Accordion>

<Accordion title="How do we measure?">
Our webAI reads the website of the company under study and searches it for text sections (paragraphs) that deal with the topic of artificial intelligence. For this purpose, webAI first searches for keywords related to AI, then analyzes the identified paragraphs to determine whether the company reports on its own AI know-how or merely communicates information on the topic of AI. If webAI has assigned a corresponding paragraph to the category “Know-how” , webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website, or the particularly relevant “top-level” sub-webpages if it is a very extensive website with hundreds of sub-webpages (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).&#x20;

WebAI thus finds a certain number of paragraphs per corporate website that deal with the topic of artificial intelligence. WebAI identifies all “know-how” paragraphs and then relates their number to the total amount of text content read on the website. Thus, webAI determines an AI Intensity for the company.
</Accordion>

<Accordion title="How do you interpret the data?">
The intensity determined in this way would be 0.0 for a company without AI-related texts. For the example of a consulting company described above, on the other hand, the intensity value could be 0.25. The startup that is particularly focused on AI could have an AI Intensity of 3.8. The regional newspaper, on the other hand, would have an AI Knowhow Intensity of 0.0.&#x20;

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

So, unlike simpler binary classifications (“AI YES/NO”), webAI outputs two continuous scores at the company level. This allows to distinguish between companies where AI is only a marginal topic and those where it plays a central role. Users of webAI data can thus easily determine for themselves how and to what extent a company should focus on AI so that it is relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland), we can say that 2.0% of the companies surveyed have an AI Intensity greater than 0.0 and thus communicate some form of know-how in the area of artificial intelligence. The average AI Intensity score for those companies is 0.32, with half of the companies having a score lower than 0.16. The maximum score achieved is 3.42, with only 7.28% achieving a score of 1.0 or higher.
</Accordion>

<Accordion title="How do we ensure the data quality?">
Like all our webAI agents, the webAI AI Agent has been developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then generates expert-level results. For this agent, ISTARI.AI collaborated with the University of Mannheim.&#x20;

The validation of the AI Intensity Scores was also done in a study on [When is AI Adoption Contagious? Epidemic Effects and Relational Embeddedness in the Inter-Firm Diffusion of Artificial Intelligence](https://www.research-collection.ethz.ch/handle/20.500.11850/589410), which was conducted by researchers from the University of Mannheim, University of Giessen, University of Hohenheim and ETH Zurich. The study is currently in peer review at an international journal and has already received the “Best Paper Award” at the “R\&D Management Conference 2022”.
</Accordion>
</AccordionGroup>
