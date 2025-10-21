---
title: Microsoft Curate - Explore and Manage Advertisers
description: Use the Advertisers screen to view metrics about your advertisers. It provides quick access to each advertiser's details and child objects, and reporting options.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Explore and manage advertisers

The **Advertisers** screen is a management screen that shows you essential metrics about all your advertisers, provides quick access to each advertiser's details and child objects, and reporting options.

## Manage advertisers

- To reach the **Advertisers** screen, select **Package** > **Advertisers** in the menu bar.
- To edit an advertiser, hover over the row for the advertiser you want to edit and then select the pencil icon.
- To activate or deactivate an advertiser, select the checkbox for each advertiser you want to activate or deactivate and select **Activate** or **Deactivate**.
- To delete an advertiser, select the checkbox next to each advertiser you want to delete and select **Delete**.

  > [!WARNING]
  > Deleting an advertiser deletes all of its child objects as well, including insertion orders, line items, campaigns, creatives conversion pixels, and segments. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (revenue budget for line items, cost budget and targeting for campaigns, etc.).

## View metrics

The metrics on the **Advertisers** screen help you assess the performance and delivery of your advertisers at a glance. These metrics are faster and more readily accessed than via standard reporting whereas reporting requires you to submit a request and then wait for a response, these stats are cached on a regular basis and are shown whenever you open the **Advertisers** screen.

Because these stats are dependent upon reporting data and are synced after reporting has closed for any given hour, for a small chunk of time each hour, there may be discrepancies between reporting and the grid data. For more details, see [Availability of Reporting Data](./availability-of-reporting-data.md).

> [!TIP]
> To sort your advertisers by any statistic, select the relevant column.

### Columns

The following stats are shown for each advertiser. Note that the data always reflects the currently selected stats interval:

- **ID** - The unique identifier of advertiser.
- **Ins Orders** - Number of insertion orders under the advertiser.
- **Line Items** - Number of line items under the advertiser.

## View advertiser details

To view advanced details about an advertiser, select the advertiser you want to view. See [View Advertiser Details](./view-advertiser-details.md) for more information.

## View child objects

The **Ins Orders**, **Line Items**, and **Campaigns** columns show you the number of insertion orders (if used), line items, and campaigns below each advertiser. You can select these numbers to navigate to the complete list of objects with their stats.

## Filter details

The **Advanced Filters** menu lets you filter for advertisers based on **State**, **Advertiser Name**, and **External Code**. You can select **Inactive** or **Active** from the **State** menu. Select **Apply** or **Apply and Save As**. The **Apply and Save As** option will save your filter for future purpose. You can also select **Active filter** from **Select a Setting** menu, so only active advertisers are listed. Note that inactive advertisers are shown with names, IDs, and stats in italics.

## Search by name/ID

You can use the search field at the top of the screen to find all advertisers whose names or IDs include a specific string of characters or numbers.

## Report on Advertisers

You can initiate a Network Analytics report for one or more advertisers directly from the **Advertisers** screen. Select the checkbox for each advertiser that you want to report on and select **Run Report**.

This takes you to the Network Analytics report, where the advertisers you selected are set as filters.

## Related topics

- [Working with Advertisers](./working-with-advertisers.md)
- [View Advertiser Details](./view-advertiser-details.md)
- [Create an Advertiser](./create-an-advertiser.md)
