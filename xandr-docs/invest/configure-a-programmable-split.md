---
title: Microsoft Invest - Configure a Programmable Split
description: In this page, learn how programmable splits can be used to split the inventory of augmented line item (ALI) and what are the advantages of using splits.  
ms.date: 10/28/2023
---


# Microsoft Invest - Configure a programmable split  

You can use programmable splits to refine line item targeting and dynamically adjust bids, budget allocation, and creative allocation across a line item's targeted inventory. Splits are recommended if you have sophisticated targeting requirements.

When you create an [augmented line item (ALI)](create-an-augmented-line-item-ali.md), you also have the option to split up its inventory using **programmable splits**. Splits allow you to:

- Target different subsections of inventory that match the line item's more general criteria
- Dynamically adjust bids based on targeting
- Allocate the line item budget to different targets
- Distribute creatives across the line item's targeted inventory

You define a split by specifying the inventory you want available for it, using any combination of split settings. These include geography, inventory performance, and segment information. If you choose, you can also specify bidding or valuation rules, budget allocations, bidding priority, and/or creative selection for each split. For more background information on how splits work, see [Understanding Splits](understanding-splits.md).

> [!NOTE]
> Split changes are only applied when you select **Review and Save** on the line item.

1. [Create a Programmable Split](create-a-programmable-split.md)

    You can create a new programmable split when creating or editing an augmented line item.

1. [Set Split Targeting](set-split-targeting.md)

    You can define targeting parameters for programmable splits that expand upon or differ from your line item's targeting parameters.

1. [Set Split Priority](set-split-priority.md)

    When using multiple programmable splits on a line item, you can prioritize your splits so that impressions applicable to multiple splits get assigned to one split over another.

1. **Optional:**
    [Set Spend Allocation and Capping on a Split](set-spend-allocation-and-capping-on-a-split.md)

    You can set percentages to designate portions of line item's daily budget to your split and determine how conflicts are handled between spend allocation and line item delivery goals.

1. **Optional:**
    [Use Segment Targeting with a Split](use-segment-targeting-with-a-split.md)

    You can target splits based on segment presence or absence, age, or value.

1. **Optional:**
    [Assign Creatives to a Split](assign-creatives-to-a-split.md)

    You can assign specific creatives for a split to deliver.

1. **Optional:**
    [Pass Custom Macros to a Split](pass-custom-macros-to-a-split.md)

    You can use split custom macros to pass values through splits'creative landing page URLs.

1. **Optional:**
    [Use User Test Groups with a Split](use-user-test-groups-with-a-split.md)

    You can perform A/B testing with user test groups, targeting distinct groups of users per split.
