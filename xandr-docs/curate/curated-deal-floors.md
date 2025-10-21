---
title: Curated Deal Floors
description: In this article, learn about curated deal floors, fixed and standard floor types, and floor type prices.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Curated deal floors

Microsoft Advertising lets you to specify a floor on curated deals. Curated deal floor types are configured on a [curated deal line item](create-a-curated-deal-line-item.md).

## Floor types

Curated deal floors corresponding to the **Revenue Type** of the [curated deal line item](create-a-curated-deal-line-item.md):

- Fixed – **CPM** selected and a **Fixed Price** entered.
- Standard – **Dynamic CPM** selected and a **Floor Price** entered.
- Market – **Dynamic CPM** selected and **Use Market Price** selected.

> [!NOTE]
> If your fixed price curated deal curates impressions from a seller who runs second price auctions, you may notice that your curated deal's clearing price is lower than the fixed price you configured.

Curated deal floors can be set with or without margins (see [Curator Margins](curator-margins.md)). Setting floors on curated deals not only allows you to set margins, but also gives buyers more guidance on how to bid more accurately. Buyers will tend to bid more often and with higher bids on impressions that come with a deal floor.

## Fixed and standard floor types

It’s important to understand how seller floor type and price can affect curator margins when the curator floor type is fixed or standard. When working with seller deals that have a fixed floor, your curator margin is effectively the *minimum* margin you may earn. Because of this, some special auction scenarios can arise which can sometimes cause a higher margin to be taken in practice or the bid to be rejected:

- When a seller deal is fixed floor and the curated deal is fixed or standard floor, you must set a margin type. If no margin has been set, the deal will throw an error in the auction because any amount above these floor prices cannot be collected by either the seller or the curator. Curators who cannot take margin cannot curate fixed price seller deals with standard or fixed price curated deal floors.
- When the seller deal is fixed floor and the curator deal is fixed floor and a margin has been set, the curator takes the difference between the two floors, regardless of what the curated margin is (assuming the minimum margin doesn't make the curator floor lower than the seller floor - if it does, the transaction is rejected).
- When the seller deal is fixed floor, the curator deal is standard floor and a margin has been set, the curator takes the difference between the buyer bid and the seller fixed price (assuming the auction is first price).

## Floor type price

Setting floor types and prices is a strategic choice. Curators can set their own floor price at a line item level. The ability to set curator floor prices above, at, or even below a seller floor gives curators maximum flexibility. For example, you might choose to set floors that are above all seller floors to ensure that buyers always clear. On the other hand, you might choose to set floors that match the lowest seller floor, indicating the lowest possible value a buyer should bid to clear some of the time.

The following table lists the outcomes of various combinations of seller and curator floor types to help guide you in determining the best settings for curator deal margin types and floor types.

| Seller Floor | Curator Floor | Outcome |
|:---|:---|:---|
| Fixed | Fixed | **Note:** If no curator margin is set, this configuration is not allowed and will cause an error. This is because the seller has expressed they do not want anything above the fixed price and you have not configured a minimum margin indicating you wish to collect anything above the seller’s fixed price.<br><br>You should account for the seller’s fixed floor when determining a curator margin and fixed floor price. For example, you might inadvertently add a margin that, when applied to the curator fixed floor price along with the curator tech fees, results in a bid that is below the seller's fixed floor price. |
| Fixed | Standard | **Note:** If no curator margin is set, this configuration is not allowed and will cause an error. This is because the seller has expressed they do not want anything above the fixed price and the curator has not configured a minimum margin indicating they wish to collect anything above the seller’s fixed price.<br><br>You should account for the seller’s fixed floor when determining a curator margin and standard floor price. For example, you might inadvertently add a margin that, when applied to the curator standard floor price along with the curator tech fees, results in a bid that is below the seller's fixed floor price. |
| Fixed | Market | Since you are not adding a fixed or standard floor, there is no additional operational risk. |
| Market | Fixed | Since seller market price floor is based on yield management (YM) floors, which can vary by creative attribute (e.g., brand), you might set a fixed price that conflicts with the YM floor. If this occurs, this error will show up in the [Curator Bid Error Report](curator-bid-error-report.md). |
| Market | Standard | Since seller market price floor is based on yield management (YM) floors, which can vary by creative attribute (e.g., brand), you might set a standard price that conflicts with the YM floor. If this occurs, this error will show up in the [Curator Bid Error Report](curator-bid-error-report.md). |
| Market | Market | Since you are not adding a fixed or standard floor, there is no additional operational risk. |
| Standard | Fixed | You should account for the seller’s standard floor when determining a curator margin and fixed floor price. For example, you might inadvertently add a margin that, when applied to the curator fixed floor price along with the curator tech fees, results in a bid that is below the seller's standard floor price. |
| Standard | Standard | You should account for the seller’s standard floor when determining a curator margin and standard floor price. For example, you might inadvertently add a margin that, when applied to the curator standard floor price along with the curator tech fees, results in a bid that is below the seller's standard floor price. |
| Standard | Market | Since you are not adding a fixed or standard floor, there's no additional operational risk. |

## Related topics

- [Curated Deals](curated-deals.md)
- [Create a Curated Deal Line Item](create-a-curated-deal-line-item.md)
- [Curator Reporting](curator-reporting.md)
- [Curator Margins](curator-margins.md)
