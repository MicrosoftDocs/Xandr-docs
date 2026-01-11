---
title: Microsoft Monetize - Seller Monitoring Workflow (SMW) grid for Advertisers
description: Explore advertiser's key role in setting up identity, orders, line items, creatives, and pixels for efficient digital buying.
ms.date: 1/12/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Seller Monitoring Workflow (SMW) grid for Advertisers

An advertiser is a company, agency, or other grouping that displays media creatives on publisher web and/or mobile inventory. The Advertiser object is the top level of the buy side of the [Object Hierarchy](object-hierarchy.md).
Setting up the advertiser defines the advertiser's identity as well as some of the buying terms. The advertiser also serves as a container for other objects including insertion orders, line items, creatives, and pixels that you can combine to begin buying digital inventory.

Creating the advertiser is the first step in the [Basic Buy-side Setup Procedures](basic-buy-side-setup-procedures.md) required for purchasing inventory.

## Explore and manage advertisers

The Advertisers screen is a management screen that shows you essential metrics about all your advertisers, provides quick access to each advertiser's details and child objects, and reporting options. To access the Advertisers screen, navigate to **Advertisers >Advertisers** from the left pane. 
<!-- - You can edit an Advertiser directly from the **Advertisers** screen by selecting the pencil icon next to the Advertiser's name or you can also edit an Advertiser from the SMW screen. To do this, hover over the Advertiser you want to edit and select it. In the right pane, navigate to the **Settings** tab and select **Edit**. -->

## Search

You can use the search field at the top of the screen to find all advertisers whose names or IDs include a specific string of characters or numbers.

## Filters

The **Filters** menu lets you filter for advertisers based on Advertiser Name, External Code and State.

- You can select **Inactive** or **Active** from the **State** menu. 
- Click on **Apply** to save your filter for future purpose.

## Columns

The following stats are shown for each advertiser. Note that the data always reflects the currently selected stats interval:

- **ID:** The unique identifier of advertiser.
- **External Code**: The user defined code for the advertiser (rather than the internal ID that Microsoft Advertising assigns automatically) used in reporting
- **Ins Orders:** Number of insertion orders under the advertiser.
- **Line Items:** Number of line items under the advertiser.
- **Rev Delivery (Last 7 days):** Money the advertiser has paid or will pay your network for clicks or conversions for full 7 days previous to the current calendar day, i.e., excluding today. This is based on revenue settings at the line item level.
- **Imps Delivery (Last 7 days):** Number of impressions for all line items under the advertiser for full 7 days previous to the current calendar day, i.e., excluding today.
- **Viewability Rate IAB (Last 7 days)**: The percentage of impressions that were viewable out of the total number of impressions measured for IAB viewability for full 7 days previous to the current calendar day, i.e., excluding today.
- **Viewability Rate Custom (Last 7 days)**: The percentage of impressions that were viewable out of the total number of impressions measured for viewability for full 7 days previous to the current calendar day, i.e., excluding today.

## Edit columns and sort
You can customize the columns that appear on the Advertisers screen. Use **Edit columns and sorts** to add, remove, or reorder columns in the grid.

Columns are grouped into the following categories.

### Basic info

| Column            | Description                                         |
| ----------------- | --------------------------------------------------- |
| **ID**            | The unique ID of the advertiser.                    |
| **External Code** | An optional external identifier for the advertiser. |

### Performance

| Column                                    | Description                                                                                                   |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Rev Delivery (Last 7 Days)**            | The amount of revenue delivered by the advertiser in the last seven days.                                     |
| **Imp Delivery (Last 7 Days)**            | The number of impressions delivered by the advertiser in the last seven days.                                 |
| **CTR (Last 7 Days)**                     | The click-through rate for impressions delivered by the advertiser in the last seven days.                    |
| **Deal Revenue**                          | The amount of revenue generated from deals associated with the advertiser.                                    |
| **Viewability Rate IAB (Last 7 Days)**    | The percentage of impressions that were viewable according to IAB standards in the last seven days.           |
| **Viewability Rate Custom (Last 7 Days)** | The percentage of impressions that were viewable based on custom viewability settings in the last seven days. |

### Related objects

| Column         | Description                                                    |
| -------------- | -------------------------------------------------------------- |
| **Ins Orders** | The number of insertion orders associated with the advertiser. |
| **Line Items** | The number of line items associated with the advertiser.       |

Click on **Apply** to save your settings.

## Managing advertisers - bulk action toolbar

- To activate or deactivate one or more advertisers, check the box for each advertiser you want to activate or deactivate and click **Activate** or **Deactivate** as required.
- To delete one or more advertisers, check the box next to each advertiser you want to delete and click **Delete**.
- To run a report on one or more advertisers, check the box for each advertiser you want to report on and click **Run Report**.
  > [!WARNING]
  > Deleting an advertiser deletes all of its child objects as well, including insertion orders, line items, campaigns, creatives, conversion pixels, and segments. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (revenue budget for line items, cost budget and targeting for campaigns, etc.).

## Viewing advertiser details

To view advanced details about an advertiser, click on the advertiser you want to view. See [View Advertiser Details](view-advertiser-details.md) for more information.

## Download

You can download advertiser details by selecting the advertiser(s) and clicking on **Download** button.

