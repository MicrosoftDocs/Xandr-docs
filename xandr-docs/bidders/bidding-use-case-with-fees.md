---
title: Bidding Use Case with Fees
description: In this article, learn about bidding use case with fees and the stages of the bidding process.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder - Bidding use case with fees

> [!NOTE]
> Xandr fees and auction mechanics were designed so that our members can bid what they think an impression is worth and still get the best deal. When a member wins an impression, they either pay the bid price or less, including any auction fees.

To understand the fees associated with Xandr's platform, see this example of a basic auction scenario. For this example, all steps are rounded to two digits after the decimal. In an actual auction, six digits after the decimal are used.

In this example, there are two fees:  

1. A Xandr fee of 5% of the final price paid for an impression.
1. A fee charged by the bidder who transacts media on behalf of an advertiser.

## Stage 1: Impression bus is contacted

1. Internet user Mark Smith visits doctorwhofans.com.
1. A TinyTag on the page tells Mark's browser to ping Xandr's impression bus.

## Stage 2: Owner phase

1. The impression bus sees in its database that doctorwhofans.com is owned by Member 12, and that Member 12 is associated with Bidder 14.

   > [!NOTE]
   > **Why would a seller work with a bidder?**
   >
   > Buyers, sellers, networks, and other entities can overlap each other; perhaps in this case the owner is also a buyer. Or perhaps the owner chose to work with a bidder to enhance the features of Xandr's platform. For example, when a seller is associated with a bidder, they get pinged first before a general Bid Request goes out to all bidders. Sellers can then set a reserve price dynamically, when they have more data about the user.

1. The impression bus makes a Bid Request to Bidder 14 only. Bidder 14 receives third-party data within the Bid Request, and according to preset logic decides to set the reserve price to $2 via the Bid Response.

## Stage 3: Bidding phase

1. The impression bus has calculated the [Estimated Clear Price](price-reduction-mechanics.md) as $3 based on historical data.
1. The Bid Request now goes out to all listening bidders with the revised reserve price and the Estimated Clear Price.
1. Member 1 (via Bidder 7) calculates a $6 bid. Bidder 7 charges a 10% Bidder Fee, so Bidder 7 submits $5.40 to the impression bus.

    > [!NOTE]
    > **Bidder Fees**  
    > Bidder fees are negotiated between bidders and members - they do not go through Xandr.

1. Member 2 (via Bidder 12) calculates a $5 bid. Bidder 12 charges a 5% Bidder Fee, so Bidder 12 submits $4.75 to the impression bus.

## Stage 4: Auction winner and price are determined

1. Because Xandr charges a 5% fee for all buys at the end of the auction, the `"seller_revenue"` price must be calculated at this stage for comparison to the reserve price. The impression bus subtracts 5% from all bids to create "net bids". Net bids are $5.13 and $4.51.

   > [!NOTE]
   > **Net Bids**
   >  
   > The net bid is a calculation of seller revenue, or how much money the seller would actually receive if this bid wins. This is so that bids can be properly compared to the seller's reserve price and to each other. To calculate the net bid, all Xandr fees are subtracted out.

1. The auction winner is determined by ranking the net bids. Bidder 7's $5.13 net bid is the best bid and Bidder 7 wins on behalf of Member 1. The price Member 1 pays is then reduced to $4.52: $0.01 more than the second price of $4.51.

    > [!NOTE]
    > The price-reduction process is different if the winning bid is passed on to a second auction. For more details, see [Price Reduction Mechanics](price-reduction-mechanics md).

1. At this point all Xandr-related fees (5% of the winning bid price) are added. The price-reduced bid of $4.52 becomes a `"buyer_buys"` price of $4.76. The seller will receive `"seller_revenue"` of $4.52. Xandr receives the difference of $.24.

    > [!NOTE]
    >
    > - In this simple scenario, both the first and second net bids were higher than the reserve and Estimated Clear Prices; thus the reserve prices and ECPs are irrelevant.
    > - The only Xandr fee in this example is the 5% fee. If a Member is using [Xandr's Digital Platform UI](xandr-s-digital-platform-ui.md), that fee will be included in step 9 above.
    >
    > **Benefits of Price Reduction**  
    > Because of the price reduction auction model, the winning bidder pays less than their initial bid but more than the reduced bid. Bidders are also encouraged to bid what they actually think the impression is worth rather than try to bid incrementally higher than a competitor.

## Bids, prices, and fees for this example

| List of bids and prices | Fees |
|---|---|
| Reserve Price | 2|
| Estimated Clear Price | 3 |
| Initial Member Bids | 6, 5 |
| Bid Response Bids | 5.40, 4.75 |
| Net Bids | 5.13, 4.51 |
| Winning Bid | 5.13 |
| Price Reduced Bid (same as Seller Revenue) | 4.52 |
| Xandr Fee | 0.24 |
| Buyer Pays | 4.76 |
