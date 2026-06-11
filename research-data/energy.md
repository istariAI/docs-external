---
description: Find companies that are engaged in the energy sector.
cover: ../.gitbook/assets/Energy.jpg
coverY: -211
---

# 🔌 Energy

<details>

<summary>What do we measure?</summary>

The webAI Energy Agent was trained by ISTARI.AI to identify companies with a focus on the energy sector and to map their focus on this topic as an individual Energy Intensity Score. This numerical indicator measures how centrally the topic of energy is communicated by the company on its own website and presented as essential for its own business model.&#x20;

We consider the entire value chain from the exploitation of energy sources to distribution to end consumers and their consumption patterns, i.e. the entire energy industry. More specifically we look at four sub-segment:&#x20;

* **Generation**: Power/energy generation is the colloquial term for energy transformation where electrical energy and heat is made available. All companies that are involved in the exploitation of energy sources up to their transformation into electrical energy or heat belong to this category. Companies that provide products or services for this purpose also belong to this category. Examples are: Oil production (oil drilling), coal mining, operators of solar parks, manufacturers of solar panels , manufacturers of steam boilers for power generation in coal-fired power plants, manufacturers of control software for nuclear power plants, waste incineration for district heating, hydrogen production.
* **Grid**: Network for the transmission and distribution of electrical energy, heat and other energy sources (gas, hydrogen etc.). This includes the manufacturers of required components (hardware and software), service providers and operators. Examples are: Contractors and commissioning authorities for the development and operation of the electricity grid and pipelines (gas, district heating, etc.), manufacturer of control software for power grids (smart grid), manufacturer and operator of energy storage systems, petrol stations, electricians who install wall boxes for electric cars and manufacturers of wall boxes, manufacturers and operators of charging stations for electric cars, manufacturers of smart electricity meters, shipping company with oil tankers.
* **Efficiency**: Efficient use and production of energy and optimized processes to reduce energy consumption, energy loss and emissions while maintaining or increasing effectiveness (“same or more for less”). All companies that are active in this area or help other companies/consumers to be more efficient belong to this category. Examples are: Energy consultant for companies and private individuals, construction company that carries out energy refurbishments of buildings, manufacturer of thermal insulation material, companies converting their vehicle fleet to models with lower fuel consumption, company that is renovating its own company headquarters to make it more energy efficient, power producer introducing measures to reduce energy loss in power generation with coal, company switches completely to renewable energies in production.
* **Market**: Includes trading of energy sources and electricity, as well as the legal framework and (state) support measures. Examples are: Energy exchanges where energy carriers (e.g. gas) and electrical energy are traded, electricity suppliers who supply the end customer but do not operate any infrastructure themselves, legislative and supervisory bodies in the field of electricity and gas markets, development banks (e.g. German KfW) with programs to promote energy-efficient construction and refurbishment, portal for comparison of energy providers for private customers.

Companies that are active in these energy-related areas, have business fields geared to them, or offer products and services with a direct connection, usually communicate this on their websites. The more central the topic is for the company, the more significant it is for the company’s external communication. For example, a startup for smart grid software communicates almost exclusively on the topic of energy, while a chemical company, which among many other products also offers specific thermal insulation components, does so only to a limited extent.

</details>

<details>

<summary>How do we measure?</summary>

Our webAI reads the website of the company under investigation and searches for text sections (paragraphs) that deal with the topic of energy. To do this, webAI first searches for keywords that are potentially related to energy, analyzes the paragraphs identified in this way, and determines whether or not they are actually energy-related texts. If webAI has assigned a corresponding paragraph to the topic of energy with a high probability, webAI remembers this paragraph and continues searching. In this way, webAI searches the entire company website or the particularly relevant “top-level” sub-pages if it is a very extensive website with hundreds of sub-pages (for more information, see the publication: [Web mining for innovation ecosystem mapping: a framework and a large-scale pilot study](https://doi.org/10.1007/s11192-020-03726-9)).

In this way, webAI finds a certain number of paragraphs per company website that deal with the topic of energy. WebAI then puts this number in relation to the total amount of text content read on the website. In this way, webAI determines a Energy Intensity for each company.

</details>

<details>

<summary>How do you interpret the data?</summary>

The Energy Intensity Score calculated in this way would be 0.0 for a company with no energy-related texts. For the example of a chemical company described above the calculated intensity value could be 0.15, and 3.97 for the startup that is particularly focused on energy. The Energy Intensity Score has no upper limit. In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the intensities from “low” to “very high”. In the example above, the chemical company would be classified as “low” intensity and the startup as “very high” intensity.

In contrast to simpler, binary classifications (“Energy YES/NO”), webAI outputs a continuous score at the company level. This makes it possible to distinguish between companies for which energy is only a peripheral issue and those for which it plays a central role. Users of the webAI data can thus easily determine for themselves how strongly a company should be engaged in the energy sector for it to be relevant to them.

As an example for the DACH region (Germany, Austria, Switzerland), it can be said that 20.5% of the companies studied have a Energy Intensity Score of greater than 0.0 and thus communicate the topic of energy in some form on their websites. The average Energy Intensity Score of these companies is 0.61 and half of the companies have a score lower than 0.30. The maximum score achieved is 6.93, with 21.63% achieving a score of 1.0 or higher.

</details>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI Energy Agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it then delivers expert-level results. For this agent ISTARI.AI has collaborated with researchers from the [University of Salzburg](https://www.plus.ac.at/?lang=en). The Energy Intensity Scores are currently also being validated in a not yet published study.

</details>
