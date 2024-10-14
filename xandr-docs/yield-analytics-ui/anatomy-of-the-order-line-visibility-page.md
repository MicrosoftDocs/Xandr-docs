---
title: Anatomy of Order Line Visibility Page
description: In this article, learn the layout of the Order Line Visibility page.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Anatomy of Order Line Visibility page

The Order Line Visibility page on the **Orders** tab shows an order line's details, flighting, and delivery, as well as any competing order lines.

## Order Line Visibility page

There are several sections on the **Order Line Visibility** page:

- **Header** - Displays the order line name, order line status, and underdelivery warning (if applicable). The header also contains the following functions:
  - **Date range filter** - Specify a standard or custom time period. Lifetime data (the range between the start and end dates) is displayed by default. Data on the screen automatically updates based on the dates you select.
  - **Export drop-down list** - Export data and/or charts into the following formats:
    - Complete report (.xls) - Excel file of complete line details, performance charts, filters, and sources.
    - Chart (.xls) - Excel file containing performance chart data.
    - Chart (.png) - .png image file of the chart as it appears on screen, at the time of export.
    - Chart (.pdf) - .pdf image file of the chart as it appears on screen, at the time of export.
  - **Actions drop-down list**
    - Add to Scenario - Available only if you use Scenario Manager. View how changing the order line's priority affects related products.
    - View in Reports - View order line information on the **Reports** tab.

- **Order line details panel** - Displays the latest details for the line. Data in this section is not affected by filters elsewhere on the screen. Select the down arrow next to the panel heading to expand and collapse each section as needed.
  - **Basics** - Displays basic information including the order line, flight dates, order line ID, order and advertiser links, industry, and salesperson.
  - **Targeting** - Displays targeting information for the order line including sold as, trafficked as, expression, priority, frequency, and flight method.
  - **Contract** - Displays contract and pricing type, rate, and inventory class for the order line.

- **Dashboard** – Displays metrics you commonly use for order line analysis. Wherever applicable, both lifetime and date range values are displayed for each metric so you can easily compare information. These values are automatically updated based on the date range you select in the header, and color-coded to match the performance chart. The following metrics are displayed in the dashboard:
  - Contracted Revenue
  - Earned Revenue
  - Contracted Impressions
  - Scheduled Impressions
  - Consumed Impressions
  - Product Availability (for the order lines "trafficked as" product)
  - Product Capacity (for the order lines "trafficked as" product)
  - Delivered Clicks
  - Click Thru Rate
  - eCPM
  - Pacing
  - C:S %
  - Revenue Against Goal

  > [!NOTE]
  > Metric values that are not included in the chart are displayed in red when they are negative.

- **Performance chart** - Displays a graphic chart of the order line's flight by specified metric. By default, the chart displays all data that is available. You can change the chart by selecting a grouping (daily, weekly, monthly, quarterly, or yearly) and metric (Contracted Revenue vs. Earned Revenue, Scheduled Impressions, Consumed Impressions, and Consumption to Schedule, or Click Thru Rate vs. Consumed Clicks).
  - The horizontal axis displays the flight date range, whereas the vertical axes reflect the metric you selected.
  - Data is color-coded for easy analysis and matches the colors in the dashboard section. When you mouse over any data point on the chart, a tool tip is displayed that describes the metric data.
  - A green vertical line on the graph represents the historical/forecast boundary.
  - Changes made to order line targeting are expressed in the chart using "T" icons. Select the icon to view the details in the **History** tab.

- **Tabs**  
  - **Competition** (default) - Displays a list of all competing order lines, with links to view their details. For example, if you want to know why a line item is expected to underperform for a certain date, you can check for any competing sponsorships on that day. You can then proactively optimize to run the order line in another space (e.g, change the geotargeting to the entire state instead of a specific city). You can choose to display competing lines by priority and time. Expand a row to view order and order ID information for the competing line.
  - **Consumption** - Displays where the order line is delivering, the products it overlaps with and is contained by, and links to view them.
  - **History** - Displays a basic change log where you can view changes to the target expression and status for a line.
  - **Notes** - Displays information about order line performance including, but not limited to, uneven delivery and forecasting issues (e.g., This order line has consumed impressions outside of its schedule; the effective date range that includes all days during which it delivered is from 08/20/2014 through 09/20/2014.).

## Related topics

- [About the Orders Tab](about-the-orders-tab.md)
- [Anatomy of the Orders Dashboard Page](anatomy-of-the-orders-dashboard-page.md)
- [Find an Order Line](find-an-order-line.md)
- [Check Revenue Against Goal](check-revenue-against-goal.md)
- [Find Orders](find-orders.md)
- [View the Full Details of an Order or Order Line](view-the-full-details-of-an-order-or-order-line.md)
- [Solving Delivery Issues with Order Line Visibility](solve-delivery-issues-with-order-line-visibility.md)
