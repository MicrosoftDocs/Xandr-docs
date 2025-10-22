---
title: Understanding the Sell-Side Object Hierarchy
description: This page deals with sell-side Object hierarchy and the relationship between objects like Publishers and placements. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---


# Understanding the sell-side Object hierarchy

Inventory on the platform is grouped within sell-side objects that exist within a specific object hierarchy. Here's the basic hierarchy:

1. Supply Partner networks work with various publishers.
1. Publishers sort inventory into placement groups, or groupings of like inventory made up of individual placements.
1. Placements are the smallest sell-side object. They are open spaces (represented by tags passed between traffickers) where ads can run.

  Here's a visualization of the relationship between objects:

  :::image type="content" source="./media/d.png" alt-text="Diagram of supply partners.":::

## Publishers and placements

The two most important objects for Supply Partners to focus on are publishers and placements. Since Domain Detection may shut off tags that send URLs violating our [Part of Service Policies](../policies-regulations/index.yml), you can protect yourself by splitting out inventory in the most granular way possible, into publishers and tags. This way, if one tag gets turned off for what Xandr considers “bad” inventory, it will not impact your ability to sell the rest of your inventory.

When setting up your account, your Xandr Technical Account Manager (TAM) will create a default publisher and placement and associate them with your member. You can then create additional publishers and placements to mirror your inventory structure, as needed.

- For guidance on using  to map your supply to Xandr, see [Use  to Synchronize Your Inventory Structure](use-the-ui-to-synchronize-your-inventory-structure.md).
- For guidance on using the API to map your supply to Xandr, see [Use the API to Synchronize Your Inventory Structure](use-the-api-to-synchronize-your-inventory-structure.md).
- If you want a Xandr representative do a once quarterly bulk mapping upload, you will need
  to [open a support ticket](https://support.ads.microsoft.com) and let us know you plan to send a formatted cvs file so that Xandr can create the mapping for you.

> [!TIP]
> The best way to synchronize publishers and placements is by creating publishers and placements to correspond to values that will be passed in on bid requests. That's `BidRequest.site.publisher.id` (for publishers) and `BidRequest.site.id` (for placements) in OpenRTB.

## Ad profiles

Your [network ad quality profile](define-ad-quality-rules.md) restricts which creatives can serve on your inventory, based on creative attributes such as buyer or brand.These rules are applied to every impression across all of your publishers.

If you need to enforce stricter ad quality rules for individual publishers, you can create ad quality profiles at the publisher level as well.
