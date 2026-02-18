---
title: Microsoft Curate - Create a Curated Deal Line Item 
description: Establish curated deals where users create buyer-specific agreements, negotiating with curators to merge assets with Microsoft Advertising Marketplace supply.
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Create a curated deal line item

> [!NOTE]
> Some clients might see different options when creating a curated deal line item. This documentation covers all options in the workflow. Contact your Microsoft Advertising representative if you have questions about certain options or settings.

A curated deal line item lets you set up a curated deal for a buyer. Curated deals represent a negotiated agreement between a buyer and a curator that combines a curator’s assets with Microsoft Advertising Marketplace supply.

Curated deal line items offer the following features:

- Pricing: choose between a fixed price, ask price, or market price for your curated deal
- Margin: configure a percentage of fixed CPM curator margin
- Inventory targeting: source inventory from seller deals or the open market, targeting categories and domains to curate the impressions you need

## Prerequisites

You will need to create or have access to the following buy-side objects:

- Advertiser: see [Work with Advertisers](working-with-advertisers.md)
- Insertion order (seamless): see [Work with Insertion Orders](working-with-insertion-orders.md)

  > [!NOTE]
  > - Legacy insertion orders are not supported with curated deal line items.
  > - Insertion orders must be configured with an unlimited budget for curated deal line items
  > - Settings you select the insertion order will apply to *all* curated deal line items under the insertion order.

## Create a new curated deal line item

From the **Advertiser Details** screen, you can create a curated deal line item from either the **Insertion Orders** screen or **Line Items** screen:

### Insertion Orders screen

1. From the **Advertiser Details** screen, select **Insertion Orders** to view the advertiser's insertion orders.
1. Select an insertion order from the list to view the **Insertion Order** details screen.
1. In the **Line Items** section, select **New Deal Line Item**.

### Line Items screen

1. From the **Advertiser Details** screen, select **Line Items** to view the advertiser's line items.
1. Select **New Deal Line Item**.

## Deal type

In the **Deal Type** section, select **Curate a Deal**.

## Basic setup

In the **Basic Setup** section, enter the basic details for the curated deal line item.

- **Insertion Orders** - The insertion order associated to the line item. If you create the line item from the **Insertion Order Details** screen, the insertion order is automatically associated. Otherwise, select **Edit** to associate the line item with an insertion order.
- **Ad Type** - Select the type of ad you plan to use. Possible values are  **Banner**, **Video** (includes audio types as well), and **Native**.
  
   > [!NOTE]
   > Selecting **Ad Type** determines the availability of other settings (e.g., **Targeting >  Completion Rate Threshold**). This is not the setting that filters out any impressions and does not impact auction logic. You can select **Media Type** under **Deal Creative Criteria** to control which types of ads are allowed to serve via the curated deal.

- **Name** - Enter the name for the curated deal line item. You will later be able to search for and report on the line item using this name. This name is not exposed to the buyer.
- **External Code** - If you want to report on the curated deal line item using an external code (rather than the internal ID that Microsoft Advertising assigns automatically), enter the code here. The code can only contain alphanumeric characters, periods, underscores, or dashes. The code you enter is not case-sensitive (i.e., uppercase and lowercase characters are treated the same). No two objects at the same level can use the same code per advertiser.
- **State** - Set the state of the curated deal line item. If **"Active"**, the line item will be eligible to serve. Best practice for curators is to set the state to **"Active"** so that buyers can serve via the curated deal as quickly as possible.
- **Insertion Order Details** - Insertion order details for **Budget Type**, **Currency**, **Total Lifetime Budget**, **Pacing**, **Start Date**, and **End Date** display in the gray box (you must select an insertion order to display these values).
- **Budget Type** - Budget is set on the parent insertion order. When you create a deal via a line item, the line item will inherit its budget from the parent insertion order, and this will impact the revenue types available on the line item.

## Deal details

1. Select **Create a Deal**.
1. Enter a **Deal Name** (this curated deal name is exposed to the buyer).
1. Select **Edit** under **Buyer** to choose a buyer for the deal.
1. On the **Select Buyer** screen, select an available buyer (you can search by Name or ID).

   > [!NOTE]
   > You cannot change the selected buyer after the curated deal line item is created and saved.

1. Select **Add**.
1. Enter the deal code in **Code** (optional, this is typically used by external buyers for deal mapping).
1. Enter a description for your deal in the **Description**  box (optional).

Details for the newly created or existing deal display in **Deal Details** including:

- **Deal ID** - ID of newly created deal (the **Deal ID** for newly created deals does not display until the line item is saved).
- **Auction Type** - **Auction Type** is always set to   "**Open Auction**" for curators.
- **Price Type** - Determined by **Revenue Type**:
  - **CPM** = "**Fixed Price**"
  - **Dynamic CPM** = "**Standard**"
- **Ask Price** - Determined by **Fixed** or **Floor Price** (set in **Revenue Type**)

> [!NOTE]
> You may select **Choose Existing** when creating a curated deal, but this is not recommended unless you have already inactivated the original line item associated with the deal. For ease of maintenance, it is recommend that you use only one curated deal line item per curated deal. If you do choose to use an existing curated deal for this curated deal line item:
>
  > 1. Select **Select Deal** to choose an existing deal.
  > 1. On the **Select a Deal** screen, select a deal (you can search by Name or ID) and select **Select**.
  > 1. Edit the **Deal Name** if desired. Please note that this name is shared with the buyer.
  >
  > If you select the wrong deal you can select **Deselect** to open the **Select a Deal** screen again and select the deal you want.

## Revenue type

Use the **Revenue Type** to define how the buyer will pay you. Select one of the following revenue types:

- **CPM** ("fixed price" deals) - The curated deal line item  competes in the auction at a fixed price
  whenever the buyer bids above that price.
  - **Fixed Price** - Enter the amount that the buyer will pay you per thousand impressions.
- **Dynamic CPM** ("standard auction") - The curated deal line item competes in either a first or second-price
  auction at the price bid by the buyer, whenever the buyer bids above the ask price.
  
  Select either:
  - **Set Floor Price** - Enter the hard floor that will apply to the buyer of the curated deal.
  - **Use Market Price** - Select this to use the seller’s yield management floors if available; if not available, open auction pricing is used.

## Margin type

Use the Margin Type settings to configure the curator margin you wish to take on each impression.

Select either:

- **Percentage** - The percentage of the buyer’s bid which will be taken as curator margin.
- **CPM** - A fixed CPM deducted from the buyer’s bid which will be taken as curator margin.

## Budget

The **Budget Type** for curated deals must be **Unlimited Budget**.

## Flights

Flights let you set up limited deals with start and end dates as well as “evergreen deals” with no end date. To create one or more flights:

1. Select either **Set Dates** or **No End Date**.
    - **Set Dates**: Enter a **Start Date** and **End Date** for each of the line item's flights. The hour settings for **Start Date** and **End Date** will default to 12:00 AM and 11:59 PM respectively (you can override the defaults). Flights may not overlap one another. All flight dates must fall within the billing period dates of the parent insertion order and be a minimum of one day in duration.
    - **No End Date**: Enter the **Start Date** for the line item. You may not create additional flights for this line item because it has no end date.
1. Select **Add Another Flight** if you want additional flights (this option is not available if you select **No End Date**).

   > [!NOTE]
   > You cannot change the **Start Date** of a flight once that date has passed. You can, however, add multiple flights to any curated deal line item.

## Supply strategy

Curated deal line items can package supply from the open exchange or through deals negotiated directly with sellers. Selecting **Deals** will allow you select specific deals associated with your account in the **Targeting** section below. Selecting **Open Exchange** allows you to curate supply sellers make available to buyers on the open exchange.

## Payment model

The **Payment Model** for curated deal line items is preset to **Pay Per Impression**.

## Inventory and brand safety

You can specify the following inventory and brand safety settings for the curated deal line item.

## Inventory

### Universal categories

Universal categories are defined by Microsoft Advertising. When Microsoft Advertising reviews inventory, we apply these categories based on the inventory's content. For example, a car dealership placement group would be assigned to the "Autos & Vehicles" category. Sellers can apply universal categories when self-reviewing inventory as well.

By default, your curated deal line item will target all universal categories. However, you can narrow your targeting to include or exclude specific universal categories:

1. On the **Universal Categories** tab, include or exclude custom categories.
    - The **Categories** lists shows all top-level universal categories defined by Microsoft Advertising. You can either include or exclude top-level categories or drill into a category to view its child
      categories.
    - The **Sub-Categories** list shows all child universal categories in the context of their parent categories. You can either include or exclude sub-categories.
     > [!NOTE]
     > When you exclude a top-level category, its sub-categories are not available for further inclusion or exclusion.
     > [!NOTE]
     > When targeting more than one universal category, the categories have an OR relationship. For example, if you target the "News" and "Finance" categories, you will bid on inventory that is in either category. The inventory does not need to be in both categories.

1. Select **Add**.

### Seller categories

**Seller Categories** are defined by sellers. Sellers create these and apply them to slices of their inventory to package their inventory for specific buyers or curators to target.

By default, your curated deal line item will target all custom categories. However, you can narrow targeting to include or exclude specific custom categories that sellers exposed to you via the open exchange:

1. On the **Custom Categories** tab, include or exclude custom categories.

   > [!NOTE]
   > When targeting more than one custom category, the categories have an OR relationship. For example, if you include "Custom Category 1" and "Custom Category 2", you will bid on inventory that is in either category. The inventory does not need to be in both categories.

2. Select **Add**.

### Seller inventory

By default, your curated line item will target all sellers. However, you can narrow targeting to include or exclude specific sellers. Additionally, if a seller has chosen to expose their publishers via the open exchange, you can include or exclude specific publishers:

1. On the **Seller Inventory** tab, include or exclude sellers.
    - Select a seller to view the publishers they have exposed for targeting and include or exclude specific publishers.

## Inventory type

To set which inventory types you wish to target, select one of the following from the menu. By default, your line items will target all inventory types (i.e., **App & Web**):

- **App & Web** - To run on both inventory types. This is the default setting.
- **App Only** - To run in applications installed on mobile tablets, phones, and Windows 8 devices.
- **Web Only** - To run on standard web sites and those optimized for browsers on mobile devices.

## Blocklist

Select one or more blocklists (by default, the **AppNexus Blocklist** will always be applied). Any inventory in the blocklists you apply will automatically be *excluded* and not bid on by this line item. You may select from Network/member-level blocklists or create a blocklist directly (see [Inventory Lists](inventory-lists-ali-only.md)) from the line item. Once applied, you can also view or export the blocklist.

## Allowlist

Select an allowlist you would like to apply to this line item. You may select from network/member-level allowlists or create an allowlist directly (see [Inventory Lists](inventory-lists-ali-only.md)) from the line item. Once applied, you can also view or export the allowlist.

> [!NOTE]
> The use of inventory lists (i.e., allowlists or blocklists) will constrain whatever **Inventory Type** selections you make. For example, if you target an **Allowlist**, the **Inventory Type** option you select will be limited to only those domains/apps in that **Allowlist**. If you target a **Blocklist**, the **Inventory Type** option you select will serve on everything but the domains/apps in that **Blocklist**.

## Ads.txt

Do not use (not supported for curated deal line items).

## Targeting options

> [!IMPORTANT]
> Curated Deal line items should not target other curated deals. Targeting curated deals within another curated deal line item may result in unexpected delivery behavior.

You can target curated deal line items in the same way you can target augmented line items. See [Buy-Side Targeting](buy-side-targeting.md) for detailed setup information on targeting. See [Inventory Performance Targeting](inventory-performance-targeting.md) for more information on best practices for inventory performance targeting.

> [!NOTE]
>
> - Cross-device enhanced by Microsoft will be automatically enabled for your curated deal at no cost if you target a segment. If you prefer not to benefit from cross-device on your curated deal, please contact your account representative to opt out of this feature.
>
>
> - Thresholds (**Viewability Threshold** or **Completion Rate Threshold**) create a hard limit for curated deal line item targeting. Any impressions with a predicted view or completion rate below the threshold won’t be matched on the curated deal. Because the threshold you choose is the minimum view/completion you will achieve, expect to see an average view/completion rate 10-15% higher than the threshold you set.

### Geography

To quickly target countries or regions, select in the **Geography** field and select the relevant checkboxes. To set up more advanced geography restrictions select **Additional Geo Restrictions**.
See [Additional Geo Restrictions](additional-geo-restrictions-ali.md) for more details.

## Deal creative criteria

You can edit the following creative attributes for a curated deal by selecting **Edit** under the attribute,
selecting the appropriate values, and selecting **Set**:

- **Media type**

## Reporting labels

Enter any reporting labels if desired. Reporting labels let you associate a person or other metadata with advertisers. You can then run reports using these labels. See [Reporting Guide](reporting-guide.md) for more information.

## Comments

Enter any comments for this curated deal line item.

## Save line item for curated deal

Select **Save** to save the curated deal line item or **Save and Duplicate** to save the curated deal line item and duplicate the settings to a new line item.
