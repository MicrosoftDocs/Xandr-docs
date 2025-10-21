---
title: Microsoft Monetize - Fee Calculations
description: Calculate partner fees by percentage or CPM, deducting from revenue. Revshare adjusts net/gross media cost, including media/data cost with BASC. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Fee calculations

When you create a [partner fee](partner-fees.md), the fee can be based on percentage or CPM. CPM fees are always deducted from revenue. Revshare fees may be calculated in multiple ways:

- Deducted from revenue
- Added to net or gross media cost
- Added to media cost and data cost

Gross media cost includes the [Buyer Auction Service Charge](buyer-auction-service-charge-mechanics.md) (BASC). Net media cost covers only pure media
cost.

> [!NOTE]
> Line item currency is inherited from the advertiser. If a fee is created in a currency other than the line item currency, then we will automatically convert the fee to the line item currency at the time of transaction.
