---
title: Deal Best Practices for Buyers
description: Learn about some best practices for buyers using the new deal functionality. This page also explains about deal delivery and deals with external sellers. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Deal best practices for buyers

This page provides some basic best practices for buyers using the new deal functionality.

## Getting started with deals

### Start slow

For buyers that are new to our deals feature, Microsoft Advertising recommends working with sellers you trust to develop a few test deals. Use and refine these test deals to learn what works best for you and your sellers before targeting a creating a lot of ad campaigns that target deals.

## Deal delivery

### Deal delivery expectations

- A deal does not guarantee delivery. Be prepared for low-reach deals.
- Avoid setting your end client's expectations about delivery on any specific deal. Low delivery should be expected to some extent. A deal contains a small slice of inventory. Add the fact that there may be other buyers competing for the deal, and low delivery is understandable.
- Targeting a deal guarantees you will be targeting a specific pool of inventory. Having a deal, even a private auction deal, does NOT guarantee you will win all of that inventory. Sellers generally expose deals to multiple buyers. Therefore, as with all other RTB, there are other buyers competing for the deal inventory.

### Targeting deals so that they deliver

- If you are not winning as much of the deal inventory as you would like, bid higher to beat the other buyers. Or include more deals in your targeting to create a larger pool of inventory.
- Avoid advanced targeting settings. These settings should only be used for targeting broad deals. For example, targeting a broad buyer-owned segment within a deal that covers a seller's entire network could produce some available impressions. For deals that contain a limited pool of inventory, applying additional targeting settings may limit delivery to zero.
- Targeting multiple deals that apply to the same inventory in a single line item or campaign is not recommended. When a single line item or campaign bids on an impression where two deals apply, the system will choose the deal with the lowest ID. You can not define which deal you would like to apply.
- When setting up your deal line item or campaign, the system will calculate a Suggested Minimum Bid. This is the minimum you must bid in order to participate in the auction. However, bidding this amount does not mean that you will win the auction.

  :::image type="content" source="media/sugg-min-bid.png" alt-text="Screenshot of Min Bid.":::

- Deal impressions face competition from other buyers. In order to win the impression, your bid needs to be both higher than the deal ask price, and higher than bids from other buyers.
- Deal line item or campaign setup is similar to non-deal setup. Often, you'll experience under-delivery due to budgeting, pacing, or other issues that are not related to the fact that you are targeting a deal.

### Identifying high performance deals

Target multiple deals within a single line item or campaign and then use [Buy-Side Reporting on Deals](buy-side-reporting-on-deals.md) to see which deals perform best. Then create a new line item or campaign to target the deals that work best.

## Deals with external sellers

### Rubicon REVV connect

- Each deal ID can only be associated with a single deal price. Enter one price when setting up a deal in REVV Connect. If multiple prices are entered, Microsoft Advertising will only map the deal to the highest possible price.
- Each deal ID can only be associated with a single buyer. Enter one buyer member when setting up a deal in REVV Connect. If multiple members are entered, Microsoft Advertising will only map the deal to the first buyer member.
- Deals with a price in a foreign currency may drift from the agreed-upon price as the exchange rate fluctuates. On the day the deal is synchronized with Microsoft Advertising, Rubicon converts the deal price to USD. Rubicon does not refresh the deal price with updated daily exchange rates. It will remain static and may drift from the agreed-upon price in the foreign currency.

### PubMatic

- Each deal ID can only be associated with a single buyer. Enter one buyer member when setting up a deal in PubMatic. If multiple members are entered, Microsoft Advertising will only map the deal to the first buyer member.
