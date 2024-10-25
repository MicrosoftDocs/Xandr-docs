---
title: Microsoft Curate - Monitor Line Items
description: In this article, learn how to access line item monitoring, understand line item metrics, search for related objects, apply filters, modify display columns, and download reports.
ms.date: 10/28/2023
---

# Microsoft Curate - Monitor line items

The **Line Items** screen displays **Upcoming**, **In Progress**, and **Completed** line items and metrics. It also lets you search for line items and related objects, apply filters, modify display columns, and download reports.

## Access monitoring

To access the **Monitoring** feature from any Microsoft Curate screen:

1. Select the **Package** menu and select **Curated Deals**.
1. In the **Line Items** window, select an appropriate progress tab (**Upcoming**, **In Progress**, or **Completed**) to view line items.

## View line items

The **Line Items** window displays line items in rows under three progress tabs: **Upcoming**, **In Progress**, or **Completed**. Line items appear under each progress tab as follows:

- **Upcoming** - line items that have not started.
- **In Progress** - line items between flights (start date/time of the first flight and end date/time of the last flight).
- **Completed** – line items that have completed and are past their end date/time of the last flight.

## Understand line item columns

The **Upcoming**, **In Progress**, or **Completed** progress tabs each list line items in rows. The rows include columns with the line item name and relevant metrics for the line items.

Hover over the tooltips next to each metric at the top of each column for a brief description of the metric. The metrics provide important information about upcoming, in progress, and completed line items without requiring you to run a report. The metrics are updated regularly.

> [!NOTE]
> There might be discrepancies between the metrics displayed in the **Line Items** monitoring view and reporting data due to slight variations in data syncing. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Search for line items

There are several ways to search for line items from the **Line Items** window. You can search for line items by line item name, line item ID, deal name, or deal ID. Inactive line items are listed in gray italic text.

## Use pagination

If you don't have a line item name, line item ID, deal name, or deal ID to search with, you can use the pagination feature at the bottom of the **Line Items** window to page through the rows of line items. The pagination feature lets you:

- select the number of rows that you want to display per page by selecting a value from the **Rows per page** menu.
- enter a specific page in the designated text field or select the arrows to navigate from page to page.

## Apply filters

You can create and save filters to search for line items. Once created and saved, you can apply a filter using the **Select a Filter** drop-down list. To create and save a new filter:

1. In the **Line Items** window, select **Advanced Filters**.

1. Make your selections.

1. Select the arrow to the right of the **Apply** button.

1. Select **Apply and Save As**.

1. Enter a name for the new filter in the **New Filter Name** field.

    > [!NOTE]
    > You can save up to 10 filters. If you already have 10 filters and want to add a new filter, delete an existing filter and try again.

1. Select the **Make Default** checkbox to apply the filter to the rows by default.

    > [!NOTE]
    > The default filter will apply each time you access the **Line Items** window.

1. Select **Apply** and **Save As** to save the filter.

    All saved filters appear in the **Select a Filter** drop-down. To remove an applied filter, select **Clear All**. To edit an applied filter, select **Edit** to open the **Advanced Filters** dialog (see Step 2 above).

You can edit saved filters at any time. To edit a saved filter:

1. In the **Line Items** window, select **Advanced Filters**.
1. In the **Advanced Filters** dialog, select a filter using the **Select a Filter** dropdown.
1. Once a filter is selected, you have options to **Deselect Filter**, **Make Default**, **Rename**, or **Delete**. You can also make any changes to the filter configurations displayed as you scroll through the **Advanced Filters** dialog.
1. Select **Apply and Save** to apply your changes and save the filter.

## Sort columns

You can sort most line item rows in the **Line Items** window into ascending or descending order by selecting each column label.

## Select column views

You can select any available column views in the **Select a View** drop-down. To reset the column view when a view is selected, select the drop-down arrow next to the selected view and select **Select a View**.

## Modify and save column views

You can modify and save column views. Saving a column view makes it available in the **Select a View** drop-down list. To modify a column view:

1. In the **Line Items** window, select **Modify Columns**.
1. In the **Modify Columns** dialog, select an existing column view from the **Select a Setting** drop-down or use the current view.
1. Select the appropriate progress tab (**Upcoming**, **In Progress**, or **Completed**).
1. Select (to show) or deselect (to hide) any column checkboxes. You can also choose **Select all**/**Deselect all** to select or deselect all columns for the progress tab.
1. Optionally, you can rearrange the columns by dragging and dropping them.
1. Do one of the following:
    - To apply the view to the current session, select **Apply**.
    - To apply and save the view so it's available in the **Select a View** drop-down list:
      1. Select the drop-down arrow next to **Apply** and select **Apply and Save As**.
      1. Enter a name for the new column setting in **New Setting Name**.
      1. Optionally, check **Make Default** if you want this column setting to be the default view.
      1. Select **Apply and Save As**.

## View line item details

To view the details of a line item listed in the **Line Items** window, select anywhere in the line item row to display the Line Item Details. See [View Line Item Details](view-line-item-details-smw.md) for more information.

## Duplicate, cancel reservation, delete, or run report for selected line items

You can duplicate, cancel reservation, delete, or run a report for selected line items by doing the following:

1. In the **Line Items** window for each progress tab (**Upcoming**, **In Progress**, or **Completed**), select the checkbox to the left of any line items.
1. When line items are selected, the **Line Items selected** bar is available at the top of the **Line Items** window with the following available actions you can perform by selecting on the action:
    - **Duplicate** - you can duplicate one or more line items simultaneously.
    - **Cancel Reservation** - for Guaranteed Delivery Line Items (GDLI) and Programmatic Guaranteed Line Items (PGLI), you can cancel the reservation of one or more of these line items.
    - **Delete** - you can delete one or more line items simultaneously.

      > [!WARNING]
      > Deleting a line item deletes all its child objects, including creatives, conversion pixels, segments, and splits. Deletions are permanent and cannot be reverted

    - **Run Report** - you can run reports for one or more line items simultaneously.

## Related topics

- [Troubleshooting Line Items](curate-troubleshooting-line-items.md)
- [View Line Item Details](view-line-item-details-smw.md)
