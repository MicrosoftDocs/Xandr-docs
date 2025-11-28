---
title: Microsoft Monetize - Publisher Guide for Deal Sync with Trade Desk 
description: Learn how a seamless deal transaction between Microsoft Advertising Monetize publishers and Trade Desk buyers is possible. This page also covers best practices to be followed for deal set up.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Publisher guide for deal Sync with Trade Desk 

> [!NOTE]
> This feature is in **Beta**. It is only available to select clients. Please consult your Account Manager if you'd like to be added to the beta test.

## Overview

Microsoft Advertising's integration with the Trade Desk Proposal API automatically synchronizes the deals created in Microsoft Monetize with the Trade Desk system. This enables a more seamless deal transaction between Microsoft Advertising Monetize publishers and Trade Desk buyers.

> [!IMPORTANT]
> You can manually set up deals with Trade Desk, but this requires buyers to manually register publisher deals in the Trade Desk user interface. (Details of the manual process can be found in [Trade Desk Buying Guide](../bidders/trade-desk-buying-guide.md)) The manual process of setting up deals can result in delays and issues due to human error.

The key benefits of using an automatic synchronization process are:

- Seamless deal set up process with Trade Desk buyers.
- Elimination of requirement for buyers to manually register deals in the Trade Desk UI.
- Automatic deal synchronization of deals and deal updates from Microsoft Monetize to Trade Desk (with some restrictions, which are explained below).

## Process

**New deal creation**

New seat ID deals created in the Microsoft Monetize UI automatically get uploaded to Trade Desk systems for buyer acceptance, as shown here:

:::image type="content" source="media/image-a.png" alt-text="Screenshot of new deal created.":::

**Deal update**

Updates to newly created deals (post deal sync enablement) automatically get uploaded to Trade Desk systems for buyer acceptance:

:::image type="content" source="media/imagee-b.png" alt-text="Diagram of deal update.":::  

**Frequency of deal sync**

- Deals will take up to 3 hours to sync with Trade desk systems.
- New deals will be uploaded up to 3 hours after being created.
- Updates to existing deals will be will be uploaded up to 3 hours after updates are done (depending on when the last sync script ran).
- Buyer acceptance statuses will take a few hours to properly sync.

## What is changing

While there are no changes to how a publisher create deals in Microsoft Monetize UI, publishers should be aware of which type of deals are automatically synchronized and which deals still continue to follow the manual workflow.

- All new deals created in the alpha are synchronized with Trade Desk, with the exceptions of:
  - Multi-Buyer Deals that are created at the Bidder level.
  - Deals created with a Trade Desk Buyer Member ID instead of a Bidder Seat ID Trade Desk Partner ID.
  - Deals created prior to the seller's enablement of deal sync with Trade Desk.

## Best practices for deal set up

**1:1 Deals and exchange curated deals (ECDs)**

- Deals must be set up with Trade Desk partner IDs. This deal synchronizing process does not support member ID deals.
- Once a partner ID is selected for a deal, it cannot be changed in subsequent updates.
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the Trade Desk UI.

**Programmatic guaranteed (PG) deals**

- Deals must be set up with Trade Desk partner IDs. This deal sync process does not support member ID deals.
- You cannot change the Trade Desk partner ID once the deal is created.
- The deal must have only **ONE** declared media type (video, banner, native, audio).
- Banner/Display PG deals must have at least one allowed creative size declared.
- Always have active communication with the buyer during the deal negotiation and setup process to ensure the buyer knows to approve the deal in the Trade Desk UI.

**Multi-Buyer deals**

- Deals set up with multiple Trade Desk seat IDs automatically get synchronized.
- Bidder-level deals (set up with ALL Trade Desk buyers) are not supported in automatic deal synchronizing.
- Microsoft Advertising systems will randomly assign one buyer to be the primary buyer on the multi-buyer deal. This primary buyer will be the only account allowed to approve the deal. You can check the primary buyer assigned to the deal in the buyer-deal-sync API or database tables.
- The primary buyer on a multi-buyer deal cannot be changed or removed
- Multi-buyer deals set up with Trade Desk member IDs will not sync. This includes deals set up with Trade Desk member ID 1088.
