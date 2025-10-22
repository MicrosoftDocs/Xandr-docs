---
title: Data Buyer Workflow
description: To access a particular data provider's segment offering, a workflow is available to make that process easier, like selecting the data providers you want to access and running campaigns targeting these third-party segments.  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Data buyer workflow

Several changes have been made to help clear the Data Provider costs and to distinguish between Media costs and Third-party costs (e.g., for user segments, etc.). This article describes these changes, and they might affect your workflow.

## Adding data providers

To access a particular data provider's segment offering, a workflow is available to make that process easier.

After selecting the data providers you want access to, refresh the page and you will see that the data provider's segments are now visible on your account. At this point, you can now run campaigns targeting these third-party segments.

## Campaign changes

When creating or editing campaigns, select **Pay on a per-impression (CPM) basis** under **Buying Strategy** and then select the option Bid a Media Cost CPM.

Once set, you can confirm these changes and click **Save**.

When selecting targeting options, if you select the **Edit** button in the **Targeting** section next to Segment, the Segments dialog displays.

The available segments (along with prices, when available) are then displayed in the Segments dialog.

You can select the various segments that you wish to include in or exclude from your targeting. To calculate the total costs of all segments selected, click **Calculate Data Cost**.

> [!NOTE]
> For any costs for which the yellow alert symbol is displayed, Xandr will not clear. These alerts denote one of the following conditions:
>
> For segments:
>
> - You have selected a segment for which the Data Provider has not supplied a price.
> - You have selected a segment from a Data Provider who is not participating in Xandr automating clearing.
> - You have selected a user-created segment (e.g., generated via a pixel) not supplied by a Data Provider.
>
> For Data Cost Totals:
>
> - One or more of the segments you selected fit the conditions listed above for segment alerts.

## Line item changes

When creating or editing line items, if you select **Cost Plus** as your Tracking Revenue Type, the Total Cost displays.
