---
title: Microsoft Monetize - Understanding Splits
description: In this article, find information about what splits are and how they work.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Understanding splits

> [!NOTE]
> This page explains what splits are and how they work. For step-by-step instructions on creating a split, see [Configure a Programmable Split](configure-a-programmable-split.md).

## What is a split?

When you create a [line item](create-an-augmented-line-item-ali.md), you specify the inventory you'd like to target, the budget you'd like to spend over the line item's flight, how you want to track revenue, and how to use Microsoft Advertising optimization. If you choose, you can also split up the line item inventory with **programmable splits**, which you can use to:

- Target different subsections of the inventory that matches the line item's criteria
- Dynamically adjust bids based on targeting
- Allocate the line item budget to different targets
- Distribute creatives

:::image type="content" source="media/li-splits.png" alt-text="Diagram that shows an example of a line item inventory split up using programmable splits.":::

In essence, the line item acts as a filter. Impressions must match the targeting specified on the line item before they are passed on to splits.

You define a split by specifying the inventory you want available for it, using any combination of targeting conditions, such as geography, inventory performance, and segment information. You can then optionally define bidding or valuation rules, budget allocations, bidding priority, and/or creative selection for each split.

> [!IMPORTANT]
> When you create a split, behind the scenes you're actually creating a logic tree, or a program, powered by [custom models](../data-science-toolkit/custom-models.md).

Here are some examples of how you can use splits:

- Manually optimize KPI (for example, attribute conversions to a third-party server)
- Manage secondary KPIs (such as spending 20% in a particular geo zone if you meet the delivery and performance goal of the line item)
- Implement dynamic creative decisioning
- Bias spend towards a particular seller or publisher to achieve business goals

## Split spend allocation

Split spend allocation is the percentage of the line item daily budget assigned to a split. Microsoft Advertising will attempt to spend as much as it can to reach the spend allocation goal.

> [!NOTE]
> In some cases, a split's spend allocation goal may conflict with a line item delivery goal. For example, consider a simple line item with two splits. Based on current performance, it looks like Split A can scale (that is, has enough inventory to reach the line item budget), but Split B cannot. If your spend allocation goals on Split A are low, then Microsoft Advertising will not be able to spend as much as required to reach the delivery goal for the line item as a whole.

## Capped and uncapped splits

To determine how conflicts between split spend allocation and line item delivery goals are addressed, you can make your splits either **capped** or **uncapped**.

- **Uncapped** - Uncapped splits prioritize delivery over spend allocation. When a line item with uncapped splits is underdelivering, the uncapped splits are permitted to exceed their spend allocation goals to reach the line item delivery goal. That is, if the line item cannot reach the delivery goal, Microsoft Advertising will ignore spend allocation goals and maximize spend on every split until the line item reaches the delivery goal. If the line item delivery goal is being met, then split spend allocation goals will be met. If the spend allocation goal isn't met, then it implies that the particular split does not have enough inventory to reach allocation goals. By default, splits are uncapped.
- **Capped** - Capped splits prioritize spend allocation over delivery. Even when line items are underdelivering, capped splits are not permitted to exceed the spend allocation goal to help line items reach their delivery goals. This will prevent overspend on a split, but may cause the line item to underdeliver.

The expected behavior for a split varies depending on whether the split is capped or uncapped and on how the line item as a whole is delivering. This table describes the expected behavior for different combinations of split capping and line item pacing.

| Split Capping | Line Item Scenario | Expected Behavior |
|---|---|---|
| All splits are uncapped | Delivering to target | - If **all** splits can scale, the spend allocation goal will be met perfectly. <br> - If any split cannot scale, Microsoft Advertising spends as much as it can on that split and reallocates the remainder of the spend to another split. As a result, some splits will exceed their spend allocation goals. |
| All splits are uncapped | Underdelivering | Maximize spend on all splits. Some splits may exceed their spend allocation goals. |
| All splits are capped | Delivering to target | - If **all** splits can scale, the spend allocation goal will be met perfectly. <br> - If a split cannot scale, Microsoft Advertising spends as much as it can on the split. The excess spend cannot be reallocated to other splits. Splits will not exceed their spend allocation goals, but the line item delivery goal will not be met. |
| All splits are capped | Underdelivering | - Maximize spend on all splits up to (but not exceeding) the spend allocation goal. |
| Some splits are capped | Delivering to target | - If **all** splits can scale, the spend allocation goal will be met perfectly. <br> - If a split cannot scale to allocation goals, Microsoft Advertising spends as much as it can on the split. <br> &nbsp;&nbsp; - If an uncapped split can scale, Microsoft Advertising reallocates excess spend to it, implying it will exceed spend allocation goals. <br> &nbsp;&nbsp; - If a capped split can scale, Microsoft Advertising reallocates excess spend to it, but only up to the spend allocation goal |
| Some splits are capped | Underdelivering | Maximize spend on all splits. <br> - If a split is capped, do not exceed spend allocation goal. <br> - If a split is uncapped, exceed spend allocation goal. |

## Line item default

Any traffic that passes the line item targeting but doesn't meet the conditions for a particular split is assigned to the **line item default split**, which is created automatically.

## Splits and Optimization

You can use splits with or without [optimization](optimization-guide-ali.md). You can [enable or disable](create-an-augmented-line-item-ali.md) optimization at the line item level.

### Splits when Optimization is enabled

Using Microsoft Advertising optimization means you specify a performance goal on the line item and then rely on Microsoft Advertising for inventory discovery and bid valuation.

If you select this option:

- **Spend Allocation** - Microsoft Advertising will prefer delivery and performance to split spend allocation. Spend allocations will only be observed if the line item can also meet its performance goal. This implies that we may not deliver on some splits if we predict that the inventory in a split does not help meet your performance goal. For example, if you have a split for cnn.com, but cnn.com is not the right inventory for your line item performance goals, we will not spend on cnn.com.

- **Valuation** - Microsoft Advertising optimization will determine the bids on splits. You will not be able to specify max bid (how much you are willing to pay for impressions) by split. Spend allocations can only be used to influence how much to spend on the split as a whole.

### Splits when Optimization is disabled

If you disable Microsoft Advertising optimization, you will be optimizing manually. There will be no discovery of inventory or valuation of bids on the inventory to reach your performance goal.

- **Spend Allocation** - Split spend allocations will only be observed if the line item can also meet its delivery goal. It is possible to buy all the inventory in a split.
- **Valuation -** You will be able to specify max bid by split. There are two ways to do this:
  - If the revenue type is cost plus or dCPM, you must specify max bid by split.
  - If the revenue type is CPM, you can specify bid multipliers by split. This modifies the CPM revenue that you entered at the line item to calculate a max bid per split. For example, if you entered $1 CPM on the line item and assigned a bid multiplier of 3 to a split, the max bid for the split would be $3 CPM.
  - If revenue type is CPC or vCPM, there is no valuation option, because revenue tracking requires that Microsoft Advertising optimization be enabled and optimization will determine the valuation.

> [!NOTE]
> The valuation provided by the split is an expected max bid and not an actual bid. Generally, we try to lower CPMs as much as we can while still reaching the line item's delivery goals and the split's spend allocation goals. However, if the line item settings favor delivery, the maximum bid may be up to twice as much as the max bid you enter.

## Related topics

- [Configure a Programmable Split](create-a-programmable-split.md)
- [Update Splits](update-splits.md)
- [Import or Export Split CSVs](import-or-export-split-csvs.md)
- [Optimization Guide - ALI](optimization-guide-ali.md)
