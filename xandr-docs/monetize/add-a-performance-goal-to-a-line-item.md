---
title: Add a Performance Goal to a Line Item
description: In this article, find step-by-step instructions for how to add a performance goal to a line item.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Add a performance goal to a line item

> [!NOTE]
> Performance goals are not available for use with Guaranteed Line Items.

Performance goals (sometimes known as "primary KPIs") are a feature on the line item that helps you to make strategic decisions about the balance of performance and delivery for your campaigns. This page walks you through the process of adding a performance goal to a line item and fine-tuning performance goal settings to ensure your campaigns are succeeding.

> [!TIP]
> For a general overview of performance goals and key use cases, see [Understanding Performance Goals](understanding-performance-goals.md) and [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md).

## Step 1. Get started

To set a new performance goal, go to **Advertiser** > **All Advertisers** and click the advertiser you want to work with. This takes you to the **Advertiser Details** screen.

From the **Advertiser Details** screen, click **Line Items**. This takes you to the **Line Items** screen. You can either create a new line item and set a performance goal for it or add a performance goal to an existing line item.

### Add a performance goal to an existing line item

From the **Line Items** screen, mouse over the line item to which you want to add a performance goal and click the edit icon that appears.

### Add a performance goal to a new line item

You can also add a performance goal to a new line item during initial line item setup by clicking **+New** on the **Line Items** screen.

> [!TIP]
> To learn more about setting up a line item from start to finish, including performance goals, see [Create a Standard Line Item](create-a-standard-line-item.md).

## Step 2. Set the goal type

Optimization (to a performance goal) selections are made via the **Primary KPI** menu. You may set your line item to a primary KPI of CPC, CPA, or CTR.

> [!IMPORTANT]
> Optimization to a Primary KPI works in conjunction with CPM, CPC, or CPA revenue types when advertisers want to meet goals that are different from the payment types they have chosen (e.g., an advertiser wants to pay CPM but would like you to meet a $50 CPA primary KPI). For all campaigns under the line item, the Microsoft Advertising optimization engine will consider your entries in the **Optimization** section fields when deciding whether or not to bid on inventory.

For more information on the relationship between revenue and tracking, see [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md).

### Set a Primary KPI of CPC

Select this option if your advertiser wants to achieve a goal based on clicks. Note that this option is not available when your revenue type is CPC. Complete the **Track performance against client goal of $__** field, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if post-click eCPC is above __** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal of $__** field uses this value for reporting purposes only. The **Do not bid if post-click eCPC is above __** checkbox controls the bid/no bid decision.

### Set a Primary KPI of CPA

Select this option if your advertiser wants to achieve a goal based on conversions. When you select CPA as the goal type, you must then select the correct conversion pixel(s) to pay attention to. Then, complete the **Track performance against client goal of $__** field, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if post-click eCPA is above $__** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal of $__** field uses this value for reporting purposes only. The **Do not bid if post-click eCPA is above $__** checkbox controls the bid/no bid decision.

### Set a Primary KPI of CTR

Select this option if your advertiser wants to achieve a goal based on click-through-rate. Complete the **Track performance against client goal of $__** field, entering the performance goal your advertiser has given you. If you would like to set a bid/no bid decisioning limit, check the **Do not bid if CTR is below __%** checkbox and enter the limit in the empty field.

> [!NOTE]
> The **Track performance against client goal of $__** field uses this value for reporting purposes only. The **Do not bid if CTR is below __%** checkbox controls the bid/no bid decision.

## Step 3. Save the line item

When you have finished setting the performance goal for the line item, click the **Save** button. This takes you back to [Explore Line Items](explore-line-items.md). You can view the performance goals on the line item by hovering over the row for that line item and clicking the graph icon that appears. This takes you to [View Line Item Details](view-line-item-details.md), which contains details about all of the settings for that line item.

> [!NOTE]
> During learn, the Microsoft Advertising platform will continuously review the  campaign's performance and exclude low-performing inventory to help the campaign optimize faster. Once the campaign moves into the optimization phase, performance goals on the line item perform a bid/no bid check using the data collected in the learn phase to determine a valuation. The default threshold for moving into the optimization phase is three success events. This setting can be changed using the **Phase Thresholds** setting under **Optimization Levers** at the campaign level. For more details about optimization, see [Optimization Levers](optimization-levers.md).

## Related topics

- [Create a Standard Line Item](create-a-standard-line-item.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Explore Line Items](explore-line-items.md)
- [View Line Item Details](view-line-item-details.md)
- [Understanding Performance Goals](understanding-performance-goals.md)
- [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md)
