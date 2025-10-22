---
title: AppNexus Bidding Protocol
description: In this article, find information about the AppNexus bidding protocol and its process for request/responses.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# AppNexus bidding protocol

> [!IMPORTANT]
>
> - **Not Supported**: The AppNexus Bidding Protocol is no longer supported; this documentation is for legacy purposes only. **This has been deprecated.**
> - If you're a new bidder integrating with AppNexus, please see the [OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

When you register a bidder instance with the AppNexus platform, you will be sent a series of requests by the AppNexus Impression Bus, the key one being the [Bid Request](bid-request.md). Your bidder will respond with a series of responses, the key one being the [Bid Response](bid-response.md). Below you will find a list of the requests and responses and brief explanations of the usage for each. A bidder will need to build "handlers" (i.e. a bid request handler, a click handler, etc) for each of the services it plans to support.

## Impression-specific request/response

There are three request/responses used for a standard impression that passes through the Impression Bus:

- [Bid Request](bid-request.md)
- [Bid Response](bid-response.md)
- [Notify Request](notify-request.md)

:::image type="content" source="media/appnexus-bidding-protocal-fig-a.png" alt-text="A diagram depicting the bidding protocol process.":::

### Process

1. An ad request (client side) originates from the user's browser on a publisher site and requests an ad from the Impression Bus through a TinyTag.
1. The Impression Bus sends a (server side) [Bid Request](bid-request.md) to all applicable bidders and awaits their responses. Each bidder's user data is passed with the Bid Request.
1. The bidders send a [Bid Response](bid-response.md) to the Impression Bus within the timeout window (currently 100ms for most sellers, longer for some sellers). This will include the javascript code that will be used to modify the User Data in the event that that bidder wins the auction.
1. The Impression Bus determines the highest paying bid, and returns the associated creative to the user's browser.
1. A [Notify Request](notify-request.md) is sent to all applicable bidders, including bidders that did not send in a Bid Response, to detail the results of the auction.

> [!NOTE]
> This process is slightly different for auctions in which the results are passed to a secondary exchange.

## Other request/responses

### Bidder ready request

Every bidder instance (see [Bidder Instance Service](bidder-instance-service.md)) is required to have a working service that responds to a [Ready Request](ready-request.md). This allows the Impression Bus know in real time what instances it should send traffic to.

### Bidder click request

A bidder may (optionally) build a click handler for the [Click Request](click-request.md). This is only needed if your bidder's members choose to use click tracking through the Impression Bus. If all of a member's creatives are third-party (e.g. DART or Atlas) tags, and they choose to use the third party solely for click tracking purposes, your bidder may not need to support this request type.

### Mobile OpenRTB for bidders

Mobile demand partners can integrate with AppNexus using the OpenRTB API specification. For more information, see [Mobile OpenRTB Integration](../supply-partners/openrtb-specs.md).
