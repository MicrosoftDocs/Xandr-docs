---
title: Line Item Pacing vs. Campaign Pacing
description: In this article, find information about the different methods of setting pacing along with best practice recommendations.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Line item pacing vs. Campaign pacing

Pacing allows you to evenly spread your budget over the course of a day or an entire line item or campaign, thereby minimizing the risk of overspending your budget in a very short period of time. The primary ways to assign pacing are at the **Line Item** level and at the **Campaign** level. While there are many advantages to using pacing at both levels, there are potential problems that must be considered. This document describes certain methods and procedures that will allow you to get the most out of pacing without unintended ramifications.

## What is pacing?

Pacing is the method by which the system determines how to spend the designated budget (or number of impressions) so that impressions serve evenly throughout over a specified period (a period can be a day or it can be the life of the campaign or line item). This method can be used if you wish to serve impressions for part of the day (called **dayparting**) or for the entire day.

You can set pacing when you are creating either a new **Line Item** or **Campaign** (or even at the insertion order level).

> [!NOTE]
> The budget allocation and pacing of your line item will be determined based on the flight dates of the underlying campaigns. As a result, we recommend that you have campaigns running for the entire duration of the parent line item's billing periods/flight dates.

### When should I use line item level pacing?

This method takes all of the campaigns under it into consideration when setting the pacing. This pacing technique allows you to control the budget of all of the campaigns in the line item as a whole. If you aren't concerned with the specific performance of individual campaigns, but you do need the line item to serve evenly, you should use this method. Note that you will not control which campaigns will use more of the line item budget and which will use less. Pacing at the line item level is based on **Revenue** or **Impressions**.

### When should I use campaign level pacing?

You should use this method when you want to control the budget of each individual campaign. While this may involve more work during setup, it is more accurate and has the added benefit of ensuring proper pacing at the line item level (assuming all campaigns pace correctly). Pacing at the campaign level is based on **Cost** or **Impressions**.

## Best practice recommendations

Microsoft Advertising makes the following suggestions regarding pacing:

### Resist pacing at multiple levels

In most cases, the benefits of pacing can be recognized by setting it at either the line item level **or** the campaign level. Setting it at both levels can be unnecessary and potentially result in uneven or under delivery. Daypart campaigns are a perfect example of this - the line item budget will attempt to pace that campaign across all 24 hours, while the campaign will pace only during the hours it is supposed to serve. These conflicting settings can lead to underspend or massive spend spikes.

There are a few rare cases where pacing at multiple levels has benefits, but if you are not certain as to why you are setting both levels, choose one or the other.

### Set pacing at the campaign level first

As a general rule, pacing should be done as specifically as possible to apply the greatest level of control. Therefore, you should always try to apply pacing to the campaign level first. Only if you cannot meet your pacing goals at the campaign level should you try to apply it at the line item level.

### Ensure that you target adequate inventory

If your campaign targets limited inventory (perhaps you have defined a very small segment or a very specific inventory source), daily pacing might limit your opportunities to serve to the point that it is practically impossible for you to spend anywhere near your daily budget. Ensure that you have an adequate inventory source so that your campaign can win enough auctions to spend properly.

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Why Use Budgeting?](why-use-budgeting.md)
- [Line Item Budgeting vs. Campaign Budgeting](line-item-budgeting-vs-campaign-budgeting.md)
- [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)
- [Daily Pacing](daily-pacing.md)
- [Key Budgeting and Pacing Concepts](key-budgeting-and-pacing-concepts.md)
