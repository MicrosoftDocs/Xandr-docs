---
title: Mediation Bid Setup Best Practices
description: In this page, learn about the best practices for Bid setup in one place like Bid price, Campaign priorities, Network Inventory ID, Targeting and Waterfall Setup.    
ms.date: 10/28/2023
---


# Mediation bid setup best practices

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

There are a number of factors to keep in mind when you're setting up bids. This page attempts to collect a number of best practices for bid setup in one place. Important factors to consider include:

- Bid Price
- Bids and Campaign Priorities
- Network Inventory ID
- Targeting
- Waterfall Setup

For detailed instructions on creating bids, see [Mediation Bids](mediation-bids.md).

## Bid price

We recommend using the last 7 days' eCPM from each of your networks as a starting point. This number can be pulled directly from each network's UI, or from the **Bids** page in our system if you have reporting enabled for that network. It is important that bids are updated on a daily basis to maximize the value of the auction. Inaccurate bids will have an adverse impact on seller revenue.

## Bids and campaign priorities

This section lists several important items to note about the interaction between bids and campaign priorities.

**Priority for non-bid managed campaigns**

When a mediated bid is present, your other campaigns with priorities less than 5 won't be evaluated in the auction.

**Priority for campaigns that are part of bids**

What we call a "bid" is actually made up of several objects, including a campaign. This campaign's priority is set to 5 by default when your bid is created in the UI, and shouldn't ever be changed.

If you change this campaign's priority the bid will stop working. This can happen if you are updating campaign priorities via the API and accidentally update a campaign that's part of a bid.

There are several ways to avoid this issue when using the API:

- Don't make any updates to advertisers, line items, campaigns, or creatives with the words "Mediated" or "Mediation" in their names.
- Creatives used for mediation have the `is_mediation` flag set. If you're updating a line item or campaign, you can check its `creatives` array to see if one of the creatives is a mediation creative. If so, don't update that line item or campaign.

## Bid optimization

We recommend using the **Bid Optimization** feature on each bid to allow the system to dynamically adjust bid price based on the frequency and recency of the user. Enabling this feature will improve the accuracy of bids and improve publisher yield. Even when bid optimization is enabled, it is important to continue updating bid prices on a daily basis.

## Network inventory IDs

It is **critical** that each bid has a unique network ID. In other words, do **not** share network IDs across bids. Using the same network ID on multiple bids will cause revenue to be overcounted in reporting.

## Targeting

Whenever possible, it is best to create different bids by:

- Placement
- Ad size
- Geo
- Operating system

We've found these attributes to have the most impact on performance within networks. Remember that each bid **must** have a unique network inventory ID.

## Network waterfall

We recommend using no more than 3 or 4 networks in the waterfall for a given impression. Using more than 4 networks will increase ad serving latency and adversely impact the end user's experience. If too many networks are active, we may not be able to retrieve an ad within the time limit for content retrieval.

## Related topic

 [Mediation FAQs](mediation-faqs.md)
