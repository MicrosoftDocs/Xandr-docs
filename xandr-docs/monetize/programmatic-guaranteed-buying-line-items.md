---
title: Microsoft Monetize - Programmatic Guaranteed Buying Line Items
description: In this article, understand what a PG buying line item and a PG deal are, the advantages of PG line items, and billing and monitoring for a PG deal.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Programmatic Guaranteed buying line items

A programmatic guaranteed buying line item (PG buying line item) provides you with a workflow specifically designed for buying a programmatic guaranteed deal (PG deal).

PG buying line items have very different targeting, budgeting, and optimization options compared to augmented line items.

## Programmatic Guaranteed deals

Programmatic Guaranteed deals (PG deals) bring the targeting, messaging, and reporting benefits of programmatic advertising to guaranteed media buys. They offer an automated solution for getting guaranteed access to media from sellers and provide an efficient approach that eliminates many of the additional steps required when buying via an insertion order.

PG buyers, using PG buying line items, transact (bid) on sellers' PG deals that define the targeting, frequency/recency, and creative specifications, for the buyer to follow.

> [!NOTE]
> Prior to transacting on a PG deal, confirm with its seller that the creatives you wish to serve meet their deal's creative format, size, and technical attribute requirements.

If you have questions about how to set up a PG deal, please contact your account manager.

## Key differences between PG line items and augmented line items

> [!IMPORTANT]
> Only PG line items can target PG deals.

| Feature | PG Line Item | Augmented Line Item |
|---|---|---|
| Budgeting | Determined by PG deal to which the line item is associated | Determined by insertion order or line item |
| Flight Dates | Inherits insertion order flight dates and deal flight dates; unique flight dates cannot be set on line item. | Flight dates can be set on insertion order and/or line item. |
| Frequency & Recency | Determined by PG deal to which the line item is associated | Determined by insertion order or line item |
| Optimization | Conversion tracking | Conversion tracking, goal priority, and selection of optimization method |
| Revenue Type | Cost Plus | CPM, CPC, Dynamic CPM, Viewable CPM, or Cost Plus |
| Targeting | Determined by PG deal to which the line item is associated. | Determined by line item. ALIs cannot target PG deals. |

## Advantages of PG line items

PG line items offer the following advantages:

- Easy access to PG deals for guaranteed buying of premium video and display media
- Streamlined execution and reporting of guaranteed media buys
- Insight into frequency, reach, and attribution of PG deals
- Predictable spending on deals

## PG deal billing

With PG deal buying, you'll never pay for more than a deal's agreed-to number of booked impressions. You only pay for a number of delivered impressions that is less than or equal to a PG deal's booked impression number. Microsoft Advertising only charges fees on the
cost-of-media collected.

> [!NOTE]
> While Microsoft Advertising's billing reports show PG deals as being capped at their agreed-to booked impressions, non-billing reports still reflect overdelivery regarding logged delivered impressions versus adjusted-for-billing impressions.

- **What happens with billing in the month that a deal ends?**

    The deal is reconciled (spend is capped), and the buyer is charged up to the agreed-upon deal amount.

- **What happens if the deal ends but is not fully delivered?**
  
    The buyer is only charged for delivery that is less than or equal to the agreed-upon deal budget.

- **What happens if a deal is modified (the deal is extended, or the deal's price rate is increased) mid-flight?**
  
    We use the latest version of a deal's size (booked imps) to determine if an adjustment is necessary. When a deal size changes mid-month, assuming it isn't changed to an amount lower than the number of delivered impressions, we use the updated impressions value for billing.

## Auto-monitoring feature

PG buying line items are required to bid on every possible impression associated with the targeted PG deal. Certain line item or PG deal setups, however, may prevent your line item from bidding on available impressions.

With **auto-monitoring**, your line item is sent a warning once its bid rate drops to a certain percentage. If the line item's bid rate percentage drops further, your line item automatically deactivates and switches to an **Inactive** state. The line item's targeted PG deal also switches its acceptance status to **Inactive**. This allows you to then troubleshoot your line item by fixing its setup issues (like member-level targeting conflicts and creative eligibility issues) or renegotiating the terms of the seller's PG deal. After making the necessary adjustments to increase your line item's bid rate, you can manually re-activate your line item to continue fulfilling the deal.

> [!NOTE]
> When your line item deactivates, Microsoft Advertising sends a notification email to all email addresses marked as **Notification Addresses** for your account's Sherlock deactivations.

## Related topics

- [Create a Programmatic Guaranteed Buying Line Item](create-a-programmatic-guaranteed-buying-line-item.md)
- [Metrics for Programmatic Guaranteed Buying Line Items](metrics-for-programmatic-guaranteed-buying-line-items.md)
- [Troubleshoot your Programmatic Guaranteed Buying Line Item Bid Performance](troubleshoot-your-programmatic-guaranteed-buying-line-item-bid-performance.md)
- [Bid Performance Messages for Programmatic Guaranteed Buying Line Items](bid-performance-messages-for-programmatic-guaranteed-buying-line-items.md)
