---
title: Optimization In-Depth
description: Explore optimization concepts, venue grouping, buying strategies, valuation, and levers influencing bid strategies in online advertising.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Optimization in-depth

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

This section explains and demonstrates the detailed concepts and components involved in optimization, such as venues and nodes, and shows you how to influence the optimization engine.

- **[Optimization Buying Strategies](optimization-buying-strategies.md)** - There are two primary types of buying: Managed and RTB. Managed buying, also known as Direct buying, refers to a situation where a network is buying inventory from a publisher with which they have a financial relationship. RTB buying, also known as Third-Party buying, refers to a situation where a network is buying inventory from publishers with whom they do not have a direct financial relationship.
- **[What is a Venue?](what-is-a-venue.md)** -  In order to maximize the accuracy of our predictions, all of the inventory on the Microsoft Advertising platform is entered into groupings of like inventory buckets called venues.
- **[Targeted Learn](targeted-learn.md)** - The Microsoft Advertising optimization engine uses a campaign's past performance data (conversion rate and click-through rate) to determine the appropriate bid for every impression relative to the campaign's cost-per-acquisition (CPA) or cost-per-click (CPC) goal. When you add a new campaign to Microsoft Advertising Monetize, however, performance data is not yet available. In this case, the Microsoft Advertising optimization engine must first "learn" what to bid for the campaign.
- **[What is an Optimization Node?](what-is-an-optimization-node.md)** - Nodes are groupings of impressions from advertisers (or networks representing advertisers) which are a combination of a campaign, a specific creative, the venue, and the conversion pixel. Optimization is performed against a single node.
- **[Learn Budget](learn-budget.md)** - The learn budget is applied to nodes in order to determine accurate bids for inventory. You can determine how much of your overall budget will be used as learn.
- **[What is Valuation?](what-is-valuation.md)** - Valuation is the process by which our system determines a bid amount. In order to obtain one success event (i.e., a success event is an impression which leads to the user taking the action intended by the advertiser, such as a purchase), it is necessary to display a certain number of impressions to users. In order to earn a profit, the advertiser must pay less for the impressions displayed to obtain the success event than the money earned by the success event.
- **[Optimization Levers](optimization-levers.md)** - Certain users have the ability to use Optimization Levers to influence how optimization works for a campaign, for example, how much you bid during the Learn phase, how many success events (clicks or conversions) it takes to move from the Learn phase to the Optimized phase, as well as whether you want to optimize to the campaign bidding strategy before optimizing to the line item booked revenue.
- **[Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)** - The Cadence Modifier adjusts the amount of a bid based on the frequency (the number of times the user has seen the creative) and recency (the amount of time that has passed since the user last saw the creative) of the user. Frequency and recency are two of many factors which influence the conversion likelihood.
- **[Sell-Side Optimization](sell-side-optimization.md)** - The online advertising marketplace is in many ways defined by its high levels of uncertainty. As a seller's revenue is often linked to an ad's success on the seller's inventory (measured through clicks or conversions), optimization gives sellers several controls that can leveraged to minimize risk and maximize return.
- **[Dynamic Learn Percentage](dynamic-learn-percentage.md)** - Dynamic learn is a sell-side optimization algorithm designed to accelerate the learning process and improve publisher revenue eCPM by determining an optimal venue learn percent through adjustments to the previous learn percent based on performance of learn versus optimized impressions.
- **[Give Up Price](give-up-price.md)** - The Give Up Price is a bid price threshold which determines the order in which bids are considered in an auction.

## Related topics

- [Optimization Guide](optimization-guide.md)
- [Understanding Optimization](understanding-optimization.md)
- [Prerequisite Knowledge](prerequisite-knowledge.md)