---
title: How Auctions Work for Sellers
description: Learn how auctions run when there are different types of demand involved.  
ms.date: 10/28/2023
---


# How auctions work for sellers

> [!NOTE]
> This topic relates to Mediation, which is available only to Microsoft Monetize Ad Server customers.

In Microsoft Monetize Ad Server, you can run
auctions for your inventory across different demand sources. In order to
sell your inventory effectively across direct, RTB, and mediated demand,
you need to understand how auctions work when these different demand
sources are involved.

This page will walk through a few examples. Our goal is to give you a
feel for how auctions run when there are different types of demand
involved.

> [!NOTE]
> Keep in mind that these examples are simplified for learning purposes. Real auctions have more complex interactions and edge cases than we can easily describe here.

## Example one - Mediated bid wins with highest bid

In this example, we will run an auction with three bids: a mediated bid,
a direct bid, and a third-party bid.

The diagram below shows all of the bids in our auction. We have created
a mediated bid of $2.00 for CoolAds, a mobile ad network. This bid is
higher than the bids from direct or RTB buyers, so CoolAds will "win"
the impression (really, the first shot at the impression). A mediation
ad call is made to the CoolAds server to get an ad.

It's important to understand that even though the CoolAds "bid" is
$2.00, CoolAds may not end up paying that amount. We will only get an
average CPM from CoolAds at the end of the day when we query their
system for the day's aggregate stats. For example, we may query the
CoolAds server and discover that they only paid $1.00 CPM on average.
The $2.00 CPM bid you set is only used for the auction ranking.

> [!NOTE]
> **Keep mediated bids up to date**: It's **very important** to keep mediated bids up to date to reflect the actual bids you're seeing from a mediated ad network. Up-to-date bids are the only way that we can run an effective auction. Out-of-date bids can have a **big** negative impact on monetization.

:::image type="content" source="media/ssp-auction-example-a.png" alt-text="Screenshot of SSP .":::

Because CoolAds "won" the first place in the initial ranking of the
auction based on your $2.00 bid setting, and then returned a creative,
they are the winners of this auction (marked in green in the diagram).
Their creative is served, and you will eventually get paid whatever they
really bid.

For instructions on creating a mediated bid, see [Mediation Bids](mediation-bids.md).

## Example Two - Direct buyer wins with second highest bid

Now let's run that same auction again. This time the mediation call to
CoolAds does not return an ad. Therefore, we simply accept the next
highest bid in the auction: the $1.75 CPM bid from our direct advertiser
deal. The auction ends and the direct advertiser is declared the winner
(shown in green). We receive $1.75 CPM and show the ad.

:::image type="content" source="media/ssp-auction-example-b.png" alt-text="Diagram of SSP .":::

## Example Three - Direct buyer wins with third highest bid

In the third example, we run an auction that's a lot like the first two.
Like before, we have created a $2.00 bid for CoolAds, and they get the
first chance to purchase the impression. The mediation call to CoolAds
does not return an ad. The second-highest bid is from an RTB buyer, for
$1.75.

Unfortunately, the brand of the creative that RTB buyer wants to serve
is banned in your ad quality settings. Therefore, the auction goes to
the third-highest bidder, a direct advertiser. The direct advertiser
wins the auction with a bid of $1.25. We receive $1.25 and show the ad.

:::image type="content" source="media/ssp-auction-example-c.png" alt-text="Diagram of SSP 3 .":::

## Related topics

- [Mediation Bids](mediation-bids.md)
- [Mediation Networks](mediation-networks.md)