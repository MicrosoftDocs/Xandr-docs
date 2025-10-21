---
title: Targeted Learn FAQ
description: In this article, find answers to frequently asked questions regarding Targeted Learn.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Targeted Learn FAQ

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

## What phases of optimization does the Targeted Learn algorithm affect?

The Targeted Learn algorithm only affects the learn phase.

## What buying strategies is the Targeted Learn algorithm used for?

Our Targeted Learn algorithm has been used for calculating learn bids in the learn phase for Managed, Cross Network CPA/CPC, and RTB campaigns using optimization.

## Where can I find out more information about Targeted Learn?

For an overview of our Targeted Learn algorithm, see [Targeted Learn](targeted-learn.md). For details about the new Learn Override optimization lever that goes with Targeted Learn, see [Optimization Levers](optimization-levers.md).

## What do you calculate a learn bid for?

We calculate a learn bid for a campaign-creative-venue-pixel combination. We try to estimate for a certain campaign-creative how frequently a pixel will fire on a specific slice of inventory (venue).

## What happens if my advertiser does not have any data?

When an advertiser has no historical data, Targeted Learn bids the average bid on a venue so the advertiser can collect data. Once the advertiser has five events in total, our algorithm will start leveraging the advertiser's historical data to calculate a learn bid.

## What happens if my campaign has multiple pixels?

Just like when your campaign is optimized, we calculate a valuation for each campaign, creative, venue, and pixel separately and then add those valuations for your bid. Likewise, during learn, we calculate a learn bid for each campaign, creative, venue, and pixel, and then add them to determine your total learn bid.

## If my campaigns under an advertiser vary in performance, will this affect my learn bids?

If your campaigns share the same events (pixels and clicks) and perform very differently, this could affect your initial learn bid. This differing in performance might make the learn bids at the Advertiser level of the Bayes Funnel a less representative average, since there is a distribution on performance. Once the learn bids are at a more granular level of the Bayes Funnel, this difference in performance among campaigns should not affect the other campaigns' learn bids. If this becomes an issue, you may consider splitting out the campaigns that are performing differently to make your calculated learn bids more accurate.

## What should I do if my campaign is underdelivering?

There are several reasons that a campaign might underdeliver, one of them being bidding low in learn. First, make sure that your campaign settings such as Inventory targeting, Segment targeting, Frequency capping, flight dates, budget, etc. are set to give your campaign access to enough inventory so that it stands a reasonable chance of winning auctions and delivering. If you believe low learn bids are causing your campaign to win fewer impressions than desired, you can increase your learn bids using the [Optimization Levers](optimization-levers.md) feature in the UI.

## How can I estimate my calculated learn bids?

When your campaign is learning, you can look at the average eCPM in learn for that campaign to estimate your learn bids. If you are just starting a campaign, you can estimate your initial learn bids by looking at the advertiser's historical RPM for those pixels. If you change the values on these pixels, you will have to modify the advertiser's historical RPM by the same amount for an accurate estimate. Note that if an advertiser has a lot of historical data on a venue, an initial learn bid will start off at the advertiser-venue level, which might differ from the calculated learn bid at the advertiser level.

## What historical data do you leverage?

The level of the Bayes Funnel dictates the historical data that targeted learn algorithm leverages. In the data it leverages, our algorithm uses the historical success rate (conversion rate or click through rate) to help calculate the learn bid.

## Are all my campaign's bids on the same level of the Bayes Funnel?

We calculate a learn bid for each campaign-creative-venue-pixel combination. Each of these combinations can be on a different level of
the Bayes Funnel.
