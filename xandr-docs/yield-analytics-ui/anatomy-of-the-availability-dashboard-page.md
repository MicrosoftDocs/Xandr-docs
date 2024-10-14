---
title: Anatomy of availability pages
description: In this article, learn the layout of the Availability Dashboard page.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Anatomy of availability pages

The following article details about various availability related pages.

## Anatomy of Availability Dashboard page

The Availability Dashboard page is the primary view for the **Availability** tab. This provides a summary of available revenue, available sell-through, and how available inventory is trending. It is displayed automatically when you select the **Availability** tab.

The Availability Dashboard page is comprised of the following three widgets:

- **Available Revenue** – Displays available revenue (calculated as Impressions × Rate Card) for the top-performing products in a given product group for a given time period (next three months by default). You can change the product group and the time period in this widget.
- **Utilization/Sell-Through** – Displays sell-through rate for the top-performing products in a given product group, for a given time period (next three months by default). You can change the product group and time period in this widget.
- **Availability Trended** – Displays impressions capacity, divided between guaranteed and preemptible impressions, across the network or for a selected product for a given time period (previous three months and next three months by default). You can change the product and time period in this widget. You can also filter the graph to show only guaranteed impressions or only preemptible impressions.

To the left of the widgets is the **Availability Tasks** panel. This is where you can select between three options to check for available inventory:

- **Check Availability** – Takes you to the **Availability Lookup** page. This is where you can search for available inventory by product and/or across products by one or more attributes. You can also create batch lookups from this page to search availability across multiple sets of product criteria.
- **View Calendar** – Takes you to the **View Calendar** page. This is where you can view daily availability for a given month to find openings for new deals. This is especially useful for sponsorships.
- **View Batch Lookups** – Takes you to the **Batch Lookups** page. This is where you can check the status of your availability batch lookups and review completed availability batch lookups (also referred to as "availability reports"). You can export batch lookups to Excel worksheet (XLS) or comma-separated values (CSV) files.

Below the Availability Tasks panel is the Processing Summary panel. This is a read-only panel that indicates when the availability forecast and order data were last updated.

## Anatomy of Availability Lookup page

On the Availability Lookup page on the **Availability** tab, you can search for available inventory using a variety of criteria, including attributes from existing products, attributes from a product group, and custom defined attributes. You can also open saved lookups, save new lookups, and create batches to search for inventory across products and run the lookup in the background.

The Availability Lookup page is comprised of the following four panels:

- **Configuration** – This panel, on the top left side of the page, is where you select the high-level settings for your lookup. This includes the time period and how you want results grouped.
- **Lookup Criteria** – This panel, on the bottom left side of the page, is where you select the products, product groups, and/or attributes for your lookup.
- **Lookup Request** – This panel is populated with the product(s) and attribute(s) you select in the Lookup Criteria panel. You can look up available inventory using a search for products that match all of a set of specified attributes and/or any of a set of specified attributes.
- **Availability Report** – This panel shows a list of the available inventory that meets your lookup criteria. For each product with available impressions, the list provides the product name, product ID, rate card CPM, ad targeting, total impressions, and total capacity. From this panel, you can access full product details for existing inventory. For available impressions that match your lookup but for which a product doesn't yet exist, you can create a new product. You can also export your lookup into an Excel spreadsheet (XLS) or comma-separated values (CSV) file.

## Anatomy of View Calendar page

The View Calendar page on the Availability tab shows a daily summary of future availability by month.

The View Calendar page can be displayed in two views:

- Calendar view – This is the default view for the page and shows a high-level graphical representation of the availability for a given month. You can mouse over each day to see a breakdown of capacity, availability, and sell-through information, as well as the number of booked, pending, and proposed order lines.
- List view – This drill-down view shows each day in the month as a row in a table. You can expand and collapse rows as needed to see full details on the order lines scheduled for that day.

To the left of the daily summary is the Filter panel, where you define how you want availability to be displayed and based on what criteria.

Above the daily summary is a toolbar, where you can switch between views and select the month for which you want to see availability. You can also export the data from the daily summary to an Excel spreadsheet (XLS) or comma-separated values (CSV) file.

### Calendar view details

The values in each date represent the following:

x% or y = (For example, 100% or 15,000,000) Percentage of impressions available or number of impressions available, depending on how you're showing availability
 = Number of booked order lines
 = Number of pending order lines = Number of proposed order lines

The colors in each date represent the following based on your selections in the Color slider in the Filter panel:

- Date is available for booking
- Date has some inventory available for booking but should be booked with caution
- Date is unavailable for booking

### List view details

The colors in each row represent the following based on your selections in the Color slider in the Filter panel:

- Date is available for booking
- Date has some inventory available for booking but should be booked with caution
- Date is unavailable for booking

## Related topics

- [Availability Overview (Old Workflow)](availability-overview-old-workflow.md)
- [Check Availability for a Combination of Targeting Attributes](check-availability-for-a-combination-of-targeting-attributes.md)
- [View Availability Batch Lookups](view-availability-batch-lookups.md)
- [View Availability in a Calendar](view-availability-in-a-calendar.md)
