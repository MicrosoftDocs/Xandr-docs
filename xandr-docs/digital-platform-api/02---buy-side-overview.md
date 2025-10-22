---
title: Buy-Side Overview
description: In this article, explore detailed information about buy-side and its various objects.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Buy-side overview

## Diagram

:::image type="content" source="media/buy-side-overview.png" alt-text="Diagram that illustrates buy-side framework.":::

## Object definitions

- [Member](member-service.md): The parent object for your account. Each member has a contractual relationship with Xandr.
- [Advertiser](advertiser-service.md): The object which represents a single advertiser on Xandr. Generally, an advertiser can be associated with a single brand.
- [Insertion Order](insertion-order-service.md): This object groups line items.  
- [Line Item](line-item-service.md): This object tracks all revenue in the system and defines how inventory will be purchased, including bidding strategies and media cost budgeting.
- [Creative](creative-service.md): The actual advertisement to be served. The specification of a creative includes format, size, and audit attributes.
- [Segment](segment-service.md): Used for targeting specific groups of users who have been added to the segment through a pixel.
- [Conversion Pixel](conversion-pixel-service.md): These objects are used for tracking conversions as well as optimization for CPA campaigns and line items.
- [Profile](profile-service.md): This object defines all of the targeting parameters for another object (e.g., line item).
    > [!NOTE]
    > A profile is the only object that does not correspond to the objects in the UI. For example, combine a profile (targeting) and a campaign (budget and flight dates) and show the campaign alone.
