---
title: Explore Line Items
description: The articles defines the Line Items screen that displays metrics for all line items under a specific advertiser, alerts about serving conditions, provides quick access to insertion order details and child campaigns, and offers bulk editing and reporting options.
ms.date: 10/28/2023
---

# Explore line items

The **Line Items** screen shows you essential metrics about all line items under a specific advertiser, informs you of conditions preventing line items from serving, provides
quick access to each insertion order's details and child campaigns, and offers bulk editing and reporting options.

For publishers, the Line Items screen is where you'll go to manage demand from your direct-sold advertisers, including standard and guaranteed delivery line items.

Things you can do on this page include:

- Use filters to quickly identify line items with specific criteria
- See delivery and performance metrics
- See important line item details and make changes quickly

## Get to the line items screen

To get to the line items screen:

- Select **Advertisers >  Line Items** from the navigation menu at the top of the screen.

  or

- From the **Advertisers** screen, find the advertiser whose line items you want to see and click the button in the **Line Items** column

Publisher users can:

- Select **Orders >  Line Items** from the navigation menu at the top of the screen.

  or

- Click **All Line Items** in the left panel on the Line Items or Orders screens.

Filter your Line Items

The column next to the line item's name (on the left) contains an icon that shows the current eligibility of that line item to serve. Possible eligibility icons include:

| Icon Type | Description |
|--|--|
| Play | The line item's campaigns are running smoothly. |
| Pause | Campaigns under the line item are inactive. Hover over |
| Warning | There are issues with the line item or its campaigns that are keeping it from serving. |
| Pause/Warning | Campaigns under the line item are inactive, and there are issues with the line item or its campaigns. |

Hover your mouse over the icon for details about that line item's state. Allowed states are:

- **Play** - Line items with the "play" icon are eligible to serve.
- **Paused** - Line items with the "paused" icon are ineligible to serve due to conditions that are likely intentional and user-driven. When a line item shows this status, hover over the icon to see exactly what conditions are preventing it from serving. The following conditions can provoke this status:
  - State is set to inactive.
  - Flight start is in the future.
  - Flight end is in the past.
  - Lifetime impression budget has been met.
  - Lifetime revenue budget has been met.
  - Daily impression budget has been met.
  - Daily revenue budget has been met.
  - All campaigns under this line item are inactive.

## Search by Name/ID

You can use the search field at the top of the screen to find all line items whose names or IDs include a specific string of characters or numbers.

## Find inactive line items

Line items with the **Inactive** state are shown with their IDs, names, and quickstats in gray italics.

## View line item details

To view a summary of details about a line item, just click the line item's name. To see a full, detailed summary and a graphical view of delivery and performance, click the graph icon that appears when you hover over the line item (it's next to the pencil).

For more information about line item details, see [View Line Item Details](view-line-item-details.md).

## View quickstats

The metrics on the Line Items screen help you quickly assess the performance and delivery of your line items. Known as "quickstats", these metrics are faster and more readily
accessed than standard reporting data. Quickstats are cached on a regular basis and are shown whenever you open the Line Items screen.

Note that Quickstats may not match the data from standard reporting exactly for technical reasons. For more information, see [Availability of Reporting Data](availability-of-reporting-data.md).

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
| ID | Unique auto-generated number that is assigned to the line item. |
| Bid Win Rate (last 10 mins) | Percentage of impressions you won in the last 10 minutes out of those you bidded on. |
| Campaigns | Number of campaigns associated to the line item. |
| Creatives | Specifies the object to which the creative is attached (campaign or line item). |
| Imps | Number of impressions for all campaigns under the the line item. |
| Clicks | Number of clicks for all campaigns under the line item. |
| Conversions | Number of times conversion pixels under the line item have loaded. Note that a conversion pixel load does not necessarily mean that a conversion was attributed to one of the advertiser's campaigns. |
| CTR | The overall click-through rate on this line item's creatives. |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| View Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Rev (USD) | Money the advertiser has paid or will pay your network as a result of campaigns under the line item.<br>Tip: Using the currency toggle, you can choose whether to show Rev in USD or in the currency set at the line item. However, note that pacing bars are not available when viewing revenue in a currency other than USD. |
| Media Cost (USD) | Money your network has spent buying media for campaigns under the line item. Media Cost always appears in USD (the currency in which Xandr transacts). |
| Third Party Costs (USD) | Aggregated data costs for all third-party services and data used when purchasing media (e.g., user segments) from the Xandr Data Marketplace. |
| Profit (USD) | Money your network has made from the advertiser as a result of campaigns under the line item. This is revenue minus media cost. Profit always appears in USD. |
| Rev eCPM | Money the advertiser has paid or will pay your network per 1000 impressions.<br>Tip: Using the currency toggle, you can choose whether to show Rev eCPM in USD or in the currency set at the line item. |
| Cost eCPM (USD) | Money your network has spent buying media per 1000 impressions. Cost eCPM always appears in USD (the currency in which Xandr transacts). |
| Rev eCPA (USD) | Total booked revenue earned per conversion. |
| Cost eCPA (USD) | Money your network has spent buying media per 1000 attributed conversions. Cost eCPA always appears in USD (the currency in which Xandr transacts). |
| Rev eCPC (USD) | Total booked revenue earned per click. |
| Days into Flight | Number of days since the line item’s current flight began. |

To get information about attributed conversions, rather than just conversion pixel loads as shown in the **Convs** column, see [Reporting on Conversions](reporting-on-conversions.md).

## Show/hide columns

You can choose the columns that are displayed by clicking the **Configure Columns** button on the upper 9right.

This opens the **Configure Columns** dialog. From there you can select or deselect the columns you wish to display using the checkboxes. Click **OK** when you are done making your selections to return to the Line Items screen.

## Show/hide pacing bars

For line items that meet certain requirements (see below), Microsoft Monetize helps you visualize how well the line items are pacing to their budgets for the selected quickstats
interval. When you turn the Pacing toggle on, the Imps or Revenue quickstat, depending on the type of budget set for the campaign, is transformed into a pacing bar.

> [!IMPORTANT]
> It is important to note that pacing bars, like all other quickstats, reflect the currently selected quickstats interval, and for each quickstats interval, there are specific requirements for pacing to be calculated. See below for more details.

For guaranteed line items with a **vCPVM** revenue type, the information displayed in the pacing bars is not based on viewable impressions yet, but we're working on it. For now, you can surface delivered viewed impressions in the grid by:

1. Clicking the grid edit button next the **Export to CSV** button.
1. Checking the **Viewable Imps** checkbox in the dialog that appears.

For more information about viewability, see our [Introduction to Viewability](introduction-to-viewability.md).

## Understanding pacing bars

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

You can initiate a report for one or more line items directly from this screen. Check the box for each line item that you want to report on and
click **Actions >  Run Report**. This takes you to the [Advertiser Analytics Report](advertiser-analytics-report.md), where the line items you selected are set as
filters. For further information about running the report, see [Advertiser Reporting](advertiser-reporting.md).

## Activate/deactivate line items

You can activate or deactivate one or more line items directly from the Line Items screen. Check the box next to each line item that you want to activate or deactivate and click
**Actions >  Activate** or **Actions >  Deactivate**.

When you deactivate a line item, the line item will typically stop serving within 10 - 15 seconds, with a maximum wait time of approximately 60 seconds.

## Related topics

- [Working with Line Items](working-with-line-items.md)
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
