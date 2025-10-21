---
title: Create a PG Deal with Third-Party Ad Server Pacing and Tag Integration
description: In this article, find information on how to create and set up a PG deal that uses pacing in your ad server of record.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create a PG deal with third-party ad server pacing and tag integration

To create a PG deal that uses pacing in your ad server of record, you need to select a buyer, ad type, CPM, impression budget, flight dates, and a placement specifically created for the PG deal.

## Before you begin

Before you begin creating a line item, make sure you've completed the following tasks:

- [Create an Advertiser](create-an-advertiser.md)

- [Create an Insertion Order](create-an-insertion-order.md)
  
  > [!NOTE]
  > To create a PG deal, you need to create a **seamless insertion order** with no end date, no budget, and an **Impression** or **Flexible** budget type.

- [Create a Placement for Third-Party Ad Server Pacing](create-a-placement-for-third-party-ad-server-pacing.md)

  It's required that you create a placement for your PG deal prior to deal creation.

  > [!NOTE]
  > The placement that you choose for your PG deal must be unique and targeted only by the PG deal that you're creating. Using a placement that is already being targeted in another PG deal causes delivery issues.

## Setting up the programmatic guaranteed deal

To set up the PG deal:

1. Navigate to the PG deal pre-selection screen.

    For more information on navigating to this pre-selection screen, see [Navigate to the Create New Programmatic Guaranteed Deal Screen](navigate-to-the-create-a-new-deal-line-item-screen-monetize.md).

1. Select **Pacing in Ad Server of Record** as your pacing option.

1. Click **Next**.

1. Enter a name for your PG deal.

    > [!NOTE]
    > This name will also be assigned to the PG deal line item.

1. Select a buyer.

1. **Optional:** Enter a deal code.

1. **Optional:** Enter a deal description.

1. Select the ad type to be used for your deal, and complete any additional steps for your selected ad type:

    > [!IMPORTANT]
    > You can currently only use banner creatives in your PG deal without Microsoft Advertising representative assistance. If you'd like to use other creative types, please contact your Microsoft Advertising account representative.

    | Selection | Step |
    |---|---|
    | **Banner** | Select one or more banner sizes for your PG deal to accept. <br><br> **Note**: Click **Add Custom Size** to create and select custom banner sizes. |
    | **Video** | Continue to **Step 6**. <br><br> **Note**: The default size selected for video creatives is **1x1**. |
    | **Native** | Select one or more native sizes for your PG deal to accept. The default size selected for native creatives is **1x1**, but you change this through the UI. <br><br> **Note**: Click **Add Custom Size** to create and select custom native sizes. |
    | **Audio** | Continue to **Step 6**. <br><br> **Note**: The default size selected for audio creatives is **1x1**. |

1. Enter a fixed CPM price to be used for your deal.

    The currency you chose for your advertiser will be used for your CPM price.

1. Set an impression budget for your deal.

1. Select flight (start and end) dates for the deal.

    > [!TIP]
    > We recommend that you only select start dates when you're confident that they won't change. Flight start dates can't be changed during an in-progress flight. End dates, however, can always be changed.

1. Select a unique placement to include in the deal.

1. **Optional:** Add reporting labels and comments to your deal.

    With reporting labels, you can associate a person or other metadata with your PG deals. You can then run reports that sort by the labels you've set for your deal.

    > [!NOTE]
    > Comments are only for personal reference and won't affect deal performance. Deal buyers aren't able to see them.

1. Click **Save**, located in the top-right corner, to finish.

You've just created your PG deal, and both a deal line item ID and deal ID have been created. You must now locate and share the deal ID to your buyer. Alternatively, if you have **deal sync** enabled, then ID sharing will be automatically handled with your buyer.

Before setting your deal line item to be active, you should ensure that your deal line item is live (flight date range has begun) and your designated buyer has begun targeting the deal. Otherwise, your deal's placement tag will fire and receive no bid, but GAM will record an impression as having occurred.

> [!WARNING]
> Ensure that you're specifically sharing the **deal ID** to the buyer.
