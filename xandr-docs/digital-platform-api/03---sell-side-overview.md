---
title: Sell-Side Overview
description: In this article, explore detailed information about sell-side and its various objects.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Sell-side overview

## Diagram

:::image type="content" source="media/sell-side.png" alt-text="Diagram that illustrates sell-side framework.":::

## Object definitions

- [Member](member-service.md): The parent object for your account. Each member has a contractual relationship with Xandr.
- [Publisher](publisher-service.md): The object which represents a single publisher on Xandr. Generally, a publisher can be associated with the owner of a piece of inventory.
- [Site](site-service.md): This object groups placements and is usually associated with a singe website (domain) or section of a website.
- [Placement](placement-service.md): Each placement corresponds to a single ad tag through which impressions come to Xandr.
- [Content Category](content-category-service.md): This object specifies attributes about the inventory which are useful for targeting with managed campaigns.
- [Payment Rule](payment-rule-service.md): This object defines how a publisher is being paid for an impression. This can be associated with a profile to define dynamic payments based on the targeting.
- [Ad Profile Service](ad-profile-service.md): Defines the types of creatives which can and cannot serve on a piece of inventory.
- [Ad Quality Rule](ad-quality-rule-service.md): This object specifies additional dynamic rules regarding which creatives can and cannot
serve.
- [Yield Management Profile](yield-management-profile-service.md): The parent object for yield management operations.
- [Yield Management Floor](yield-management-floor-service.md): This object defines dynamic yield management price floors.
- [Yield Management Bias](yield-management-bias-service.md): This object defines dynamic yield management biases.
- [Profile](profile-service.md): This object defines all of the targeting parameters for another object (e.g., payment rule).
