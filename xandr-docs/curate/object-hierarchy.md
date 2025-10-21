---
title: Microsoft Curate - Object Hierarchy
description: Learn about the key objects in Microsoft Curate for managing media buys and sales, including members, advertisers, and creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Object hierarchy

This page introduces the main objects that you work with to buy and sell media.

## Buy-side hierarchy

:::image type="content" source="media/ali-buy-side-object-hierarchy.png" alt-text="A diagram that shows the buy-side object hierarchy.":::

### Member

The [member](../monetize/network-guide.md) represents your account as a whole. At this level, you decide who's eligible to sell to you and what level of inventory audit you require, you create lists of domains and apps for efficient allowlist or blocklist targeting in campaigns, you put in place a cap on how much you are willing to spend per day on third-party inventory, and more.

### Advertiser

An [advertiser](working-with-advertisers.md) represents a single client or brand on whose behalf you want to serve ads on web and/or mobile inventory. At this level, you set the defaults to use in some of the objects under the advertiser (e.g., default currency, time format, time zone), a brand and offer category to apply to all creatives under the advertiser, and more.

You can have many advertisers in your network.

### Insertion order

An [insertion order](working-with-insertion-orders.md) represents a financial agreement you have with your advertiser that specifies what they would like you to execute. The insertion order contains information such as the total budget an advertiser allocates to you for a period of time or which third party verification the advertiser utilizes. Insertion orders also allow you to group line items accordingly.

You can have many insertion orders under a single advertiser.

### Line item

The line item(s) under an advertiser or insertion order represent the agreed upon strategies you will be executing for the advertiser. It contains information that the advertiser specifies, such as how much your advertiser has budgeted toward an offering or which targeting the advertiser requires.

You can have many line items under a single advertiser or insertion order.

### Creative

A creative is an actual ad, hosted either by Microsoft Advertising or by a third-party ad server. The Microsoft Advertising platform enables you to traffic a wide range of creative types, from banners to rich media types like interstitials and expandables.

Creatives belong to a specific advertiser. You can associate each creative to many line items under an advertiser.

### Segment pixel

A [segment pixel](working-with-segments.md) is placed on web pages to collect data about users, such as pages they visit, actions they take, or qualities such as gender, location, and wealth. When a segment pixel fires, the user is added to a segment, which can later be targeted in campaigns to attempt to reach the user again (retargeting).

Segment pixels belong either to the entire network or to a specific advertiser. Member-level segments are available for targeting in all line items under all advertisers. Advertiser-level segments are available for targeting only in line items under that specific advertiser.

### Conversion pixel

A conversion pixel is placed on web pages to track user actions in response to an advertiser's creatives, such as registering at a site or making a purchase. When a conversion pixel fires, Microsoft Advertising determines if the conversion (the registration, the purchase, etc.) can be "attributed", or tied to the user selecting or viewing one of the advertiser's creatives previously.

You can have many conversion pixels under a single advertiser. You associate each conversion pixel to many line items.

### Third-party creative pixel

A third-party creative pixel is used to trigger a third-party action when a creative is served, for example, performing ad verification, collecting data about the creative, or applying an AdChoices icon.

You can have third-party pixels at the network, advertiser, or creative levels. Defining these pixels at the network and advertiser levels lets you save time by applying pixels to creatives across the network or advertiser rather than one-by-one and helps you avoid the repeat auditing of creatives.

### Impression tracker

An impression tracker is used to track impressions associated with creatives that are hosted by off-platform (non-Microsoft Advertising) ad servers. This is done by attaching the tracker as a "piggyback pixel" on the externally hosted creative.

You can have many impression trackers under a single advertiser.

### Click tracker

A click tracker is used to track clicks associated with creatives that are hosted by off-platform (non-Microsoft Advertising) ad servers. This is done by attaching the tracker as a "piggyback pixel" on the externally hosted creative.

You can have many click trackers under a single advertiser.
