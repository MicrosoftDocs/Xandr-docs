---
title: Microsoft Monetize - Inventory Performance Targeting
description: In this article, learn how to target specific pools of inventory based on historical performance.
ms.date: 10/28/2023
---

# Microsoft Monetize - Inventory performance targeting

You can target specific pools of inventory based on historical performance. By using targeting criteria, you can specify the desired video completion rate. Inventory targeting may only be specified at the line item level.

To target inventory based on performance your options are:

- **No inventory performance target** - Default option.
- **Video Completion Rate** - Target video inventory with a projected percentage of video completions. The percentage is based on historical performance data and is defined as the number of video completions / number of ad impressions for a particular line item or campaign.
  
  > [!NOTE]
  > Video completion rate targeting should only be used on VAST-based video inventory (not in-banner players).

- **Audio Completion Rate** - Target audio inventory with a projected percentage of audio completions. The percentage is based on historical listen-through rate and is defined as the number of audio completions / number of ad impressions for a particular line item or campaign.
- **Viewability Rate** - Target inventory based on a projected percentage of viewed impressions. Viewability rate is defined as the percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps). For more information regarding viewability measurements, see [Reporting on Viewability](reporting-on-viewability.md).

    > [!IMPORTANT]
    > Viewability rate targeting is available only to some members at present. We are working hard to make it available to everyone!

## Video performance best practices

- We recommend using Video Completion Rate as a minimum threshold.
- If your solution requires balancing multiple KPIs, you can use a Video Completion Rate threshold in conjunction with an optimization goal, including the Video Completion Rate goal type.

For example, suppose you have a business requirement to purchase only inventory with at least a 30% Video Completion Rate. You also have a goal to optimize towards a 70% Video Completion Rate. You can achieve both by applying a 30% Video Completion Rate threshold and setting a 70% Video Completion Rate optimization goal.

Another example: you're required to purchase inventory with at least a 30% Video Completion Rate. You also have two more goals: to optimize towards 1% CTR, and to achieve 25% margin. In this case, you should:

- Under **Viewability & Environment Targeting** (**Targeting** for standard line items), target a `30%` **Video Completion Rate threshold**.
- Under **Optimization**, set a `1%` **CTR optimization goal**.
- Under **Goal Priority**, select **Margin** and specify `25%`. However, if you have set your **Revenue Type** to **Cost Plus** under **Budgeting and Scheduling**, you can ignore this step.

> [!NOTE]
> Using Video Completion Rate targeting on deals could lead to under-delivery. We suggest that you don't use Video Completion Rate targeting until your deal-targeted line item or campaign has enough experience learning about the predicted completion rate.

## Related topics

- [Comparison of Video Complete Buying Strategies](comparison-of-video-complete-buying-strategies.md)
- [Buy-Side Targeting](buy-side-targeting.md)
- [Listen-Through Targeting](listen-through-targeting.md)
