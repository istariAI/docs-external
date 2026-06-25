---
title: "👩‍⚕️ SDG 3"
description: >-
  Find companies that are engaged in the Sustainable Development Goal 3 - "Good
  Health and Well-Being"
cover: ../images/syringe.jpg
coverY: 0
---

<details>

<summary>What do we measure?</summary>

The webAI SDG 3 Agent was trained by ISTARI.AI to derive companies’ commitment to Sustainable Development Goal 3 (Good Health and Well-Being) from their websites and to display it as an individual SDG 3 Intensity Score. This numerical indicator reflects how centrally the topic of Sustainable Development Goal 3 is communicated by the company on its own website and presented as essential for its own business model.

SDG 3 is to be understood as a broad concept. This includes services and products that are used directly to improve health and well-being (e.g., pharmaceutical companies, healthcare providers, or manufacturers of medical equipment), but also, for example, businesses involved in health education, mental health services, and wellness initiatives. Thus, players from sectors such as healthcare, biotechnology, fitness, and mental health care are considered.

Moreover, WebAI also identifies companies that specialize in developing health technologies, such as telemedicine or wearable health devices, organizations that focus on health-related research, or those involved in providing access to clean water and sanitation, which are crucial for maintaining good health.

</details>

<details>

<summary>How do we measure?</summary>

Our webAI reads the website of the company under investigation and searches for text sections (paragraphs) that deal with the topic of SDG 3. To do this, webAI first searches for keywords that are potentially related to SDG 3, analyzes the paragraphs identified in this way, and determines whether or not they are actually relevant texts. If webAI has assigned a corresponding paragraph to the topic of SDG 3 with a high probability, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website or the particularly relevant “top-level” sub-pages if it is a very extensive website with hundreds of sub-pages.

In this way, webAI finds a certain number of paragraphs per company website that deal with the topic of SDG 3. WebAI then puts this number in relation to the total amount of text content read on the website. In this way, webAI determines a SDG 3 intensity for each company.

</details>

<details>

<summary>How do you interpret the data?</summary>

The SDG 3 Intensity Score calculated in this way would be 0.0 for a company with no SDG 3-related texts. For a consulting company, for example, the value could be 0.21, and for a startup that is particularly focused on SDG 3-related topics, it could be 2.81. The SDG 3 Intensity Score has no upper limit.

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the consulting company would be classified as “low” intensity and the startup as “very high” intensity.

Unlike simpler, binary classifications (“SDG 3 YES/NO”), webAI therefore outputs a continuous score at company level. This makes it possible to distinguish between companies for which SDG 3-related topics are only a marginal issue and those for which they play a central role. Users of webAI data can thus easily determine for themselves how strongly a company should focus on SDG 3 in order for it to be relevant to them.

</details>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI SDG3 Agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then delivers expert-level results. The SDG3 Intensity Scores are currently also being validated in a not yet published study.

</details>
