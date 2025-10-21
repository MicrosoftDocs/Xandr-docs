---
title: Microsoft Monetize - Creative Rotation (ALI)
description: In this article, find information on what creative rotation is and how it works for ALIs.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Creative rotation (ALI)

When multiple creatives of the same size are trafficked to a line item, you can set a creative delivery strategy using the **Creative Rotation** settings in the **Associated Creatives** section on the **Create New Line Item** and **Edit Line Item** screens.

## How creative rotation works

The following table outlines the available creative rotation strategies and describes how they work.

> [!NOTE]
> If you're using a custom model to deliver creatives, a message will display indicating that a model is attached. For more information, see [Custom Models](../data-science-toolkit/custom-models.md).

| Creative Rotation Strategy | Description |
|---|---|
| Auto-optimize creative weight | The creative within a size bucket with the highest click-through-rate (CTR) delivers the most. This is the default setting. <br> Microsoft Advertising assigns weights per creative for nodes (tag and inventory URL combinations) that have at least 50,000 impressions and 10 clicks served by the line item. When the creative is new, default weights are assigned instead. |
| Evenly weight creatives | Impressions are allocated evenly across same-sized creatives, which is handled automatically by our system. |
| Inherit creative weight from splits | The rotation is based on a user-supplied weight that is defined per split. Impressions are allocated per split with weights assigned to the splits themselves. For example, if a split has a spend allocation of 50%, 50% of impressions will go to that split. If multiple creatives are associated with a split, impressions are distributed evenly among the associated creatives. |
| Manually weight creatives | The rotation is based on a user-supplied weight. If you select the manual weighting option, you'll have the option to set the creative weight when you edit the creative. The allowed weight is between 1 and 999. The default weight is 10. <br> The allocation percentage is determined by dividing this creative's weight by the sum of the weights of all same-sized creatives. For example, if you set the weight of a 300x50 creative to 30, and the weights of all 300x50 creatives on the line item total 100, this creative will bid on that line item's behalf 30% of the time. For more information, see the [How Manual Weighting Works](#how-manual-weighting-works) section below. |

### How manual weighting works

Let's say your line item has the following creatives competing to serve and you've selected the **Manually weight creatives** option:

- Creative A is 300x600 with a weight of 50
- Creative B is 300x600 with a weight of 100
- Creative C is 300x600 with a weight of 150

As a result, these creatives will bid on your line item's behalf as follows:

- Creative A will bid on 17% of eligible impressions
- Creative B will bid on 33% of eligible impressions
- Creative C will bid on 50% of eligible impressions

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Working with Programmable Splits](working-with-programmable-splits.md)
- [Create a Programmable Split](create-a-programmable-split.md)
- [Buying Strategies](buying-strategies.md)
