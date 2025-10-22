---
title: Auction Overview
description: In this article, learn about the auction procedure step by step.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Auction overview

This section takes you through an auction step by step. For a general overview of Xandr, from Xandr's tags to post-auction reports, please see [The Big Picture](the-big-picture.md).

## Step 1. The impression bus receives an ad call

On each ad call, the impression bus receives the following information:

- The inventory:
  - size, URL, placement
  - reserve price (optional)
- The user:
  - unique Xandr user ID
  - session recency, frequency, total impression clicks
  - publisher-supplied demographics (age, gender, etc)
  - user data segments previously stored by members and data providers

## Step 2. The impression bus reaches out to data providers

The impression bus, in real time, reaches out to all integrated to gather other relevant information about the user and the inventory source to pass along to the bidders. The data providers are given 10 ms to respond, at which point data is appended to the bid requests for those bidders who have contractual rights with the data providers to view their data.

## Step 3. The impression bus sends bid requests to bidders

The impression bus sends out a [bid request](outgoing-bid-request-to-bidders.md) to all bidders, including [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md). Bidders may opt out of certain impressions based on the inventory, see [Enhanced Bidder Profiles](enhanced-bidder-profiles.md). Within the bid request, each bidder is passed all relevant information about the user and inventory, as well as the publisher's advertiser exclusion profile. Each bidder is also passed all data within that bidder's reserved user cookie space.

## Step 4. Bidders submit CPM bids

The bidders use their real-time algorithms to analyze each bid request and produce CPM bids for each of their members. If a bidder is facilitating buys for multiple members, it will respond with the highest bid among all participating members. Along with this bid they submit a Xandr ID or third-party ID (when using codes) for a creative that has been previously registered with Xandr's API and approved by the inventory source.

> [!TIP]
> The impression bus will run all auctions in USD. Bidders and [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md) may submit bids in one of these [supported currencies](supported-currencies.md) and the impression bus will take the previous day's closing exchange rate to USD, perform the auction, and then convert the price paid on the auction back to the currency that was submitted by the bidder or [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md) and send the notify request (or populate the `${PRICE_PAID}` macro).

## Step 5. The impression bus chooses the highest eligible bid

When all participating bidders have returned their [Bid Response](incoming-bid-response-from-bidders.md) or the 150 ms timeout is reached, the impression bus chooses the highest bid with an approved creative. Note that Xandr runs a first price auction: the highest bidder pays the bid price (with some exceptions made for inventory that is ultimately decisioned by a third party ad `server). See [Price Reduction Mechanics](price-reduction-mechanics.md) for details.

The impression bus either:

- passes the ad (the winning creative) back to the user's browser (for non-conditional tags).
- passes the bid and the tag or URL (for the winning creative) back to the publisher's tag/adserver which will decide in real time whether to accept the bid.

> [!NOTE]
> Xandr does not allow bids greater than $999 CPM. Any bids over $999 CPM (or effective CPM for CPA/CPC bids) will be reduced to $999 CPM.

## Step 6. The impression bus notifies bidders of the auction results

The impression bus passes the results of the auction, win or lose, to each bidder in a [Notify Request](notify-request.md) for the bidder's internal reporting and real-time analytics needs. If the auction was initiated from a Preemptive tag, the winning bidder will be informed that the auction is pending the publisher's acceptance, and will be notified again should the publisher choose to serve the supplied ad.

## Related topics

- [Price Reduction Mechanics](price-reduction-mechanics.md)
- [Bidding Use Case with Fees](bidding-use-case-with-fees.md)
