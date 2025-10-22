---
title: September 30, 2015 
description: Learn about enhancements to the bidding protocol and to version 1.16 of the AppNexus Impression Bus API. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# September 30, 2015 

We are excited to announce the following enhancements to the bidding protocol and to version 1.16 of the AppNexus Impression Bus API.

## Impression Bus API

### New services

### Spend protection pixel service

As part of the Beta phase of the AppNexus Spend Protection program, the new read-only [Spend Protection Pixel Service](#spend-protection-pixel-service) allows you to retrieve the pixel `id` of your third-party verification partner. You then include that pixel in any bid responses for which you wish to enable AppNexus Spend Protection using the `spend_protection_pixel_ids` array in Bid Response of the Bidding protocol.

### Changed reports

**Platform buyer report and platform seller report**

Four new viewability metrics are available in the [Bidder Platform Buyer Report](bidder-platform-buyer-report.md) and the [Platform Seller Report](platform-seller-report.md). The metrics are:

- `imps_viewed` - The number of measured impressions that were viewable.
- `view_measured_imps` - The total number of impressions that were measured for viewability.
- `view_rate` - The percentage of impressions that were viewable out of the total number of impressions measured for viewability.
- `view_measurable_rate` - The percentage of impressions measured for viewability out of the total number of impressions.

## Bidding protocol

**Bid request**

If you were participating the Alpha phase of the AppNexus Spend Protection program, the `certified_supply` field (Alpha) has been deprecated. Instead, the `spend_protection` field (Beta) is now used to specify that the inventory associated with the [Bid Request](bid-request.md) is associated with the AppNexus Spend Protection program.

Several new arrays have been added to the `deals` array:

- To support changes to media settings on placements sold through deals, the `allowed_media_types` and `allowed_media_subtypes` arrays have been added to the Deals array. The `allowed_media_types` array is used to limit the media type, or the general display style of creatives, that can serve on placements that are part of a given deal. The `allowed_media_subtypes` array is used to limit the media subtype, or the specific display style of creatives allowed to serve on placements that are part of a given deal.
- To support the ability to allow deals to serve a greater range of creatives, the `ad_quality_override` field has been added. This field can be used to permit creatives to serve with no restrictions on ad quality, or to allow creatives that are pending review to serve.
