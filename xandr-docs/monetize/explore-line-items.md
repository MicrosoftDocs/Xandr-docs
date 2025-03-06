---
title: Explore Line Items
description: Explore streamlined management for advertisers and publishers on the Line Items screen. Access metrics, alerts, and bulk editing options effortlessly.
ms.date: 10/28/2023
---

# Explore line items

The **Line Items** screen provides essential metrics for all line items under a specific advertiser. It helps identify conditions preventing line items from serving, offers quick access to insertion order details and child campaigns, and allows you to manage demand, monitor delivery, and make bulk edits.

Things you can do on this page include:

- Use filters to quickly identify line items with specific criteria
- See delivery and performance metrics
- See important line item details and make changes quickly

## Get to the line items screen

To get to the line items screen:

- Select **Advertisers** >  **Line Items** from the navigation menu at the top of the screen.

  or

- From the **Advertisers** screen, find the advertiser whose line items you want to see and click the **Line Items** button in the **Order settings** screen.

## Filter your line items

You can filter line items using the **Advanced Filters** available in the **SMW Line Items** screen.

### How to access Advanced Filters

1. Navigate to **Advertisers → Line Items** from the navigation menu.
2. Alternatively, click the **Line Items** button on the **Order settings** screen.
3. In the **SMW Line Items** screen, locate and expand the **Advanced Filters** panel, at the top center of the screen.

   > [!NOTE]
   > To save a filter for future use, select **Quick filters** from the dropdown next to **Advanced filters**.
4. Use the available filters to refine your search based on specific criteria.

| Field | Description |
|---|---|
| Settings | Select settings. It allows you to select predefined filter configurations for quick access. These settings help streamline the filtering process by applying commonly used criteria with a single selection.|
| Advertisers |Search for and select an advertiser associated with the line item. Enter the advertiser’s name or keyword to find results.|
| Insertion Orders| Search for and select an insertion order linked to the advertiser. Enter the insertion order name or ID to filter results.|
| Line Item Name| Enter the line item name to identify and filter specific line items. |
| Deal | Search for and select a deal linked to the advertiser.|
| Buyer | Select a buyer for the line item. Choose Any Buyer to include all buyers or Selected Buyer to search and add a Demand-Side Platform (DSP) or Deal Buyer.|
| Line Status| Filter line items based on their current status. <br> Available statuses: <br> - Reserved – Allocated but not yet active. <br> - Scheduled – Set to start at a future date. <br> - Live – Currently running. <br> - Paused – Temporarily stopped. <br> - Inactive – No active delivery. <br> -Complete – Finished as per schedule. <br> - Canceled – No longer active.|
| Creative Status | Filter line items based on creative assignment. <br> The options include: <br> 1) Missing creative – No creative assigned. <br> 2) Creative assigned – A creative has been added.|
| Creative Audit Status | The creative audit status <br> indicates the review status of the creative assigned to a line item. The available statuses are: <br> 1) Needs Review – The creative requires approval. <br> 2) Approved – The creative has passed the audit. <br> 3) Rejected – The creative did not meet the requirements. <br> 4) Mixed – The line item contains creatives with different statuses. <br> 5) Missing Creatives – No creative is assigned. <br> 6) Processing – The creative is being reviewed.|
| State | Indicates the current status of the item. The states are: <br> 1) Active - The item is currently in use or operational. <br> 2) Inactive - The item is not in use or has been deactivated.|
| Expected Delivery | Select the checkbox if it is likely to underdeliver.|
| Pacing | The percentage range from 0% to over 100%, representing the pacing of the delivery or performance. |
| Priority |A numeric value between 0 and 20, representing the priority level.|
| Flight Start Date | The specific date when the flight starts. This can be entered manually.|
| Flight End Date| The specific date when the flight ends. This can be selected.|
| Last Modified | Indicates when the item was last modified. You can select from rolling options such as today, next, or last, or enter a specific date.|
| Type | Indicates the type of agreement or arrangement, which could be one of the following: <br> - Augmented <br> - Guaranteed (Imp) <br> - Guaranteed (Exclusive) <br> - Guaranteed (Legacy) <br> - Deal PG (Imp) <br> - PG (3rd Party Pacing) <br> - Standard
House |
| Ad Type | Specifies the type of advertisement, such as: <br> - Banner <br> - Video <br> - NativeBanner <br> - Video <br> - Native|
| Viewability Rate | The percentage of viewability, ranging from 0% to over 100%.|
| Trafficker | The individual responsible for trafficking the advertisement.|
| Salesperson | The salesperson associated with the advertisement or campaign.|

## Search by Name/ID

- Enter a **full or partial** name or ID in the search box.  
- Use the wildcard symbol `%` to broaden your search.  
  - Example: Searching for `%deal` will return all line items containing "deal" in their name.  

### Advanced Filter options

In addition to searching by Name/ID, you can filter line items using:

| Filter Type| Available Options| Description |
|---------------|----------------------|----------------------|
| **Status** | Active, Paused, or Completed |Filter based on the status of the line item.|
| **Date Range**| Flight start or end date| Filter by the flight start or end date. |
| **Campaign Association** | Specific campaigns | Show only line items linked to specific campaigns.|
| **Budget** | Remaining or spent budget | Filter based on the remaining or spent budget. |

To access these filters, navigate to **Advertisers** → **Line Items** or select the **Line Items** button on the **Order settings** screen.  

## Find inactive line items

Line items with the **Inactive** state are shown with their IDs, names, and quickstats in gray italics.

## View line item details

To view a summary of details about a line item, just click the line item's name. To see a full, detailed summary and a graphical view of delivery and performance, click the **graph** icon that appears when you hover over the line item (it's next to the pencil).

For more information about line item details, see [View Line Item Details](view-line-item-details.md).

## View quickstats

The metrics on the **Line Items** screen help you quickly assess the performance and delivery of your line items. Known as "quickstats", these metrics are faster and more readily
accessed than standard reporting data. Quickstats are cached on a regular basis and are shown whenever you open the Line Items screen.

> [!NOTE]
> Quickstats may not match the data from standard reporting exactly for technical reasons. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).
> [!TIP]
> To sort your line items by any given quickstat, click on the column name, e.g., **Profit**.

## Intervals

Use the drop-down at the top right of the screen to choose the interval for quickstats. Available intervals include:

- **Today** Current calendar day up to the last hour.
- **Yesterday** Full 24-hour period of the previous calendar day.
- **Last 7 Days** Full 7 days previous to the current calendar day, i.e., excluding today.
- **Lifetime** Entire lifetime of each line item, including the current calendar day.

## Columns

The following quickstats are shown for each line item. Note that the data always reflects the currently selected quickstats interval:

| Line Item | Name of the line item. |
|--|--|
| **ID** | Unique auto-generated number that is assigned to the line item. |
| **Bid Win Rate (last 10 mins)** | Percentage of impressions you won in the last 10 minutes out of those you bidded on. |
| **Campaigns** | Number of campaigns associated to the line item. |
| **Creatives** | Specifies the object to which the creative is attached (campaign or line item). |
| **Imps** | Number of impressions for all campaigns under the the line item. |
| **Clicks** | Number of clicks for all campaigns under the line item. |
| **Conversions** | Number of times conversion pixels under the line item have loaded. Note that a conversion pixel load does not necessarily mean that a conversion was attributed to one of the advertiser's campaigns. |
| **CTR** | The overall click-through rate on this line item's creatives. |
| **Viewable Imps** | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| **View-Measured Imps** | The total number of impressions that were measured for viewability. |
| **Viewability Rate** | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| **View Measurement Rate** | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| **Rev (USD)** | Money the advertiser has paid or will pay your network as a result of campaigns under the line item.<br>**Tip**: Using the currency toggle, you can choose whether to show **Rev** in USD or in the currency set at the line item. However, note that pacing bars are not available when viewing revenue in a currency other than USD. |
| **Media Cost (USD)** | Money your network has spent buying media for campaigns under the line item. Media Cost always appears in USD (the currency in which Microsoft Advertising transacts). |
| **Third Party Costs (USD)** | Aggregated data costs for all third-party services and data used when purchasing media (e.g., user segments) from the Microsoft Advertising Data Marketplace. |
| **Profit (USD)** | Money your network has made from the advertiser as a result of campaigns under the line item. This is revenue minus media cost. Profit always appears in USD. |
| **Rev eCPM** | Money the advertiser has paid or will pay your network per 1000 impressions.<br>Tip: Using the currency toggle, you can choose whether to show **Rev eCPM** in USD or in the currency set at the line item. |
| **Cost eCPM (USD)** | Money your network has spent buying media per 1000 impressions. Cost eCPM always appears in USD (the currency in which Microsoft Advertising transacts). |
| **Rev eCPA (USD)** | Total booked revenue earned per conversion. |
| **Cost eCPA (USD)** | Money your network has spent buying media per 1000 attributed conversions. Cost eCPA always appears in USD (the currency in which Microsoft Advertising transacts). |
| **Rev eCPC (USD)** | Total booked revenue earned per click. |
| **Days into Flight** | Number of days since the line item’s current flight began. |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the **Convs** column, see [Reporting on Conversions](reporting-on-conversions.md).

## Show/hide columns

You can choose the columns that are displayed by clicking the **Configure Columns** button on the upper right.

This opens the **Configure Columns** dialog. From there you can select or deselect the columns you wish to display using the checkboxes. Click **OK** when you are done making your selections to return to the **Line Items** screen.

## Show/hide pacing bars

For line items that meet certain requirements (see below), Microsoft Monetize helps you visualize how well the line items are pacing to their budgets for the selected quickstats interval. When you turn the Pacing toggle on, the Imps or Revenue quickstat, depending on the type of budget set for the campaign, is transformed into a pacing bar.

> [!IMPORTANT]
> It is important to note that pacing bars, like all other quickstats, reflect the currently selected quickstats interval, and for each quickstats interval, there are specific > requirements for pacing to be calculated. See below for more details.
>
> For guaranteed line items with a **vCPVM** revenue type, the information displayed in the pacing bars is not based on viewable impressions yet, but we're working on it. For now, you can surface delivered viewed impressions in the grid by:
>
> 1. Clicking the grid edit button next the **Export to CSV** button.
> 1. Checking the **Viewable Imps** checkbox in the dialog that appears.
>
> For more information about viewability, see our [Introduction to Viewability](introduction-to-viewability.md).
>
## Understand pacing bars

Each pacing bar tells you the following. Note that for a line item with a revenue budget, the pacing bar will show revenue rather than impressions.

- The pacing bar shows **how much of the line item budget has been spent.**
- The bold black number that appears across the pacing bar shows **the number of impressions or amount of dollar spend that has actually occurred for the line item.**
- The gray number below the pacing bar shows **the lifetime budget, in impressions or currency.**
- The blue line represents how much of your budget you should have spent: **lifetime budget/total number of days in the flight x actual number of days in the flight.**
- The percent shows how closely your line item is pacing according to even daily pacing: **actual budget spent/how much of your budget you should have spent.**

The exact requirements for calculating pacing depend on the quickstats interval selected, the type of budget set, and whether or not there's a flight end date. For each quickstats interval, the requirements are as follows:

| Quickstats Interval | Requirements |
|--|--|
| Lifetime | Lifetime Budget and Flight End Date |

## Report on line items

You can initiate a report for one or more line items directly from this screen. Check the box for each line item that you want to report on and click **Actions >  Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md), where the line items you selected are set as filters. For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).

## Activate/deactivate line items

You can activate or deactivate one or more line items directly from the **Line Items** screen. Check the box next to each line item that you want to activate or deactivate and click **Actions >  Activate** or **Actions >  Deactivate**.

When you deactivate a line item, the line item will typically stop serving within 10 - 15 seconds, with a maximum wait time of approximately 60 seconds.

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
