---
title: Add Basic Line Item Details to Traffic a Programmatic Guaranteed Deal
description: In this article, find step-by-step instructions for how to add basic line item details to a Programmatic Guaranteed deal
ms.date: 10/28/2023
---

# Add basic line item details to traffic a Programmatic Guaranteed deal

You can associate one or more insertion orders to the programmatic guaranteed line item, create a deal for a buyer, as well as set an ad type, name, and state, all from the **Basic Setup** section.

1. Associate insertion orders to the line item by doing the following:
    1. Click **Edit** in the line item and in **Edit Line Item** screen, click on pencil icon in the **Insertion Orders** box.

        A list of corresponding insertion orders displays automatically.

    1. Search for additional existing insertion orders if necessary.
    1. Select the corresponding check marks to associate the necessary insertion orders that display.

        > [!NOTE]
        > To use PG selling line items, you need to create and associate a **seamless insertion order** with no end date, no budget, and an **Impression** revenue type.

    1. Click **Save**.

1. Select the appropriate **Ad Type**.

    > [!NOTE]
    > You can currently only use banner creatives in your PG deal without Microsoft Advertising representative assistance. If you'd like to use other creative types, please contact your Microsoft Advertising account representative.

    - **Banner**
    - **Video (Audio)**
    - **Native**

    The ad type must match the type of creative(s) that the buyer intends to traffic.

1. If you want, enable **Roadblocking**.
    1. Select a size for the **Master creative**.
    1. Select a size for the **Companion creative**.
    1. If necessary, click **Add Companions** to include additional companion creatives and select their sizes.

    **Roadblocking** allows buyers to serve multiple creatives together on the same page. When you use seller tags to conduct a single auction for multiple ad slots on a page, you can serve multiple linked creatives.

    > [!NOTE]
    > Programmatic roadblocks are currently a **Closed Beta** feature, so some clients don't have access to it. If you'd like access to this feature, please contact your account representative.

1. Specify the ad size(s) of your banner creatives (**required** only if you selected **Banner** for **Ad Type**).
    1. Click the pencil icon.
    1. Choose either **Include all sizes** or **Specific sizes...**

        You will be asked to select **Standard** and/or **Custom** ad sizes if you chose **Specific sizes...**.

    1. Click **Save**.

1. Enter the name you will use to search for and report on the line item.

1. Click **+External Code** and enter a code if you want to report on a line item using your own code (rather than the internal ID that Microsoft Advertising assigns automatically).

    External codes must follow these guidelines:
    - They can contain only alphanumeric characters, periods, underscores, or dashes.
    - Codes are not case-sensitive (upper- and lower-case characters are treated the same).
    - No two objects can use the same code per advertiser. For example, two line items cannot both use code "ABC."

1. Set the **State**.

1. Create a deal.
    1. Enter a **Deal Name**.
    1. Select **Buyers** - Click **Edit** under **Buyer** to choose buyers for your new deal.
    1. On the **Select Buyer** screen, select your desired buyers (you can search by **Name** and **ID**).

        > [!WARNING]
        > After creating the deal, you cannot change the selected buyer.

    1. Click **Add**.
    1. **Code** - (Optional) Enter a custom deal code in **Code** (typically used by external buyers for deal mapping).
    1. **Description** - (Optional) Enter a description for your deal in the **Description** box.

1. Enter a **Fixed Price** for **Revenue Type**.

    > [!NOTE]
    > PG selling line items must have a **CPM** revenue type. **Fixed Price** pertains to deals where the line item competes in the auction at a fixed price whenever the buyer bids above that price.

1. Set a **Budget**.

    Enter an amount for each flight and adjust the **% of daily average allocation** as necessary using the slider.

    PG selling line items can only be set to **Lifetime Budget**.

1. Set **Flight**.

    Enter your desired flight dates.

    > [!NOTE]
    > Only one flight can be made currently for PG selling line items.

1. Choose a **Priority**.

    Select a priority level (**1-5**: Open Auction, **6-20**: Private Auction) for the PG selling line item in the **Line Item Priority** drop-down.

    The priority level you set determines the **Auction Type** for the deal line item and the order in which bids are considered at auction. For more information, see [Deal Auction Mechanics](deal-auction-mechanics.md).

    > [!NOTE]
    > PG selling line items require a **Managed** supply strategy.

## Related topic

[Create a Programmatic Guaranteed Deal](create-a-programmatic-guaranteed-selling-line-item.md)
