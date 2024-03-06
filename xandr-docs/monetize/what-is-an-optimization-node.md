---
title: What is an Optimization Node?
description: Explore enhanced prediction by grouping inventory based on venues. Nodes undergo learning or optimization phases for efficient results.
ms.date: 10/28/2023
---

# What is an optimization node?

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide ALI](optimization-guide-ali.md).

Nodes are groupings of impressions from advertisers (or networks representing advertisers) which are a combination of a campaign, a specific creative, the venue, and the conversion pixel. Optimization is performed against a single node.

Each individual node can be in either a **Learn** phase or an **Optimized** phase. A campaign can use multiple nodes at once; therefore, part of a campaign could be in the Learn phase while other part is in the Optimized phase.

## Optimization phases: Learn and Optimized

As auctions run and information about the bids associated to a campaign is recorded, the data is parsed into one of the two possible optimization phases - Learn or Optimized - depending on how much data the node has accumulated.

> [!IMPORTANT]
> In both phases, the valuation equation is altered to account for the limitations in the amount of data we have. This is discussed in the [What is Valuation?](what-is-valuation.md) section.

## Learn phase

In the beginning stages of a campaign, impressions are recorded as part of the **Learn** phase. In this phase, the system is trying to determine the optimized bid valuation and needs to collect data to determine the value of a click or conversion. As a node starts to accumulate more and more data, our confidence in the bid valuations increases.

Example:

When bidding on inventory that you are not familiar with, or if you have a new creative, you must bid in such a way that you learn what amount is too high (wins all auctions but is not profitable) or too low (wins no auctions at all). For this reason, bids at the beginning of the learn phase can vary greatly. Only by seeing what happens when you make bids
can you get an understanding of the market. For example, if you bid $.15 on inventory and win no auctions, you learn that you must bid higher in order for end users to view your creative. If you bid $5.00 on inventory and win every auction, you learn that you should lower your bid to save money on those impressions and therefore become more profitable.

## Optimized phase

The advertiser can establish the number of success events that are required to advance from the Learn stage to the Optimized stage. If you set that number appropriately, the statistical sample enables the bidder to bid an amount which wins the number of auctions you need while spending an amount of money on each bid to keep you profitable.

For additional information on how learn and optimized work, see the [Learn Budget](learn-budget.md) section.

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Learn Budget](learn-budget.md)
- [Targeted Learn](targeted-learn.md)
- [What is Valuation?](what-is-valuation.md)
- [Optimization Levers](optimization-levers.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
