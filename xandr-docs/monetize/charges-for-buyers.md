---
title: Microsoft Monetize - Charges for Buyers
description: Explore buyer charges, including Buyer Auction Service Charge (BASC), BASC as Bid Reduction, and related fees.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Charges for buyers

## Buyer Auction Service Charge (BASC)

The charge for purchases of third-party inventory. Quoted as a percentage of media cost, this charge can be either a fee or a deduction, and may differ in amount when buying from Microsoft Advertising's platform sellers (Platform Inventory) and supply partners (Partner Inventory).

> [!NOTE]
> You can view the BASC deduction or fee amount for a specific invoice period using one of the billing reports in the UI. For more details about how this charge is calculated, see [Buyer Auction Service Charge Mechanics](buyer-auction-service-charge-mechanics.md).

## BASC as a deduction (Bid reduction)

When specified as a bid reduction in your contract, the BASC is set to be a component of media cost by default and is therefore not itemized separately on your invoice. Applied as a bid reduction, BASC is accounted for within your budget (e.g., insertion order or line item). Alternately, you can contact your Microsoft Advertising Account Representative to have your BASC set to be a disclosed deduction. This will cause it to appear as a separate line item on your invoice.

## BASC as a fee

When charged as a fee, the BASC is itemized separately on your invoice and not accounted for within your budget.

## Creative overage fee

This fee **only** applies to hosted banner creatives. This includes creatives uploaded with HTML-5 zip files, as they are treated as hosted banners and charged for creative overage.

The amount charged for serving creatives that are over the maximum size specified in your contract. For each oversized creative, the difference between (a) the size of the creative and (b) the maximum creative size outlined in your contract is multiplied by (c) the number of impressions where the creative served, and then by (d) the bandwidth charge in your contract is equal to the creative overage fee we charge each month. You can [reconcile](reconciling-your-invoice-with-reporting.md) the creative overage fee on your invoice in the UI with the Buying Billing Report.

> [!NOTE]
> (b) the **maximum creative size** is in **KB** where as (d) the **bandwidth charge** is in **GB**. When converting from GB to KB, **divide by 976,563** because Microsoft Advertising uses the **kibibyte** metric for KB.

For **example**, let's say the maximum creative size in your contract is (b) 40KB, you have a (a) 60KB creative that served (c) 100,000 times, and your bandwidth fee is (d) $2.50 per GB (which converts to 976,563 KB).

Your creative overage fee is calculated as follows: `[[(a)60KB - (b)40KB ] x 100,000 imps] x [(d) $2.50 / 976,563 KB] = $5.12`

## Creative audit

The charge for each creative audit performed by Microsoft Advertising, both initial audits and re-audits. The creative audit fee is the standard audit rate with standard turnaround time. Priority audit is a higher fee with expedited turnaround time. You can view the creative audit amount for a specific invoice period using the **Completed Creative Audits Report** in the UI.
