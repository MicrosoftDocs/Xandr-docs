---
title: Selling Inventory on a CPC and CPA Basis
description: Explore maximizing Microsoft Ad ecosystem by reselling inventory on CPC/CPA, ensuring higher payouts via Microsoft Monetize for effective risk management.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Selling inventory on a CPC and CPA basis

In order to foster a stronger ecosystem on Microsoft Advertising, we pioneered the ability to resell your inventory on a CPC or CPA basis in real time. Since many networks negotiate financial terms with publishers based on a revenue share per conversion or click, it makes sense that networks should be able to resell inventory in this fashion to other networks.

Selling inventory in this fashion allows you to demand a larger payout for accepting more risk as the seller. We have built capabilities into Microsoft Monetize to support this tradeoff.

## Overview

Sellers can now opt in to selling their inventory on a CPC and CPA basis by publisher. Sellers can also set which payment types they accept on a buyer-by-buyer basis. For more information, see [Edit Buyer Eligibility, Allowed Payment Types, and Targeting Access](edit-buyer-eligibility-allowed-payment-types-and-targeting-access.md).

You can choose to accept CPC and CPA payment types when you [Create a Publisher](create-a-publisher.md).

## Publisher risk premium

Sellers take more risk when accepting [CPC and CPA Payment Types](cpc-and-cpa-payment-types.md), and should be compensated for taking this risk. In order to compensate sellers, we allow them to set risk premium per publisher. Setting a risk premium allows them to demand that a CPA or CPC payment from a buyer be a certain percentage higher than a CPM bid.

The table below shows how eCPM bids will be recalculated based on the publisher's risk premium to derive a final bid:

| Payment Type | eCPM Bid | Publisher Risk Premium | Final Bid after Risk Premium is Applied |
|---|---|---|---|
| $ 8 CPA | $0.8 | 25% | $0.60 |
| $0.50 CPC | $0.50 | 10% | $0.45 |
| 6 CPA Goal | $0.60 | n/a | $0.60 |

Based on the example, the CPA payment type will win the auction. The creative is served and the buyer will pay the seller $8 **if** the user converts.

## Allowing payment types on a per-buyer basis

Sellers can choose which buyers they will accept CPA and CPC payment types from. For instructions, see the [Edit Buyer Eligibility, Allowed Payment Types, and Targeting Access](edit-buyer-eligibility-allowed-payment-types-and-targeting-access.md).

## Related topics

- [CPC and CPA Payment Types](cpc-and-cpa-payment-types.md)
- [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md)
