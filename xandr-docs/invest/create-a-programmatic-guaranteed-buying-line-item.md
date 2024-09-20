---
title: Microsoft Invest - Create a Programmatic Guaranteed Buying Line Item
description: This page covers prerequisites and steps to setup a Programmatic Guaranteed Buying Line Item in Microsoft Invest. 
ms.date: 10/28/2023
---

# Microsoft Invest - Create a programmatic guaranteed buying line item

A programmatic guaranteed buying line item (PG line item) provides you with a workflow specifically designed for buying a programmatic guaranteed deal (PG deal).

A PG line item can only target one PG deal. PG line items have very different targeting, budgeting, and optimization options compared to augmented line items. For more information before creating one, see [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md).

## Before you begin

Before you create a PG line item, you must perform the following tasks:

- [Create an Advertiser](create-an-advertiser.md)
- [Create an Insertion Order](create-an-insertion-order.md)

The insertion order you created must have at least one Billing Period with dates in the future.

You must also have access to one or more PG deals to target. Sellers must first create these deals for buyers to access them for targeting. If you have questions about how to gain access to a PG deal, contact your account manager.

The following tasks are recommended but not required:

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)

## Start a new PG line item

To create a new PG line item, do the following:

1. Select **Create New** in the **Line Item** menu or section. If prompted, select an advertiser in the **Select an Advertiser** screen. The **Create New Line Item screen** opens.
1. On the **Create New Line Item** screen, select **Programmatic Guaranteed** under **Line Item Type**.

   > [!IMPORTANT]
   > You must have an **advertiser** and **insertion order** associated with the line item in the Advertiser and Insertion Order sections. If necessary, select an advertiser and insertion order.

1. Select **Next** to open the **Create a Programmatic Guaranteed Line Item** screen.

## Basic setup

In the **Basic Setup** section, enter the following details for the PG line item:

- **Programmatic Guaranteed Deal**: The Programmatic Guaranteed Deal associated with the PG line item. Enter the name of the PG deal and select it. The details of the PG deal are displayed and include the following:
  
  > [!IMPORTANT]
  > The PG deal details shown are configured by the seller of the deal and cannot be changed by settings in the PG line item.

  - **Seller**: Name of the seller of the deal.
  - **Start Date**: The Date the deal becomes active.
  - **End Date**: The Date after which the deal is no longer active.
  - **Projected Media Cost**: Total projected media cost derived from the projected number and price of impressions reserved for this PG deal.
    - **Impressions**: Number of impressions reserved for this PG deal.
    - **Price**: Price of impressions for this PG deal.
  - **Geo Targeting**: Location of geo-targeting used by this PG deal.
- **Insertion Order**: The insertion order associated with this PG line item. If you create the line item from the **Insertion Order Details** screen, the insertion order is automatically associated. Otherwise, select **Edit** to associate the line item with an insertion order.
  
  > [!NOTE]
  > PG line items **override** insertion order budgets, all levels of targeting, and any established frequency caps to ensure you fulfill your agreement with the publisher. PG line items **do not override** insertion order flight dates. You can keep a PG line item from being spent by setting it to **"Inactive"** at any time.

- **Line Item Name**: Enter the name for the PG line item. You will later be able to search for and report on this PG line item using this name.
- **External Code**: If you want to report on this PG line item using an external code, enter the code here. The code may only contain alphanumeric characters, periods, underscores, or dashes. The code you enter is not case-sensitive (i.e., uppercase and lowercase characters are treated the same). PG line items associated with the same advertiser cannot use the same external code.
- **State**: Set the state of the line item. If **"Active"**, the line item will be eligible to serve.
- **Revenue Type - Cost Plus**: It's the required revenue type for PG line items. With **Cost Plus**, the advertiser will pay for your media cost (whatever you spend on buying inventory) plus an extra amount (a margin) that you charge the advertiser in addition to the media cost. You can set this margin as a percentage of cost (**% margin**) or as a fixed CPM fee (**CPM margin**). You must enter a percentage for **% margin** or a fee for the **CPM margin** greater than or equal to zero.

## Optimization

You can use conversion tracking on PG line items; see [Create a Conversion Pixel](create-a-conversion-pixel.md).

## Conversion tracking

Select the **edit** icon to associate conversion tracking pixels with this PG line item. Note that these pixels aren't used by optimization but can be used to track the line item's performance.

## Associated creatives

### Creative requirements for this PG deal

The creative requirements for the PG deal associated with this PG line item are displayed here.

> [!IMPORTANT]
> The PG line item must be associated with a PG deal for the **Creative Requirements for this PG Deal** to display (see [Basic Setup](#basic-setup) to assign a PG deal to the PG line item). The seller of the PG deal configures these creative requirements, and settings in the PG line item can't change them. You must have at least one associated creative for each media type and ad size listed for the PG deal.

- **Media Type**: Creative media type for the PG deal.
- **Ad Sizes**: Ad size for the PG Deal.

> [!NOTE]
> Prior to transacting on a PG deal, confirm with its seller that the creatives you wish to serve meet their deal's creative format, size, and technical attribute requirements.

### Creative rotation

Select the creative rotation strategy you want to use:

- **Auto-optimize creative weight**: The creative with the highest click-through-rate (CTR) delivers the most.
- **Evenly weight creatives**: Even rotation is handled automatically by our system.
- **Manually weight creatives**: Rotation is based on a user-supplied weight.

## Select creatives

1. Select the creatives you want to associate with your PG line item from the **Search creative name or ID** list by checking the box next to the name, or enter multiple creatives using the **Paste List of IDs**. Selected creatives will appear in the **Creatives Associated** list. Ensure that you have at least one associated creative for each media type and ad size listed in the **Creative Requirements for this PG Deal**.
1. Select specific flights or custom dates that fall within the date range for the Programmatic Guaranteed deal to schedule when associated creatives will serve by doing the following, if necessary:

   1. Select the corresponding checkbox for a creative and select the **pencil icon** in the Dates section.
   1. Choose **All Flight** or select the **Select Dates** button from the **Associate Dates** dialog if the creative will serve during specific flights.
   1. Select start and end dates to specify a date range that doesn't include any dates before the start date or after the end date of the deal. For example, if the flight has a start date of November 1 and an end date of December 1, then the custom date range cannot be any date before November 1 or after December 1. You can add multiple flights using the **Add Another** button.
   1. Select **Apply**.
1. When you finish making your selections, select **Save**.

## Reporting labels

Reporting labels allow you to report by metrics that are important to your business (see [Reporting Labels](reporting-labels.md)). You can assign the following labels to a PG line item:

> [!IMPORTANT]
> It will take about 30 minutes for the labels to show up in reporting.

- **Trafficker**: PG Deal Trafficker
- **Sales Rep**: PG Deal Sales Representative
- **Line Item Type**: Type of line item (e.g., PGLI)

## Fees

Select inside the **Associated Fees** search box to see a list of eligible third-party partner fees, or search for a fee name and select the desired fee. Fees required for all of the advertiser's line items are already applied automatically and are indicated by a lock icon.

For more information, see [Partner Fees](partner-fees.md).

## Comments

You can add comments to the PG line item in the **Comments** box. Comments are for reference only and will not affect the performance of the PG line item.

## Projected impact overview

The **Projected Impact Overview** calculates the projected spend, media cost, partner fees, and revenue for a line item based on your current settings. It is composed of the following parts:

- **Spend Breakdown**: The media cost and the Buyer Auction Service Charge (BASC) charged by Microsoft Advertising. For more information on BASC, see [Understanding Your Pricing Terms](understanding-your-pricing-terms.md) (separate login required).
- **Partner Fees**: Third-party fees associated with the line item.
- **Revenue**: The projected margin based on the line item's revenue type.

## Review and save changes

Review the PG line item configuration and select **Save**.

## Related topics

- [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md)
- [Bid Performance Messages for Programmatic Guaranteed Buying Line Items](bid-performance-messages-for-programmatic-guaranteed-buying-line-items.md)
- [Troubleshoot your Programmatic Guaranteed Buying Line Item Bid Performance](troubleshoot-your-programmatic-guaranteed-buying-line-item-bid-performance.md)
