---
title: Microsoft Monetize - View Line Item Details
description: Explore Line Item Details for insights—settings, metrics, visualizations. Swiftly access child campaigns' performance.
ms.date: 5/3/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - View Line Item Details

The **Line Item details** page provides a consolidated view of a line item's configuration, delivery settings, targeting rules, and associated resources. This page allows you to review the current configuration of a line item and navigate to related components such as creatives, segments, and pixels.

## Access line item details

To view the details of a line item:

1. In the left navigation menu, select **Line Items**.
2. Locate the line item in the grid.
3. Select the **line item name**.

The line item's detail page opens and displays its configuration.

---

## Page layout

The line item details page contains the following main sections:

- **Header information**
- **Settings tab**
- **History tab**
- **Associated resources menu**

---

## Header information

At the top of the page, the header displays key identifiers and status information for the line item.


::contentReference[oaicite:0]{index=0}


The header includes:

- **Advertiser** – The advertiser associated with the line item.
- **Insertion Order** – The parent insertion order.
- **Line Item Name and ID** – The unique identifier for the line item.
- **Status** – Indicates whether the line item is active or inactive.
- **Delete** – Deletes the line item.

---

## Settings tab

The **Settings** tab displays the current configuration of the line item, organized into several sections.

### Details

The **Details** section provides basic information about the line item.

| Field | Description |
|------|-------------|
| **Line Name** | The name of the line item. |
| **Type** | The line item type (for example, Standard). |
| **Ad Type** | The ad format used by the line item. |

---

### Budgeting and Scheduling

The **Budgeting and Scheduling** section defines the line item's delivery budget and flight schedule.

| Field | Description |
|------|-------------|
| **Budget Type** | The budget configuration applied to the line item. |
| **Payment Model** | The pricing model used for delivery (for example, CPM). |
| **Revenue** | The revenue associated with the line item. |
| **Budget** | The total budget allocated to the line item. |
| **Current Flights** | The active delivery time period for the line item. |
| **Underspend Catch-Up** | Determines how the system compensates for underdelivery. |
| **Daily Pacing Allocation** | Defines how delivery is paced throughout the day. |

---

### Insertion Order Summary

The **Insertion Order Summary** section displays information inherited from the parent insertion order.

| Field | Description |
|------|-------------|
| **Name** | The name of the insertion order. |
| **State** | The status of the insertion order. |
| **Currency** | The currency used for the insertion order. |
| **Budget Type** | The budget type configured at the insertion order level. |
| **Total Lifetime** | The total lifetime budget for the insertion order. |
| **Pacing** | The pacing strategy applied to the insertion order. |
| **Billing Periods** | The billing periods defined for the insertion order. |
| **Budget** | The budget allocated for the billing period. |

---

### Optimization

The **Optimization** section controls delivery optimization settings.

| Field | Description |
|------|-------------|
| **Optimization Method** | Defines the optimization strategy used for delivery. |
| **Goal Priority** | Specifies the priority of delivery goals. |
| **Conversion Pixel** | Indicates whether conversion tracking is associated with the line item. |

---

### Key Value Targeting

The **Key Value Targeting** section displays any custom key-value targeting rules applied to the line item.

These rules determine which inventory matches the targeting criteria.

---

### Creative Rotation

The **Creative Rotation** section defines how creatives rotate during delivery.

| Field | Description |
|------|-------------|
| **Creative Rotation** | Specifies the creative rotation strategy (for example, Even). |
| **Associated Creatives** | Displays creatives assigned to the line item. |

---

### Fees

The **Fees** section lists any fees associated with the line item.

| Field | Description |
|------|-------------|
| **Associated Fees** | Displays fees applied to the line item. |

---

### Inventory & Environment Targeting

This section defines where the line item is eligible to deliver.

| Field | Description |
|------|-------------|
| **Geography** | Targeted geographic locations. |
| **Device Type** | Devices eligible for delivery. |
| **Inventory Type** | The type of inventory targeted (for example, app or web). |
| **Inventory** | Specific inventory sources targeted. |
| **System** | System-level targeting conditions. |
| **Page Properties** | Additional page-level targeting rules. |

---

### Audience Targeting

The **Audience Targeting** section defines audience-based delivery rules.

| Field | Description |
|------|-------------|
| **Audience and Location Segments** | Target audience segments. |
| **Anonymous Reach Expansion** | Determines whether delivery can expand beyond selected segments. |

---

### Reporting Labels and Comments

This section allows you to add reporting metadata.

| Field | Description |
|------|-------------|
| **Reporting Labels** | Custom labels used for reporting and organization. |
| **Comments** | Internal comments associated with the line item. |

---

## Associated resources

The **Associated resources menu** provides quick access to related components used by the line item.

Available options include:

- **Creatives**
- **Inventory Lists**
- **Conversion Pixels**
- **Segments**
- **3rd Party Pixels**

Selecting one of these options opens the corresponding management interface.

---

## History tab

The **History** tab provides an audit log of all changes made to the line item.

The history log includes:

- Timestamp of each change
- User who made the change
- Fields modified
- Previous and updated values

This allows administrators to track configuration updates and troubleshoot delivery issues.
<!-- Navigate to **Advertisers > Line Items** from the vertical navigation menu on the left. The **Line Item Details** screen shows you the settings and essential metrics for a specific line item, informs you of conditions preventing the line item from serving, provides visualizations of the line item's performance and delivery, offers quick access to the line item's child campaigns, and more.

## Getting to the Line Item Details pane

On the **Line Items** screen, hover over the line item for which you want to view advanced details and click the **graph** button.

This takes you to the **Line Item Details** screen.
<!--
## Viewing visual success data

Visual Success is a tool designed to help campaign managers achieve better overall performance. It provides easy access to performance, delivery, and other metrics for your line item. You can use these metrics to see how the campaigns under your line item are performing as a group, and assess for possible trouble spots at the campaign and line item levels.

With Visual Success, you can:

- View flight progress, delivery, performance, and margin
- Scan for problems using easy-to-read data visualizations
- Keep track of how well line items are pacing to goals
- Hover over the visuals to see specific data for a single day

Visual Success features appear at the top of the **Line Item Details** screen. The metrics sections and graphs show important information about the line item's flight, delivery, performance and margin.

For more information, see [Improve Performance with Visual Success](improve-performance-with-visual-success.md).

## Viewing line item settings

Click on any of the Line item to open the **Settings**  section on the right pane that shows the basic details, frequency caps, reporting labels, commissions, associated insertion orders (when relevant), and dynamic landing page URL, as well as inventory, geography, and system targeting (if set).

The **Basic Settings** button shows the **Basic Setup**, **Frequency Cap**, **Geography Targeting**, **System Targeting**, **Inventory Targeting**, **Key Value Targeting**, and **Insertion Order Settings** (if applicable).

The **All Settings** button shows these settings as well as **Commissions**, **Comments**, **Dynamic Landing Page**, and parent **Insertion Orders** (if applicable).

## Basic setup

- **State**: The state of the line item (active or inactive).
- **Lifetime Budget**: The lifetime budget for the line item (in impressions or revenue).
- **Daily Budget**: The daily budget for the line item, in impressions or revenue.
- **Revenue Type**: The basis on which the advertiser has agreed to pay you. For example, CPM (per thousand impressions) or CPA (per conversion). For more information about each revenue type, see [Create a Standard Line Item](create-a-standard-line-item.md).
- **Revenue Value**: The amount that the advertiser will pay you for the specified revenue type.
- **Conversion Tracking**: The name and ID of each conversion pixel associated to this line item.
- **Performance Goal Type**: The type of goal that the advertiser wants you to achieve (CPC, CPA, CTR). A performance goal is used to achieve a goal that is different from how the advertiser has agreed to pay you. For example, the advertiser wants to pay a CPM but expects you to meet a $50 CPA goal. For more information about performance goals, see [Create a Standard Line Item](create-a-standard-line-item.md).
- **Performance Goal Tracking**: The amount for the performance goal.

## Frequency caps

- **Frequency Caps**: How frequently the creatives associated to campaigns under this line item can be shown. This can be:
  - Number of creatives shown to a given user over the lifetime of the line item
  - Number of creatives shown to a given user per day
  - Number of minutes/hours/days that must pass before a given user can be shown another creative
- **Cookies**: Whether or not the creatives associated to campaigns under this line item can be shown to users without cookies. Be aware that frequency caps do not apply to such users.

  > [!NOTE]
  > Frequency caps and whether to show to cookieless users can also be set at the advertiser, insertion order, campaign, and creative levels, or any combination of the five levels. The most restrictive setting always takes precedence. For more information, see [Frequency Targeting](frequency-and-recency-caps.md).

## Reporting labels

This section shows if a **Trafficker**, **Salesperson**, or **Campaign Type** has been associated with the line item. If so, you can run reports by these labels. For example, you might associate a salesperson with each of your line items and then run a report grouped by salesperson to compare line item performance across salespersons.

## Commissions

This section shows any commissions that have been associated with the line item. Commissions let you attribute revenue to third-parties. They are deducted from the booked revenue (the amount the advertiser pays you) of the line item and can be defined either as a percentage of booked revenue or a flat CPM. For more information about commissions, see [Broker Fees](broker-fees.md).

## Associated insertion orders

This section shows the names and IDs of all insertion orders to which the line item is associated.

## Dynamic landing page

If you have associated multiple creatives to a single landing page, this section shows the landing page URL to use for the creatives. Note that you can set a dynamic landing page at the campaign level as well. For more information, see [Dynamic Landing Pages](dynamic-landing-pages.md).

## Comments

This section shows any comments that have been recorded with the line item. Comments are for reference only and do not affect line item delivery.

## Viewing sibling line items

You can view the other line items under the same advertiser or insertion order in the sibling line item list at the side of the screen. You can click on any line item in the list to go to the **Line Item Details** screen for that line item. The slider at the side of the screen allows you to expand and adjust the view.

## Viewing associated campaigns and campaign details summaries

## Viewing associated campaigns

You can view the campaigns that belong to the line item on the **Line Item Details** screen. To do so, click to expand the **Campaigns** section to view the campaign list.

## Viewing campaign details

From the line item campaign list, you can also view specific campaigns and their settings. To do so, select the desired campaign from the line item campaign list by clicking anywhere on the row. A details summary will appear below the campaign you have selected.

## Editing the line item

To change any of the line item's settings, click the **Edit** icon at the top of the screen or the **Edit** link in the **Details** section.

## Editing campaign settings

You can also edit campaign settings directly from the **Line Item Details** screen in the **Campaign Details** pane. Wherever a pencil icon appears, you can click the icon to edit that setting.

Clicking the pencil icon next to the campaign name at the top of the pane will take you to the full **Edit Campaign** screen. Clicking the pencil icon in the **Inventory**, **Geography**, or **System Targeting** or **Associated Creatives** sections will open an editing dialog for that setting/feature.

## Reporting on the line item

To run a report for the line item, click **Advertisers** and select **Reporting** from the menu that appears.

This takes you to the **Advertiser Reporting** screen, where you can select to run an **Analytics**, **Site Domain Performance**, **Attributed Conversions**, or **Creative Frequency & Recency** report. For more information about these reports, see [Advertiser Reporting](advertiser-reporting.md).

## Viewing child object details

To view child object details:

1. Click the **Associated Objects** menu on the right of the **Details** pane.
1. Select the appropriate object category such as **Creatives**.

## Related topics

- [Explore Line Items](explore-line-items.md)
- [Create a Standard Line Item](create-a-standard-line-item.md) -->
