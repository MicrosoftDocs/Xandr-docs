---
title: What is a Venue?
description: Explore optimizing predictions by grouping platform inventory into venues for uniform performance assessments based on user behavior variations. 
ms.date: 10/28/2023
---

# What is a venue?

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide ALI](optimization-guide-ali.md).

## Overview

In order to maximize the accuracy of our predictions, all of the inventory on the Microsoft Advertising platform is entered into groupings of like inventory buckets called venues so that:

1. Each venue can be expected to similarly impact response rates. For example, users visiting the New York Times website from the UK are likely to respond differently to offers than visitors from the US. Similarly, users are likely to respond differently to a front page placement on a site compared to one nested several layers deep.
1. The venue contains enough impressions to allow us to make some determination of performance relatively quickly while still being as uniform as possible in terms of the above characteristics.

Venues are groupings used to categorize inventory at a high level. There are six different levels of granularity for venues:

1. **Member**
1. **Member - Publisher**
1. **Member - Publisher - Tag**
1. **Member - Publisher - Tag - Geo**
1. **Member - Publisher - Tag - URL**
1. **Member - Publisher - Tag - URL - Geo**

As you move further down the list, the level of granularity increases (i.e., there is a greater level of detail in **Member - Publisher - Tag - URL** than in **Member - Publisher**). At the start of the optimization procedure, data from older venues that most closely match the current campaign situation are used to provide a basis for determining learn bids. The closer and more detailed that the components of the existing venue are to the details of the current campaign, the closer the data from that venue is to the current campaign, making that data more valuable for comparison purposes (which means less money spent in the learn phase).

## Venue creation

We begin the process of venue creation by collecting data on combinations of the most granular level in the list of possible venue levels (defined above). We calculate the average of the last 14 days' worth of data to derive an average daily impression number per venue (e.g., the number of impressions that meet all of the criteria in a venue).

There are two sets of criteria used to create a venue:

- In an external (non-Microsoft Advertising) environment, there must be an average of 2,500,000 impressions recorded each day over the 14-day period.
- In an internal (Microsoft Advertising) inventory environment, there must be an average of 100,000 impressions recorded each day over the 14-day period.

When one of these criteria are met, a venue gets created on that level, corresponding to whichever tag-url-geo (or tag-url, or tag-geo, or tag, etc.) on which the threshold is exceeded.

> [!IMPORTANT]
> When calculating average impression numbers for venue creation, days in which no impressions were recorded are not counted, but they are counted as part of the 14-day period. For example, if 1,200,000 impressions were recorded in the last 14 days, but four of those days had zero impressions, the system will divide 1,200,000 by 10 (14-4) to determine the daily average. In this case, the result (120,000) would be sufficient to create a venue from Microsoft Advertising inventory. However, if even one impression was recorded on each of those four days, the system would divide 1,200,000 by 14 to determine the daily average. In this case, the result (85,714) would not be sufficient to create a venue for inventory from Microsoft Advertising.

## Example

Assume that you have a daily average of 4,000,000 impressions, all with the same **Member - Publisher - Tag - URL**, but with 10 different **Geo** values (with no more than 600,000 impressions on any single **Geo**) from External inventory. The venue will be created at the **Member - Publisher - Tag - URL** level, because that is the most granular level with a daily average of at least 2,500,000 impressions.

> [!IMPORTANT]
> Remember that a venue can be created at any of the six levels described above. Venues further down in the list have greater granularity and are therefore more valuable when determining bids.

In order to avoid double-counting impressions, all impressions are counted only at the lowest-level (most granular) venue. When a new venue is created, it immediately absorbs the count of the impressions that created it; subsequently, the parent venue (in which those impressions were counted until the new venue was created) is reduced by the same
number, because it is no longer the lowest-level.

## Venue deletion

Venues are deleted when the average number of daily impressions over the previous 14 days drops below 20,000 (see Venue Creation above) to determine the method of calculating the daily average). The impressions are then transferred up one level to the parent venue (i.e., the reverse of the process that happens when a venue is created). In most cases, the
venues that get deleted are on the **Tag** level, and so the impressions are transferred back to the **Publisher** level. Venues created within the previous two days will not be deleted.

## Resurrection of a deleted venue

If the optimization engine creates a venue and then deletes it due to a lack of impressions, that venue is resurrected if it exceeds 100,000 average daily impressions over the previous 14 days (see Venue Creation above) to determine the method of calculating the daily average. As before with venue creation, the impression data will be transferred from
the parent venue to the resurrected child venue. An inactive venue is always available for resurrection, regardless of the length of time it has been inactive.

Throughout the entire process of creation, deletion, and resurrection of venues, data is maintained and transferred between parent and child venues.

## How the Microsoft Bidder determines which venue to use?

At the time of an auction, the bidder determines which venue to use by matching the current inventory to the closest venue, starting with the most-granular (since high granularity makes for a more accurate bid amount, the bidder wants to use the highest degree of granularity):

1. **Member - Publisher - Tag - URL - Geo**
1. **Member - Publisher - Tag - URL**
1. **Member - Publisher - Tag - Geo**
1. If there are no matching entries, it looks for a **default venue** for the **Tag**.
1. If there is no default venue for the **Tag**, the bidder looks for a **default venue** for the **Publisher**.
1. If there is no default venue for the **Publisher**, the bidder looks for the a **default venue** for the **Member**. If the Member does not have a default venue, the bidder defaults to a global default bid value of **$1**.

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Targeted Learn](targeted-learn.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Learn Budget](learn-budget.md)
- [What is Valuation?](what-is-valuation.md)
- [Optimization Levers](optimization-levers.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
