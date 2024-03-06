---
title: Shorten the Targeted Learn Phase Using Bid Type Reports
description: Explore Bid Type reports to expedite learning for new goals in campaigns and this is applicable solely to legacy line items.
ms.date: 10/28/2023
---

# Shorten the targeted learn phase using bid type reports

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

Whether you optimize to a percentage margin or a predicted performance goal (e.g., CPC or CPA), a new campaign will need to buy inventory and use the Microsoft Advertising optimization engine to learn which groupings of inventory will deliver the desired performance.

During this learning phase, a percentage of your budget will be spent in venues that will not necessarily deliver the results expected (so that our optimization can learn what performs best). If you are under a tight budget or timeline, there are a few things you could do to help speed up the [Learn Budget](learn-budget.md) process and reduce budget spending in areas that are not performing. This page outlines one of these manual optimization tips: using Bid Type reports for inventory exclusion.

## Step 1: Create a bid type report

To perform manual optimization use the Bid Type report. This report can be run at either the Network or the Advertiser levels. To create the Bid Type Report:

1. Go to **Reporting** and select **Analytics Report** from the **Type** pull-down.
1. Filter by the **campaign** you are interested in analyzing.
1. Use the following **dimensions**: **Seller**, **Publisher**, **Placement**, and **Bid Type**.

## Step 2: Analyze by bid types

The report will show you exactly which placements within a publisher are still in the learn phase by displaying **learn** in the **Bid Type** column.

> [!IMPORTANT]
> Visit the Bid Type Definitions in the [Advertiser Reporting](advertiser-reporting.md) page to learn more about bid types in Microsoft Advertising.

By analyzing the performance of placements in learn phase, you can begin to derive three main criteria:

- **Placements to exclude**: placements where performance has been poor and cost higher than average.
- **Placements to watch**: placements where the data points are still inconclusive and you therefore need to observe for a little longer.
- **Placements to keep**: placements where performance is pointing in the right direction and will potentially move into optimized soon.

> [!NOTE]
> The criteria suggested above is not exhaustive. Depending on the complexity of this analysis, you might derive additional ways of classifying your data and refining the selection of inventory to exclude.

The end goal of this step is to create a list of placements to remove from your campaign targeting. The broader objectives are:

- To focus spend on the most promising placements still in learn.
- To stop campaign spend on placements where the current trajectory
  indicates the desired performance is unlikely to ever be attained.

In some instances, you may want to aggregate reporting at the Publisher or even Seller level to assess performance in a more general way. This aggregation would allow you to be more aggressive with your exclusions (e.g., instead of using individual placements, you could exclude an entire publisher).

## Step 3: Exclude inventory by publisher or placement ID

Now that you have that list of placements (or perhaps even publishers) you would like to exclude, select **Campaign Manager**. In your campaign under **Targeting** \>  **Inventory**, click **Edit**. Select **3rd Party Inventory**, switch to **text** mode, and choose to target **placement**. Enter the IDs of the placements you wish to exclude. To exclude entire publishers instead of just placements, select **publishers** from the menu.

Click the **Exclude** button and click **Add** to confirm the action. **Save** your changes in the **Campaign Manager**.
