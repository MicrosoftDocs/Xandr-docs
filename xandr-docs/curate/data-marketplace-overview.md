---
title: Microsoft Curate - Data Marketplace Overview
description: Learn how to enable data providers, target Data Marketplace segments in curated deals, manage data costs, and review reporting and billing.
ms.date: 09/10/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: v-garittar
---

# Microsoft Curate - Data Marketplace Overview

The Data Marketplace brings together data offerings from a variety of third-party providers. It automatically calculates and clears costs for third-party data used in curated deals.

Available segments include both addressable and non-addressable data and support use cases such as:

- Brand safety
- Demographic targeting
- Semantic targeting

To contact a data provider, see [Data Marketplace Partners](data-marketplace-partners.md).

## Get started

Before you can use Data Marketplace segments, you must enable the data providers you want to work with.

1. Go to **Audiences** > **Segment Manager**.
1. Select **Manage Data Providers**.

    > [!NOTE]
    > If you don't see this option, contact your account representative.

1. Select the data providers you want to use, then select **Save**.
1. Select **Segment Manager** to return to the segment list.
1. Open the **Data Marketplace** tab to view available segments and pricing from your enabled providers.

When you use Data Marketplace segments in curated deals, Microsoft automatically calculates and clears applicable data costs.

> [!NOTE]
> After enabling a provider, it can take 2 to 4 hours for its segments to appear in the **Data Marketplace** tab.

## Target Data Marketplace segments

You can use Data Marketplace segments when creating or editing a curated deal.

1. Under **Basic Settings**, select the edit icon next to **Segment Targeting** and open the **Data Marketplace** tab.
1. Browse available segments or use search and filters to find specific segments.

    Available filters include:

    - Data Provider
    - Ad Type
    - Device Type
    - Segment Type
    - Geography

1. Combine Data Marketplace segments with first-party segments using the same Boolean targeting logic. For more information, see [Segment Targeting](segment-targeting.md).
1. As you build your targeting criteria, an estimated data cost is displayed. This estimate reflects the pricing methodologies used by the selected data providers.

    The estimate is shown as a range because actual costs can vary by auction depending on which segments are available.

    For more information, see [Data Cost Calculation](data-cost-calculation.md).

1. To view audience overlap across multiple selected segments, select **View Overlap Visualization**.

## Manage data costs

If you have permission to apply a margin to curated deals, the **Automatically increase margin to cover vendor costs** option is selected by default in the **Margin Type** section.

When enabled, your margin automatically increases during each auction to cover the exact data costs incurred.

### Example

| Item | Value |
| :--- | :--- |
| Buyer's bid | $7.00 |
| Curator margin | 10% |
| Data cost | $0.25 |
| Total curator deduction | $0.95 |

Calculation:

`(10% × $7.00) + $0.25 = $0.95`

If this option is disabled, only your configured margin is deducted. In this example, the curator margin would be **$0.70**.

> [!NOTE]
> Data costs calculated at auction time do not include applicable sales tax. Any required sales tax is automatically added to data costs when invoiced.

## Report on data costs

You can track data costs using the following reports.

### Curator Analytics Report

Use:

- **Vendor Costs** to view total data costs accumulated for a curated deal.
- **Incremental Curator Margin** to view any additional margin collected to cover those costs.

For more information, see [Curator Analytics Report](curator-analytics-report.md).

### Curator Vendor Usage Report

Use:

- **Imps**
- **Vendor Costs**

These metrics provide a detailed breakdown of costs by:

- Deal
- Vendor (data provider)
- Targeted segment
- Other available dimensions

For more information, see [Curator Vendor Usage Report](curator-vendor-usage-report.md).

## Invoices and statements

If you use Data Marketplace segments and incur data costs during a billing month, you will receive an invoice that includes a **Cost of Segment Data** line item. This amount reflects your total data costs, including any applicable sales tax.

If you enable **Automatically increase margin to cover vendor costs**, the **Curator Margin** line item on your Seller Activity Statement includes the additional margin collected to cover those costs.

> [!IMPORTANT]
> Cost of Segment Data charges and Curator Margin amounts are not netted on the Seller Remittance Statement. You must pay the invoice amount by the invoice due date.
