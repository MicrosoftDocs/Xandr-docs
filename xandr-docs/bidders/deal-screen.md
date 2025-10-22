---
title: Deal Screen
description: Highlight the deals screen, informing bidders about publisher deals. Utilize buyer Access Service for additional details.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Deal screen

The **Deals** screen is where a bidder can see the deals Xandr publishers have set up with their buyers and get further details about the deal. For additional details on the deal, bidders can use the [Deal Buyer Access Service](deal-buyer-access-service.md).

## Deal screen access

1. Sign in to the Bidders UI: [https://bidder.xandr.com](https://bidder.xandr.com/)
1. Select the bidder.
1. Click **Switch to Default User**. The **Profiles** screen is accessed.
1. Click on the **Deals** tab to access the **Deals** screen. (It is located to the right of the **Profiles** tab).

## Main screen metrics

The Main deal screen lists all of the deals for a bidder, and their associated attributes/metadata. The table below details each of the columns displayed:

| Column Name | Filterable | Description |
|--|--|--|
| **Buyers** | Yes | The buying member or seat who can target this deal. Can be Xandr Member ID or DSP `Buyer Seat ID`.<br>Both the ID and name for the buyer is listed in this column. |
| **Sellers** | Yes | The selling member who is offering the deal. <br>Both the ID and name for the seller is listed in this column. |
| **Activity Status** | Yes | Indicates if deal is Active or Inactive. |
| **Deal Name/ID** | Yes | Name of the deal and Xandr Deal ID. |
| **Deal Types** | Yes | The type of deal. A deal can be an **open auction** or a **private auction**.<br> - **Open Auction**<br>: In an "Open Auction", **buyers targeting the deals and buyers targeting the inventory via other means compete for the impression.** If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction, paying either the second-highest bid or the deal floor price, whichever is higher. If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid or ECP, whichever is higher. <br> - **Private Auction**<br>: In a "Private Auction", **buyers targeting the private deals compete for the impression first**. Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction, paying either the second-highest bid from the private auction or the deal floor price, whichever is higher. If no private auction deals clear their floors, the highest bid in the open auction wins, paying either the second-highest bid from the open auction or ECP, whichever is higher.<br>For examples showing how these different types of auctions work, see [Deal Auction Mechanics](deal-auction-mechanics.md). |
| **Ask Price** | No | The  price associated with the deal. This is the minimum amount the seller will accept for this inventory. |
| **Start Date** | Yes | The day and time when the deal starts being available to the buyer. Null corresponds to "immediately". |
| **End Date** | Yes | The day and time when the deal stops being available to the buyer. Null corresponds to "indefinitely". |
| **Last Modified** | Yes | The date and time when the deal was last modified. |
| **Imps Won** | No | The total number of impressions won.<br>Can select data from: <br> - Today<br> - Yesterday<br> - Trailing 7 days<br> - Last 30 days |
| **Imps Matched** | No | The total number of impressions that match the seller's settings on the deal. |

## How to filter data on main screen

To filter data by any of the filterable columns (see table above):

1. Click on the column heading to enable the search box or filter selection values.
1. Once you select your filter values, click on the **Search** button on the top right hand corner.
1. Your search results will display on the main screen.

## Side panel

Access additional details about the deal by clicking on the deal row to open a side panel. The below deal details are included in the side panel display.

> [!NOTE]
> If the field is not present in the side panel, it means the details is not applicable to the deal.

| Field Name | Description |
|--|--|
| Seller | The seller name and Seller ID (included in parenthesis) for the deal. |
| Buyer | The buyer member id or buyer seat ID eligible to bid on the deal. Id is included in parenthesis. |
| Type | Details whether the deal is:<br> - public deal<br> - private deal<br> - programmatic guaranteed deal |
| Imps Matched | The total number of impressions that match the deal's targeting. |
| Bid Requests | The number of bid requests sent that include the deal. |
| Bids Received | The number of times a buyer bids. |
| Bid Rate | The percentage of deal auctions in which the buyer bid |
| % Ineligible | The percentage of bids rejected due to errors (Learn more about bid errors: [Bid Error Codes](bid-error-codes.md)). |
| Imps Sold | The total number of impressions won. |
| Spend | Total spend on the deal in USD. |
| Gross Win Rate | The percentage of impressions won out of all imps matched. |
| Net Win Rate | The percentage of impressions won out of all bids on deal. |
| Deal Name | Name for the deal in Xandr systems. |
| Price | The ask price or bid floor for the deal. |
| Lifetime Budget | The negotiated impression amount to be delivered on the deal (relevant only to PG deals). |
| Auction Type | The pricing type for the deal. Possible values: first price, second price, and fixed price. |
| Start Date | Starting date for the deal. |
| End Date | End date for the deal. |
| Media Type | Allowed media types for deal. |
| Sizes | Allowed creative sizes for deal. |

## Download Data

Users can download data displayed from the main deal screen by clicking the "download view" and **download last xx** buttons on the top right hand side of the deal screen.

**Download View:** This will download all the deals currently displayed on the screen into a CSV file.

**Download last XX:** This will download all of the deals currently displayed on the screen as well as all deals in previous pages. For example, if user is viewing page 3 of the deals list, then deals from all 3 pages will be downloaded to the CSV.
