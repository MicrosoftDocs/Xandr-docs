---
title: Evaluate the Yield of an Order
description: In this article, explore step-by-step instructions on how to evaluate the yield of an order.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Evaluate the yield of an order

The following article explais about evaluation and other processes to measure the yield of an order.

## Process flow

Use the **Orders** tab and Evaluate Orders to see how a proposal is expected to deliver and be consumed.

1. On the **Orders** tab, in the **Order Tasks** panel, select **Evaluate Orders**.
1. Use the **Filters** panel to find the proposal to evaluate:
    - The Time Period filter searches the order's start date.
    - The Order, Order Status, Advertiser, Agency, Industry, and Salesperson filters search parameters imported from your order management system.
    - The Flags filter searches for orders that have pricing (! Price) or availability (! Avails) flags.
1. Select the order in the **Orders** panel list. A preview of the order appears in the **Order details** panel below.
1. In the **Order details** panel, select the name of the order to open it in **Evaluate Orders**, or select **View** and select **Evaluate Orders**.
1. In the **Key Metrics** panel of the **Order Analytics** tab of the **Evaluate Orders** page, view the bar charts to compare the selected order to all other orders, making any additional changes:
    1. Change the comparison basis by selecting **All Customers** and selecting one of the following four values:
        - All Customers
        - This Industry
        - This Agency
        - This Advertiser
    1. Change the time period for the comparison's underlying data. By default, the time period is the Last 365 Days.
1. On the **Order Composition** panel, view the two pie charts:
    - The Contracted Revenue by Pricing Type chart shows how much of the order's revenue is associated with CPM vs. CPD placements.
    - The Contracted Revenue by Contract Type pie chart shows how much of the order's revenue is associated with standard placements vs. sponsorships.
1. Select the **Order Lines** tab to evaluate order lines in the focus order. This uses filters to find specific order lines, and flags to highlight pricing or availability issues.

## Add a proposal to a scenario

You can add a proposal or an order to Scenario Manager to better understand how it impacts other orders.

1. On the **Orders** tab, in the **Order Tasks** panel, select **Evaluate Orders**.
1. In the **Evaluate Orders Search** page, in the **Orders** panel, select the order.
1. In the **Order preview** panel, select the order's name to open it in **Evaluate Orders**.
1. Select **Add to Scenario** at the top of the page. The order is added to a scenario.
1. Go to **Scenario Manager** to run the scenario.

## Use alternative products to solve pricing/availability issues

Alternative products are available in Evaluate Orders to help resolve ! Price and ! Avails flags.

### About alternate products

The score for an alternate product indicates how closely it's related to the order line's product, based on the following criteria:

- Alternate sizes – Products with the same targeting as the order line's product, but with a different value for Size.
- Audience affinity – Products that heavily overlap the same set of other products.
- Purchase behavior – Products that frequently appear together on the same orders.

### View alternate products

In the **Product Details** panel, select the **Alternate Products** tab.

### Add an alternate product to a proposal

1. Select the **Add** button to the left of the product's name. A new order line with the selected product is created at the top of the **Order Line Listing** above the **Product Details**.
1. Enter or change the order line parameters (e.g., Start date, End date, Imps) as needed.
1. Select **Update**.

To remove the order line, select **Edit** and clear the **Included** checkbox.

## Flags in evaluate orders

Use the flags in Evaluate Orders to find and resolve potential availability and pricing issues related to the line items on each proposal.

### Types of flags

There are three types of flags in Evaluate Orders:

- ! Price flags (CPM order lines only) indicate when the sold CPM value is either below the floor price or below the configured discount threshold.
- ! Avails flags indicate that a line item is targeting a product that does not have enough available impressions to accommodate the order line.
- ! Sellthru flags indicate that an order line is targeting a product that is more than 50% sold through, though the percentage is configurable for your agency.

## Related topics

- [Anatomy of the Evaluate Orders Page](anatomy-of-the-evaluate-orders-page.md)
- [Anatomy of the Evaluate Orders Search Page](anatomy-of-the-evaluate-orders-search-page.md)
