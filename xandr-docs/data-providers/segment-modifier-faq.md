---
title: Segment Modifier FAQ
description: In this article, explore answers to frequently asked questions about Segment Modifier.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Segment Modifier FAQ

This article contains frequently asked questions and answers about Segment Modifier.

## What is the Segment Modifier feature?

Segment modifier is a feature available to seats where campaigns can be associated with segments in such a fashion that permits users to override or modify the bid valuation provided by Xandr's internal optimization engine with values associated with the "modifying" segments.

## Is there a segment modifier "app"?

There is not a segment modifier "app" or API service. Segment modifier is a feature available to members that permits them to combine segments with values associated with them to the `"campaign_modifiers"` array of campaigns so that the campaigns may bid according to an external bidding strategy that is partially or not at all dependent on the optimization-generated bid valuations.

## Does the platform generate segment modifier values that I can use in Segment Modifier?

The Segment Modifier feature is for clients who wish to implement their own valuation models on Xandr's platform. We don't generate values to be fed into the feature. We suggest the optimization-produced valuations as the bids for an auction.

## How many segment modifiers can I associate to a campaign in the `"campaign_modifiers"` array of campaigns?

To be properly functional, the campaign_modifiers array of campaign objects must have a maximum of three elements: one of each modifier type (`segment_modifier_id`, `segment_price_id` and `segment_weight_id`). It is important to note that the `"value"` of segment modifier types `"segment_modifier_id"` and `"segment_price_id"` correspond to the Xandr ID of segments that are used to modify or override bid valuations (based on associated values with the segments). The `"value"` of segment modifier type `"segment_weight_id"` will simply be the weight by which the campaigns valuation will be modified each time it bids (it is unrelated to a segment).

## Related topics

- [Segment Modifier](segment-modifier.md)
- [Segment Modifier Data Provider Integration](segment-modifier-data-provider-integration.md)
