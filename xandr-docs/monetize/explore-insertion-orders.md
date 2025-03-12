---
title: Microsoft Monetize - Explore Insertion Orders
description: Explore vital metrics, swiftly access individual insertion orders, and provide reporting options on the Insertion Orders screen for a specific advertiser. 
ms.date: 10/28/2023
---
# Microsoft Monetize - Explore insertion orders

The **Insertion Orders** screen shows you essential metrics about all insertion orders under a specific advertiser, provides quick access to each insertion order's details, and reporting options.

This document describes the Insertion Order screen for individual advertisers.

Things you can do on this page include:

- Navigate to insertion orders quickly using filters
- See performance metrics
- Drill down into line items to configure or troubleshoot
- Create and edit insertion orders

## Get to the insertion orders screen

To get to the insertion orders screen:

- On the **Advertisers** screen, find the advertiser for which you want to view insertion orders and click the button in the **Ins Orders** column.
- In **Advertiser's Details** view, click on **Insertion Orders**.

## Filter your insertion orders

The **Advanced Filters** menu lets you filter for insertion orders based on Advertiser, State, Type, Insertion Order Name, Flight Start and End Date, and External Code. Click on **Apply** or **Apply and Save As**. The **Apply and Save As** option will save your filter for future purpose.

## View stats

The metrics on the **Insertion Orders** screen help you quickly assess the performance and delivery of your insertion orders. These metrics are faster and more readily accessed than standard reporting data. They are cached on a regular basis and are shown whenever you open the **Insertion Orders** screen.

Note that these stats may not match the data from standard reporting exactly for technical reasons. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Columns

The following stats are shown for each insertion order. Note that the data always reflects the currently selected stats interval:

| Stats | Description |
|--|--|
| **ID** | The unique identifier of insertion order. |
| **Impressions (Lifetime)** | Number of impressions for all line items for the entire lifetime under the insertion order. |
| **Issues** | Setup issues that may prevent the insertion order or its associated line items from delivering. |
| **Billing Period** | Insertion order's current billing period. |
| **Billing Period Imps Delivery** | Number of impressions delivered during the current billing period. |
| **Billing Period Rev Delivery** | Revenue for the current billing period. |
| **Billing Period eCPM** | The billing period for the money the advertiser has paid or will pay your network per 1000 impressions. |
| **Billing Period Media Cost** | The billing period for the money your network has spent buying media for campaigns under the line item. |
| **Clicks (Lifetime)** | Number of clicks for all line items for the entire lifetime under the insertion order. |
| **Deal Revenue (Lifetime)** | Total revenue from deals for entire lifetime of each insertion order, including the current calendar day. |
| **Revenue (Lifetime)** | Money the advertiser has paid or will pay your network for entire lifetime of each insertion order, including the current calendar day as a result of campaigns under the insertion order. This is based on revenue settings at the line item level. |
| **Type** | The type of the insertion order. |
| **Today's Delivery** | Displays the number of impressions delivered on the current calendar day. |
| **Order Status** | The status of the insertion order (Active or Inactive). |
| **Line Items** | Total number of in-progress, active, and associated line items under the insertion order. |
| **Last Hour's Delivery** | Displays the number of impressions delivered on the current calendar day up to the last hour. |
| **Last 7 Days Delivery** | Displays the number of impressions delivered on full 7 days previous to the current calendar day, i.e., excluding today. |
| **Yesterday's Delivery** | Displays the number of impressions delivered on full 24-hour period of the previous calendar day. |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the Convs column, see [Reporting on Conversions](reporting-on-conversions.md).

## Modify columns

You can choose the columns that are displayed by clicking the **Modify Columns** button.

This opens the **Modify Columns** dialog. From there you can use the checkboxes to select or deselect the columns you want to display. If you want the columns to appear in a certain order, then you can drag and drop the columns at your desired location.

## View insertion order details

To view advanced details about an insertion order, click the insertion order's name.

See [View Insertion Order Details](view-insertion-order-details.md) for more information.

## Search by name/ID

You can use the search field at the top of the screen to find all insertion orders whose names or IDs include a specific string of characters or numbers.

## Report on insertion orders

You can initiate a report for one or more insertion orders directly from this screen. Check the box for each insertion order that you want to report on and click **Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md),  For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).

## Related topics

- [View Insertion Order Details](view-insertion-order-details.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Update Insertion Orders](update-insertion-orders.md)
