---
title: Learn Budget
description: In this article, learn what Learn budget is and our recommendations on how to use Learn budget.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Learn budget

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

Learn budgets are part of the total campaign budget, and apply in any optimized campaign. They control how much the campaign will spend when the optimization engine does not yet have enough data to bid optimized as there have been too few events to meet the learn threshold.

## Overview

The process of optimization in a campaign is gradual because it occurs on each node individually, and there can be several thousand nodes in a campaign. When you begin a campaign, none of the nodes are optimized, and therefore all of your spend is in learn. As the campaign progresses, nodes become optimized, and some of the campaign budget can be allocated as optimized. The amount of inventory in a campaign that is optimized increases as more and more nodes are optimized. Eventually, the campaign reaches a state where the amount of learn budget and optimized budget remain constant (there is always an influx of new inventory and, therefore, new nodes to be optimized while serving ends on other sites), so the daily cap can remain constant.

When bidding on inventory that you are not familiar with, or if you have a new creative, the optimization engine uses historical advertiser data to determine the range of the learn bids (i.e., the bid amount that wins the desired number of auctions but also represents the point at which the campaign becomes profitable). At the start of a campaign, every bid on inventory is a learning bid, as the optimization engine attempts to determine the best price to spend on each piece of inventory. When a defined number of success events (called the threshold) is reached on each node, more inventory is optimized and the campaign has the opportunity to spend more of its budget in the optimized phase. Learn bids are not as profitable as optimized bids, so the goal is to get as many nodes as possible to the optimized phase as quickly as possible.

Depending on how the threshold is set, it may take many hours or even days before there are any optimized nodes in a campaign. It is beneficial for your campaign to spend as much as possible in the optimized phase, but it is necessary to set the threshold sufficiently high so that the system has sufficient data to properly determine an optimized bid.

Here's a basic example of how the learn budget works: If your campaign budget is $100 and your learn budget is $10, you will spend a maximum of $100 on that campaign of which a maximum of $10 will be spent in the learn phase. If you run out of learn budget, the campaign will stop bidding in learn and only bid on optimized nodes. The benefit of a learn budget is that your spend can be concentrated on the inventory that best meets your goals. However, it's only a good idea to use a learn budget if you have a sufficient percentage of impressions optimized as you may risk poor delivery otherwise. For more information on optimization see [Understanding Optimization](understanding-optimization.md).

## Lifetime learn budget

You can set a learn budget amount over the entire life of a campaign. This is the maximum amount of the budget that will be applied to learn auctions for the life of the campaign. However, it is not always beneficial to define this amount. For example, as specified above, the beginning of a campaign is spent entirely in learn. If you specify a lifetime learn budget amount that is small in comparison to your overall budget, you run the risk of exhausting the entire learn budget at the very beginning of the campaign. Not only will this exclude you from bidding on any new inventory for the remainder of the campaign, you will also be unable to bid until some optimized inventory becomes available.

## Daily learn budget cap

You can also set a daily cap amount, indicating the maximum amount of the budget that can be applied to learn bids each day. You can update this amount as needed during the life of the campaign. Ideally, you want to minimize the amount spent in the learn phase and use as much since optimized spend is almost always more profitable. To do so, you should adjust the daily learn cap on a regular basis to account for the amount of optimized spend you anticipate for the coming day (based on growth of optimized spend over the previous days).

## Recommendations

We recommend using the learn budget in various ways, depending on where a campaign is in its lifecycle.

:::image type="content" source="media/learn-budget.png" alt-text="Diagram that shows a graph of time against spend for a campaign.":::

### 100% learn budget

At the start of a campaign, when there is no optimized inventory, you may want to leave the lifetime learn budget and the learn budget daily cap undefined (unlimited). Leaving these settings undefined would allocate the entire campaign budget towards learning. If you do define a daily cap, once the campaign reaches this amount, it will stop all bidding for the day (there is no optimized inventory yet, and the campaign cannot spend any more learn budget).

### Adjusting daily learn budget cap

As optimized inventory begins to appear in the campaign, you should define the learn budget to have the campaign bid on as much optimized inventory as possible. As the amount of optimized inventory grows, you should adjust the learn cap accordingly (or, if possible, increase the overall budget and keep the learn cap amount constant) to spend as much as possible on the optimized inventory.

### Fixed learn budget: Optimized budget ratio

Eventually, the amount of optimized inventory will reach a plateau (where the majority of nodes have been optimized and the amount of new inventory remains constant). At this point, the campaign has reached a state of equilibrium between the two phases and it is no longer necessary to make adjustment to the daily cap.

You can estimate the amount of the cap during the adjusting period by applying the following formula:

```
Daily Learn Budget = Total Campaign Daily Budget - ( Optimized Spend Yesterday + m )
```

In this formula, *m* is the average daily increase of optimized spend. While the growth of the optimized spend amount will not be constant, this formula allows you to proceed with a reasonably accurate estimate. You can update the daily learn cap as often as you feel it is necessary (most people update this value every couple of days).

The goal of using the learn budget and the daily cap is to find a roughly stable daily learn spend to maintain the highest possible amount of optimized spend. But it is not advisable to terminate the learn budget spend, which would make us ineligible for new inventory as it becomes available.
