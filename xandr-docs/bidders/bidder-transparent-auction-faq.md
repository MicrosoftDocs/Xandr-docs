---
title: Bidder Transparent Auction FAQ
description: Explore answers to FAQs about the bidder transparent auction, gaining a clear understanding of the auction type you're engaging in.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder transparent auction FAQ

Xandr aims to provide full transparency for bidders to help ensure each bidder knows the auction type they're participating in. This page provides answers to some of the most common questions around transparent auctions.

## What are transparent auctions?

Transparent auctions are a way of letting bidders know what type of auction they're participating in so they can make more informed decisions on the amounts they bid.

In the past, auctions were always first price (pay what you bid) or second price (winning bid is price-reduced to achieve a fairer market price). In addition, some auctions included soft floors, which use a floor price to achieve a combination of first and second price in a single auction. While the type of auction being held could be different depending on the situation, that information was invisible to bidders. Bidders had no way of knowing which type of auction they were bidding into.

With transparent auctions, bidders now receive an auction type (see below) in the bid request. This auction type tells the bidder which type of auction is being held.

## What auction types are sent in the bid requests?

There are two auction types: impression (at) and deal (pmp.deal.at). There are three possible values for auction type:

| Value | Description |
|:---|:---|
| 1 | - First price auction<br> &nbsp;&nbsp;- or -<br> - Xandr is not confident that the auction is a second price auction. Typically this means soft floors are in place, which produce some first-price and some second-price auctions. |
| 2 | - Second price auction<br>&nbsp;&nbsp;- and -<br> - There are no soft floors, non-transparent price reductions, or custom auction types. There may be static or dynamic (pre-bid) hard floors. |
| 3 | *Deals (pmp.deal.at) Only*<br>Fixed price. The bid floor is the agreed-upon deal price. |

Most bid requests have auction type = 1 (`"at": 1`). For example:

```
{
    "id": "43212345678987",
    "at": 1,
    "imp": [{
        "secure": 0,
        "tagid": "443322",
        "video": {
            "playbackmethod": [
                2
            ],
            "mimes": [
                "video/mp4",
                "application/javascript",
                "video/x-flv",
                "application/x-shockwave-flash"
            ]....
```

## Who determines if the auction is first price or second price?

Xandr determines the auction type (as shown in the table under "[How does Xandr determine the auction types?](#how-does-xandr-determine-the-auction-types)") and sends the auction type in the bid request. We do not use auction types passed to us.

Transparent auction has not changed the actual behavior of the auction; only the determination as to which auction type is sent in the bid request is different than is was previously.

## Do you pass the auction type (at) flag on all open auction and PMP deals?

Yes. Auction type is always passed in the bid request.

## Will Xandr ultimately decide winning/clearing price? Are there any modifications made?

Xandr determines the highest bid that gets sent to the publisher. Buyer fees are taken into account when sending the final bid.

## How does Xandr determine the auction types?

| Auction Type | Xandr Deal Auction Type Config on Deal ID | Bid Request Auction Type (`at`) | Deal Object Auction Type (`pmp.deal.at`) | Result for Buyer | OptimalBiddingRecommendation |
|---|---|---|---|---|---|
| **First-Price Auction:**<br> - Winning bid = price paid.<br> - No soft floors.<br> - Hard floors are allowed, including dynamic.<br> - Header bidding auctions are always first price. | standard | 1 | 1 |  - Bid ranked based on bid<br> - Pay what you bid | Shade |
| **Trusted Second Price Auction:**<br> - Winning bid always price reduced.<br> - No soft floors, buyer-friendly.<br> - Hard floors are allowed, including dynamic. | standard | 2 | 2 | - Bid ranked based on bid<br>- Pay second price or Deal Ask Price | Don't Shade |
| **Trusted Second Price Auction:**<br> - Winning bid always price reduced.<br> - No soft floors, buyer-friendly.<br> - Hard floors are allowed, including dynamic. | fixed | 2 | 3 | - Bid ranked by Deal Ask Price<br> - Pay Deal Ask Price | Bid more than Ask |
| **Soft Floor / Legacy Second Price Auction:**<br> - Soft floors, seller-friendly.<br> - Auction logic sometimes first-prices.<br> - Buyers, ECP soft floors, hard floors allowed, including dynamic. | standard | 1 | 1 | - Bid ranked based on bid<br> - Pay first price or second price, Deal Ask Price depending | Shade |
| **Soft Floor / Legacy Second Price Auction:**<br> - Soft floors, seller-friendly.<br> - Auction logic sometimes first-prices.<br> - Buyers, ECP soft floors, hard floors allowed, including dynamic. | fixed | 1 | 3 | - Bid ranked by Deal Ask Price<br> - Pay Deal Ask Price | Bid more than Ask |
| **External Auction (SSPs):**<br>Xandr doesn't know the rules, we assume soft floors and first price. | standard | 1 | 1 | - Bid ranked based on bid<br> - Pay what you bid | Shade |

## What actions do I need to take as a bidder?

- Continue to listen to all auction types in RTB and deals.
- Apply bid shading to first- price auctions as needed.
- Engage with us if you have questions.

## Can a seller be both first and second price?

A single seller cannot be both first and second price on a single impression, but the different publishers associated with a seller can have first price or second price auctions.

## Can a domain be both first and second price?

Yes, across many auctions. (Not on a single impression.) Because of this, you'll need to listen to the auction type signal in real-time rather than infer post-auction.

## How do I identify the type of inventory?

There are two signals currently available on the OpenRTB [bid request](outgoing-bid-request-to-bidders.md) that you can use to identify the type of inventory: `publisher_integration.is_header` and `source.fd`.

`is_header`:

- `0`: This is not a header bidding integration.
- `1`: Integration into a wrapper.

`fd` :

Entity responsible for the final impression sale decision, where:

- `0`: Exchange (default). Xandr holds the final auction.
- `1`: Upstream source. Bid is passed along to header bidding auction or external supply.

The following chart outines how `is_header` and `fd` work together with the auction type (`at`) to identify the type of inventory:

| Inventory Type | `at` | `is_header` | `fd` |
|:---|:---|:---|:---|
| Header | 1 | 1 | 1 |
| Xandr's exchange with soft floor | 1 | 0 | 0 |
| External | 1 | 0 | 1 |

## Why does using a soft floor often result in a first price being sent even though the auction is a second-price auction?

In a second-price auction, if no floors have been set the winning bid is price-reduced to the second-highest bid (plus $0.01). However, when a soft floor has been set, the winning bid is one of the following:

- If the bid is *above* the soft floor: The greater of the second-highest bid plus $0.01 or the soft floor.
- If the bid is *below* the soft floor: The winning bid (with no price reduction).

In the latter case, the second-price auction appears to function as a first-price auction: the highest bid wins that auction and is not price-reduced.

## Where do I go if I need help?

Contact your Xandr representative or [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) for assistance.
