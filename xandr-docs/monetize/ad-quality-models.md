---
title: Microsoft Monetize - Ad Quality Models
description: Learn how Ad Quality Models use AI to detect and filter misleading, sensitive, or low-quality ads, enhancing user experience and platform credibility.
ms.date: 10/28/2023
---

# Microsoft Monetize - Ad Quality models

Ad quality is a critical aspect of maintaining a trustworthy and engaging advertising ecosystem. To enhance ad quality and protect users from misleading or inappropriate content, Microsoft Monetize introduces **Ad Quality Models** powered by AI and deep learning.

## Overview

Ad Quality Models help evaluate and classify advertisements based on predefined quality parameters. These models ensure that ads adhere to quality standards, improving user experience and engagement.

Ad Quality Models leverage large language models (LLMs) and neural networks to detect and filter ads that contain misleading, inappropriate, or low-quality content.

This page will serve as a centralized resource for current and future Ad Quality Models, providing detailed descriptions, supported categories, and enablement processes.

## Categories

Microsoft Monetize has introduced two new ad quality models as part of the integration of the Xandr Platform into Microsoft Advertising. These models leverage AI and deep learning to enhance ad quality management.

Currently, the Ad Quality Models feature supports the following categories:

- **Clickbait Model (Category 695)**
- **Image Sensitivity & Aesthetics Model (Category 703)**

These models will expand over time to support additional categories.

### Clickbait (category 695)

#### Clickbait detection (Category 695)

Clickbait ads use sensational, exaggerated, or misleading headlines, images, or phrases to attract user attention. These ads often lead to:

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

#### Image sensitivity & aesthetics model(Category 703)

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

### Enablement

Currently, enabling these models requires engineering support. However, future updates may introduce UI-based controls for easier accessibility and management.

### Future Developments

As Ad Quality Models evolve, additional categories and features will be introduced to further refine ad quality. This page will be updated with new models as they become available.

## Next Steps

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
