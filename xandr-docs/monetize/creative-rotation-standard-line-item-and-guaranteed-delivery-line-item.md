---
title: Creative Rotation
description: In this article, find information on what creative rotation is and how it works for standard line items and guaranteed delivery line items.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Creative rotation

> [!IMPORTANT]
> This document describes the creative rotation feature for standard line items and guaranteed delivery line items. For information about creative rotation for augmented line items, see [Creative Rotation (ALI)](creative-rotation-ali.md).

When multiple creatives of the same size are trafficked to a line item or campaign, you can set a creative delivery strategy using the **Creative Rotation** settings.

> [!IMPORTANT]
> Creative rotation will only work for Guaranteed Delivery Line Items and Direct Campaigns. It does not work for RTB.

## How Creative rotation works

The table below lists the available creative rotation strategies and describes how they work.

> [!NOTE]
> If you are using other optimization strategies in addition to creative rotation such as a [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md), Creative Rotation will probably be overridden by those other strategies.

| Creative Rotation Strategy | Description |
|---|---|
| Auto-optimize creative weight | The creative with the highest click-through-rate (CTR) delivers the most. 75% of delivery is allocated to the highest performing creative (based on CTR). All remaining creatives of the same size receive equal allocations of the remaining 25% of overall delivery. |
| Evenly weight creatives | Impressions are allocated evenly across same-sized creatives, which is handled automatically by our system. This is the default setting. |
| Manually weight creatives | The rotation is based on a user-supplied weight. If you select the manual weighting option, you'll have the option to set the creative weight in the dialog that appears when you edit the creative. The allowed weight is between 1 and 999. The default weight is 10. <br> The rotation is based on a user-supplied weight. The allocation percentage is determined by dividing this creative's weight by the sum of the weights of all same-sized creatives. For example, if you set the weight of a 300x50 creative to 30, and the weights of all 300x50 creatives on the line item total 100, this creative will bid on that line item's behalf 30% of the time. |

## Using creative rotation with creatives of different sizes

Creative rotation can apply to creatives of different sizes, specifically in the case where an impression is allowing multiple sizes (also known as "promo sizes"). For more information about promo sizes, see [Using Promo Sizes](using-promo-sizes.md).

See the sections below to better understand how promo sizes interact with the following creative rotation strategies:

- Manually Weighted
- Auto-Optimized

### Manually weighted

Let's say your line item has the following creatives competing to serve and you've selected the **Manually weight creatives** option:

- Creative A is 160x600 with a weight of 20
- Creative B is 300x600 with a weight of 30
- Creative C is 300x600 with a weight of 50

As a result, these creatives will bid on your line item's behalf as follows:

- Creative A will bid on 20% of eligible impressions
- Creative B will bid on 30% of eligible impressions
- Creative C will bid on 50% of eligible impressions

### Auto-optimized

The creative within a size bucket with the highest click-through-rate (CTR) delivers the most. This is the default setting.

Microsoft Advertising assigns weights per creative for nodes (tag and inventory URL combinations) that have at least 50,000 impressions and 10 clicks served by the line item. When the creative is new, default weights are assigned instead.

## Related topics

- [Create a Standard Line Item](create-a-standard-line-item.md)
- [Using Promo Sizes](using-promo-sizes.md)
- [Understanding Performance Goals](understanding-performance-goals.md)
