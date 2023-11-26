---
title: Bidders - Deal Auction Mechanics
description: The article outlines the deal auction mechanism in digital advertising, focusing on scenarios where inventory in an "open auction" deal is up for bidding. The mechanism involves a dynamic process where bids determine the winning advertiser for a given advertising space.
ms.date: 10/28/2023
---
# Bidders - Deal auction mechanics

> [!NOTE]
> This documentation is based on first-price auction. If you're still using second-price auction, then [Deal Auction Mechanics for Second Price Auction](../monetize/deal-auction-mechanics-for-second-price-auction.md).

A deal auction can be **open** or **private**, depending on how the seller defined the deal. This page explains how these different types of auctions work and provides examples.

> [!NOTE]
> The explanations on this page apply only to deals with Microsoft Monetize sellers, not to deals with external supply partners. For information about an external supply partner's deal types or auction mechanics, contact the external supply partner directly.

## Open auctions

When a piece of inventory included in an "open auction" deal comes up for auction, buyers targeting the deal, and buyers targeting the
inventory via other means, compete for the impression.

- If a buyer targeting the deal submits the highest bid and the bid clears the deal's ask price, that buyer wins the auction, paying the bid price.
- If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying the bid price.

> [!NOTE]
> Deal Ask Prices vs. Reserve Prices
>
> - If the seller has set a reserve price on their RTB inventory, the deal ask price will take priority over the reserve price.
> - A default creative reserve price will always take priority over the placement reserve price.
> - A dynamic floor will always take priority over the placement and default creative reserve price.

## Examples (for successful deal bids and non-deal bids)

**Deal bid wins**

:::image type="content" source="media/open-auction-deal-wins-fp.png" alt-text="The screenshot that provides an explanation of Deal Bid Wins":::

**Case 1: non-deal bid wins**

:::image type="content" source="media/open-auction-non-deal-wins-fp.png" alt-text="The screenshot that provides the details of non-Deal Bid Wins":::

**Case 2: non-deal bid wins**

:::image type="content" source="media/open-auction-non-deal-wins-fp-b.png" alt-text="The screenshot that provides an explanation of non-Deal Bid Wins":::

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

- If a buyer targeting the deal submits a bid higher than the deal's ask  price and higher than any other private auction bids, that buyer wins the auction, paying the bid price.
- If no private auction bids clear their ask prices, the highest bid in the open auction wins, paying the bid price.

## Examples (for deal bid wins in private auction)

**Deal bid wins in private auction (no open auction held)**

:::image type="content" source="media/private-auction-deal-wins-fp.png" alt-text="The screenshot that explains the process of Private Auction Deal bid Wins when no open auctionsa are held":::

**Higher priority deal bid wins in private auction (no open auction held)**

:::image type="content" source="media/private-auction-high-priority-wins-fp.png" alt-text="The screenshot that illustrates how higher priority deal bids secure wins in private auctions without open auctions.":::

**Non-deal bid wins in open auction (no private auction winner)**

:::image type="content" source="media/private-auction-non-deal-bid-wins-fp.png" alt-text="The screenshot that illustrates how higher priority deal bids secure wins in open auctions.":::

## Deal prices and yield management rules

Both a deal and a YM rule can apply to the same piece of inventory. This section explains which rules are considered when that piece of inventory comes up for auction.

## Deal pricing and floors

If you have set a price for your deal, it will override other pricing mechanisms including floor rules. In other words, deal prices take
priority over floor prices.

- If you have a deal with no ask price, that is considered a deal with no floor. Your existing floor rules apply to the deal inventory.
- If you have a deal with an ask price of 0, that is considered a deal with a floor of 0. The deal floor of 0 takes priority over any YM
  floors you have.
- A YM floor will always take priority over the placement and default creative reserve price.
- If the YM floor has Reserve Price Override disabled, then the YM floor will take priority over a dynamic floor.
- If the YM floor has Reserve Price Override enabled and the dynamic floor is less than the YM floor, then the YM floor will take priority
  over a dynamic floor.
- If the YM floor has Reserve Price Override enabled and the dynamic floor is greater than the YM floor, then the dynamic floor will take
  priority over a YM floor.

### Deal bid meets deal floor and wins

:::image type="content" source="media/deal-bid-ym-floors-fp.png" alt-text="The screenshot that demonstrates the meeting of Deal Bid and Deal Floor, resulting in a successful win.":::

## Fixed price deals

If you select a **Fixed Price** auction, you will need to enter an ask price. Any buyer who bids above this value (plus relevant fees) will be eligible to bid on the deal. The winning buyer is responsible for the fixed price plus fees. A bid is only eligible if it is above the applicable price for the deal. Any bids below the ask price will be considered ineligible for the deal and the auction. IDs on fixed price deals are ranked according to the deal's ask price (minus relevant fees).

:::image type="content" source="media/winners-pays-deal-ask-price.png" alt-text="The screenshot explains that in a Fixed Price auction, bids above the ask price (plus fees) are eligible, and the winning bid covers both the fixed price and fees, whereas bids below the ask price are ineligible. l":::

### Deal pricing and biases

Yield management biases will still be applied to deal bids, even if you have set a price for your deal.

## Related topic

- [Buying Deals](../monetize/buying-deals.md)
- [Selling Deals](../monetize/selling-deals.md)
- [Create a Floor Rule](../monetize/create-a-floor-rule.md)
