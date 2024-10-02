---
title: Netflix Programmatic Guaranteed Buying Line Item
description: This article provides instructions to create a programmatic guaranteed line item. A PG line item offers a specific workflow for buying a guaranteed deal.
ms.date: 10/28/2023
---

# Netflix programmatic guaranteed buying line item

## Overview

A Programmatic Guaranteed Line Item (PG line item) provides you with a workflow specifically designed for buying a Programmatic Guaranteed deal (PG deal). A PG line item can only target one PG deal. PG line items have very different targeting, budgeting, and optimization options compared to regular Line Items. See a [Programmatic Guaranteed Buying Line Items](./programmatic-guaranteed-buying-line-items.md) for more information before creating one.

## Before you begin

Before you create a PG line item, you must perform the following tasks:

- [Create an Advertiser](./create-an-advertiser.md)
- [Create an Insertion Order](./create-an-insertion-order.md)

The insertion order you created must have at least one billing period with dates in the future. You must also have access to one or more PG deals to target. Sellers must first create these deals for buyers to access them for targeting. If you have questions about how to gain access to a PG deal, contact your account manager.

## Access Netflix PG deals

To access a Netflix PG deal, do the following:

1. Select **Your Deals** in the **Inventory** menu. You can also access the Netflix PG Deals via a **notification** button on the **Inventory Library** screen from the **Inventory** menu.
2. In the **Your Deals** screen, ensure that the **Deal Type** is set to **PG**.
3. Choose the appropriate deal from the **Your Deals** screen.
4. Select the corresponding **Advertiser** and **Insertion Order** associated with that particular PG Deal.
5. Select **Go To PG Line Item Create** to launch the page to create the PG Line Item.

## Start a new PG line item

To create a new PG line item, do the following:

1. Select **Create New** in the **Line Item** menu.
1. On the **Create New Line Item** screen, select **Programmatic Guaranteed Line Item** under **Line Item Type**.

   > [!IMPORTANT]
   > You must have an **Advertiser** and **Insertion Order** associated with the line item in the **Advertiser** and **Insertion Order** sections. If necessary, select an advertiser and insertion order.

1. Select **Next** to open the **Create a Programmatic Guaranteed Line Item** screen. You can also create the PG line Item by selecting the **Go To PG Line Item Create** button from **Action Center** on the **Your Deals** screen.

## Important PG guidelines

PG Line items behave differently from regular line items in several ways. For more information on CTV Guidelines, see [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md).

- PG line items do not have flight budgets, budgets will only exist on the deal which is agreed upon between the buyer and seller beforehand.
- PG line items will ignore IO budgets.
- PG line items will ignore frequency and/or recency capping at the IO/LI/Creative level, and settings made by the publisher is enforced.
- PG line items do not support audience segment targeting, this is required to be layered from the publisher's side.
- The IO billing periods for PG line items should encompass all targeted PG deals to ensure the IO is active and spending through the entire duration.

## Basic setup of a PG line item

### Programmatic guaranteed basic setup instructions and creating line items

In the **Basic Setup** section, enter the following details for the PG line item:

- **Programmatic Guaranteed Deal** - The programmatic guaranteed deal associated to the PG line item. Enter the name of the PG deal and select it. The details of the PG deal display includes the following:
  > [!IMPORTANT]
  > The PG deal details shown are configured by the seller of the deal and cannot be changed by settings in the PG line item.

  - **Seller** - Name of the seller of the deal.
  - **Start Date** - Date the deal becomes active.
  - **End Date** - Date after which the deal is no longer active.
  - **Projected Media Cost** - Total projected media cost derived from the projected number and price of impressions reserved for the PG deal.
    - **Impressions** - Number of impressions reserved for the PG deal.
    - **Price** - Price of impressions for the PG deal.
  - **Geo Targeting** - Location of geo targeting used by the PG deal.
- **Insertion Order** - The insertion order associated to the PG line item. If you create the line item from the **Insertion Order Details** screen, the insertion order is automatically associated. Otherwise, select **Edit** to associate the line item to an insertion order.
  
  > [!NOTE]
  > PG line items **override** insertion order budgets, all levels of targeting, and any established frequency caps to ensure you fulfill your agreement with the publisher. PG line items do not override insertion order flight dates. You can keep a PG line item from spending by setting it to **Inactive** at any time.

- **Line Item Name** - Enter the name for the PG line item. You will later be able to search for and report on this PG line item using this name.
- **External Code** - If you want to report on this PG line item using an external code, enter the code here. The code may only contain alphanumeric characters, periods, underscores, or dashes. The code you enter is not case-sensitive (i.e., uppercase and lowercase characters are treated the same). PG line items associated to the same advertiser cannot use the same external code.
- **State** - Set the state of the line item. If **Active**, the line item will be eligible to serve.
- **Revenue Type** - **Cost Plus** is the required revenue type for PG line items. With **Cost Plus**, the advertiser will pay for your media cost (whatever you spend on buying inventory) plus an extra amount (a margin) that you charge the advertiser in addition to the media cost. You can set this margin as a percentage of cost (**% margin**) or as a fixed CPM fee (**CPM margin**). You must enter a percentage for **% margin** or a fee for **CPM margin** greater than or equal to zero.

  > [!NOTE]
  > PG Line Items will have pre-negotiated PG fees associated and should be manually included in billing. If you have questions on what the **%fee** is, contact your commercial partners.

## Associated creatives

### Creative requirements for Netflix programmatic guaranteed buying

#### Creative requirements for Netflix PG deals

To serve on Netflix inventory, CTV creatives must meet strict guidelines and technical specifications that have been set by Netflix to ensure an optimal user experience. We recommend that Microsoft Invest buyers consider dedicated creatives when buying Netflix, and consider the context that the advertisement is in and how it will appear on Netflix content. For more information on CTV creatives specification, see [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md).

> [!IMPORTANT]
> The PG line item must be associated to a PG deal for the **Creative Requirements for this PG Deal** to display [Basic Setup](./create-a-programmatic-guaranteed-buying-line-item.md) to assign a PG deal to the PG line item. The seller of the PG deal configures these creative requirements, and settings in the PG line item can not change them. You must have at least one associated creative for each media type and ad size listed for the PG deal.
> [!NOTE]
> Prior to transacting on a Netflix PG deal, confirm that the creatives you wish to serve meet Netflix’s [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md) which include creative format, size, and technical attribution requirements.

#### Locate Associated Creatives screen

1. Search for the creative name or the ID, to open the **Associated Creatives** dialog.
1. Select the creatives you want to associate to your PG line item from the **Available Creatives** list by selecting on the check next to the name. Selected creatives will appear in the **Selected Creatives** list. Ensure that you have at least one associated creative for each media type and ad size listed in **Creative Requirements for the PG Deal**. For more information on how to add creatives, see [Add a Creative](./add-a-creative.md) and [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md).a
1. When you finish making your selections, select **Save**.

## Related topics

- [Programmatic Guaranteed Buying Line Items](./programmatic-guaranteed-buying-line-items.md)
- [Create an Insertion Order](./create-an-insertion-order.md)
- [Add a Creative](./add-a-creative.md)
- [Creative CTV Guidelines and Specifications](./creative-ctv-guidelines-and-specifications.md)
