---
title: Microsoft Curate - Monitor Splits
description: Learn about monitoring curated deal splits using the Supply Shaping grid. Analyze spend, performance, and optimize delivery effectively.
ms.date: 11/14/2023
---

# Microsoft Curate - Monitor splits

You can monitor the delivery and performance of curated deal splits using two approaches:

1. Supply Shaping Grid
1. Deal Metrics Troubleshooting Report

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

    - Lower this split’s configured allocation to bring it closer to its natural allocation.
    - Expand the targeting of this split to give it more potential to generate spend.
    - Reduce the margin on the split to enhance bid competitiveness.
    - Investigate and address high proportions of ineligible bids.

1. **Analytics**

   This group provides lifetime deal data, including:

    - Performance metrics such as CPM, CPC, CTR, and viewability.
    - Custom Margin and Custom Floor settings for each split.

These columns are useful when optimizing for specific buyer KPIs. Adjust margins or floors to boost delivery for splits meeting the desired KPIs.

### Deal Metrics troubleshooting report

  1. Click the **Troubleshooting** tab.
  1. Open the **Troubleshooting Reports** panel.
  1. Select **Deal Metrics** as the report type and **Split** under **Breakout Deal Metrics** By.

This report provides insights into:

- **Imps Matched** and **Bid Requests**: Availability metrics for each split.
- **Bids** and **Imps Won**: Buyer bidding activity on each split.
- **Ineligible Bids**: High volumes of these may indicate issues to address.

You can also use the **Modify Columns** button to include metrics like **Participation Rate**, helping you track its evolution over time.

## Related topics

- [Introduction To Splits](intro-to-splits.md)
- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Curator Supply Shaping](curator-supply-shaping.md)
- [Create Splits](create-splits.md)
- [Report On Splits](report-on-splits.md)
