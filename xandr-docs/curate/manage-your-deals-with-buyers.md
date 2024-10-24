---
title: Microsoft Curate - Manage Your Deals with Buyers
description: Learn how as a seller, you can manage all deals you have with buyers on the Deals screen. This page covers exploring, filtering, monitoring, creating, editing, deleting, cancelling and reporting deals. 
ms.date: 11/14/2023
---


# Microsoft Curate - Manage your deals with buyers

> [!NOTE]
> As of May 3, 2021, Imps Matched and Bid Requests will be randomly sampled at a rate of 10 percent. The sampled values will be multiplied by 10 to give a reasonable estimate in all screens where these two metrics are reported. No other deal metrics will be affected.

As a seller, you can manage all deals you have with buyers on the **Deals** screen. You can view deal details, monitor each deal's health, trigger detailed reports, edit or cancel deals, and create new deals.

You can also manage your deals with a specific buyer on the [Partnership Details Screen](partnership-details-screen-buyer-view.md).

## Access the Deals screen

To reach the **Deals** screen, select **Inventory** \> **Seller Deals** in the main navigation.

## View basic and advanced deal metrics

The following details display for each deal. Columns that show an arrow in the header when you hover over them are sortable.

- **Deal ID** - The ID of the deal.
- **Imps Matched** - The number of impressions matched to the deal.
- **Bid Requests** - The total number of bids requested from the buyer.
  
  > [!NOTE]
  > For deals with an on-platform buyer, **Bid Requests** will equal **Imps Matched**. For deals with an external bidder, filtering due to the bidder's profile may reduce the number of Bid Requests.

- **Bid Rate** - The buyer's participation rate in the deal, which is the percentage of auctions in which the buyer bid.

  > [!NOTE]
  > When the Microsoft Advertising Impbus is doing the bidding for on-platform deals, all deals will be eligible for participation because they will have already passed quality and other eligibility checks on the platform. When third-party deals are active, the total number of bids may be greater than the number of bids marked eligible.

- **Final Bids** - The total number of auctions on which a buyer submitted eligible bids to participate in the deal.
- **Imps Sold** - The total number of imps sold on a given deal.
- **Gross Win Rate** - The percentage of impressions the buyer won out of bid requests sent to the buyer. This figure will be approximately equal to **Imps Won** divided by **Bid Requests**.
- **Net Win Rate** - The percentage of impressions the buyer won out of those the buyer bid upon. This figure will be approximately equal to **Imps Won** divided by **Bids**.
- **Ineligible Bids** - Information about bid ineligibility and the reasons bids were rejected.
  - **% Ineligible**- The percent of bids deemed ineligible.
  - **Reason** - The reason bids were rejected.

    > [!NOTE]
    > For more information on bid rejections, Impbus error codes, and  actions buyers and sellers can take to resolve errors, see [Understand Bid Rejections](understanding-bid-rejections.md).

- **Avg. Net Bid**- The average net bid CPM over all bids received. This figure does not include fees.
- **Floor**- The average floor price applied to all bids received, including both the deal floor and YM floors.
- **Rev eCPM** - The average revenue you made per bid on this deal. This figure has fees removed.
- **Revenue**- Your total revenue from this deal during the selected time interval, after fees. This value will be approximately equal to **Imps Sold** multiplied by Rev **eCPM** and divided by 1000.
- **Deal Settings**:
  - **Start/End Date** - The start and end dates for the deal.
  - **Type**- The auction type. For more information on the different auction types, see [Deal Auction Mechanics](deal-auction-mechanics.md).
  - **Ask Price** - The price, if any, associated with the deal. This is the minimum amount you must bid in order to compete for the deal inventory.
  - **Suggested Min Bid** - The minimum bid value that will clear the seller's deal floor, net of fees.
  - **From Package** - Indicates whether or not the deal was generated from a package. Deals associated with a package are affected if the package's status changes.

## Filter and search for deals

By default, you see all current deals. Use the **Filters** in the left column to filter by deal status or buyers, or use the search boxes to search for specific deals or buyers.

## Monitor deal health

Review the statistics for your deals to see how they are performing. If the number of deal impressions shown is low, there may be an issue with your deal settings or with your inventory. If the number of deal impressions the buyer has bid on is low, the buyer may have campaign setup issues.

## View a specific deal's details

Select a deal to display the **Details** pane, where all of the deal's details are visible. You can use the slider to resize the pane as desired. You can edit or duplicate a deal directly from the **Details** pane using the **Edit** or **Duplicate** button.

## Create a new deal

Select **New** to create a deal. For step-by-step instructions on creating a deal, see [Create a Curated Deal Line Item](create-a-curated-deal-line-item.md).

## Duplicate a deal

Use the duplicate feature to easily create a new deal that is similar to an existing deal, or to create the same deal for a different buyer. Hover over the deal you would like to copy in order to display the duplicate icon, and then Select the duplicate icon to display the **Create Deal** panel.

## Edit a deal

Current and upcoming deals can be edited at any time. Hover over the deal you would like to update in order to display the edit icon, and then Select the edit icon to make the deal editable.

> [!WARNING]
> Campaigns targeting the deal will be immediately affected by the changes you make. Use the Activity Stream on the [Partnership Details Screen](partnership-details-screen-buyer-view.md) to communicate with the buyer before making changes to the deal dates, auction type, inventory, segment, creative size, or brand.

After you have made the necessary updates, Select **Save** to save your changes. To exit edit mode, Select **Cancel**.

## Cancel a deal

If a current or upcoming deal no longer works for you, you can cancel it at any time. Check the checkbox near a deal, and then Select **Actions** \> **Cancel Deals**.

> [!WARNING]
> Campaigns targeting the deal will stop serving when you cancel the deal. Use the Activity Stream on the  [Partnership Details Screen](partnership-details-screen-buyer-view.md) to communicate with the buyer before canceling the deal.

## Report on deals

You can run reports to see how your deals are performing. Check the checkbox near the desired deals, and then Select **Actions** \> **Show in Reporting**.

Select **Run Report** in the reporting screen to run the report with these settings, or select additional settings as desired and then Select **Run Report**.

## Report on creatives served

To see which creatives have already served through a particular deal, Select the name of the deal you wish to review. In the details pane that opens below, under **Allowed Creatives**, Select the link under the **Creatives Served** header.

This will open the reporting tab, where you can run a Seller Brand Review report that has been pre-populated with the right filters and dimensions for you.

Select **Run Report** to run the report with these settings, or select additional settings as desired and then Select **Run Report**.

## Switch to buyer mode

If you are a network that also represents **sellers**, Select the Sellers button to view all of the deals you have as a buyer.

## Related topics

[Partnership Details Screen - Seller View](partnership-details-screen-seller-view.md)
