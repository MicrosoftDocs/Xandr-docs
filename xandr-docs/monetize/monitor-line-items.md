---
title: Microsoft Monetize - Monitor Line items 
description: This page is an overview on Line items. Learn how to access the Seller Monitoring Workflow (SMW) feature for Line items from any Microsoft Monetize screen.
ms.date: 10/28/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Monitor Line items

This document describes the Seller Monitoring Workflow (SMW) feature for Line items.

The **Line Items** screen displays **All**, **Upcoming**, **In Progress**, and **Completed** Line items and metrics. It also lets you search for Line items and related objects, apply filters, modify display columns, and download reports. 

## Access Seller Monitoring Workflow (SMW) for Line items:

To access the **Seller Monitoring Workflow (SMW)** feature for Line items:

1. Navigate to **Advertisers** > **Line Items** from the left pane. 
1. The **Line items** screen displays Line items in rows under four progress tabs: **All**, **Upcoming**, **In Progress**, or **Completed**. In the **Line items** window, select an appropriate progress tab to view the Line items:
    - **All** - All available Line items (includes upcoming, in progress, and completed Line items)
    - **Upcoming** - Line items that have not started.
    - **In Progress** - Line items between flights (start date/time of the first flight and end date/time of the last flight).
    - **Completed** – Line items that have completed and are past their end date/time of the last flight.

## Understand Line item columns

The **All**, **Upcoming**, **In Progress**, and **Completed** progress tabs each list Line items in rows. The rows include columns with the line item name and relevant metrics for the Line items.

Hover over the tooltips next to each metric at the top of each column for a brief description of the metric. The metrics provide important information about upcoming, in progress, and completed Line items without requiring you to run a report. The metrics are updated regularly.

> [!NOTE]
> There might be discrepancies between the metrics displayed in the **Line items** monitoring view and reporting data due to slight variations in data syncing. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Search for Line items

There are several ways to search for Line items from the **Line items** window. You can search for Line items by Line item name, Line item ID, Deal name, or Deal ID. Inactive Line items are listed in gray italic text.

## Use pagination

If you don't have a Line item name, Line item ID, Deal name, or Deal ID to search with, you can use the pagination feature at the bottom of the **Line items** window to page through the rows of Line items. The pagination feature lets you:

- Select the number of rows that you want to display per page by selecting a value from the **Rows per page** menu.
- Enter a specific page in the designated text field or click the arrows to navigate from page to page.

## Apply filters

You can create and save filters to search for Line items. Once created and saved, you can apply a filter using the **Select a Filter** drop-down list. To create and save a new filter:

1. In the **Line items** screen, click **Advanced Filters**.

1. Make your selections.

1. Click the dropdown arrow on the **Apply** button.

1. Select **Apply and Save As**.

1. Enter a name for the new filter in the **New Filter Name** field.

    > [!NOTE]
    > You can save up to 10 filters. If you already have 10 filters and want to add a new filter, delete an existing filter and try again.

1. Select the **Make Default** checkbox to apply the filter to the rows by default.

    > [!NOTE]
    > The default filter will apply each time you access the **Line items** window.

1. Click **Apply** and **Save As** to save the filter.

    All saved filters appear in the **Select a Filter** drop-down. To remove an applied filter, click **Clear All**. To edit an applied filter, click **Edit** to open the **Advanced** **Filters** dialog (see Step 2 above).

You can edit saved filters at any time. To edit a saved filter:

1. In the **Line items** window, click **Advanced Filters**.
1. In the **Advanced Filters** pane, select a filter using the **Select a Setting** drop-down.
1. Once a setting is selected, you have options to **Deselect Filter**, **Make Default, Rename**, or **Delete**. You can also make any changes to the filter configurations displayed as you scroll through the **Advanced Filters** pane.
1. Click **Apply and Save** to apply your changes and save the filter.

## Sort columns

You can sort most Line item rows in the **Line items** screen into ascending or descending order by clicking each column label.

## Select column views

You can select any available column views in the **Select a View** drop-down. To reset the column view when a view is selected, click the drop-down arrow next to the selected view and click **Select a View**.

## Modify and save column views

You can modify and save column views. Saving a column view makes it available in the **Select a View** drop-down list. To modify a column view:

1. In the **Line items** screen, click **Modify Columns**.
1. In the **Modify** Columns pane, select the appropriate progress tab (**All**, **Upcoming**, **In Progress**, or **Completed**).
1. Select (to show) or deselect (to hide) any column checkboxes. You can also choose **Select all**/**Deselect all** to select or deselect all columns for the progress tab.
1. Optionally, you can rearrange the columns by dragging and dropping them.
1. Do one of the following:
    - To apply the view to the current session, click **Apply**.
    - To apply and save the view so it's available in the **Select a View** drop-down list:
      1. Select the drop-down arrow next to **Apply** and select **Apply and Save As**.
      1. Enter a name for the new column setting in **New Setting Name**.
      1. Optionally, check **Make Default** if you want this column setting to be the default view.
      1. Click **Apply and Save As**.

## View Line item details

To view the details of a Line item listed in the **Line items** window, click anywhere in the Line item row to display the Line Item Details. See [View Line Item Details](view-line-item-details-smw.md) for more information.

## Duplicate, Activate, Deactivate, Delete, or Run report for selected Line items

You can Duplicate, Activate, Deactivate, Delete, or Run a report for selected Line items, by doing the following:

1. In the **Line items** window for each progress tab (**All**, **Upcoming**, **In Progress**, or **Completed**), select the checkbox to the left of any Line items.
1. When Line items are selected, the **Line items selected** bar is available at the top of the **Line items** window with the following available actions you can perform by clicking on the action:
    - **Duplicate** - You can duplicate one or more Line items simultaneously.<br>**Note**:When duplicating a line item with a start date in the past, the duplicate line item's start date will be set to ‘Today.’ For PG line items, it will be set to ’Tomorrow.’ All other line items will retain the original flight dates.
    - **Activate** - You can activate one or more Line items simultaneously.
    - **Deactivate** - You can deactivate one or more Line items simultaneously.
    - **Delete** - You can delete one or more Line items simultaneously.
      > [!WARNING]
      > Deleting a line item deletes all its child objects, including creatives, conversion pixels, segments, and splits. Deletions are permanent and cannot be reverted
    - **Run Report** - You can run reports for one or more Line items simultaneously. See [Network Reporting](network-reporting.md) for more information.
 
 <!-- **Cancel Reservation** - for Guaranteed Delivery Line items (GDLI) and Programmatic Guaranteed Line items (PGLI), you can cancel the reservation of one or more of these Line items.-->

## Data availability

Object details such as line item name and flight dates are updated immediately in SMW. However, metrics like impressions, revenue, media cost, and CTR are not available in real time. These can lag behind Network Analytics data by up to three hours.

If you run an analytics report for a line item that’s currently active and includes data from the last three hours (or six hours for real-time analytics metrics), expect discrepancies — SMW may not yet reflect the most recent data.

Minor differences at the cent level are also normal, as data aggregation methods differ between systems.

Deal metrics such as Imps Matched, Bid Requests, Bids, Wins, Renders and Ineligible Bids are available in real-time. 

### Metrics in SMW grid

| **Metric**               | **Scope**              | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                            | **Base Report**               | **Supports Real Time** |
|---------------------------|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|-------------------------|
| **Imps Matched**          | Deals                  | The count of available impressions matching the deal's targeting and buyer's deal acceptance status.                                                                                                                                                                                                                                                                                                                                                          | Seller Deal Metrics           | Yes                     |
| **Bid Requests**          | Deals                  | The count of requests sent to the buyer with the deal included. Bid Request Rate can be calculated by dividing Bid Requests by Imps Matched.                                                                                                                                                                                                                                                                                                                  | Seller Deal Metrics           | Yes                     |
| **Bids**                  | Deals                  | The count of deal auctions with a bid from the buyer. This metric represents the presence of a single bid per buyer, even if the buyer bids multiple times on the same auction. Bid Rate can be calculated by dividing Bids by Bid Requests.                                                                                                                                                                                                                   | Seller Deal Metrics           | Yes                     |
| **Wins**                  | Deals                  | The count of bids that successfully won the Xandr auction. This metric does not account for secondary auctions. Win Rate can be calculated by dividing Wins by Bids.                                                                                                                                                                                                                                                                                          | Seller Deal Metrics           | Yes                     |
| **Renders**               | Deals                  | The count of successful creative renders on the deal. Render Rate can be calculated by dividing Renders by Wins.                                                                                                                                                                                                                                                                                                                                              | Seller Deal Metrics           | Yes                     |
| **Ineligible Bids**       | Deals                  | The count of bids that were rejected on the deal. Ineligible Bid Rate can be calculated by dividing Ineligible Bids by total Bids from a buyer on an impression, including when a buyer bids multiple times on a single auction.                                                                                                                                                                                                                                | Seller Deal Metrics           | Yes                     |
| **Pacing**                | Guaranteed Delivery    | Percentage of delivered budget relative to expected budget based on flight progress (assuming even distribution across all hours of the flight). Roadblock delivery is based on the master creative only. <br> **Note:** Line item must have a defined lifetime budget to display pacing. Daypart targeting is not accounted for in pacing; lines may indicate overpacing. <br><br> ≥101%: **PURPLE** <br> 100–101%: **GREEN** <br> 85–99%: **YELLOW** <br> <85%: **ORANGE** | –                             | No                      |
| **Last 60 Minutes Delivery** | Line Items and Deals | Delivery over the last 60 minutes. For roadblock line items, delivery represents both master and companion impressions.                                                                                                                                                                                                                                                                                                                                       | Network Analytics (Real-time)  | Yes                     |
| **Impressions**           | Line Items and Deals   | Impressions delivered during the flight. Guaranteed roadblock line items will show master creative impressions only.                                                                                                                                                                                                                                                                                                                                          | Network Analytics             | No                      |
| **Clicks**                | Line Items and Deals   | The number of clicks recorded.                                                                                                                                                                                                                                                                                                                                                                                                                                | Network Analytics             | No                      |
| **CTR**                   | Line Items and Deals   | The number of clicks divided by the number of impressions.                                                                                                                                                                                                                                                                                                                                                                                                    | Network Analytics             | No                      |
| **Revenue**               | Line Items and Deals   | Revenue delivered during the flight based on the line item's currency.                                                                                                                                                                                                                                                                                                                                                                                        | Network Analytics             | No                      |
| **Conversions**           | Line Items and Deals   | The number of conversions.                                                                                                                                                                                                                                                                                                                                                                                                                                    | Network Analytics             | No                      |
| **Viewability**           | Line Items and Deals   | The number of viewable imps divided by the number of view measurable imps.                                                                                                                                                                                                                                                                                                                                                                                    | Network Analytics             | No                      |
| **Viewable Imps**         | Line Items and Deals   | The number of impressions that could be measured for viewability.                                                                                                                                                                                                                                                                                                                                                                                             | Network Analytics             | No                      |
| **Video Comp Rate**       | Line Items and Deals   | The number of video completions divided by the number of impressions.                                                                                                                                                                                                                                                                                                                                                                                         | Network Analytics             | No                      |
| **Expected Delivery**     | Line Items and Deals   | –                                                                                                                                                                                                                                                                                                                                                                                                                                                             | –                             | Yes                     |
| **Rev eCPC**              | Line Items and Deals   | The revenue per click.                                                                                                                                                                                                                                                                                                                                                                                                                                        | Network Analytics             | No                      |
| **Rev eCPM**              | Line Items and Deals   | The revenue per 1000 impressions.                                                                                                                                                                                                                                                                                                                                                                                                                             | Network Analytics             | No                      |
| **Rev eCPA**              | Line Items and Deals   | The revenue per conversion.                                                                                                                                                                                                                                                                                                                                                                                                                                   | Network Analytics             | No                      |
| **Pulse**                 | Line Items and Deals   | Today's impression delivery as of midnight. Data resets every day.                                                                                                                                                                                                                                                                                                                                                                                            | –                             | Yes                     |


### Line-Item Analytics Tab 

The top chart showing active delivery is real-time data from the last 60 minutes. All other data on the analytics tab is not real-time. 

### Deal History Tab 

The last 60 minutes time selection shows real-time data. Other time selections do not include real time data. 


## Related topics

- [Troubleshoot Line items](troubleshoot-line-items.md)
- [View Line Item Details](view-line-item-details-smw.md)
