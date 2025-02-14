---
title: Microsoft Monetize - Ad Quality Models
description: Learn how Ad Quality Models use AI to detect and filter misleading, sensitive, or low-quality ads, enhancing user experience and platform credibility.
ms.date: 10/28/2023
---

# Microsoft Monetize - Ad Quality models

Ad quality is a cornerstone of your business, and at Microsoft Monetize, we provide technology to help you manage it effectively. The integration of the Xandr platform into Microsoft Advertising introduces two AI-powered ad quality models that identify and filter low-quality or harmful content.

Ad quality models use large language models (LLMs) and neural networks to detect and filter ads containing misleading, inappropriate, or low-quality content.

## Enable Ad Quality model categories

Ad Quality Models are applied to specific categories to ensure comprehensive coverage and effective filtering. Users have the flexibility to block specific categories at both the network and publisher levels, allowing for tailored ad quality management.

For detailed instructions on how to apply categories to your Ad Quality rules, please refer to the following resources:

- [Network Ad Quality Screen](network-ad-quality-screen.md)
- [Define ad quality rules](../supply-partners/define-ad-quality-rules.md)

### Categories

Microsoft Monetize has introduced two new ad quality models as part of the integration of the Xandr Platform into Microsoft Advertising. These models leverage AI and deep learning to enhance ad quality management.

Currently, the Ad Quality Models feature supports the following categories:

- **Clickbait model (Category 695)**
- **Image sensitivity & aesthetics model (Category 703)**

> [!NOTE]
> These models will evolve to support more categories over time. Microsoft Monetize continuously enhances ad quality filtering, and additional topics may be added to these models in the future.

#### Clickbait model (category 695)

Clickbait is a form of online advertising that uses sensational, exaggerated, or misleading headlines, images, or phrases to attract attention and entice users to click on a link. These ads often lead to:

- Low-quality or irrelevant content
- Malicious or fraudulent websites
- Decreased platform credibility

The Clickbait Model applies AI-driven content analysis across various ad categories, including:

- Finance
- Cryptocurrency
- Health
- Gaming

The model utilizes advanced language analysis to identify patterns commonly associated with deceptive or misleading ad content. This model uses sophisticated LLMs to detect and filter misleading ad content, ensuring high-quality ad experiences.

#### Image sensitivity & aesthetics model (category 703)

This model checks ads for sensitive topics and visual aesthetics to improve user experience. It scans for content related to:

- Pharmaceuticals
- Adult content
- Weapons
- End-of-life services
- Weight loss
- Religion
- Drugs
- Smoking
- Cryptocurrency

## Related topics

- [Working with Ad Quality](working-with-publisher-ad-quality.md)
- [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)
- [Ad quality](monetize-insights-ad-quality.md)
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
- [Network Ad Quality Screen](network-ad-quality-screen.md)
- [Update Your Network Profile](update-your-network-profile.md)
- [Create a Publisher Template](create-a-publisher-template.md)
- [Ad Quality Order of Operations](ad-quality-order-of-operations.md)
