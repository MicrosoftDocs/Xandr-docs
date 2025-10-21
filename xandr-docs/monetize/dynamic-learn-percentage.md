---
title: Dynamic Learn Percentage
description: Learn about Dynamic Learn and how it can used to accelerate the learning process and improve publisher revenue eCPM. This page lists steps to show how dynamic learn is used. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Dynamic learn percentage

> [!TIP]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

Dynamic learn is a sell-side optimization algorithm designed to accelerate the learning process and improve publisher revenue eCPM by determining an optimal venue learn percent through adjustments to the previous learn percent based on performance of learn versus optimized impressions.

Since dynamic learn is only applied when optimizing to a performance goal (e.g., CPC, CPA), this content does not apply to campaigns/line items that do not use optimization.

> [!TIP]
> The **RPM** (Revenue Per Thousand) of a node is inverse to volume; low volume means that we will allocate a greater portion of our impressions to the highest performing nodes to optimize return.

On the Microsoft Advertising platform, there are two types of auctions that occur: **Learn Auctions**, which give preference to bids from nodes in a learn state, and **Revenue Auctions**, which give preference to bids from nodes in an optimized state. The percentage of auctions that will actively search for learn bids is automatically determined by the system. However, you can determine the maximum learn percentage at the publisher level. This setting is called **Override dynamic learn**. For more details, see [Create a Publisher](create-a-publisher.md).

For more information about how this setting affects the learn and optimized phase, see the [Learn Budget](learn-budget.md) section.

As a general rule:

- Publishers want to run Learn Auctions to run newer creatives on their inventory, thereby exposing the site to new campaigns that offer continuing bids and may offer greater profit. However, the amount of money recognized from a learn bid can vary greatly.
- Publishers want to run Revenue Auctions to maximize the profit they recognize on their inventory (the money they earn for running the impression is fairly certain). However, revenue campaigns have finite lifespans, so it is not feasible to run only revenue auctions. Refer to [Give Up Price](give-up-price.md) for a detailed description of Learn and Revenue Auctions.

By default, a brand new publisher is set to have up to 80% of its auctions run as dynamic learn. After that, the dynamic learn algorithm runs twice a day, adjusting learn allocation up or down by at most 20% per algorithm execution.

> [!TIP]
> If a publisher sets the dynamic learn percentage manually, the algorithm still executes and updates the learn allocation, but our system ignores the calculated amount. If the user removes the manual override, the calculated amount is again used.

The system does not remember the starting point for existing publishers that were previously using a manual learn allocation. Therefore, we recommend that publishers allow the system algorithm to determine the dynamic learn rate. (A venue that has diverged from another venue will retain the percentage rate used by the parent venue.)

Dynamic learn is able to adjust learning rates at a very granular level, allocating as needed to ensure that allocation and targeting adjustments are made to follow high-performing auctions.

## How dynamic learn is used

The following steps illustrate the mechanics of the dynamic learn algorithm at a high level:

1. Each new venue starts at a default max learn percent; either 80% for a new publisher, or the most recent max learn percent of the venue from which it diverged. Existing publishers/venues will use their current max learn percent as a starting value.

1. Twice daily, when updating max learn percent, we will aggregate the data for each venue since the last update, separated into learn and optimized impressions. One of the items we aggregate is the **RPM**.

1. If the **Optimized RPM** is higher than **Learn RPM**, we reduce the max learn percent. If **Learn RPM** is higher than **Optimized RPM**, we will increase max learn percent. The max learn percent cannot increase nor decrease by more than 20% at one time.

    When an optimization node at the top of learn queue becomes optimized, optimized RPM will likely go up and learn RPM will likely go down. As a result, the dynamic learn algorithm lowers the max learn percent, which is appropriate since an additional optimized node exists. Additionally, if a new, high-performing campaign starts learning on a venue, the campaign jumps to the top of the learn queue and learn is likely to increase. As a result, the dynamic learn algorithm increases the max learn percent, allowing this new campaign to become optimized faster.

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Targeted Learn](targeted-learn.md)
- [Learn Budget](learn-budget.md)
- [Optimization Levers](optimization-levers.md)
- [Sell-Side Optimization](sell-side-optimization.md)