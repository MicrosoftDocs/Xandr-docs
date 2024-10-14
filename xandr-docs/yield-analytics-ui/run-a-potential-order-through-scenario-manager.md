---
title: Run a Potential Order through Scenario Manager
description: Scenario Manager allows testing sales proposals by creating new order lines for a product and analyzing potential revenue consequences.
ms.date: 11/06/2023
ms.custom: yield-analytics-ui
---

# Run a potential order through Scenario Manager

You can test sales proposals by creating one or more new order lines for a product and running them through Scenario Manager. The results enable you to study the potential revenue consequences of booking new order lines over the specified time period.

When you create a new order line by selecting a product first, you add the order line to the system. This means that every existing order line that's already running during the specified time period will be analyzed in the scenario.

There are three main steps to using Scenario Manager to run a simulated new order:

1. [Find the product and add it to Scenario Manager](#find-the-product-and-add-it-to-scenario-manager)
1. [Modify the new order line you're focusing on](#modify-the-new-order-line-you-are-focusing-on)
1. [Run and analyze the scenario](#run-and-analyze-the-scenario)

## Find the product and add it to Scenario Manager

You can add the product to Scenario Manager from the **Find Products** page. Or, complete the following process:

1. On the **Scenario Manager** page, from the **Scenario Time frame** dropdown menu, specify the time period for the scenario.
1. In the **Change Type** dropdown menu, choose **Select product for order line creation** and select **Go**.
1. On the **Find Products** page that is displayed, use the filer criteria to find the specific product.
1. Select for the product and select **Add to Scenario**.
1. Return to **Scenario Manager**.

The product that you added to Scenario Manager is displayed in the **New Order Lines** section.

## Modify the new order line you are focusing on

Make the changes that you want to simulate.

1. Select the checkbox for the product and select the **Edit** button.
1. In the **Edit Values** dialog, make changes to any of the following values:
    - Order
    - Advertiser
    - Order Line
    - Start Date
    - End Date
    - Priority
    - Type
    - Pricing Type
    - Sold Price
    - Impressions
    - State

1. Select **Update**.
1. (Optional) Repeat the above steps to create any additional new order lines for additional products.

If you include multiple new order lines in your simulation, you can apply the same changes to all of them at once by selecting their checkboxes, selecting the **Edit** button, making the changes, and selecting **Update**.

## Run and analyze the scenario

Run the scenario when you have finished editing one or more order lines. When the scenario is done running, you can analyze it to determine how it will impact delivery.

1. Select the **Run Scenario** button. The **Scenario** link in the upper-right corner of the page displays spinning arrows while Scenario Manager is running. You can let Scenario Manager run in the background while working on other tasks and tabs.
1. When the scenario has completed, select the **Scenario Summary** tab. This allows you to view a summary of revenue Gain, Losses, and Net Gain Loss, together with data for the number of order lines, orders, and products impacted by the modifications.

## Related topics

- [About Using Scenario Manager](./about-using-scenario-manager.md)
- [Anatomy of the Scenario Manager Page](./anatomy-of-the-scenario-manager-page.md)
- [Run an Existing Order Line Through Scenario Manager](./run-an-existing-order-line-through-scenario-manager.md)
- [Run an Existing Order Through Scenario Manager](./run-an-existing-order-through-scenario-manager.md)
- [Interpreting Scenario Manager Results](./interpreting-scenario-manager-results.md)
- [Anatomy of the Scenario Manager Page](./anatomy-of-the-scenario-manager-page.md)
