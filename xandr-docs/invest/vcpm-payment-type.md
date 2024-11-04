---
title: Microsoft Invest - vCPM Payment Type
description: Viewable CPM is a payment type where buyers pay only for viewable impressions. Impressions don't incur a cost until a post-auction event, after which buyers pay the full value of the vCPM bid.
ms.date: 10/28/2023
---

# Microsoft Invest - vCPM payment type

Viewable CPM (vCPM) is a payment type that allows buyers to pay only for impressions that are measured "viewable" (read our [Introduction to Viewability](./introduction-to-viewability.md) for more information on viewability measurement). vCPM is similar to CPC and CPA payment types in that the impression does not incur a cost until a post-auction event occurs. For vCPM, the post-auction event is a signal that the impression was viewable. Once that event is received, the buyer will pay the full value of the vCPM bid.

## Buy inventory on a vCPM basis

To use the vCPM payment type, select **Viewable CPM** as your revenue type and enter your bid price.

The **vCPM** payment type supports the ability to use a custom definition for viewable impressions. We currently support two definitions, the IAB standard and the Group M standard. The IAB standard definition is used by default. If you would like to use a custom definition, contact your Microsoft Advertising Account Manager.

### vCPM payment bid calculations

Buyers submit bids at a vCPM rate, just as they would with CPC or CPA. In order for that bid to participate in an RTB auction, the bid must be converted into an eCPM to compete with other CPM bids. Microsoft Advertising calculates the eCPM by multiplying the vCPM bid amount by the estimated view rate for that impression.

> [!NOTE]
> vCPM calculations are only used to manage auction mechanics for the seller. It does not impact the buyer's final media cost or the fact that they pay only for viewable impressions.

## Example

1. vCPM bid won the auction because its eCPM was higher than the CPM bid. Additionally, the impression was viewed, therefore the advertiser pays the publisher the full $10 vCPM bid amount.
1. vCPM bid won the auction because the eCPM was still higher than the CPM bid of $4.00. However, there was no payout because the impression was not viewed.
1. The CPM bid won the bid. The 20% estimated view rate translates to an eCPM for Bid 1 that is lower than the CPM bid.

### Generate report on payment types

**Payment Type** is an available **Filter** and **Dimension** in analytics reporting.

To generate a report for all vCPM buying activity, select **Edit** on the **Payment Type** filter and select the **vCPM** option.

Alternatively, to generate a report broken down by Payment Type, select the **Payment Type** checkbox in the **Dimension** column.

> [!NOTE]
> The vCPM Payment Type is only available when reporting on buying activity. For selling activity, use the **Revenue Type** option.
