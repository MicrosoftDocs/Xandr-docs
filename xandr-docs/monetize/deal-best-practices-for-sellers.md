---
title: Deal Best Practices for Sellers
description: This page gives an overview on some basic best practices for sellers using deals. This page covers when you should create a deal, when you should avoid creating a deal and setting up a deal.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Deal best practices for sellers

This page provides some basic best practices for sellers using deals.

## Getting started with deals

### Start slowly

For sellers that are new to our deals feature, we recommend creating a few test deals with buyers you trust. Use and refine these test deals to learn what works best for you and your buyers before putting a lot of deals out in the market.

### When to create a deal

- Create a deal to provide a buyer with special privileges.
- Create a deal to sell special access to premium inventory.
- Create a deal to sell inventory in bulk for discounted rates.

### When NOT to create a deal

Sometimes, your goal can be achieved with other tools in Monetize rather than a deal.

- Don't use a deal to try to capture every impression coming from a buyer.
- Don't use a deal to maximize pricing or revenue without the buyer's involvement.
- Don't create a deal without the buyer's approval.
- The buyer's contact receives an email every time you create a new deal. Overwhelming the buyer with too many deals might lead them to disregard your deal proposals. Reach out to the buyer with the list of deals you have to offer and let the buyer choose what works for them. Or ask the buyer to propose a deal that will meet their needs. This will ensure that both you and the buyer are satisfied with the deal you create.
- Buyers expect a deal to be something out of the ordinary in terms of delivery or performance. Keep that in mind when creating deals
- Don't create a deal for the same inventory the buyer can get via RTB. For example, creating a deal for an exposed custom category with a price that is the same or higher than your usual reserve price for the same inventory. The buyer will realize they can get the same inventory for an equal or better price without targeting the deal you provided. This will lead the buyer to no longer trust your deals.

## Deal setup

### Efficient deal management

- We recommend assigning one person to oversee all deals. This will help you to:
  - prevent excessive deal overlap and make sure private deals do not compete often
  - maintain the integrity of your pricing structure
  - help buyers with deal troubleshooting
- In general, we recommend creating deals that run indefinitely (no deal end date). End dates can be used for seasonal or time-sensitive type deals such as a Cyber Monday special.

### Setting deal pricing

Consider the right pricing for each deal to ensure maximum revenue while providing value to your buyers.

- Create a deal with an ask price higher than the usual market price when your deal provides additional value to the buyer. For example, a deal where you provide extra targeting access privileges or a deal where you provide first-party publisher data. In general, the more granular the deal the higher the ask price should be.
- Create a deal with an ask price lower than the usual market price when your deal is rewarding the buyer for adding value. For example, a deal where the buyer agrees to a spend goal or a deal created for strategic relationship purposes to reward or entice the buyer.
  
  > [!NOTE]
  > For deals where the buyer agrees to a spend goal in exchange for lower pricing, you can run reports to check the buyer's pace toward the goal.

- Create a deal with no ask price when you are using a deal strictly to classify and differentiate inventory. For example, a deal where you group your inventory into channels or verticals to expose them to buyers. Since buyers on external platforms such as Doubleclick or Mediamath can not see content categories or placement IDs, this is a good way to allow external buyers to target a specific pool of your inventory.

### Selecting an open or private auction

- We recommend creating open auction deals as often as possible to maintain market competition. An open auction is part of the regular RTB auction where the buyer competes with the larger pool of RTB buyers. Open auctions are used to easily allow the buyer to target the deal inventory without interfering with the pricing. For examples of how an open auction works, see [Deal Auction Mechanics](deal-auction-mechanics.md).
- We recommend using private auctions conservatively to maintain market competition and avoid overlapping private auction deals. In a private auction, the buyer will only compete with other buyers who have a private auction deal for the impression. If used conservatively, private auctions can command higher prices from buyers who will view the privilege as preferred treatment. For examples of how a private auction works, see [Deal Auction Mechanics](deal-auction-mechanics.md).
- In a private auction, a buyer will encounter no competition only if it can be definitively confirmed that no other overlapping private auction deals are in place for other buyers. If this cannot be guaranteed, it is essential to establish clear expectations: participation in a private auction does not ensure a winning bid. To secure the impression, a buyer must outbid any competing participants in other private auction deals. If prioritization of a specific buyer is required, this can be achieved by appropriately configuring the priority level of their deal.
- Establishing multiple private deals for the same inventory diminishes the exclusivity—and thus the value—of each individual deal. For example, if private deals are created with two buyers for the same inventory, those two buyers will compete against each other. Similarly, if deals are established with twenty buyers, all twenty will compete for access to the same inventory.
- We recommend choosing either Open Auction or Private Auction while maintaining the default priority level, which is pre-configured to optimize yield performance. Modifying the priority level is considered an advanced configuration and should be undertaken with care, as improper adjustments may adversely affect revenue outcomes. If it becomes necessary to modify the priority level, our general recommendation for encouraging competition and maximizing yield is to consolidate priorities wherever feasible. This includes aligning the priority levels of both private auction deals and programmatic guaranteed deals.
- For ad server clients utilizing guaranteed line items in the Monetize Ad Server, it is recommended to configure private deals at a lower priority level than the member’s reselling priority. This approach helps avoid delivery conflicts and minimizes the risk of underdelivery for guaranteed campaigns. For a comprehensive explanation of how priority settings influence delivery and competition, see [Deal Auction Mechanics](deal-auction-mechanics.md) documentation.

### Creating deals that deliver

- High-volume deals are recommended. Similar to campaigns targeting small segments, deals that only apply to small segments will have low availability. Keep buyer expectations realistic for delivery on a deal for small segments.
- Set buyers expectations for open auction deals. Buyers should be aware that they are competing on the open exchange and they will need to bid competitively on the deal in order to win.
- When creating a deal that targets a low volume of impressions, use a private auction deal to make sure it delivers as much as possible.
- Advise buyers against adding advanced targeting to deals campaigns, as this will narrow their campaign's reach.

### Creating off-platform deals

- Work with off-platform buyers to identify the correct Partner Center member with which to set up deals. Consider [Partner Center Screen - Seller View](partner-center-screen-seller-view.md) for easy retrieval in the future.
- If a buyer represented by a DSP doesn't have a member in Monetize, create your deal with the DSP's member instead. Restricting DSP deals by brand is recommended in order to limit use by other buyers the DSP represents.
- Communicate frequently with off-platform buyers, as you will not have the same level of visibility into their deal usage as you would with a buyer. For example, A targeted icon (green check mark) will display in Monetize near deals that a platform buyer is targeting. Microsoft Advertising doesn't have insight into deal campaigns set up behind a DSP, so the targeted icon will not be available for off-platform buyers. Additionally, off-platform buyers will not be notified when you create a deal for them. You will need to let them know the details of what has been created so that they can get things set up in their DSP.
