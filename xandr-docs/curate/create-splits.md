---
title: Microsoft Curate - Create Splits
description: Learn to enable Supply Shaping, configure splits, set priorities, and activate the catch-all split in the Supply Shaping panel.
ms.date: 11/14/2023
---

# Microsoft Curate - Create splits

Use **Supply Shaping** to optimize curated deals by defining specific splits and settings.

Follow the steps below to configure **Supply Shaping** effectively:

1. From the **Supply Shaping** panel, click the toggle to enable **Supply Shaping** for your curated deal. The **splits** entry grid will appear.
1. From the **Targeting** dropdown, select which targeting criteria you want to define for your splits. This will add a column to the entry grid from which you can configure the targeting for each split.
1. Select a split to display the action bar, allowing you to:
    1. Move a split higher or lower in the priority order.
    1. Deactivate a split if it is not needed temporarily.
    1. Delete a split if it’s no longer needed at all.
1. Click the **New** button to add more splits to the entry grid.
1. Use the checkboxes at the top of the entry grid to define further settings for your splits. These settings are described in the subsequent sections.
1. Enable the **catch-all split toggle** to turn on the catch-all split. For more information on **catch-all split**, See the [Introduction to Splits](intro-to-splits.md) page.

## Custom margins

You can customize margins for each split if your Curate seat and user have the necessary permissions. Follow the steps below to enable and configure custom margins.

1. If your Curate seat and user are permissioned to take a margin, the **Use Custom Margins** checkbox will be available. Check the box to add the **Margin** column to the splits entry grid.
1. By default, each split will use the same margin value defined for your deal line item in the **Basic Settings** section. You can override this margin value by setting a specific value on each split.
1. Your splits always use the same **Margin Type**—either percentage or CPM—that you selected for your deal line item in the **Basic Settings** section.

## Custom floors

If you’ve setup your deal line item with a **Floor Price** in the **Basic Settings** section, the **Use Custom Floors** checkbox will be available. Check the box to add the **Floor** column to the entry grid.

When using custom floors, you must enter an explicit floor value for each split. The splits do not inherit a floor value from their deal line item.

> [!NOTE]
> For DSPs where the Microsoft Advertising platform automatically syncs deals, the floor you configure for the deal line item under the Basic Settings section is used when syncing the deal with the DSP. Custom floors defined on splits are only sent on the bid request, auction-by-auction.

## Spend allocations

Enabling the **Use Spend Allocations** checkbox allows you to configure a percentage of buyer spend you would like each split to represent. For example, by creating two splits and setting each to 50%, the spend allocation algorithm will automatically weight the splits such that they each represent half of the buyer’s spend hour by hour.

When configuring spend allocations there are two types of splits:

- **Capped** splits, where you enter an explicit, non-zero percentage which the algorithm tries to respect during every hour where the deal is delivering.

- **Uncapped** splits, where you do not enter an explicit percentage. All uncapped splits are considered as a group that can deliver any remaining spend allocation not already taken by the capped splits. For example, if you have one capped split at 80% and two uncapped splits, the algorithm allows the latter to contribute 20% of spend through the deal based on their availability. Note that the catch-all split, if enabled, is always uncapped.

Your total spend allocation percentages must be less than or equal to 100%. When the total is less than 100% the remaining allocation is shared amongst uncapped splits.

### Spend allocation algorithm

There are three different types of allocations which the spend allocation algorithm considers:

- **Natural allocation** – this is the relative spend each split achieves if the algorithm does nothing. For example, a split targeting a large seller might naturally generate 80% of spend through the deal while a split targeting a small seller generates 20%.
- **Configured allocation** – this is the relative spend you want each split to represent which usually deviates in some way from the natural allocation. For example, a split naturally generates 80% of spend through the deal but you want it to represent 50%.
- **Achieved allocation** – this is the relative spend each split actually delivered as a result of the spend allocation algorithm’s intervention.

The spend allocation algorithm aims to influence the natural allocation so that the achieved allocation is as close as possible to the configured allocation. To do this the algorithm sets a participation rate for each split.

As a recap, when the Microsoft Advertising platform receives an ad call it checks if it meets a deal line item’s targeting criteria. If so, it checks the deal line item’s splits and selects the first split whose targeting criteria are met (see the Introduction to Splits page for more information).

If a split has been selected but is below its participation rate threshold, its curated deal won’t be added to the auction. This allows the algorithm to intervene when a split’s achieved allocation is higher than its configured allocation. By adding the curated deal to fewer auctions, it can reduce the buyer spend on that split.

The participation rate is calculated according to the split’s historical spend and availability which are reliable indicators for its future potential spend. For example, consider a simple curated deal with two splits and the following historical spend:

|Split|Historical spend|Natural spend allocation|Configured spend allocation|Required participation rate| Achieved spend allocation|
|---|---|---|---|---|---|
| 1  | $400  | 80% | 50% | 25%| $100 |
| 2  | $100  | 20% | 50% | 100%| $100|

When you configure new spend allocations or edit existing spend allocations, the algorithm lets all splits participate at 100% for 1 hour to gather data about the splits’ natural spend allocation. It then sets participation rates for each split to meet the configured allocations. It recalculates the participation rates every 30 minutes. The algorithm can redistribute up to 5% of spend across splits in order to maximise a curated deal’s delivery.

### Common scenarios

- **No spend on the curated deal** – If you’ve configured spend allocations for a curated deal but the buyer is not currently spending, the algorithm will not set any participation rates. All splits will participate at 100% until the algorithm has 1 hour of data to determine the natural spend allocation.
- **No spend on a split** – If a split has a capped spend allocation but is not generating any spend, the algorithm will continue to try to respect its configured allocation without preventing us splits from delivering. However, a capped split with zero spend will severely limit the curated deal’s overall delivery.

## Related topics

- [Introduction To Splits](intro-to-splits.md)
- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Curator Supply Shaping](curator-supply-shaping.md)
- [Curator Analytics Report](curator-analytics-report.md)
- [Split Report Details](report-on-splits.md)
