---
title : The Big Picture
description : Learn about impression bus in this page.  
ms.date : 11/28/2023
---


# The big picture

## The Impression bus and tags

The impression bus is the heart of Xandr's
platform. It is a server cluster that processes ad requests, feeds data
to members, conducts auctions, returns ads to the publishers, keeps
track of billing and usage, returns auction-result data, and enforces
quality standards. At the ad call, the impression bus receives a unique
user ID and additional page information.

Even if the inventory is tagged with a third-party tag, all inventory is
associated with a unique TinyTag ID that maps to tag data stored server
side. If a seller uses Xandr tags on their
pages, once the tag is in place, all relevant details can be modified
without having to re-tag the page. Simply add or change information
about that tag within Xandr's platform.

With TinyTag and the Pixel Request, the impression bus will send your
bidder the appropriate user and page information.

## The Impression bus holds an auction

When an ad call from one of the Xandr tags or
from an Xandr supply partner hits the impression
bus, we review the content and send a bid request to the various bidders
on the Xandr platform. The bid request will
include the content categorization, page information, user information,
and possibly a reserve price and reserve creative. 

Data providers integrated on our platform recognize the user ID and can
input any information they may have on that specific ID and will pass
the user data to bidders that have the rights to that information. The
bidders then evaluate the ad call on behalf of their advertisers and
return a bid value to the impression bus. 

For a closer look at the auction process, please see the [Auction Overview](auction-overview.md).

> [!NOTE]
> Xandr does not allow bids greater than $999 CPM. Any bids over $999 CPM (or effective CPM for CPA/CPC bids) will be reduced to $999 CPM.

## Serving the impression

The impression is served in one of these ways:

- **Find highest bid and serve immediately:**
  Xandr's impression bus determines the highest
  bidder and will serve the winning bidder's creative as dictated in the
  bidder response.
- **Highest bid wins if it beats reserve price:** If a reserve price is
  passed via a Xandr ad tag, the impression bus
  passes this price as well as the other ad call information to all
  bidders.  Bidders respond with a bid value and creative ID, and the
  highest bid that beats the reserve price will serve its creative.  If
  no bid beats the reserve price, the impression bus will pass the ad
  call on to a third-party system.
- **Send highest bid to third party:** The ad call is directed to the
  Xandr impression bus first.  The impression
  bus holds an auction as usual among its bidders and then passes the
  highest bid on to a third-party system to decide how to fill the ad
  call. If the highest Xandr bid is chosen as
  the winner, then the ad call be passed back to
  Xandr where the impression will serve the
  winning bidder's creative.

## Auction postmortem

One of the main problems with working in a closed advertising ecosystem
is that it is difficult for bidders to understand why they won or lost
an impression. If you bid $2.00 for a car buyer on nytimes.com/autos and
consistently lose, what action should you take? Are you being outbid by
$0.05 or $5.00? If you are selling inventory, which user segments are
driving your CPMs? This crucial information will be passed to your
bidder via [Notify Request](notify-request.md) and the Reporting User
Interface.

Couple this with full reporting and API support, and you have all the
tools you need to make informed and powerful decisions for your clients.

## End results

- Optimized ad delivery
- Brand control and quality
- Full control over CPMs; publishers can decide whether or not to accept
  the winning bid
- Independent platform allowing deep integration with technologies,
  optimization engines, and bidders
- Increase the number of high-value users for your clients while
  decreasing the number of low-value users
