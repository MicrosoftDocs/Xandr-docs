---
title: Publisher Analysis - Cross Network CPA and CPC
description: In this article, learn what cross network CPA/CPC is and how it affects the dynamic learn algorithm.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Publisher analysis - Cross network CPA and CPC

Our dynamic learn algorithm automatically adjusts the amount of a venue's inventory that we're allocating to learn. Our new algorithm does this by comparing the revenue eCPM of learn offers against the revenue eCPM of optimized offers. If learn offers are outperforming optimized offers on a venue, our algorithm will automatically increase the percent of traffic that we allow to learn on that venue. This adjustment enables your learn offers to optimize faster. Once that offer becomes optimized, the performance of learn offers versus the performance of optimized offers will change. The next time our algorithm runs, it notices that change and throttles down the learning allocation. Since we always want to reserve some portion of a publisher's inventory for learning, we never allow our algorithm to go below 5%.

Why is that important? When you enable cross network CPC/CPA offers to run on your inventory, those offers are only eligible for learn impressions. If cross network CPC/CPA offers never perform better than managed CPC/CPA/CPM or external CPM offers, our algorithm will quickly throttle learning allocation down to 5%. As such, cross network CPC/CPA offers would never get more than 5% of your publisher's traffic. The only way that external CPC/CPA offers can win more than 5% of your traffic is by outperforming all other available offers.

Now let's look at graphs of a few publishers' impression allocations. Note that the highlighted section indicates when cross network CPC/CPA was enabled.

## Publisher 1

Below is a graph of impression allocation over time:

:::image type="content" source="media/pub-a.png" alt-text="Graph that shows impression allocation over time for Publisher 1.":::

- After five days of having cross network CPC/CPA demand enabled, approximately 20% of the publisher's impressions are still going to those offer types. This indicates that those offers are bringing value to the publisher.
- CPC offers represent a small fraction of total impressions. This indicates that CPC offer types are either not as competitive as the CPA bids for this Publisher or that there is simply a lack of CPC demand. Based on our experience, it is generally the later.

Below is a graph of Total Network RPM over time:

:::image type="content" source="media/pub.png" alt-text="Graph that shows total network RPM over time for Publisher 1.":::

- Since enabling cross network CPC/CPA demand, the total network RPM for this publisher has been on an increasing trend, indicating that these offer types are performing on this publisher.
- It will take time for these offer types to optimize on your inventory. It's important to always compare the same day of week performance (Monday vs Monday, Tuesday vs Tuesday, etc.) to eliminate natural day of week performance differences.

## Publisher 2

Below is a graph of impression allocation over time:

:::image type="content" source="media/pub-c.png" alt-text="Graph that shows impression allocation over time for Publisher 2.":::

- After five days of having cross network CPC/CPA demand enabled, ~23% of the publisher's impressions are still going to those offer types. This indicates that those offers are bringing value to the publisher.
- As you can see above, resold CPM impressions were virtually unaffected while default impressions dropped by ~60%.
Below is a graph of Total Network RPM over time:

:::image type="content" source="media/pub-b.png" alt-text="Graph that shows total network RPM over time for Publisher 2.":::

- As you can see above, Total Network RPM has increased by ~45% since enabling cross network CPC/CPA demand.

> [!NOTE]
> It's important to account for how you were previously monetizing those default impressions.

## Publisher 3

Below is a graph of impression allocation over time:

:::image type="content" source="media/pub-d.png" alt-text="Graph that shows impression allocation over time for Publisher 3.":::

- For this particular publisher, cross network CPC/CPA impression allocation has been hovering around ~4%.
- This low allocation rate was due to the fact that managed campaigns were targeting this inventory with a higher priority.
- This low allocation means that it will take longer for CPC/CPA offers to learn on this inventory since they are restricted by the number of impressions available for "learn".

## Related topics

- [Targeted Learn](targeted-learn.md)
- [CPC and CPA Payment Types](cpc-and-cpa-payment-types.md)
