---
title: Price Reduction Mechanics
description: In this article, learn about Price Reduction Mechanics and the Estimated Clear Price (ECP) mechanism.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Price reduction mechanics

With the Estimated Clear Price mechanism, the winning bidder may pay:

- A price equal to $0.01 more than the second-highest bid (a standard second-price auction)
- An Estimated Clear Price (the price at which the ad is likely to win, or "clear")
- The actual winning bid

As an example of why this mechanism is necessary, imagine Toyota bids $5 and MasterCard bids $3 for a particular impression. In a Xandr-only auction the winning bidder, Toyota, would usually pay $0.01 more than the second-highest bid, which is $3.01. However, in this case the publisher has chosen to pass on the highest Xandr bid to a second ad exchange. If the bid of $3 is passed on, it might lose to a $4 bid even though Toyota was willing to pay $5. If the $5 bid is entered into another exchange, it might beat a $4 bid.

## ECP solution

To solve this problem, Xandr created a new type of auction to determine the amount of the winning bid.

1. The ad call comes in to Xandr.

1. Xandr calculates an ECP which is an estimate of a bid that is likely to win the ad.

    > [!NOTE]
    > The ECP is determined by observing historical bids and their success or failure in the publisher's ad server. While a bid below this threshold may be submitted, the risk of losing the auction in the publisher's ad server will be much greater.

1. The ECP is automatically included in the bid request sent to bidders. Bidders can still bid whatever they want, above or below the ECP.

1. If the winner's bid is above the ECP, the bid price sent on to the next auction is either $0.01 more than the second-highest bid or the ECP, **whichever is higher.**

    > [!NOTE]
    > Xandr does NOT reduce the bid price sent on the next auction if that auction runs its own second-price auction.

1. If the winner's bid is below the ECP, the bid price is the winning bid (i.e. no price reduction).

## Example

The ECP is calculated to be $4.

- The two highest bids are $5 and $6: $5 is sent on
- The two highest bids are $3 and $5: $4 is sent on
- The two highest bids are $2 and $3: $3 is sent on

> [!NOTE]
> Bids within $0.0005 CPM are considered tied.
