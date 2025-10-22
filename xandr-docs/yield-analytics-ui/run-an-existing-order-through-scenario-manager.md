---
title: Run an Existing Order through Scenario Manager
description: Use Scenario Manager to simulate how changes to an existing order would deliver and impact other products.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Run an existing order through Scenario Manager

Run an existing order through Scenario Manager to simulate how changes to it would deliver and impact other products.

There are three main steps to using Scenario Manager to run a simulated change on an order:

1. [Find the order and add it to Scenario Manager](#find-the-order-and-add-it-to-scenario-manager)
1. [Modify the order you're focusing on](#modify-the-order-you-are-focusing-on)
1. [Run and analyze the scenario](#run-and-analyze-the-scenario)

## Find the order and add it to Scenario Manager

You can add the order to Scenario Manager from its **Order Visibility** page. Or complete the following process:

1. On the **Scenario Manager** page, from the **Scenario Time frame** dropdown menu, specify the time period for the scenario.
1. In the **Change Type** dropdown menu, choose **Select order to modify** and select **Go**.
1. On the **Find Orders** page that is displayed, use the filer criteria to find the specific order.
1. Select for the order and select **Add to Scenario**.
1. Return to **Scenario Manager**.

The orders that you added to Scenario Manager appear twice:

- The Old order shows the original values, which you can't change in Scenario Manager. It is displayed for your comparison.
- The New order is the order that you edit to run the simulation.

## Modify the order you are focusing on

Make the changes that you want to simulate.

1. Select the **New** checkbox for the order and select the **Edit** button. If needed, you can search again for additional orders to include in your simulation.
1. In the **Edit Values** dialog, make changes to any of the following values:
    - Start Date
    - End Date
    - Priority
    - Type
    - Pricing Type
    - Sold Price
    - Impressions
    - State
1. Select **Update**. The changes that you made are displayed in red. You can compare this to the old version above.

If you include multiple orders in your simulation, you can apply the same changes to all at once by selecting their checkboxes, selecting the **Edit** button, making the changes, and selecting **Update**.

## Run and analyze the scenario

Run the scenario when you have finished editing one or more order lines. When the scenario is done running, you can analyze it to determine how it will affect delivery.

1. Select the **Run Scenario** button. The **Scenario** link in the upper-right corner of the page displays spinning arrows while Scenario Manager is running. You can let Scenario Manager run in the background while working on other tasks and tabs.
1. When the scenario has completed, select the **Scenario Summary** tab to view a summary of revenue Gain, Losses, and Net Gain Loss, You can also view data for the number of order lines, orders, and products impacted by the modifications.

## Related topics

- [About Using Scenario Manager](./about-using-scenario-manager.md)
- [Anatomy of the Scenario Manager Page](./anatomy-of-the-scenario-manager-page.md)
- [Run a Potential Order Through Scenario Manager](./run-a-potential-order-through-scenario-manager.md)
- [Run an Existing Order Line Through Scenario Manager](./run-an-existing-order-line-through-scenario-manager.md)
- [Interpreting Scenario Manager Results](./interpreting-scenario-manager-results.md)
- [Anatomy of the Scenario Manager Page](./anatomy-of-the-scenario-manager-page.md)
