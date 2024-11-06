---
title: Microsoft Invest - View Line Item Details
description: Learn about the Line Item Details screen.
ms.date: 10/28/2023
---

# Microsoft Invest - View line item details

The **Line Item Details** screen displays settings for a specific line item, essential metrics and performance visualizations, and related objects that may have been set up under the line item.

## Locate the Line Item Details pane

Select the appropriate tab (Upcoming, In Progress, or Completed) from the **Line Items** menu. From the **Line Items** grid, select anywhere within one of the rows to view details for a specific line item.

You can use the search field at the top of the **Line Items** screen to search for a specific line item or navigate from page to page using the pagination functionality at the bottom of the screen. For more information, see [Searching for Objects](using-the-buyer-monitoring-grids.md).

## View line item settings

The settings that display here are read-only and can be edited by selecting **Edit** at the top of the **Line Items Details** screen. For
more information, see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md).

| Settings | Description |
|--|--|
| Peer Approval | Indicates whether or not peer approval is required before the line item can be set to active. <br> **Note**: This setting cannot be updated at the line item level. For more information, see [Peer Approval](peer-approval.md). |
| Optimization & and Budgeting | Specifies the optimization method and goal priority as well as all budgeting information that includes the following: payment model, revenue, budget, and total lifetime budget. |
| Flights | Specifies the start and end dates to indicate when the line item will begin and end based on the advertiser's time zone. Daypart settings also display here to define how you want to target users based on the day and time when they see impressions. For more information, see [Daypart Targeting](daypart-targeting.md). |
| Programmable Splits | Indicates whether any programmable splits exist for the line item. For more information, see [Working with Programmable Splits](working-with-programmable-splits.md). |
| Creatives | Specifies the creative type, such as banner, and rotation that defines the creative delivery strategy that will be used when multiple creatives of the same size are trafficked to a line item, and includes the number of associated creatives along with their dimensions, name, and ID. If there's an issue with the creative, a yellow triangle indicator will display to the right of the uploaded file. For more information, see [Working with Creatives](working-with-creatives.md). |
| Supply Strategy | Specifies the buying strategy, such as Open Exchange, Managed, or Deals, which is also referred to as the supply source, as well as settings related to: <br>- **Deals**: Indicates whether all deals or specific deals will be targeted.<br>-  **Inventory Type Targeting**: Specifies the inventory types (app and/or web) that will be targeted. <br> - **Inventory Targeting**: Specifies the inventory list (allowlists and blocklists) that will be used to constrain the inventory type. |
| Viewability | - **Threshold**: Specifies if a viewability threshold exists in which only impressions that contain a certain percentage of predicted viewability will be bought. <br> - **Video Targeting**: Defines how you want target your video inventory based on the playback method, player size, and position. <br> - **Page Targeting**: Displays details about the tag position and query strings.For more information, see [Video Targeting](video-targeting.md). |
| Brand Safety Targeting | Specifies the brand safety segments, which are pre-defined by third-party verification vendors, that will be used to target inventory. These segments help apply additional quality controls to the inventory that is being targeted, such as exclude drugs. |
| Audience Targeting | - **Demographics**: Specifies the demographics, such as age and gender, that will be targeted. <br>- **System Targeting**: Specifies the operating systems, browsers, languages, device models, and carriers that will be targeted. For more information, see [System Targeting](system-targeting.md) and [Cross-device targeting](enable-cross-device-targeting-and-measurement-for-a-line-item.md). |
| Segment Targeting | Specifies the segments that will be used to target various users. For more information, see [Segment Targeting](system-targeting.md). |
| Environment Targeting | - **Device Type Targeting**: Specifies the devices, such as PCs, phones, tablets, TVs, game consoles, and set-top boxes, that will be targeted. <br> - **System Targeting**: Specifies the operating systems, browsers, languages, device models, and carriers that will be targeted.For more information, see [Segment Targeting](system-targeting.md). |
| Key Value Targeting | Specifies the categories and items that will be targeted. Examples of keys include cars, cities, and countries. For more information, see [Key/Value Targeting](key-value-targeting.md). |
| Reporting Labels | Indicates whether a **Trafficker**, **Salesperson**, or **Line Item Type** has been associated to the line item. If so, these labels can be used when running reports. For example, if a salesperson is associated with the line item, the report will be grouped by salesperson to compare line item performance across salespersons. |
| Comments | Displays any comments that have been recorded with the line item. Comments are for reference only and do not affect line item delivery. |

## View line item analytics

The **Analytics** tab provides detailed metric information in the form of graphs and charts so that you can:

- view flight progress, delivery, performance, and margin with a high level of granularity to keep track of how well your line items are pacing against the optimization goals that have been set.
- monitor associated splits to keep track of how they are delivering and performing.
- scan for problems using easy-to-read data visualizations.
- hover over the visuals to see specific data for a single day.

For more information, see [Monitor Splits](monitor-splits.md).

## Troubleshoot line item delivery and bid performance

The **Troubleshooting** tab displays a prioritized list of top issues and bid performance messages to help you improve your line item delivery and impression count. For more information, see [Troubleshoot Your Augmented Line Item Delivery and Bid Performance](troubleshoot-your-augmented-line-item-delivery-and-bid-performance.md) and [Bid Performance Messages for Augmented Line Items](bid-performance-messages-for-augmented-line-items.md).

## View child object details

To view child object details:

1. Select the **Associated Objects** menu on the right of the **Details** pane.
1. Select the appropriate object category such as **Creatives**.

## Related topics

- [Using the Buyer Monitoring Grids](using-the-buyer-monitoring-grids.md)
- [Update Line Items](update-line-items.md)
- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Create an Insertion Order](create-an-insertion-order.md)
