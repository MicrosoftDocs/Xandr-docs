---
title: Microsoft Monetize - Working with Insertion Orders
description: Explore simplified line item management, sharing budgets & diverse targeting through Insertion Orders in the Object Hierarchy.
ms.date: 1/16/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Working with insertion orders

Insertion orders allow you to easily manage collections of line items that may share a common budget, time span, and business terms. Insertion orders are a standard part of the [Object Hierarchy](object-hierarchy.md). An insertion order can contain one or more line items. For example, you may want to set a common budget and billing periods for several line items, but have each line item target a different region or buy different types of media.

## Explore insertion orders

The **Insertion Orders** screen shows you essential metrics about all insertion orders under a specific advertiser, provides quick access to each insertion order's details, and reporting options.

This article describes the SMW grid for Insertion order for individual advertisers.

Things you can do on this page include:

- Navigate to insertion orders quickly using filters
- See performance metrics
- Drill down into line items to configure or troubleshoot
- Create and edit insertion orders

## Get to the insertion orders screen

To get to the insertion orders screen:

Navigate to **Advertisers > Insertion Orders** from the vertical navigation menu on left.

## Search

You can use the search field at the top of the screen to find all insertion orders whose names or IDs include a specific string of characters or numbers.

## Filters

The **Filters** menu lets you filter for insertion orders based on Advertiser, Insertion Order Name, Status and Type.

- You can select **Inactive** or **Active** from the **State** menu. 
- Click on **Apply** to save your filter for future purpose.

<!-- ## Filter your insertion orders

The **Advanced Filters** menu lets you filter for insertion orders based on Advertiser, State, Type, Insertion Order Name, Flight Start and End Date, and External Code. Click on **Apply** or **Apply and Save As**. The **Apply and Save As** option will save your filter for future purpose.

## View stats

The metrics on the **Insertion Orders** screen help you quickly assess the performance and delivery of your insertion orders. These metrics are faster and more readily accessed than standard reporting data. They are cached on a regular basis and are shown whenever you open the **Insertion Orders** screen.

Note that these stats may not match the data from standard reporting exactly for technical reasons. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md). -->

## Columns

The following stats are shown for each insertion order. Note that the data always reflects the currently selected stats interval:

| Stats | Description |
|--|--|
| **ID** | The unique identifier of insertion order. |
| **Line Items** | Total number of in-progress, active, and associated line items under the insertion order. |
| **Billing Period** | Insertion order's current billing period. |
| **Today's Delivery** | Displays the number of impressions delivered on the current calendar day. |
| **Yesterday's Delivery** | Displays the number of impressions delivered on full 24-hour period of the previous calendar day. |
| **Last 7 Days Delivery** | Displays the number of impressions delivered on full 7 days previous to the current calendar day, i.e., excluding today. |
| **Lifetime Impressions** | Number of impressions for all line items for the entire lifetime under the insertion order. |
| **Lifetime Clicks** | Number of clicks for all line items for the entire lifetime under the insertion order. |
| **Lifetime Revenue** | Money the advertiser has paid or will pay your network for entire lifetime of each insertion order, including the current calendar day as a result of campaigns under the insertion order. This is based on revenue settings at the line item level. |
<!--
| **Issues** | Setup issues that may prevent the insertion order or its associated line items from delivering. |
 
| **Billing Period Imps Delivery** | Number of impressions delivered during the current billing period. |
| **Billing Period Rev Delivery** | Revenue for the current billing period. |
| **Billing Period eCPM** | The billing period for the money the advertiser has paid or will pay your network per 1000 impressions. |
| **Billing Period Media Cost** | The billing period for the money your network has spent buying media for campaigns under the line item. |

| **Deal Revenue (Lifetime)** | Total revenue from deals for entire lifetime of each insertion order, including the current calendar day. |

| **Type** | The type of the insertion order. |

| **Order Status** | The status of the insertion order (Active or Inactive). |

| **Last Hour's Delivery** | Displays the number of impressions delivered on the current calendar day up to the last hour. |



To get information about attributed conversions, rather than just conversion pixel loads as shown in the Convs column, see [Reporting on Conversions](reporting-on-conversions.md). -->

<!-- ## Modify columns

You can choose the columns that are displayed by clicking the **Modify Columns** button.

This opens the **Modify Columns** dialog. From there you can use the checkboxes to select or deselect the columns you want to display. If you want the columns to appear in a certain order, then you can drag and drop the columns at your desired location. -->

## Edit columns and sort

You can customize the columns that appear on the Insertion Order screen. Use **Edit columns and sorts** to add, remove, or reorder columns in the grid.

### Edit columns

You can customize the columns that appear on the screen. Use Edit columns and sorts to add, remove, or reorder columns in the grid.

Columns are grouped into the following categories.

**Basic info**

| Column             | Description                                             |
| ------------------ | ------------------------------------------------------- |
| **ID**             | The unique ID of the insertion order.                   |
| **Billing Period** | The billing period associated with the insertion order. |
| **Type**           | The type of insertion order.                            |

**Performance**

| Column                   | Description                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------- |
| **Order Status**         | The current delivery status of the insertion order.                                 |
| **Today’s Delivery**     | The amount delivered by the insertion order today.                                  |
| **Yesterday’s Delivery** | The amount delivered by the insertion order yesterday.                              |
| **Last 7 Days Delivery** | The amount delivered by the insertion order in the last seven days.                 |
| **Lifetime Impressions** | The total number of impressions delivered by the insertion order over its lifetime. |
| **Lifetime Clicks**      | The total number of clicks delivered by the insertion order over its lifetime.      |
| **Lifetime Revenue**     | The total revenue delivered by the insertion order over its lifetime.               |

**Related objects**

| Column         | Description                                                   |
| -------------- | ------------------------------------------------------------- |
| **Line Items** | The number of line items associated with the insertion order. |

### Edit sorts

You can sort the data displayed on the screen by selecting one or more fields. Use Edit columns and sorts, then select the Sorts tab to add, remove, or reorder sorts.

Sorts are applied in the order shown, from top to bottom.

**Basic info**

| Sort | Description |
|-----|-------------|
| **Insertion Order ID** | Sorts insertion orders by their unique ID. |

**Billing period**

| Sort | Description |
|-----|-------------|
| **Budget Interval End Date** | Sorts insertion orders by the end date of the current budget interval. |

**Performance**

| Sort | Description |
|-----|-------------|
| **Order Status** | Sorts insertion orders by their current delivery status. |
| **Today’s Delivery** | Sorts insertion orders by the amount delivered today. |
| **Yesterday’s Delivery** | Sorts insertion orders by the amount delivered yesterday. |
| **Last 7 Days Delivery** | Sorts insertion orders by the amount delivered in the last seven days. |
| **Lifetime Impressions** | Sorts insertion orders by total lifetime impressions. |
| **Lifetime Clicks** | Sorts insertion orders by total lifetime clicks. |
| **Lifetime Revenue** | Sorts insertion orders by total lifetime revenue. |

**Related objects**

| Sort | Description |
|-----|-------------|
| **Line Items** | Sorts insertion orders by the number of associated line items. |

Click on **Apply** to save your settings.

## View insertion order details

To view advanced details about an insertion order, click the insertion order's name.

See [View Insertion Order Details](view-insertion-order-details.md) for more information.

## Managing insertion orders - bulk action toolbar

- To activate or deactivate one or more insertion orders, check the box for each insertion order you want to activate or deactivate and click **Activate** or **Deactivate** as required.
- To delete one or more insertion orders, check the box next to each insertion order you want to delete and click **Delete**.
- To run a report on one or more insertion orders, check the box for each insertion order you want to report on and click **Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md),  For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md). 
  > [!WARNING]
  > Deleting an insertion order deletes all of its child objects as well.

<!-- ## Search by name/ID

You can use the search field at the top of the screen to find all insertion orders whose names or IDs include a specific string of characters or numbers. -->

<!-- ## Report on insertion orders

You can initiate a report for one or more insertion orders directly from this screen. Check the box for each insertion order that you want to report on and click **Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md),  For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md). -->

## Related topics

- [View Insertion Order Details](view-insertion-order-details.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Update Insertion Orders](update-insertion-orders.md)























<!-- Note that there are two types of insertion orders (for more information, see [Create an Insertion Order](create-an-insertion-order.md)):

- **Legacy** - Legacy insertion order required for legacy guaranteed and non-guaranteed line items.
- **Seamless** - Seamless insertion order compatible with augmented line items (ALI), guaranteed delivery augmented line items (GDALI), and programmatic guaranteed line items (PGLI). -->
<!-- 
Some useful procedures when creating and working with insertion orders here:

- **[Create an Insertion Order](create-an-insertion-order.md)** - Set up an insertion order (formerly "seamless insertion order") in Microsoft Monetize.
- **[Explore Insertion Orders](explore-insertion-orders.md)** - View essential metrics about insertion orders under a specific advertiser, get quick access to each insertion order's details and child line items, and use bulk editing and reporting options.
- **[View Insertion Order Details](view-insertion-order-details.md)** - View the settings and essential metrics for a specific insertion order, analyze visualizations of the insertion order's performance, get quick access to the insertion order's child objects, and more.
- **[Update Insertion Orders](update-insertion-orders.md)** - Update the details of an insertion order in Microsoft Monetize.
- **[Reporting on Insertion Orders](explore-insertion-orders.md)** - Initiate an advertiser analytics report for one or more insertion orders.
<!-- - **[Create a Legacy Insertion Order](create-a-legacy-insertion-order.md)** - Set up an old-style insertion order in Microsoft Monetize. Legacy insertion orders do not use billing periods, can't be used with the recommended augmented line item, and are no longer the best practice.
- **[View Legacy Insertion Order Details](view-legacy-insertion-order-details.md)** - View the settings and essential
  metrics for a specific legacy insertion order, analyze visualizations of the insertion order's performance, get quick access to the insertion order's child objects, and more. -->
