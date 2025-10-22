---
title: Bidders - Deal Sync with DV360 - Publisher Guide 
description: Explore streamlined transactions by integrating Microsoft Monetize deals with Google DV360 via DV360 Seller API, improving publisher-buyer interaction.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Deal sync with DV360 - Publisher guide

## Overview

Xandr's integration with the Display & Video 360 (DV360) Seller API automatically synchronizes the deals created in Microsoft Monetize with the Google DV360 system. This enables a more seamless deal transaction between Microsoft Monetize publishers and DV360 buyers.

> [!NOTE]
> All DV360 Partner ID deals created after August 14, 2023, will automatically sync to the DV360 platform, as all Monetize sellers and curators will be enabled for this product (no additional enablement required). As of August 7, 2023, DV360 no longer supports manual deal creation in the [DV360 user interface](https://support.google.com/displayvideo/answer/7505945#view_existing_negotiations). Deals that were created manually prior to this date will continue to operate as is.

The key benefits of using an automatic synchronization process are:

- Seamless deal set up process with DV360 buyers.
- Elimination of requirement for buyers to manually register deals in the DV360 UI.
- Automatic deal synchronization of deals and deal updates from Monetize to DV360 (with some restrictions, which are explained below).  

## Process

### New deal creation

New seat ID deals created in the Monetize UI automatically get uploaded to DV360 systems for buyer acceptance, as shown here:

:::image type="content" source="media/deal-sync-with-dv360-publisher-guide-a.png" alt-text="Screenshot that illustrates how new seat ID deals created in Monetize UI are automatically uploaded to DV360 systems for buyer acceptance.":::

### Deal update

Updates to newly created deals (post deal sync enablement) automatically get uploaded to DV360 systems for buyer acceptance:

:::image type="content" source="media/deal-sync-with-dv360-publisher-guide-b.png" alt-text="Screenshot that shows that newly created deals, with post-deal sync enabled, are automatically uploaded to DV360 systems for buyer acceptance.":::

### Frequency of deal sync

- We synchronize deals every hour.
- New deals are uploaded up to 1 hour after being created.
- Updates to existing deals are uploaded up to 1 hour after it is created (depending on when the last sync script ran).
- Buyer acceptance statuses are synchronized every hour.

## Best practices for deal set up

### 1:1 Deals and Exchange Curated Deals (ECDs)

- Deals must be set up with DV360 partner IDs. This deal synchronizing process does not support member ID deals.
- Once a partner ID is selected for a deal, it cannot be changed in subsequent updates.
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the DV360 UI.  

### Programmatic Guaranteed (PG) deals

- Deals must be set up with DV360 partner IDs. This deal sync process does not support member ID deals.
- You cannot change the DV360 partner ID once the deal is created.
- The deal must have only ONE declared media type (video, banner, native, audio).
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the DV360 UI.
- Only update deal details when necessary and **always** notify the buyer to approve the changes. The DV360 buyer continues to bid using previous PG deal details until new deal updates are approved.
- PG deals must include allowed creative sizes for banner and display.
