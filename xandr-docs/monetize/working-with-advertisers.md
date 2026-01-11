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

## Managing advertisers - bulk action toolbar

- To activate or deactivate one or more advertisers, check the box for each advertiser you want to activate or deactivate and click **Activate** or **Deactivate** as required.
- To delete one or more advertisers, check the box next to each advertiser you want to delete and click **Delete**.
- To run a report on one or more advertisers, check the box for each advertiser you want to report on and click **Run Report**.
  > [!WARNING]
  > Deleting an advertiser deletes all of its child objects as well, including insertion orders, line items, campaigns, creatives, conversion pixels, and segments. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (revenue budget for line items, cost budget and targeting for campaigns, etc.).

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

