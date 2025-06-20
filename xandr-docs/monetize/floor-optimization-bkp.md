---
title: Floor Optimization
description: Optimize revenue by establishing calculated hard floors for floor rules, maximizing seller earnings based on individual impression value.
ms.date: 10/28/2023
---

# Floor optimization

You can enable floor optimization for any floor rule. When enabled, floor optimization adjusts the hard floor for every impression to better protect and value a seller's inventory.

> [!NOTE]
> Floor Optimization is currently in a closed Beta. We are working to roll this feature out to more clients. This feature was built to support second-price auctions, and may not perform as expected in other auctions.

## What is floor optimization

Floor optimization works to maximize seller revenue by calculating a hard floor based on an individual impression's value to the seller. Floor optimization incorporates characteristics, such as inventory, geography, and other factors, and quickly adjusts to changes in marketplace liquidity. Optimal floors are set before bids are received.

Regardless of whether or not floor optimization is enabled, bids are never reduced below a hard floor. If floor optimization is turned on for a floor rule, soft floors are not available. For more information about soft floors, see [Understanding Yield Management](understanding-yield-management.md).

## How to turn on floor optimization

Floor optimization can be enabled or disabled for any base or conditional floor rule.

1. From the **Floor Rules** screen, select the checkbox for each floor rule that you want to edit.
1. Click **Actions** >  **Enable Floor Optimization** or **Actions** >  **Disable Floor Optimization** to enable or disable **Floor Optimization** for the selected floor rules.
1. Click **OK** in the confirmation dialog to confirm the change.

> [!NOTE]
> Soft floors are ignored if **Floor Optimization** is enabled for a floor rule.

To add floor optimization to a [floor rule](create-a-floor-rule.md), click the **Floor Optimization** toggle in the **Floor Pricing** section.

## Floor optimization in debug auctions

Sellers with the **Floor Optimization** toggle enabled can see the optimal floor price and whether it was used in the auction.

For more information about debug auctions, see [Understanding the Debug Auction](understanding-the-debug-auction.md).

## Related topic

[Create a Floor Rule](create-a-floor-rule.md)
