---
title: Microsoft Curate - Monitor Splits
description: Learn about monitoring curated deal splits using the Supply Shaping grid. Analyze spend, performance, and optimize delivery effectively.
ms.date: 11/14/2023
---

# Microsoft Curate - Monitor splits

You can monitor the delivery and performance of curated deal splits using two approaches:

1. Supply Shaping Grid
1. **Deal Metrics Troubleshooting** Report

## Supply shaping grid

1. To begin, navigate to **Package** -> **Curated Deal** screen and select the curated deal you wish to monitor.
1. Click the **Analytics** tab to bring up the splits monitoring grid.

The grid has two main column groups:

1. **Spend allocations**

    The Spend Allocations group is the first group of columns in the grid and shows you data from the last 24 hours:

    - **Natural** – The spend each split would have achieved without the spend allocation algorithm. It represents the maximum possible spend for the split.
    - **Configured** – The desired spend allocation set during split creation or editing.
    - **Achieved** – The actual spend delivered due to the allocation algorithm's participation rates.

   Use these columns to identify limiting splits—splits where the configured allocation significantly exceeds the natural allocation (e.g., a natural allocation of 20% versus a configured allocation of 80%). These splits restrict the deal’s overall delivery, as the algorithm must adjust other splits to meet this allocation.

   **Actions to Improve Deal Delivery**:

    - Lower the configured allocation for this split to bring it closer to its natural allocation.
    - Expand the targeting for this split to give it more potential to generate spend.
    - Reduce the margin for the split to enhance bid competitiveness.
    - Investigate and address high ineligible bid proportions.

1. **Analytics**

   This group provides lifetime deal data, including:

    - Performance metrics such as CPM, CPC, CTR, and viewability.
    - Custom Margin and Custom Floor settings for each split.

These columns are useful when optimizing for specific buyer KPIs. Adjust margins or floors to boost delivery for splits meeting the desired KPIs.

### Deal Metrics troubleshooting report

  1. Select the **Troubleshooting** tab and then open the **Troubleshooting Reports** panel.
  1. Under **Report Type**, select **Deal Metrics**, and under **Breakout Deal Metrics By**, select Split.

This report provides the availability of each split based on **Imps Matched** and **Bid Requests** metrics. It also shows buyer bidding activity using the **Bids** and **Imps Won** metrics and highlights splits generating significant volumes of **Ineligible Bids**.

Select the **Modify Columns** button to add other metrics, such as **Participation Rate**, to track how each split's rate has evolved over time.

## Related topics

- [Introduction To Splits](intro-to-splits.md)
- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Curator Supply Shaping](curator-supply-shaping.md)
- [Create Splits](create-splits.md)
- [Split Report Details](report-on-splits.md)
