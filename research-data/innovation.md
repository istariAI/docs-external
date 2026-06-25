---
title: "💡 Innovation"
description: Find innovative companies.
cover: ../images/innovation.jpg
coverY: -4
---

<mark style="color:red;">`This indicator is available for companies based in Germany and Austria only.`</mark>

<Accordion title="What do we measure?">
The webAI InnoProb agent was trained by ISTARI.AI to derive the status of companies as innovators from their websites and to map it as an individual Innovation Probability Score (InnoProb). This indicator between 0.0 and 1.0 reflects the probability of a company being an innovator.

Innovation is defined here in terms of the OECD Oslo Manual: An innovation is the introduction of a new or significantly improved product (good or service) or process, a new marketing method, or a new organizational method in business practice, workplace organization, or external relations.

Websites are used by companies as platforms to provide information about their products and services, performance, strategies, and relationships. All these aspects can be associated with the innovations developed by the company. The InnoProb Score does not intend to identify individual innovations (e.g. new products), but companies with an innovation-related activity profile. This probability (the InnoProb Score) can be interpreted as a continuous innovation indicator at company level.
</Accordion>

<Accordion title="How do we measure?">
We use a traditional company-level indicator based on a questionnaire-based innovation survey (Community Innovation Survey for Germany) to train webAI with the websites of innovative and non-innovative companies. In this training webAI learns independently how the websites of innovative and non-innovative companies differ. After the training, we can then apply webAI to any other company website. Based on the textual content, webAI then calculates how likely it is that the company under study is innovative.
</Accordion>

<Accordion title="How do you interpret the data?">
The InnoProb score calculated in this way would be close to 0.0 for a company that is highly unlikely to be an innovative company. A very likely innovative company, on the other hand, would have an InnoProb Score close to 1.0.

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the probabilities of being an innovative company from “very low” to “very high”.

So, unlike simpler, binary classifications (“innovative YES/NO”), webAI outputs a continuous score at the company level. Users of webAI data can thus easily determine for themselves the probability with which a company should be innovative in order to be relevant to them. For the binary classification into innovative and non-innovative companies, we recommend a classification threshold of 0.4.

As an example for Germany, we can say that 15.12% of the examined companies are assessed as innovative by webAI InnoProb (InnoProb Score > 0.4). The average InnoProb Score of all companies is 0.25. Half of the companies have a score greater than 0.20. The maximum score achieved is 0.94 and the lowest is 0.03. The figure below shows the distribution of InnoProb scores as a histogram.
</Accordion>

<Frame>
  <img src="/images/image-13.png" alt="" />
</Frame>

<Accordion title="How do we ensure the data quality?">
Like all our webAI agents, the webAI InnoProb agent has been developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then generates expert-level results. For this agent, ISTARI.AI collaborated with the University of Giessen and the ZEW – Leibniz Centre for European Economic Research in Mannheim. ZEW is one of the leading German economic research institutes with a high European reputation.

The InnoProb scores were also validated by comparing them with patent data from the European Patent Office, with projections based on survey data from the Mannheim and Berlin Innovation Panels, and with regional innovation indicators from the German Federal Statistical Office. The corresponding study [Predicting innovative firms using web mining and deep learning](https://doi.org/10.1371/journal.pone.0249071) was published in the international journal PLOS ONE.
</Accordion>
