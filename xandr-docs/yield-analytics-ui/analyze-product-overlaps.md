---
title: Analyze Product Overlaps
description: In this article, follow our step-by-step instructions for analyzing overlapping impressions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Analyze product overlaps

Using the **Audience Planner** page, you can identify products with overlapping impressions or overlapping audiences. Overlap analysis is particularly useful for packaging products, exploring similar inventory, and extending reach.

## Analyze overlapping impressions

By analyzing overlapping impressions, you can compare how impressions are shared between a selected focus product, or set of target attributes and the products that overlap it.

1. On the **Products Dashboard** page, in the Products Tasks panel, select **Analyze Overlaps**. The Audience Planner page appears.

1. In the **Configuration** panel on the left side of the page, select the criteria for your analysis as follows:

      > [!IMPORTANT]
      > By default, the analysis on the right side of the page is refreshed automatically as you select your configuration criteria. To manually update your analysis instead, change the **Update** field from **Automatic** to **Manual**. You will then be prompted to update when you make changes to your configuration.

    - In the **Focus Product or Attribute** fields, select the link for the current selection (e.g., None). In the Focus Product or Attribute dialog that appears, choose either the product you want to analyze (on the **Products** tab), or choose a set of target attributes on which to focus your analysis (on the **Attributes** tab). Select **Update**.
    - In the **Primary Metric** field, select **Overlapping Impressions**.
    - Specify whether you want to show non-overlapping impressions.
      Choose whether you want analysis results to be sorted in ascending or descending order.

1. (Optional) In the **Filters** panel, you can narrow the analysis as follows:

    > [!IMPORTANT]
    > By default, the analysis on the right side of the page is refreshed automatically as you select your filter options. However, if you turned off automatic updating (see the warning in step 2), you will be prompted to update the analysis as you make changes to your filter options.  

    - Select a different time period for analysis (the current month is selected by default).
    - Select one or more product groups.
    - Select one or more target attributes.
    - Select a parent product.
    - Select one or more specific products.
    - Select one or more product types (rate type products are displayed by default). For more information on product types, see [Products Overview](products-overview.md).
    - Select one or more specific overlap types. For more information on overlap types, see [Overlap Types](overlap-types.md).
    - Specify whether to show products with overlapping values of zero.

1. To see details on how a product in the analysis chart overlaps with the focus product (and with other overlapping products), mouse over the bar for the product. A tooltip appears.

    > [!NOTE]
    >
    > - Overlap as % of Focus = The percentage of overlapping impressions shared by the focus product and comparison product. This is based on the capacity of the focus product.
    > - Overlap as % of Comparison = The percentage of overlapping impressions shared by the focus product and comparison product. This is based on the capacity of the comparison product.

1. To view the analysis in a table instead of the default chart view, above the Configuration panel, select the list view button. The analysis chart is redisplayed as a product list - with performance metrics for the focus product and each overlapping product.

## Analyze overlapping audiences

By analyzing audience index instead of overlapping impressions, you can determine where audience is heavily overlapping between products, using a particular baseline. For example, if you begin with a baseline target of "Men 18-24" and choose "Analyzed Network" as the baseline, there may be certain products that have a disproportionately higher audience of young males when compared to the site as a whole.

The image below details how to understand the chart when looking at overlapping audience data, or when the 'Show Non-Overlapping Impression' option in the Configuration Setting is set to 'yes':

[image]

> [!NOTE]
> The main metric in this analysis is Audience Index Compared to Baseline. This is calculated as follows:
>
> Overlap as a percentage of the comparison product / Overlap as a percentage of the baseline product.

1. On the **Products Dashboard** page, in the Products Tasks panel, select **Analyze Overlaps**. The Audience Planner page appears by default. The product list is filtered to show active rate card products.

1. In the **Configuration** panel on the left side of the page, select the criteria for your analysis as follows:

    > [!IMPORTANT]
    > By default, the analysis on the right side of the page is refreshed automatically as you select your criteria. You can turn off this feature and update your analysis manually by selecting **Automatic** in the **Update** field and selecting **Manual** from the drop-down list that appears.

    - In the **Focus Product or Attribute** field, select the link for the current selection (e.g., None). In the Focus Product or Attribute dialog that appears, choose either the product you want to analyze (on the **Products** tab), or choose a set of target attributes on which to base your analysis (on the **Attributes** tab).
      Select **Update**.
    - In the **Primary Metric** field, select **Audience Index**.
    - By default, the baseline for your analysis is the full analyzed network. To use a specific product instead, select one in the **Baseline Product** field.
    - Specify whether you want analysis results to be sorted in ascending or descending order.

1. (Optional) In the **Filters** panel, you can narrow the analysis as follows:
    - Select a different time period for analysis.
    - Select one or more product groups.
    - Select one or more target attributes.
    - Select a parent product.
    - Select one or more specific products.
    - Select one or more product types (rate type products are displayed by default). For more information on product types, see [Products Overview](products-overview.md).
    - Select one or more specific overlap types. For more information on overlap types, see [Overlap Types](overlap-types.md).
    - Specify whether to show products with overlapping values of zero.

1. To see details on how the audience index for a product in the analysis chart compares to the audience index for the baseline product, mouse over the bar for the product. A tooltip appears.

1. To view the analysis in a table instead of the default chart view, above the Configuration panel, select on the list view button. The analysis chart is redisplayed as a product list with performance metrics for the focus product, and each overlapping product.

## Related topics

- [Anatomy of the Audience Planner Page](anatomy-of-the-audience-planner-page.md)
- [Overlap Types](overlap-types.md)
- [Products Overview](products-overview.md)
