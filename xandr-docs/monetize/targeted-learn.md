---
title: Targeted Learn
description: In this article, learn what Targeted Learn is and how it works with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Targeted Learn

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

The Microsoft Advertising optimization engine uses a campaign's past performance data (conversion rate and click-through rate) to determine the appropriate bid for every impression relative to the campaign's cost-per-acquisition (CPA) or cost-per-click (CPC) goal. When you add a new campaign to Microsoft Monetize, however, performance data is not yet available. In this case, the Microsoft Advertising optimization engine must first learn what to bid for the campaign. This page describes the learn process.

## Overview

When a campaign starts, no performance data is yet available. The Version 7 optimization engine uses historical data to make an educated guess for success rate and then calculates a learn bid accordingly. As the campaign wins impressions, the algorithm takes new data into account, causing learn bids to increase on well performing venues (slices of inventory) and to decrease on poorly performing venues. In summary, by leveraging broader historical data, our new Targeted Learn algorithm makes learn bids more accurate faster and causes you to spend more efficiently while learning.

> [!NOTE]
> You have the ability to control certain areas of the learn process with the [Optimization Levers](optimization-levers.md), including the ability to override the learn bid amounts.
> [!TIP]
> To [Shorten the Targeted Learn Phase Using Bid Type Reports](shorten-the-targeted-learn-phase-using-bid-type-reports.md) for a campaign with a tight budget or timeline, use the Bid Type report for inventory exclusion.

## How Targeted Learn leverages historical data

The Targeted Learn algorithm leverages historical data from multiple levels, moving from less granular to more granular data as the campaign gets more success events. The order in which we leverage historical data is known as the Bayes Funnel, named as such due to its use of Bayes' theorem, a mathematical formula for calculating probability based on known conditions.

- advertiser
- advertiser, venue
- advertiser, venue, campaign,
- advertiser, venue, campaign, creative size
- advertiser, venue, campaign, creative size, creative

### Example

The most intuitive way to demonstrate how Targeted Learn leverages data is through an example with Venn diagrams. Assume that you have just created a new Pancakes campaign for the advertiser Bob's Diner. You had a similar campaign running previously that used the same pixel, Pixel A.

#### Step 1. Leverage advertiser data

Once the advertiser Bob's Diner has at least five conversions (Pixel A firing five times), we leverage all of the advertiser's data to calculate a learn bid.

:::image type="content" source="media/advertiser-data.png" alt-text="Diagram of Advertiser Data.":::

#### Step 2. Leverage advertiser and venue data

Since the advertiser has run this offer before, it may have even gotten five conversions on a single venue (Pixel A firing five times on a specific venue for that advertiser). In this case, when calculating a learn bid for this venue, our algorithm leverages the advertiser's data specific to this venue. This data is represented by the intersection of the advertiser and venue data.

:::image type="content" source="media/advertiser-venue-data.png" alt-text="Diagram that shows the intersection of Advertiser and Venue Data.":::

#### Step 3. Leverage advertiser, venue, and campaign data

At some point, the Pancakes campaign will get five conversions on a specific venue. In this case, when calculating a learn bid on this venue, our algorithm leverages the campaign's data specific to that venue. This data is represented by the intersection of the advertiser, venue, and campaign data.

:::image type="content" source="media/advertiser-venue-campaign-data.png" alt-text="Diagram that shows the intersection of Advertiser, Venue, and Campaign Data.":::

#### Step 4. Leverage advertiser, venue, campaign, and creative size data

Let's say the Pancake Campaign has three 300 x 250 creatives. Eventually, the 300 x 250 creatives will cumulatively get five conversions on a single venue. At this point, when any of the 300 x 250 creatives are bidding on a venue, our algorithm uses the 300 x 250 creative size data on that venue to calculate a learn bid. This data is represented by the intersection of the advertiser, venue, campaign, and size data.

:::image type="content" source="media/advertiser-venue-campaign-size-data.png" alt-text="Diagram that shows the intersection of Advertiser, Venue, Campaign, and Creative Size Data.":::

#### Step 5. Leverage advertiser, venue, campaign, creative size, and creative data

Finally, one of the Pancakes Campaign's creatives will receive three success events on a venue. When that creative is bidding on this venue, our algorithm leverages the creative's data specific to that venue to calculate a learn bid. This data is represented by the intersection of the the advertiser, venue, campaign, size, and creative data.

:::image type="content" source="media/advertiser-venue-campaign-size-creative-data.png" alt-text="Diagram that shows the intersection of Advertiser, Venue, Campaign, Creative Size, and Creative Data.":::

#### Step 6. Continue to learn

The Targeted Learn algorithm then leverages this level of data further while the campaign continues learning. Once the campaign gets enough events to exit the learn phase, it goes to the optimized phase as usual.

## If an advertiser has no data

When a new campaign is started under an advertiser with no historical data to leverage, the optimization engine determines the average bid on each venue and use this data to start winning impressions. Once the advertiser has three success events, the engine begins to leverage historical information to calculate learn bids.

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Learn Budget](learn-budget.md)
- [What is Valuation?](what-is-valuation.md)
- [Optimization Levers](optimization-levers.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
