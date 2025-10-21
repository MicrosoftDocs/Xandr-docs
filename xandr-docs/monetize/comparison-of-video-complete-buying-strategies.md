---
title: Microsoft Monetize - Comparison of Video Complete Buying Strategies
description: Explore Video Complete Buying Strategies (CPCV), highlighting their related features, benefits, and applications.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Comparison of video complete buying strategies

CPCV optimization and Guaranteed Completes are related features with different benefits and applications: you can't use them simultaneously. Similarly, you can choose to optimize for video completion rate (VCR) or target inventory with a set video completion rate. While you can use these features together, their use cases are different.

| Name | Description | When to Use | How to Configure |
|--|--|--|--|
| CPCV (Cost Per Completed View) Goal Optimization | Budget your video ad buys in terms of impressions, while optimizing toward a goal of purchasing completed video plays. | Use CPCV optimization when the advertiser is paying the buyer on an impression basis, while asking the buyer to meet a CPCV KPI. | 1. Select **Video** as the **Ad Type** in the line item **Basic Settings**.<br> 2. Select **CPCV** as an optimization goal in the line item **Optimization** settings. |
| Guaranteed Completes | Budget your video ad buys in terms of video completes. Only paying for video completes ensures a 100% completion rate. Note that Microsoft Advertising charges a market-making fee when you purchase Guaranteed Completes. | Use Guaranteed Completes when the advertiser is paying the buyer on an event basis (where the event is a video complete). | See [Configuring a Line Item to Buy Guaranteed Outcomes](configuring-a-line-item-to-buy-guaranteed-outcomes.md). |
| VCR (Video Completion Rate) Goal Optimization | Optimize your inventory purchasing to maximize the rate of video completes, based on the historical performance of the inventory. | Use VCR optimization when the advertiser is paying the buyer on an impression basis, while asking the buyer to meet a VCR KPI. | 1. Select **Video** as the **Ad Type** in the line item **Basic Settings**.<br> 2. Select **VCR** as an optimization goal in the line item **Optimization** settings. |
| Video Completion Rate Targeting | Video Completion Rate Targeting is a feature of Inventory Performance Targeting, which allows buyers to target inventory based on historical performance. It allows buyers to bid only on inventory that is projected to meet a specified completion rate threshold based on historical data. | Use Video Completion Rate Targeting when the advertiser has communicated a business requirement to the buyer not to purchase inventory with a projected completion rate below a certain value. | See [Inventory Performance Targeting](inventory-performance-targeting.md). |

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [Set Up Line Item Optimization](set-up-line-item-optimization.md)
- [Add Basic Line Item Details](add-basic-line-item-details.md)
