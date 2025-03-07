---
title: Explore Line Items
description: Explore streamlined management for advertisers and publishers on the Line Items screen. Access metrics, alerts, and bulk editing options effortlessly.
ms.date: 10/28/2023
---

# Explore Line Items

The **Line Items** screen provides essential metrics for all line items under a specific advertiser. It helps identify conditions preventing line items from serving, offers quick access to insertion order details and child campaigns, and allows you to manage demand, monitor delivery, and make bulk edits.

Things you can do on this page include:

- Use filters to quickly identify line items with specific criteria
- See delivery and performance metrics
- See important line item details and make changes quickly

## Access the Line Items screen

To access Line Items screen:

- Select **Advertisers** >  **Line Items** from the navigation menu at the top of the screen.

  or

- From the **Advertisers** screen, find the advertiser whose line items you want to see and click the **Line Items** button on the **Order Settings** screen.

## Filter your line items

You can filter line items using the **Advanced Filters** available in the **SMW Line Items** screen.

### Access Advanced Filters

1. Select **Advertisers** → **Line Items** from the navigation menu.
1. Alternatively, click the **Line Items** button on the **Order settings** screen.
1. In the **SMW Line Items** screen, locate and expand the **Advanced Filters** panel, at the top center of the screen.

    > [!NOTE]
    > To save a filter for future use, select **Apply and Save As** from the dropdown next to **Apply**.
1. Use the available filters to refine your search based on specific criteria.

The following table describes the available fields and their values:

| Field | Description |
|---|---|
| Setting | Select from previously saved filters.|
| Advertisers |Search for and select an advertiser associated with the line item. Enter the advertiser’s name or a keyword to find results.|
| Insertion Orders| Search for and select an insertion order linked to the advertiser. Enter the insertion order name or ID to filter results.|
| Line Item Name| Enter the line item name to identify and filter specific line items. |
| Deal | Search for and select a deal linked to the advertiser.|
| Buyer | Select a buyer for the line item. Choose Any Buyer to include all buyers or Selected Buyer to search and add a Demand-Side Platform (DSP) or Deal Buyer.|
| Line Status| Filter line items based on their current status. <br> Available statuses: <br> **Reserved** – Allocated but not yet active. <br> **Scheduled** – Set to start at a future date. <br> **Live** – Currently running. <br> **Paused** – Temporarily stopped. <br> **Inactive** – No active delivery. <br> **Complete** – Finished as per schedule. <br> **Canceled** – No longer active.|
| Creative Status | Filter line items based on creative assignment. <br> The options include: <br> 1) **Missing creative** – No creative assigned. <br> 2) **Creative assigned** – A creative has been added.|
| State | Indicates the current status of the item. The states are: <br> 1) **Active** - The item is currently in use or operational. <br> 2) **Inactive** - The item is not in use or has been deactivated.|
| Expected Delivery | Select the checkbox to filter line items expected to underdeliver.|
| Pacing | The percentage range from 0% to over 100%, representing the pacing of the delivery or performance. |
| Priority |A numeric value between **0** and **20**, representing the priority level.|
| Flight Start Date | The specific date when the flight starts. This can be entered manually.|
| Flight End Date| The specific date when the flight ends. This can be selected.|
| Last Modified | Indicates when the item was last modified. You can select from rolling options such as today, next, or last, or enter a specific date.|
| Type | Filter based on the line item type.|
| Ad Type | Specifies the type of advertisement, such as: <br> - Banner <br> - Video <br> - Native Banner <br> - Video <br> - Native|
| Viewability Rate | The percentage of viewability, ranging from 0% to over 100%.|
| Trafficker | The individual responsible for trafficking the advertisement.|
| Salesperson | The salesperson associated with the advertisement or campaign.|

## Save and Apply filters

- After setting your desired filters, click on the arrow next to the **Apply** button and select **Apply and Save As**.
- Enter a name for the new filter.
- Select the **Make Default** checkbox if you want this filter to be automatically applied by default.
- Click **Apply and Save** As to save the filter.

All saved filters are available from the **Select a Filter** pull-down menu. To remove an applied filter, select **Clear All**. You can update any saved filter at any time by selecting the **Edit** link or by accessing **Advanced Filters**. From the **Advanced Filters** dialog, you can rename, delete, or set a saved filter as the default.

## Find inactive line items

Line items with the **Inactive** state are shown with their IDs, names, and quickstats in gray italics.

## View line item details

To view a summary of details about a line item, just click the line item's name. To see a full, detailed summary and a graphical view of delivery and performance, click the **graph** icon next to the pencil when you hover over the line item.

For more information about line item details, see [View Line Item Details](view-line-item-details.md).

## Columns

The following QuickStats are displayed for each line item. The data reflects the currently selected QuickStats interval:

| Line Item | Name of the line item. |
|--|--|
| **Select All/ Deselect All** | Allows users to select or deselect all columns at once. |
| **Line ID** | Unique identifier assigned to the line item. |
| **Deal Name** | Name of the deal associated with the line item. |
| **Deal ID** | Unique identifier assigned to the deal. |
| **Type** | Specifies the type of line item or deal. |
| **Priority** | Priority level assigned to the line item. |
| **Deal Buyer** | Identifies the buyer associated with the deal. |
| **Flight Dates** | Start and end dates for the line item’s campaign. |
| **Issues** | Displays any issues or errors associated with the line item. |
| **Flight Budget** | Budget allocated for the line item during its flight period. |
| **Revenue Value** | Revenue generated by the line item. |
| **Pacing** | The rate at which the budget is spent over time. |
| **Last 60-minute Delivery** | Performance data showing impressions delivered in the last 60 minutes. |
| **Impressions** | Number of times an ad was served. |
| **Clicks** | Number of clicks on ads under this line item. |
| **CTR (Click-Through Rate)** | Percentage of impressions that resulted in clicks. |
| **Revenue** | Total revenue generated by the line item. |
| **Creative Status** | Status of the creative (e.g., approved, pending, rejected). |
| **Creative Audit Status** | Displays the audit status of the creative. |
| **Creatives** | List of creatives associated with the line item. |
| **Line Status** | The current status of the line item (e.g., active, paused, completed). |
| **Deal Health** | Indicates the overall health/performance of the deal. |
| **Conversions** | Number of successful actions taken by users after interacting with the ad. |
| **Viewability** | Percentage of impressions that were viewable based on industry standards. |
| **Viewable Imps** | Number of impressions that met the viewability criteria. |
| **Video Completion Rate** | Percentage of video ads watched to completion. |
| **Trafficker** | Person responsible for managing the line item. |
| **Salesperson** | Sales representative assigned to the deal. |
| **Expected Delivery** | Estimated volume of impressions/clicks to be delivered. |
| **Last Modified** | Timestamp of the last modification made to the line item. |
| **Advertiser** | Name of the advertiser associated with the line item. |
| **Insertion Order** | The insertion order linked to the line item. |
| **Rev eCPC (Revenue Effective Cost Per Click)** | Total booked revenue earned per click. |
| **Rev eCPM (Revenue Effective Cost Per Mille)** | Money the advertiser has paid or will pay your network per 1000 impressions.<br>Tip: Using the currency toggle, you can choose whether to show **Rev eCPM** in USD or in the currency set at the line item |
| **Rev eCPA (Revenue Effective Cost Per Acquisition)** | Total booked revenue earned per conversion. |
| **Pulse** | Metric related to campaign performance monitoring. |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the **Convs** column, see [Reporting on Conversions](reporting-on-conversions.md).

## Show/hide columns

You can customize the columns displayed in the **Line Items** screen.

1. Click the **Configure Columns** button in the upper right corner.
   This opens the **Configure Columns** panel
1. Select or deselect columns using the checkboxes.
   Changes are applied immediately, and the selected columns will remain visible across sessions.

## Wildcard filtering

To search for line items with multiple words, use the wildcard (`%`) at both ends of a keyword.  

For example, entering `%DEAL%Line%` will return results that contain both **DEAL** and **Line**, even if they are not adjacent.  

Example match:  
**DEAL March Line**  

## Understand pacing bars

Pacing bars visually indicate how a line item is delivering against its planned pacing. They help you monitor whether a line item is ahead, behind, or on track with its expected delivery.

The pacing bar appears in the **Pacing** column if the column is enabled. The color and length of the bar represent the delivery status:

- **Green**: On track  
- **Yellow**: Slightly behind  
- **Red**: Significantly behind  

> [!NOTE]
> Pacing bars are not available for all line items.

To enable the **Pacing** column:

1. Click **Modify Columns**.
1. Select **Pacing**.
1. Save your settings.

## Report on line items

To generate a report on selected line items:

1. Select the checkbox next to each line item you want to include in the report.  
2. In the **blue actions toolbar**, click **Download Report**.  
3. Choose the desired format and settings, then confirm to generate the report. For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).

## Activate/deactivate line items

To activate or deactivate line items:  

1. Select the checkbox next to the line item.  
2. In the **blue actions toolbar**, click **Activate** or **Deactivate** as needed.  

The status of the selected line items updates immediately.  

## Related topics

- [Work with Line Items](working-with-line-items.md)
- [View Line Item Details](view-line-item-details.md)
- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Update Line Items](update-line-items.md)
- [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md)
- [Using Multiple Campaigns with a Guaranteed Line Item](using-multiple-campaigns-with-a-guaranteed-line-item.md)
- [Guaranteed Delivery Pacing](guaranteed-delivery-pacing.md)
- [Create an Insertion Order](create-an-insertion-order.md)
- [Object Hierarchy](object-hierarchy.md)
- [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md)
- [Buy-Side Targeting](buy-side-targeting.md)
