---
title: Microsoft Monetize - Ad Quality Models
description: Learn how Ad Quality Models use AI to detect and filter misleading, sensitive, or low-quality ads, enhancing user experience and platform credibility.
ms.date: 10/28/2023
---

# Microsoft Monetize - Ad Quality Models

Ad quality is a cornerstone of your business, and at Microsoft Monetize, we are committed to empowering you with best-in-class technology to manage it. With the integration of the Xandr Platform into Microsoft Advertising, we are excited to introduce two new ad quality models as part of our suite, leveraging AI and deep learning. These models enhance ad quality management by identifying and filtering out low-quality or potentially harmful content, ensuring higher ad standards.

Ad Quality Models use large language models (LLMs) and neural networks to detect and filter ads that contain misleading, inappropriate, or low-quality content.

This page serves as a centralized resource for current and future Ad Quality Models, providing detailed descriptions, supported categories, and enablement processes.

## Categories

Microsoft Monetize has introduced two new ad quality models as part of the integration of the Xandr Platform into Microsoft Advertising. These models leverage AI and deep learning to enhance ad quality management.

Currently, the Ad Quality Models feature supports the following categories:

- **Clickbait Model (Category 695)**
- **Image Sensitivity & Aesthetics Model (Category 703)**

These models will expand over time to support additional categories.

### Clickbait Model (category 695)

Clickbait is a form of online advertising that uses sensational, exaggerated, or misleading headlines, images, or phrases to attract attention and entice users to click on a link. These ads often lead to:

- Low-quality or irrelevant content
- Malicious or fraudulent websites
- Decreased platform credibility

The Clickbait Model applies AI-driven content analysis across various ad categories, including:

- Finance
- Cryptocurrency
- Health
- Dating
- Gaming

The model utilizes advanced language analysis to identify patterns commonly associated with deceptive or misleading ad content. By leveraging sophisticated LLMs, this model detects and filters misleading ad content to maintain high-quality ad experiences.

### Image Sensitivity & Aesthetics Model (category 703)

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

Additionally, it utilizes the **Multilingual CLIP Embedding Model** from OpenAI to identify unappealing and low-quality images that negatively impact engagement.

By implementing this model, advertisers can maintain a high-quality, appropriate visual experience for their audiences.

## Enabling Ad Quality Model categories

Ad Quality Models are applied to specific categories to ensure comprehensive coverage and effective filtering. Users have the flexibility to block specific categories at both the network and publisher levels, allowing for tailored ad quality management.

For detailed instructions on how to apply categories to your Ad Quality rules, please refer to the following resources:

- [Define ad quality rules](network-ad-quality-screen.md)
- [Define ad quality rules](../supply-partners/define-ad-quality-rules.md)

> [!NOTE]
> Categories 695 and 703 currently require internal enablement. If you are interested in applying these new categories, please reach out to your account manager. Enablement via the Microsoft Monetize UI will be available in the future.

### Future developments

As Ad Quality Models evolve, additional categories and features will be introduced to further refine ad quality. This page will be updated with new models as they become available.

## Next steps

- Work is ongoing to expand Ad Quality Models with additional categories.
- Stay tuned for updates on UI enablement for self-service management.

For more details, reach out to the Microsoft Monetize support team.

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
