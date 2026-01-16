---
title: Microsoft Monetize - View the SMW Grid for Insertion Orders
description: Explore vital settings, metrics, and visuals in Insertion Order Details. Boost video viewability by using the VPAID wrapper. Learn how to access the Seller Monitoring Workflow (SMW) feature for Insertion Orders from any Microsoft Monetize screen.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - View the SMW grid for Insertion orders

The **Insertion Order** screen on the Seller Monitoring Workflow (SMW) grid displays settings for a specific Insertion order, essential metrics, and performance visualizations.

## Locate the Insertion order screen

To access the [Insertion Order](explore-insertion-orders.md) screen: 
- Navigate to **Advertisers > Insertion Orders** from the vertical navigation menu on left pane.
- Select an Insertion Order whose details you want to view. 
- The SMW grid for the **Insertion Order** details will be displayed. 

The screen contains the following sections:
- **Settings**: It provides basic information about the Insertions order such as budgeting, billing, supply strategy, reporting labels, etc.. See [View Insertion Order Settings](#view-insertion-order-settings) for more information.
- **History**: The **History** tab displays a detailed audit log of changes made to the object. It helps you track when changes were made, what fields were updated, and who made the updates. See [View Change History](#view-change-history) for more information.
- **Edit**: It helps you edit an Insertion order.
    <!-- - **Line Items**: It provides a list of the Line items currently associated with the Insertion order.
    - **Associated Objects**: It provides a list of associated objects with the Insertion order. See [View Child Object Details](#view-child-object-details) for more information.-->

## View Insertion order settings

The settings that display here are read-only and can be edited by selecting **Edit** at the top of the **Insertion Order Details** screen. For more information, see [Create an Insertion Order](create-an-insertion-order.md).

| Setting | Description |
|---|---|
| Associated Line Items | Displays a list of the Line items currently associated with the Insertion order.|
| Budgeting | Displays budget and fee information associated with the insertion order. |
| Billing | Displays billing code and any billing periods set up on the insertion order. |
| Teams | Displays the teams that has been associated with the insertion orders. |
| Reporting Labels | Indicates whether a **Trafficker, Sales Representative, and Insertion Order Type** has been associated with the advertiser. If so, these labels can be used when running reports. For example, if a salesperson is associated with the insertion order, the report will be grouped by salesperson across insertion orders. |
| Comments | Displays comments entered for the line item. |
| Supply Strategy | Displays the insertion order's inventory type targeting, inventory lists, and viewability standard. |
| Frequency & Recency | Displays frequency and recency caps applied to the insertion order. |

<!-- Political Advertising | If political advertising is enabled, displays the political organization associated with the insertion order, along with required disclosures and forms. -->

## View child object details

To view child object details:

1. Select the **Associated Objects** menu on the top right corner of the SMW grid.
1. Select the appropriate object category such as **Creatives** or **Inventory Lists**.

## View change history

Use the filters at the top of the page to narrow down results:
- **Select Date** – Filter changes by date range.
- **Select Users** – Filter changes made by specific users.
- **Time Zone** – All timestamps are displayed in UTC.

You can expand or collapse individual entries, or use **Collapse All** to manage visibility.

**Change details**

Each history entry includes:
- **Date and time** the change was made
- **Object type and ID** (for example, insertion order)
- **Number of fields changed**

When expanded, each entry shows a comparison table with the following columns:

| Column | Description |
|------|-------------|
| **Field Name** | The name of the field that was changed. |
| **Old Value** | The value of the field before the change. |
| **New Value** | The value of the field after the change. |

Complex fields (such as objects or lists) can be expanded to view detailed JSON-level changes.


This audit history helps ensure transparency and accountability by providing a complete record of configuration and delivery changes.


## Related topics

- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Change Log History Tool](change-log-history-tool.md)
