---
title: Floor Prices
description: Explore the auction dynamics, the seller's minimum accepted net bid, known as the floor price and winning requires bidding at or above this set amount.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Floor prices

A floor price is the minimum net bid price that a seller is willing to accept for a bid in an auction. To win an auction that has a set floor price, the buyer's bid must be greater than or equal to the floor price.

Bids that are below a seller's established floor price won't be accepted for that auction. It's also possible for a win-less auction to occur in which no buyer has made a bid that meets the net floor price.

## Floor types

Two types of floors exist:

- **Hard Floor:** The minimum net price that a seller will accept for a bid. If the net price for the hard floor isn't met, then no bids are accepted and the auction ends without a winner, or a default creative is served. A bid will be considered only if it is equal to or greater than the hard floor.
  
  > [!NOTE]
  > When there is only one bid that exceeds the hard floor and wins the auction, that bid is reduced to the value of the hard floor, assuming there is no soft floor.

- **Soft Floor:** The lowest net price that a bid is reduced to by the seller. Essentially, a soft floor allows the network to alter the mechanics of the standard second-price auction. In a second-price auction, the winning bidder pays the value of the second highest bid in addition to $0.01. However, when a soft floor is set, the winning bidder pays either the soft floor's net price or the second bidder's bid depending upon which one is greater. If the winner’s bid is higher than the hard floor, but lower than the soft floor, the winner pays the price that they've bid. <!--For more information, see https://theviewpoint.com/insights/blog/first-price-vs-second-price-auctions-ultimate-comparison/. -->.
  
  > [!NOTE]
  > A soft floor can't be lower than a hard floor.

## Hierarchy of floor price settings

The following numbered table shows the order in which floor price settings are honored. A setting higher in the table will take precedence over the settings lower in the table.

> [!NOTE]
> All set floor prices within Monetize are net values.

| Option | Description | Where to Set |
|--|--|--|
| 1. Deal Ask Price | When creating a deal, you can set a net ask (floor) price for buyers to pay you that follows the current market price (default selection), or you can set a custom ask price for your deal. For more information on deal ask prices, see [Deal Auction Mechanics](deal-auction-mechanics.md). | When creating a deal (**Partners** > **Deals**) |
| 2. Native Asset (Floor) Pricing | You can set net floor prices for native assets placements (Main Image and Video) that you create during the native assembly configuration process. For more information on native assets, see [Create a Native Assembly](create-a-native-assembly.md).<br>**Note**: If you select the **Market Price** radio button for your ask price selection when creating a deal, floor prices set at the native asset level will be used if available. If no floor prices have been set for your native assets, then the floor prices that you set at the yield management level will be used if available. | When creating or editing a native asset placement (**Publishers** > **Native Assembly**) |
| 3. Yield Management Floor Rules | Networks can use yield management tools to set floor prices, which ultimately help sellers optimize their revenue generation. For more information on yield management, see [Understanding Yield Management](understanding-yield-management.md).<br>**Note**: Yield Management isn't available by default. If you're interested in gaining access or discussing potential use cases that may apply to your business, please reach out to your Microsoft Advertising representative. | The Yield Management **Floor Rules** screen (**Publishers** > **Floor Rules**) |
| 4. Default Creative Reserve (Floor) Prices | To prevent serving blanks (no creatives) or [Default PSAs](default-psas.md), you can set up a default creative and assign it to a placement. Default creatives are served when the highest eCPM bid on a placement is lower than the net eCPM (floor) price that you've set for that placement. For information on assigning a default creative, see [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md). | When creating or editing a placement (**Publishers > Inventory Manager**) |
| 5. Placement Reserve (Floor) Prices | You can set reserve (floor) prices for individual placements. When you set a reserve price for a placement, you're ensuring that no creative can serve on that placement at a net price that is lower than your set reserve price. Placement reserve prices are calculated according to either your total network or publisher revenue. For more information about setting a placement reserve price, see [Update a Placement](update-a-placement.md). | When creating or editing a placement (**Publishers** > **Inventory Manager**) |

## Related topics

- [Outgoing Bid Request to Bidders](../bidders/outgoing-bid-request-to-bidders.md)
- [Incoming Bid Request from SSPs](../supply-partners/incoming-bid-request-from-ssps.md)
- [Seller Best Practices](../industry-reference/seller-best-practices.md)
- [Placement Tag Parameters](placement-tag-parameters.md)
- [Target Video Attributes via Query String Parameters](target-video-attributes-via-query-string-parameters.md)
