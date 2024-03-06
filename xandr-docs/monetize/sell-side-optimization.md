---
title: Sell-Side Optimization
description: Learn how optimization gives sellers several controls that can be leveraged to minimize risk and maximize return. This page also explains about uncertain revenue and certain revenue.   
ms.date: 10/28/2023
---


# Sell-Side optimization

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

The online advertising marketplace is in many ways defined by its high levels of uncertainty. As a seller's revenue is often linked to an ad's success on the seller's inventory (measured through clicks or conversions), optimization gives sellers several controls that can be leveraged to minimize risk and maximize return.

Publishers consider buyer auction bids to be either **Uncertain Revenue** or **Certain Revenue**.

- **Uncertain revenue**

  When a campaign begins serving impressions on inventory in the RTB marketplace, it is unclear how much revenue nearly all non-managed CPC or CPA bids will generate; while the buyer (network) has agreed to pay a fixed rate for each success event on their ad, the optimization engine doesn't know how frequently success events will occur. This is uncertain revenue and cannot be accurately quantified until a significant number of success events have occurred to give a statistically valid sample (by determining the net revenue from each).

- **Certain revenue**

  While evaluating the value of uncertain bids, sellers can also choose to hold auctions that maximize bids from sources designated as certain revenue. Optimized bids can be any CPM base-bids, optimized CPC bids, or optimized CPA bids. These bids are treated as certain revenue because, through repeated success events occurring during the learn phase of the optimization process, it is possible to estimate an accurate value from those impressions.

Optimization uses an algorithm to intelligently allocate a percentage of total auctions to each of these two categories. The process, called [Dynamic Learn Percentage](dynamic-learn-percentage.md), considers success rates before maximizing revenue from an expanded group of certain revenue sources.

Sellers can also establish a [Give Up Price](give-up-price.md). The give up price is a bid price threshold which determines how bid prices are ranked in **Learn Auctions** and **Revenue Auctions**. If all bids offered in the auction type are below the user specified give up price, the auction is opened up to all bids.

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Targeted Learn](targeted-learn.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Learn Budget](learn-budget.md)
- [What is Valuation?](what-is-valuation.md)
- [Optimization Levers](optimization-levers.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
