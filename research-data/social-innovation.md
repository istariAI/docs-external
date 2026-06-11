---
description: Find socially innovative companies.
cover: ../.gitbook/assets/social_innovation.jpg
coverY: -42
---

# 🤰 Social Innovation

<details>

<summary>What do we measure?</summary>

The webAI Social Innovation agent was trained by ISTARI.AI to derive from companies’ websites their engagement in social innovation and to map it as an individual Social InnoProb Score. This indicator, ranging from 0.0 to 1.0, reflects the likelihood that a company is a social innovator.

Social innovations are innovations that improve human interaction in many areas, for example, how people work, organize their leisure time, shop, live or how they are mobile. However, unlike product innovations, there is still no internationally standardized definition of social innovations. We at ISTARI.AI follow the current working definition as it is currently being elaborated by [OECD](https://www.oecd.org/) and [Eurostat](https://ec.europa.eu/eurostat/web/main/home): Social innovation also described as the emergence, implementation and diffusion of new social practices in the societal domain that are directly related to the search for viable and sustainable solutions to societal problems and challenges. If a company has introduced such a social innovation in the last three years through changes in the company or brought it to market as a new or improved product or service, then it is considered a social innovator.

Websites are used by companies as platforms to provide information about their products and services, performance, strategies and relationships. All these aspects can be associated with the social innovations developed by the company. The Social InnoProb Score is not intended to identify individual innovations (e.g. new products), but companies with an innovation-related activity profile. This probability can be interpreted as a continuous innovation indicator at the company level.

</details>

<details>

<summary>How do we measure?</summary>

We use a traditional company-level indicator based on a questionnaire-based innovation survey (Community Innovation Survey Germany) to train webAI with the websites of socially innovative and non-innovative companies. In doing so, we use survey waves from several years to identify companies that answered positively to questions related to social innovation. Examples of such questions are the cooperation of the company with associations, the introduction of new methods of work organization or the promotion of togetherness and family atmosphere in the company. During this training webAI learns independently how the websites of socially innovative and non-innovative companies differ. After the training, we can then apply webAI to any other company website. Based on the textual content, webAI then calculates how likely it is that the company under investigation is innovative.

</details>

<details>

<summary>How do you interpret the data?</summary>

The Social InnoProb score calculated in this way would be close to 0.0 for a company that is very unlikely to be a socially innovative company. A very likely socially innovative company, on the other hand, would have a Social InnoProb score close to 1.0.

In addition, we integrate an auxiliary column into our data as an interpretation and reading aid. It categorizes the probabilities of being an innovative company from “very low” to “very high”.

Thus, unlike simpler, binary classifications (“innovative YES/NO”), webAI outputs a continuous score at the company level. Users of webAI data can thus easily determine for themselves the probability with which a company should be socially innovative in order to be relevant to them. For the binary classification into socially innovative and non-innovative companies, we recommend a classification threshold of 0.5.

As an example for the DACH region (Germany, Austria, Switzerland), we can say that 24.35% of the analyzed companies are rated as socially innovative by webAI Social InnoProb (Social InnoProb Score > 0.5). The average Social InnoProb score of all companies is 0.44. Half of the companies have a score of more than 0.41. The highest score achieved is 0.85 and the lowest is 0.14. The figure below shows the distribution of the Social InnoProb score for the DACH region.



</details>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>How do we ensure the data quality?</summary>

Like all our webAI agents, the webAI Social InnoProb agent was developed and validated together with independent subject matter experts. This ensures that we train the webAI agent with real expert knowledge and that it subsequently generates expert-level results. For this agent, ISTARI.AI collaborated with [ZEW – Leibniz Centre for European Economic Research in Mannheim](https://www.zew.de/en/). The ZEW is one of the leading German economic research institutes with a high European reputation.

</details>
