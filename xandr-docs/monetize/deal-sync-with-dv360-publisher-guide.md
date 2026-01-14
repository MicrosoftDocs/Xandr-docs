---
title: Microsoft Monetize -  Publisher Guide for Deal Sync with DV360 
description: Learn all about Microsoft Advertising's integration with the Display Video 360 (DV360) Seller API in this page. This page also covers steps in deal creation and best practices to be followed during deal set up.
ms.date: 1/14/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---


# Microsoft Monetize -  Publisher guide for deal sync with DV360 

<!-- > [!NOTE]
> This feature is in **Closed Beta**. It is only available to select clients. Please consult your Account Manager if you'd like to be added to the beta test. -->

## Overview

Microsoft Advertising's integration with the Display Video 360 (DV360) Seller API automatically synchronizes the deals created in Microsoft Monetize with the Google DV360 system. This enables a more seamless deal transaction between Microsoft Monetize publishers and DV360 buyers.

<!-- > [!IMPORTANT]
> You can manually set up deals with DV360, but this requires buyers to manually register publisher deals in the DV360 user interface. (Details of the manual process can be found in [DV360 Buying Guide](../bidders/dv360-buying-guide.md).) The manual process of setting up deals can result in delays and issues due to human error.-->

The key benefits of using an automatic synchronization process are:

- Seamless deal set up process with DV360 buyers.
- Elimination of requirement for buyers to manually register deals in the DV360 UI.
- Automatic deal synchronization of deals and deal updates from Microsoft Monetize to DV360 (with some restrictions, which are explained below).

## Process

**New deal creation**

New seat ID deals created in the Microsoft Monetize UI automatically get uploaded to DV360 systems for buyer acceptance, as shown here:

:::image type="content" source="media/publisher-a.png" alt-text="Screenshot of New Seat ID deals created in the Microsoft Monetize UI.":::
  
**Deal update**

Updates to newly created deals (post deal sync enablement) automatically get uploaded to DV360 systems for buyer acceptance:

:::image type="content" source="media/publisher-b.png" alt-text="Screenshot of Deal Update.":::

 **Frequency of deal sync**

- We synchronize deals every hour.
- New deals are uploaded up to 1 hour after being created.
- Updates to existing deals are uploaded up to 1 hour after it is created (depending on when the last sync script ran).
- Buyer acceptance statuses are synchronized every hour.

<!-- ## What is changing

While there are no changes to how a publisher create deals in Microsoft Monetize UI, publishers should be aware of which type of deals are automatically synchronized and which deals still continue to follow the manual workflow.

- All new deals created in the alpha are synchronized with DV360, with the exceptions of:
  - Multi-Buyer Deals that are created at the Bidder level.
  - Deals created with a DV360 Buyer Member ID instead of a Bidder Seat ID DV360 Partner ID.
- In a later phase, we plan to begin synchronizing older deals that match the above criteria. -->

## Checking deal sync status

You can view a deal’s sync status in the **Deal screen** under the **Buyer** column. For **single-buyer deals**, the sync status appears directly in the grid. For **multi-buyer deals**, buyer-specific sync details are available in the **Settings** side pane. Sync status is not displayed for deals targeted to the entire DSP.

The following sync status labels may appear:

- **Syncing** – The deal is queued for synchronization in the next hourly batch.  
- **Syncing Error** – The deal attempted to sync but an error occurred. The system will retry in the next batch.  
- **Pending** – The deal was successfully sent to the DSP and is awaiting buyer acceptance.  
- **Accepted** – The buyer has accepted the deal in their DSP.  
- **Targeted** – The buyer is actively targeting the deal with at least one line item.  
- **Archived** – The buyer archived the deal in the DSP and can no longer buy against it.  
- **Declined** – The buyer declined the deal. Contact the buyer directly for more information.

You can also filter deals by sync status using the **Filters** option at the top of the Deal screen, next to the search bar.

## Best practices for deal set up

**1:1 Deals and exchange curated deals (ECDs)**

- Deals must be set up with DV360 partner IDs. This deal synchronizing process does not support member ID deals.
- Once a partner ID is selected for a deal, it cannot be changed in subsequent updates.
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the DV360 UI.

**Programmatic guaranteed (PG) deals**

- Deals must be set up with DV360 partner IDs. This deal sync process does not support member ID deals.
- You cannot change the DV360 partner ID once the deal is created.
- The deal must have only **ONE** declared media type (video, banner, native, audio).
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the DV360 UI.
- Only update deal details when necessary and **always** notify the buyer to approve the changes. The DV360 buyer continues to bid using previous PG deal details until new deal updates are approved.
- PG deals must include allowed creative sizes for banner and display .

**Multi-Buyer deals**

- Deals configured with DV360 **Central Partner IDs** are automatically synchronized.  
- For instructions on creating a multi-buyer deal with DV360, see [Set up multi-buyer deals with DV360 buyers](multi-buyer-deals-with-dv360-buyers.md).  
- Once a DV360 Central Partner ID is added to a deal, it cannot be removed.
