---
title: Anatomy of Order Visibility Page
description: In this article, learn the layout of the Order Visibility page.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Anatomy of Order Visibility page

The Order Visibility page on the **Orders** tab shows basic information about the order, as well as the order lines it contains. Select an order line's name to display its **Order Line Visibility** page. This shows the order line's flighting and delivery, as well as any competing order lines.

## Order Visibility page

There are several sections on the **Order Visibility** page:

- **Header** - Displays the order line name, order status, and underdelivery warning (if applicable). The header also contains the following functions:
  - **Date range filter** - Specify a standard or custom time period. Lifetime data (the range between the start and end dates) is displayed by default. Data on the screen automatically updates based on the dates you select.
  - **Export drop-down list** - Export data and/or charts into the following formats:
    - Complete report (.xls) - Excel file of complete line details, performance charts, filters, and sources.
    - Chart (.xls) - Excel file containing performance chart data.
    - Chart (.png) - .png image file of the chart, as it appears on screen at the time of export.
    - Chart (.pdf) - .pdf image file of the chart, as it appears on screen at the time of export.
  - **Actions drop-down list**
    - Add to Scenario - Available only if you use Scenario Manager. View how changing the order line's priority affects related products.
    - View in Reports - View order line information on the **Reports** tab.

- **Order details panel** - Displays the latest details for the order. Data in this section is not affected by filters elsewhere on the screen. Select the down arrow next to the panel heading to expand and collapse as needed.
  - **Basics** - Displays basic information about the order. This includes the order name, flight dates, order line ID, order and advertiser links, industry, and salesperson.

- **Dashboard** – Displays a quick overview of order performance with metrics you commonly use for order analysis. Wherever applicable, both lifetime and date range values are displayed for each metric, so you can easily compare information. These values are automatically updated based on the date range you select in the header, and color-coded to match the performance chart. The following metrics are displayed in the dashboard:
  - Contracted Revenue
  - Earned Revenue
  - Contracted Impressions
  - Scheduled Impressions
    - Consumed Impressions
    - eCPM
    - Pacing
    - C:S %
    - Revenue Against Goal
    - Delivered Clicks
    - Click Thru Rate

    > [!NOTE]
    > If a metric appears in the dashboard, but not in the performance chart, it may appear in red text.

- **Performance chart** - Displays a graphic chart of the order's performance based on revenue or impressions. You can change the chart by selecting a group (daily, weekly, monthly, quarterly, or yearly), and metric (impressions, revenue, or clicks). The horizontal axis displays the flight date range, whereas the vertical axes reflect the metric you selected. Data is color-coded for easy analysis and matches the colors in the dashboard section. When you mouse over any data point on the chart, a tool tip is displayed that describes the metric data. A green vertical line on the graph represents the historical/forecast boundary.

- **Order Lines** – Displays a summary or expanded view of all lines in the order. If you choose to view cancelled lines, these lines will be included in metric data in the **Dashboard** and **Performance chart**. Order lines projected to underdeliver are flagged with a warning.

## Report on orders

If you use the **Reports** tab, select the Advertiser name in the order Basics panel to open a pre-configured report to analyze the order. For consistent reporting, the **Dashboard** uses the same metrics that are available in the **Reports** tab.

## Related topics

- [About the Orders Tab](about-the-orders-tab.md)
- [Anatomy of the Orders Dashboard Page](anatomy-of-the-orders-dashboard-page.md)
- [Find Orders](find-orders.md)
- [Find an Order Line](find-an-order-line.md)
- [Check Revenue Against Goal](check-revenue-against-goal.md)
- [View the Full Details of an Order or Order Line](view-the-full-details-of-an-order-or-order-line.md)
- [Solving Delivery Issues with Order Line Visibility](solve-delivery-issues-with-order-line-visibility.md)
