---
title: Bidder - Auction Overview
description: This page is an overview on how Impression bus holds an auction when an ad call from one of the Xandr tags or from an Xandr supply partner hits the impression bus. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder - Auction overview

This section provides a general overview of Xandr, from Xandr's tags to post-auction reports.

## Impression bus and tags

The impression bus is the heart of Xandr's platform. It is a server cluster that processes ad requests, feeds data to members, conducts auctions, returns ads to the publishers, keeps track of billing and usage, returns auction-result data, and enforces quality standards. At the ad call, the impression bus receives a unique user ID and additional page information.

Even if the inventory is tagged with a third-party tag, all inventory is associated with a unique TinyTag ID that maps to tag data stored server side. If a seller uses Xandr tags on their pages, once the tag is in place, all relevant details can be modified without having to re-tag the page. Simply add or change information about that tag within Xandr's platform.

With TinyTag and the Pixel Request, the impression bus sends your bidder the appropriate user and page information.

## Impression bus holds an auction

When an ad call from one of the Xandr tags or from an Xandr supply partner hits the impression bus, we review the content and send a bid request to the various bidders on the Xandr platform. The bid request includes the content categorization, page information, user information, and possibly a reserve price and reserve creative.

Data providers integrated on our platform recognize the user ID and can input any information they may have on that specific ID. They pass the user data to bidders that have the rights to that information. The bidders then evaluate the ad call on behalf of their advertisers and return a bid value to the impression bus.

For a closer look at the auction process, see [Auction - Detailed overview](#auction---detailed-overview).

> [!NOTE]
> Xandr does not allow bids greater than $999 CPM. Any bids over $999 CPM (or effective CPM for CPA/CPC bids) are reduced to $999 CPM.

## Serving the impression

The impression is served in one of these ways:

- **Find highest bid and serve immediately**: Xandr's impression bus determines the highest bidder and serves the winning bidder's creative as dictated in the bidder response.
- **Highest bid wins if it beats reserve price**: If a reserve price is passed via a Xandr ad tag, the impression bus passes this price as well as the other ad call information to all bidders. Bidders respond with a bid value and creative ID, and the highest bid that beats the reserve price serves its creative. If no bid beats the reserve price, the impression bus passes the ad call on to a third-party system.
- **Send highest bid to third party**: The ad call is directed to the Xandr impression bus first. The impression bus holds an auction as usual among its bidders and then passes the highest bid on to a third-party system to decide how to fill the ad call. If the highest Xandr bid is chosen as the winner, then the ad call is passed back to Xandr where the impression serves the winning bidder's creative.

## Post-auction analysis

One of the main problems with working in a closed advertising ecosyste is that it is difficult for bidders to understand why they won or lost an impression. If you bid $2.00 for a car buyer on nytimes.com/autos and consistently lose, what action should you take? Are you being outbid by $0.05 or $5.00? If you are selling inventory, which user segments are driving your CPMs? This crucial information is passed to your bidder via [Notify Request](notify-request.md) and the Reporting User Interface.

Couple this with full reporting and API support, and you have all the tools you need to make informed and powerful decisions for your clients.

## End results

- Optimized ad delivery
- Brand control and quality
- Full control over CPMs; publishers can decide whether or not to accept the winning bid
- Independent platform allowing deep integration with technologies, optimization engines, and bidders
- Increase the number of high-value users for your clients while decreasing the number of low-value users

## Auction - Detailed overview

This section takes you through an auction step by step.

### Step 1. Impression bus receives an ad call

On each ad call, the impression bus receives the following information:

- The inventory:
  - size, URL, placement
  - reserve price (optional)
- The user:
  - unique Xandr user ID
  - session recency, frequency, total impression clicks
  - publisher-supplied demographics (age, gender, etc)
  - user data segments previously stored by members and data providers

### Step 2. Impression bus reaches out to data providers

The impression bus, in real time, reaches out to all integrated to gather other relevant information about the user and the inventory source to pass along to the bidders. The data providers are given 10 ms to respond, at which point data is appended to the bid requests for those bidders who have contractual rights with the data providers to view their data.

### Step 3. Impression bus sends bid requests to bidders

The impression bus sends out a [bid request](outgoing-bid-request-to-bidders.md) to all bidders, including [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md). Bidders may opt out of certain impressions based on the inventory, see [Enhanced Bidder Profiles](enhanced-bidder-profiles.md). Within the bid request, each bidder is passed all relevant information about the user and inventory, as well as the publisher's advertiser exclusion profile. Each bidder is also passed all data within that bidder's reserved user cookie space.

### Step 4. Bidders submit CPM bids

The bidders use their real-time algorithms to analyze each bid request and produce CPM bids for each of their members. If a bidder is facilitating buys for multiple members, it responds with the highest bid among all participating members. Along with this bid they submit a Xandr ID or third-party ID (when using codes) for a creative that has been previously registered with Xandr's API and approved by the inventory source.

> [!TIP]
> The impression bus runs all auctions in USD. Bidders and [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md) may submit bids in one of these [supported currencies](supported-currencies.md) and the impression bus takes the previous day's closing exchange rate to USD, perform the auction, and then convert the price paid on the auction back to the currency that was submitted by the bidder or [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md) and send the notify request (or populate the `${PRICE_PAID}` macro).

### Step 5. Impression bus chooses the highest eligible bid

When all participating bidders have returned their [Bid Response](incoming-bid-response-from-bidders.md) or the 150 ms timeout is reached, the impression bus chooses the highest bid with an approved creative. Note that Xandr runs a first price auction: the highest bidder pays the bid price (with some exceptions made for inventory that is ultimately decisioned by a third party ad `server). See [Price Reduction Mechanics](price-reduction-mechanics.md) for details.

The impression bus either:

- passes the ad (the winning creative) back to the user's browser (for non-conditional tags).
- passes the bid and the tag or URL (for the winning creative) back to the publisher's tag/adserver which decides in real time whether to accept the bid.

> [!NOTE]
> Xandr does not allow bids greater than $999 CPM. Any bids over $999 CPM (or effective CPM for CPA/CPC bids) are reduced to $999 CPM.

### Step 6. Impression bus notifies bidders of the auction results

The impression bus passes the results of the auction, win or lose, to each bidder in a [Notify Request](notify-request.md) for the bidder's internal reporting and real-time analytics needs. If the auction was initiated from a Preemptive tag, the winning bidder is informed that the auction is pending the publisher's acceptance, and is notified again should the publisher choose to serve the supplied ad.

## Related topics

- [Price Reduction Mechanics](price-reduction-mechanics.md)
- [Bidding Use Case with Fees](bidding-use-case-with-fees.md)
