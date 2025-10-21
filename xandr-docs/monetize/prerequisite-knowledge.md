---
title: Prerequisite Knowledge
description: In this article, find information about some foundational concepts to be aware of to use optimization effectively.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Prerequisite knowledge

This page explains foundational concepts that you should be familiar with before diving into optimization. These concepts are not specific to optimization but understanding them will help you use optimization effectively.

## Booked revenue

This is the amount paid to the network by the advertiser. When line items are created, they are budgeted in this manner because the advertiser has indicated their goals and how much money they will give the network to achieve those goals, but it is up to the network to determine how to meet those goals.

## Performance goals

Performance goals are applicable if your advertiser's goal for earnings from a campaign are different than how they are paying you. For example, an advertiser may pay on a CPM basis but tell their network they want to meet a $20 CPA goal. This $20 CPA goal is used as a benchmark to determine whether to bid or not bid (i.e., the bid is checked to ensure that the specified amount will result in meeting the performance goal before it is actually submitted).

For more details, see [Understanding Performance Goals](understanding-performance-goals.md).

## Campaign budgets (media cost)

The campaign budget (also known as media cost) is the amount that the network has to spend purchasing inventory. The larger the budget, the more money that can be spent learning what works. With a smaller budget, it might be necessary to manually optimize somewhat. The size of your budget dictates inventory targeting, the number of campaigns and creatives to run, and how users are targeted.

## Bidding strategies

Only the following bidding strategies incorporate optimization:

- **Optimize to a predicted CPC or CPA goal**
- **Optimize to a % margin of booked revenue**
- **Pay on a Per-click (CPC) basis or Pay on a Per-conversion (CPA) basis**
- **CPC or CPA booked revenue**

For additional details on these strategies, review [Optimization Buying Strategies](optimization-buying-strategies.md).

## Campaign setup

When deciding how to create campaigns, you should keep optimization in mind. Each campaign represents the ability to bid on an impression, so the decisions made during setup influence the inventory or audience on which bids are placed and how the bid is calculated:

- **Targeting**: The targeting settings for geography, operating system, segment targeting etc., all determine which impression a campaign bids on.
- **Number of Creatives or Inventory**: A high number of creatives and landing pages in a campaign hinders performance because there are too many different variables to optimize, indicating that fewer creatives should be used. This is also true for inventory; there is a point where too much inventory significantly slows down optimization and should be limited. This number of creatives and the breadth of the available inventory must be determined for each campaign.

## Pacing

You can establish whether campaigns or line items will spend their budgets as fast as they possibly can (i.e., they bid in every auction they can) or if they will moderate their spend so as to spend their budget evenly over a given period (i.e., they "sleep" for a period between auctions) to make their budgets last. Pacing can be done over the lifetime of a campaign or it can be done on a daily basis.

## Frequency and Recency

Users are generally more likely to convert the first few times they see a creative (frequency). Additionally, they are more likely to convert when they have just seen the creative (recency).

Users who have not seen a creative many times, or have not seen that creative in a long time, are more valuable to an advertiser, and therefore the bid amount will be higher. You can set frequency and recency caps at the Advertiser, Insertion Order, Line Item, Campaign, or Creative levels.

Because users value impressions differently as the frequency and recency changes, the cadence modifier modifies the calculated bid based on how many times the user has seen the creative and how long it has been since the last creative. The bid is increased for users more likely to click or convert and decreased for those who are less likely.

## Conversion attribution

Conversion attribution determines if a click or conversion by a user can be associated to that user seeing the creative sometime in the past. When a user clicks an impression or performs the task directed by the landing page, a conversion pixel reports the action, and the system checks to see how long ago that user was exposed to the creative that led to the landing page. If the user saw the creative within a defined period, that click/conversion is attributed to that impression and is therefore counted by the campaign as a success event.

A [lookback period](conversion-attribution.md) that is set too short won't capture the full impact from ad exposure and will provide more limited data than necessary for optimization to work with. A period that is set too long can result in more conversions being counted that didn't actually result from seeing advertising. For example, an offer involving an online brokerage account might require more thought and consideration before a user makes the move to sign up, requiring a longer lookback window. An ad for ring tone downloads would likely result in more immediate conversions, requiring a shorter lookback window.

## Historical data and Current data

There are two main sources of data used by the optimization engine: **Historical Data** and **Current Data**.

- **Historical Data**: This data is drawn from older nodes which have served ads on venues which are identical or close to the current node. Prior to the beginning of a campaign, the optimization engine has no data regarding how much it should bid. Data from similar venues provide a point of reference and allow the system to determine a starting bid which is in a reasonable range. A good starting bid is important, as it shortens the learn phase of optimization, allowing the campaign to be optimized more quickly and therefore saving money. With this type of data, a lookback window restricts older data in favor of newer data; the default lookback period is **30** days.
- **Current Data**: This data comes from the bidding activity of the current node. As a campaign begins to bid on auctions, the results are sent back to the system and applied to the bid formula (see above). As auctions are won or lost, the greater number of impressions and success events provides a greater data sample. At a certain point (determined by the **Learn Threshold** setting in the [Optimization Levers](optimization-levers.md)), the node moves to the **Optimized** phase.

## Related topics

- [Optimization Guide](optimization-guide.md)
- [Understanding Optimization](understanding-optimization.md)
- [Optimization In-Depth](optimization-in-depth.md)
- [Understanding Performance Goals](understanding-performance-goals.md)
- [Conversion Attribution](conversion-attribution.md)
- [Optimization Levers](optimization-levers.md)
