---
title: Smart Audience Line
description: This document outlines how the Smart audience line serves performance campaigns for Microsoft Invest to enhance ROAS.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Smart audience line

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative.

This article outlines how the Smart audience line serves performance campaigns for Microsoft Invest customers with the aim of enhancing Return on Ad Spend (ROAS). It involves accessing advertising inventory and leveraging bidding strategies to optimize performance.

## Process flow
The process begins with the advertiser configuring the following components within the Microsoft Invest Demand Side Platform (DSP):

- Smart Insertion Order(s)
- Smart Line Item(s)
- Profile
- Creative(s)

When the customer implements the Smart audience line feature to set up the objects in Microsoft Invest, specific attributes for budgeting, configurations, and targeting parameters are incorporated into the Smart Insertion Order and Smart Line Item. These parameters are sent to an object translation layer, which then integrates performance demand from Microsoft Invest into Microsoft Ads. Once saved on the Microsoft Ads platform, the bidder leverages automated bidding strategies to execute the advertiser's campaigns.

## Related topics
- [Smart Insertion Order(s) Service](smart-insertion-order-service.md)
- [Smart Line Item(s) Service](smart-line-item-service.md)
- [Enhancement in Profile and Creative Services](enhancements-in-profile-and-creative-services.md)
