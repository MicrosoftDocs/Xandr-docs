---
title: Microsoft Monetize - Create a Programmatic Guaranteed Buying Line Item
description: In this article, find information on how to create and set up a programmatic guaranteed buying line item.
ms.date: 10/28/2023
---

# Microsoft Monetize - Create a programmatic guaranteed buying line item

A programmatic guaranteed buying line item (PG line item) provides you with a workflow specifically designed for buying a programmatic guaranteed deal (PG deal).

A PG line item can only target one PG deal. PG line items have very different targeting, budgeting, and optimization options compared to augmented line items. See [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md) for more information before creating one.

## Before you begin

Before you create a PG line item, you must perform the following tasks:

- [Create an Advertiser](create-an-advertiser.md)

- [Create an Insertion Order](create-an-insertion-order.md)

  The insertion order you created must have at least one Billing Period with dates in the future.

You must also have access to one or more PG deals to target. Sellers must first create these deals for buyers to access them for targeting. If you have questions about how to gain access to a PG deal, please contact your account manager.

The following tasks are recommended but not required:

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)

## Start a new PG line item

To create a new PG line item, do the following:

1. To get to the insertion orders screen:

1. Select **Advertisers** >  **Line Items** from the vertical navigation menu on left
1. Click **+ New**.
1. Select **Line Item**
1. On the **Line Item Type** screen, select **Guaranteed Delivery** under **Type**.
1. Click **Okay** to open the **Create a Programmatic Guaranteed Line Item** screen.

## Basic setup

In the **Basic Setup** section, enter the following details for the PG line item:

- **Programmatic Guaranteed Deal** - the Programmatic Guaranteed deal associated to the PG line item. Enter the name of the PG deal and select it. The details of the PG deal display and include the following:

  > [!IMPORTANT]
  > The PG deal details shown are configured by the seller of the deal and cannot be changed by settings in the PG line item.

  - **Seller** - name of the seller of the deal
  - **Start Date** - date the deal becomes active
  - **End Date** - date after which the deal is no longer active
  - **Projected Media Cost** - total projected media cost derived from the projected number and price of impressions reserved for this PG deal
    - **Impressions** - number of impressions reserved for this PG deal
    - **Price** - price of impressions for this PG deal
  - **Geo Targeting** - location of geo targeting used by this PG deal
- **Insertion Order** - the insertion order associated to this PG line item. If you create the line item from the **Insertion Order Details** screen, the insertion order is automatically associated. Otherwise, click **Edit** to associate the line item to an insertion order.
  
  > [!NOTE]
  > PG line items **override** insertion order budgets, all levels of targeting, and any established frequency caps to ensure you fulfill your agreement with the publisher. PG line items **do not override** insertion order flight dates. You can keep a PG line item from spending by setting it to "**Inactive**" at any time.

- **Line Item Name** - enter the name for the PG line item. You will later be able to search for and report on this PG line item using this name.
- **External Code** - if you want to report on this PG line item using an external code, enter the code here. The code may only contain alphanumeric characters, periods, underscores, or dashes. The code you enter is not case-sensitive (i.e., uppercase and lowercase characters are treated the same). PG line items associated to the same advertiser cannot use the same external code.
- **State** - set the state of the line item. If "**Active**", the line item will be eligible to serve.
- **Revenue Type** - **Cost Plus** is the required revenue type for PG line items. With Cost Plus, the advertiser will pay for your media cost (whatever you spend on buying inventory) plus an extra amount (a margin) that you charge the advertiser in addition to the media cost. You can set this margin as a percentage of cost (**% margin**) or as a fixed CPM fee (**CPM margin**). You must enter a percentage for **% margin** or a fee for **CPM margin** greater than or equal to zero.

## Optimization

You can use conversion tracking on PG line items, see [Create a Conversion Pixel](create-a-conversion-pixel.md).

## Conversion tracking

Click **Edit** to associate conversion tracking pixels to this PG line item. Note that these pixels are not used by optimization, but can be used to track the line item's performance.

## Associated creatives

### Creative requirements for this PG deal

The creative requirements for the PG deal this PG line item is associated to display here.

> [!IMPORTANT]
> The PG line item must be associated to a PG deal for the **Creative Requirements for this PG Deal** to display (see [Basic Setup](#basic-setup) to assign a PG deal to the PG line item). The seller of the PG deal configures these creative requirements, and settings in the PG line item can not change them. You must have at least one associated creative for each media type and ad size listed for the PG deal.

- **Media Type** - creative media type for the PG deal
- **Ad Sizes** - ad size for the PG Deal

> [!NOTE]
> Prior to transacting on a PG deal, confirm with its seller that the creatives you wish to serve meet their deal's creative format, size, and technical attribute requirements.

### Creative rotation

Select the creative rotation strategy you want to use:

- **Auto-optimize creative weight**: the creative with the highest click-through-rate (CTR) delivers the most
- **Evenly weight creatives**: even rotation is handled automatically by our system
- **Manually weight creatives**: rotation is based on a user-supplied weight

## Associate creatives

1. Click **Edit** to open the **Associated Creatives** dialog.
1. Select the creatives you want to associate to your PG line item from the **Available Creatives** list by clicking on the green check next to the name. Selected creatives will appear in the **Selected Creatives** list. Ensure that you have at least one associated creative for each media type and ad size listed in **Creative Requirements for this PG Deal**.
1. When you finish making your selections, click **Save**.

## Reporting labels

Reporting Labels allow you to report by metrics that are important to your business (see [Reporting Labels](reporting-labels.md)). You can assign the following labels to a PG line item:

> [!NOTE]
> It will take about 30 minutes for the labels to show up in reporting.

- **Trafficker** - PG deal trafficker
- **Sales Rep** - PG deal sales representative
- **Line Item Type** - type of line item (e.g., PGLI)

## Fees

Click inside the **Associated Fees** search box to see a list of eligible third-party partner fees, or search for a fee name, and select the desired fee. Fees required for all of the advertiser's line items are already applied automatically, and are indicated by a lock icon.

For more information, see [Partner Fees](partner-fees.md).

## Comments

You can add comments to the PG line item in the **Comments** box. Comments are for reference only and will not affect performance of the PG line item.

## Projected impact overview

The **Projected Impact Overview** calculates the projected spend, media cost, partner fees, and revenue for a line item based on your current settings. It is composed of the following parts:

- **Spend Breakdown** - The media cost and the Buyer Auction Service Charge (BASC) charged by Microsoft Advertising. For more information on BASC, see [Understanding Your Pricing Terms](understanding-your-pricing-terms.md).
- **Partner Fees** - Third-party fees associated with the line item.
- **Revenue** - The projected margin based on the line item's revenue type.

## Review and save changes

Review the PG line item configuration and click **Save**.

## Related topics

- [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md)
- [Bid Performance Messages for Programmatic Guaranteed Buying Line Items](bid-performance-messages-for-programmatic-guaranteed-buying-line-items.md)
- [Troubleshoot your Programmatic Guaranteed Buying Line Item Bid Performance](troubleshoot-your-programmatic-guaranteed-buying-line-item-bid-performance.md)
