---
title: Microsoft Monetize - Object Hierarchy
description: Explore vital media transaction elements, streamlining buying/selling with key objects for efficient transactions.
ms.date: 10/28/2023
---

# Microsoft Monetize - Object hierarchy

This page introduces the main objects that you work with to buy and sell media.

### Augmented line item

The following image illustrates the augmented line item.

:::image type="content" source="media/buy-side-object-hierarchy.png" alt-text="Diagram that defines augmented line item in buy-side hierarchy.":::

## Network

The [Network](network-guide.md) represents your account as a whole. At this level:

- You decide who's eligible to sell to you and what level of inventory audit you require [seller settings](set-seller-defaults.md).
- You put in place a cap on how much you are willing to spend per day on third-party inventory [safety budget](capping-daily-spend-on-third-party-inventory-safety-budget.md) and more.

## Advertiser

An [advertiser](working-with-advertisers.md) represents a single client or brand on whose behalf you want to serve ads on web and/or mobile inventory. At this level, you set the defaults to use in some of the objects under the advertiser (e.g., default currency, time format, time zone), a brand and offer category to apply to all creatives under the advertiser, and more.

You can have many advertisers in your network.

## Insertion order

An [insertion order](working-with-insertion-orders.md) represents a financial agreement you have with your advertiser that specifies what they would like you to execute. The insertion order contains information such as the total budget an advertiser allocates to you for a period of time, or which third party verification the advertiser utilizes. Insertion orders also allow you to group line items accordingly.

You can have many insertion orders under a single advertiser.

## Line item

The [line item(s)](working-with-line-items.md) under an advertiser or insertion order represent the agreed upon strategies you will be executing for the advertiser. It contains information that the advertiser specifies, such as how much your advertiser has budgeted toward an offering, or which targeting the advertiser requires.

You can have many line items under a single advertiser or insertion order.

## Creative

A [creative](exploring-creatives.md) is an actual ad, hosted either by Microsoft Advertising or by a third-party ad server. The Microsoft Advertising platform enables you to traffic a wide range of [creative types](add-creatives-in-bulk.md), from banners to rich media types like interstitials and expandables.

Creatives belong to a specific advertiser. You can associate each creative to many line items under an advertiser.

## Segment Pixel

A [segment pixel](working-with-segments.md) is placed on web pages to collect data about users, such as pages they visit, actions they take, or qualities such as gender, location, and wealth. When a segment pixel fires, the user is added to a segment, which can later be targeted in line items to attempt to reach the user again (retargeting).

Segment pixels belong either to the entire network or to a specific advertiser. Network-level segments are available for targeting in all line items under all advertisers. Advertiser-level segments are available for targeting only in line items under that specific advertiser.

## Conversion pixel

A [conversion pixel](working-with-conversion-pixels.md) is placed on web pages to track user actions in response to an advertiser's creatives, such as registering at a site or making a purchase. When a conversion pixel fires, Microsoft Advertising determines if the conversion (the registration, the purchase, etc.) can be "attributed", or tied to the
user clicking on or viewing one of the advertiser's creatives previously [conversion attribution](conversion-attribution.md).

You can have many conversion pixels under a single advertiser. You associate each conversion pixel to many line items (for tracking payment or performance goals on a CPA basis).

## Third-Party creative pixel

A [third-party creative pixel](create-a-third-party-network-pixel-for-your-creatives.md) is used to trigger a third-party action when a creative is served, for example, performing ad verification, collecting data about the creative, or applying an AdChoices icon.

You can have third-party pixels at the network, advertiser, or creative levels. Defining these pixels at the network and advertiser levels lets you save time by applying pixels to creatives across the network or advertiser rather than one-by-one and helps you avoid the repeat auditing of creatives.

## Impression tracker

An [impression tracker](create-an-impression-tracker.md) is used to track impressions associated with creatives that are hosted by off-platform (non-Microsoft Advertising) ad servers. This is done by attaching the tracker as a "piggyback pixel" on the externally hosted creative.

You can have many impression trackers under a single advertiser.

## Click tracker

A [click tracker](create-a-click-tracker.md) is used to track clicks associated with creatives that are hosted by off-platform (non-Microsoft Advertising) ad servers. This is done by attaching the tracker as a "piggyback pixel" on the externally hosted creative.

You can have many click trackers under a single advertiser.

## Sell-side hierarchy

The following sections in this article explain the sell-side hierachy. The details in the following image are covered in these sections.

:::image type="content" source="media/sell-side-object-hierarchy.png" alt-text="The diagram that defines sell-side hierarchy.":::

## Account control and customization in the network

The [network](network-guide.md) represents your account as a whole. At this level, you decide who's eligible to buy from you and what type of payment and targeting access you allow for those eligible  ([buyer settings](set-default-buyer-eligibility-allowed-payment-types-and-targeting-access.md)), you decide which publishers will be [exposed for targeting by third-party resellers](managing-your-inventory-reselling-exposure.md), and more.

## Network ad quality

Your [network ad quality](working-with-network-ad-quality.md) restricts which creatives can serve on inventory in your network, based on creative attributes such as buyer or brand. These rules are applied to every impression across all publishers in your network.

Restrictions set in a your network ad quality profile cannot be loosened at the publisher level by a [publisher template](create-a-publisher-template.md) or [custom profile](create-a-custom-profile.md); publisher-level ad quality settings may only be more strict than network ad quality, never less.

## Content category

Microsoft Advertising provides a set of "universal" content categories, which are commonly used categories that you can apply to placement groups and placements for buyer targeting. You can also create your own [custom content categories](manage-custom-content-categories.md) and apply them to placement groups and placements for buyer targeting.

Direct campaigns can target your universal and custom categorization by default, but you must [expose universal and custom content targeting to third-party buyers](edit-buyer-eligibility-allowed-payment-types-and-targeting-access.md) in the Partner Center.

## Package and deal

A [package](selling-deals.md) is a pre-made combination of your inventory and/or data. Buyers can browse your packages and create deals from them "off-the-shelf", or they can use your packages as a jumping-off point for deal negotiations.

A [deal](create-a-custom-deal.md) is a one-off custom package for a specific buyer.

## Publisher

A [publisher](working-with-publishers.md) represents a single client on whose behalf you want to sell inventory. At this level, you define your affiliation to the publisher (managed or owned & operated), whether or not the publisher will accept CPA or CPC deals from your managed advertisers as well as other trusted partners on the platform, how much information you want to expose in targeting and reporting when reselling the publisher's inventory, and more.

You can have many publishers in your network.

## Payment rule

A [payment rule](working-with-payment-rules.md) represents the financial agreement between you and a publisher.

You can have a single payment rule for all impressions from a publisher, or you might have a base rule that serves as a default and more specific [conditional payment rules](create-payment-rules.md) that apply to individual impressions based on geography, frequency, or other targeting criteria.

## Publisher ad quality

A [publisher ad quality profile](working-with-publisher-ad-quality.md) restricts which creatives can serve on a specific publisher's inventory, based on creative attributes such as buyer or brand. Note that restrictions set in your [network ad quality profile](working-with-network-ad-quality.md) cannot be loosened in a publisher ad quality profile; publisher-level ad quality settings may only be more strict than network ad quality, never less.

## Placement group

A [placement group](working-with-placement-groups.md) provides a way for you to organize a publisher's placements. At this level, you define the appropriate supply type for the placements in the group, decide whether or not the placements in the group are available for reselling to third-parties, and apply inventory categorization and self-auditing criteria to the placements in the group by default.

You can have many placement groups under a single publisher.

## Placement

A [placement](working-with-placements.md) represents a piece of web or mobile inventory where a creative with matching specifications can serve. At this level, you select the size and types of creatives that can serve on the placement, set a reserve price, and self-classify the placement with categories and sensitive attributes for line item targeting and reporting.

You can have many placements under a single placement group.
