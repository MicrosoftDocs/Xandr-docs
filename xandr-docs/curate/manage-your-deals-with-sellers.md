---
title: Microsoft Curate - Manage Your Deals with Sellers
description: Learn to manage all deals you have with sellers on the Deals screen. This page covers exploring, filtering, searching, reporting on deals and switching to seller mode to view all your deals you have as a seller.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---


# Microsoft Curate - Manage your deals with sellers

You can manage all deals you have with sellers on the **Deals** screen. You can view basic and advanced deal metrics, monitor each deal's health, and run detailed reports.

You can also manage your deals with a specific seller on the **Partner Details** screen, see [Partnership Details Screen](partnership-details-screen-buyer-view.md) for more information.

> [!NOTE]
> Information the user should notice even if skimmingNote: For information on setting deal preferences, declining deals, managing the status of deals, and assigning internal names (deal alias) to deals see [Control Your Deals with Sellers](control-your-deals-with-sellers.md).

## Access Deals screen

To reach the **Deals** screen, select **Inventory** \> **Seller Deals**.

## View basic and advanced deal metrics

The following details display for each deal. Columns that show an arrow in the header when you hover over them are sortable.

- **Seller** - The name of the seller with whom you have the deal.
- **Deal Name** - The name of the deal.
- **Deal Alias** - The internal name of the deal assigned by buyer. See [Control Your Deals with Sellers](control-your-deals-with-sellers.md).
- **Buyer Deal Status** - The buyer deal status. See [Control Your Deals with Sellers](control-your-deals-with-sellers.md).
- **Deal ID** - The ID of the deal.
- **Imps Matched**- The number of impressions eligible for the deal.
- **Bid Rate** - Your participation rate in the deal, which is the percentage of impressions on which you bid.
- **Bids** - The total number of times you bid on the deal.
- **Submitted Bids** - If the deal is with an SSP, **Submitted Bids** is the number of your bids that were submitted to the SSP, which may be a lower number than **Bids**.
- **Imps Won** - The total number of impressions you won on the deal. This figure will be approximately equal to **Bids** multiplied by **Net Win Rate**.
- **Gross Win Rate**- The percentage of impressions you won out of those which were available to bid upon. This figure will be approximately equal to **Imps Won** divided by **Imps Matched**.
- **Net Win Rate** - The percentage of impressions you won out of those on which you bid. This figure will be approximately equal to **Imps Won** divided by **Bids**.
- **Ineligible Bids**
  - **% Ineligible**- The percent of bids that were ineligible to participate in the deal.
  - **Reasons** - The reasons why bids were rejected, shown in a color-coded bar.

  > [!NOTE]
  > For more information on bid rejections, Impbus error codes, and actions buyers and sellers can take to resolve errors, see [Understanding Bid Rejections](understanding-bid-rejections.md).

- **Winning eCPM** - The average value of your bids which won impressions on this deal. The average is taken after the auction is won, but before price-reduction.
- **Cost eCPM** - The average cost of your bids which won impressions on this deal. This average includes price-reduction.
  
  > [!TIP]
  > The difference between **Winning eCPM** and **Cost eCPM** indicates the amount of price reduction occurring and may reveal information about price floors and bid density that can inform bidding strategy.
  
- **Media Cost** - Your total cost on this deal during the selected time interval. This value will be approximately equal to **Imps Won** multiplied by **Cost eCPM**, divided by 1000.
- **Deal Settings**
  - **Start/End Date** - The start and end dates for the deal.
  - **Type**- The auction type.
  - **Ask Price** - The price, if any, associated with the deal. This is the minimum amount you must bid in order to compete for the deal inventory.
  - **Suggested Min Bid** - The minimum bid value that will clear the seller's deal floor, net of fees.
  - **From Package** - Indicates whether or not the deal was generated from a package. Deals associated with a package are affected if the package's status changes.

## Filter and search for deals

By default, you see all current deals. Use the filters in the left column to filter by deal status or sellers, or use the search boxes to search for specific deals or sellers.

## View a specific deal's details

Select a deal to display the **Details** pane, where all of the deal's details are visible. You can use the slider to resize the pane as desired.

## Generate deal reports

Run a report to see how your deals are performing. Check the checkbox near the desired deals, and then select **Show in Reporting**. A new tab opens displaying the [Network Analytics Report](../monetize/network-analytics-report.md) with the selected deals as filters and **Deal** selected as a dimension.

Select **Run Report** in the reporting screen to run the report with these settings, or set additional settings as desired and then select **Run Report**.

## Switch to seller mode

If you are a network that also represents buyers, select the **Buyers** button to view all of the deals you have as a seller.

## Related topics

- [Control Your Deals with Sellers](control-your-deals-with-sellers.md)
- [Partnership Details Screen](partnership-details-screen-buyer-view.md)
