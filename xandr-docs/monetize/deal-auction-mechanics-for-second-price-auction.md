---
title: Deal Auction Mechanics for Second-Price Auction
description: Learn how a deal auction can be open or private. This page gives an overview on open and private auctions along with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Deal auction mechanics for second-price auction

A deal auction can be **open** or **private**, depending on how the seller defined the deal. This page explains how these different types of auctions work and provides examples.

> [!NOTE]
> The explanations on this page apply only to deals with Microsoft Monetize sellers, not to deals with external supply partners. For information about an external supply partner's deal types or auction mechanics, contact the external supply partner directly.

## Open auctions

When a piece of inventory included in an "open auction" deal comes up for auction, buyers targeting the deal, and buyers targeting the inventory via other means, compete for the impression.

- If a buyer targeting the deal submits the highest bid and the bid clears the deal's ask price, that buyer wins the auction, paying either the second-highest bid (plus one cent) or the ask price, whichever is higher. If the deal does not have an ask price, the buyer pays either the second-highest bid (plus one cent) or ECP, whichever is higher.
- If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid (plus one cent) or ECP, whichever is higher.

> [!IMPORTANT]
> **ECP** stands for Estimated Clear Price, which is an estimate of the bid price that is likely to win the impression from a given publisher based on observing historical bids.
> [!NOTE]
> Deal Ask Prices vs. Reserve Prices
>
> - If the seller has set a reserve price on their RTB inventory, the deal ask price will take priority over the reserve price.
> - A default creative reserve price will always take priority over the placement reserve price.
> - A dynamic floor will always take priority over the placement and default creative reserve price.

## Examples for open auctions

### Deal bid wins

:::image type="content" source="media/open-auction-deal-bid-wins.png" alt-text="Screenshot of Deal bid wins.":::

### Non-Deal bid wins

:::image type="content" source="media/open-auction-non-deal-bid-wins.png" alt-text="Screenshot of Non-Deal bid wins.":::

### Non-Deal bid wins

:::image type="content" source="media/open-auction-non-deal-bid-wins-b.png" alt-text="Diagram of Non-Deal bid wins.":::

> [!IMPORTANT]
> **Why does this example have two floors? And why does the non-deal bid win?**
>
> In the example above, each of the deal bids has a different floor applied to it. This can happen when the seller uses floor rule demand filtering to target the floor to a specific buyer, brand, or offer category.
>
> The highest non-deal bid wins because:
>
> - The deal does not have a deal ask price, and
> - Neither of the deal bids met the floor targeted to their bids

## Private auctions

When a piece of inventory included in a "private auction" deal comes up for auction, buyers targeting the private deal compete for the impression first. Additionally, private deals can be given a numeric deal priority. Deals with a higher priority will always win over lower priority deals.

If none of the private deal buyers win, the auction is opened to buyers targeting the inventory via other means.

- If a buyer targeting the deal submits a bid higher than the deal's ask price and higher than any other private auction bids, that buyer wins the auction, paying either second-highest bid (plus one cent) from the private auction or the ask price, whichever is higher. If the deal does not have an ask price, the buyer pays either the second-highest bid (plus one cent) or ECP, whichever is higher.
- If no private auction bids clear their ask prices, the highest bid in the open auction wins, paying either the second-highest bid (plus one cent) from the open auction or ECP, whichever is higher.

## Examples for private auctions

### Deal bid wins in private auction (no open auction held)

:::image type="content" source="media/private-auction-deal-bid-wins.png" alt-text="Screenshot of deal bid wins in private auction.":::

### Higher priority deal bid wins in private auction (no open auction held)

:::image type="content" source="media/private-auction-higher-priority-wins.png" alt-text="Diagram of higher priority deal bid winning in private auction.":::

### Non-Deal bid wins in open auction (no private auction winner)

:::image type="content" source="media/private-auction-non-deal-bid-wins.png" alt-text="Screenshot of Non-Deal bid winning in open auction.":::

## Deal prices and yield management rules

Both a deal and a YM rule can apply to the same piece of inventory. This section explains which rules are considered when that piece of inventory comes up for auction.

### Deal pricing and floors

If you have set a price for your deal, it will override other pricing mechanisms including floor rules. In other words, deal prices take priority over floor prices.

- If you have a deal with no ask price, that is considered a deal with no floor. Your existing floor rules apply to the deal inventory.

- If you have a deal with an ask price of 0, that is considered a deal with a floor of 0. The deal floor of 0 takes priority over any YM floors you have.

- A YM floor will always take priority over the placement and default creative reserve price.

- If the YM floor has Reserve Price Override disabled, then the YM floor will take priority over a dynamic floor.

- If the YM floor has Reserve Price Override enabled and the dynamic floor is less than the YM floor, then the YM floor will take priority over a dynamic floor.

- If the YM floor has Reserve Price Override enabled and the dynamic floor is greater than the YM floor, then the dynamic floor will take priority over a YM floor.

### Deal bid meets deal floor and wins

:::image type="content" source="media/deal-floor-vs-ymfloor.png" alt-text="Screenshot of deal bid meets deal floor and wins.":::

## Fixed price deals

If you select a **Fixed Price** auction, you will need to enter an ask price. Any buyer who bids above this value (plus relevant fees) will be eligible to bid on the deal. The winning buyer is responsible for the fixed price plus fees. A bid is only eligible if it is above the applicable price for the deal. Any bids below the ask price will be considered ineligible for the deal and the auction. IDs on fixed price deals are ranked according to the deal's ask price (minus relevant fees).

### Deal pricing and biases

Yield management biases will still be applied to deal bids, even if you have set a price for your deal.

## Related topics

- [Buying Deals](buying-deals.md)
- [Selling Deals](selling-deals.md)
- [Create a Floor Rule](create-a-floor-rule.md)
