---
title: Supply Type Targeting
description: Explore supply type targeting specific supply types through the Inventory Type field in line item setup to streamline supply type focus.
ms.date: 10/28/2023
---

# Supply type targeting

Supply Types (**App & Web**, **App Only**, or **Web Only**) can be targeted via the **Inventory Type** field in the **Inventory and Brand Safety** section of the line item setup (see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)).

To restrict the placement types where your creatives may run, select the **Set custom supply type** checkbox and set the relevant supply toggles to **OFF**:

- **Web Placements** - Standard web sites.
- **Mobile Web Placements** - Web sites optimized for browsers on mobile tablets and phones.
- **Mobile Apps Placements** - Applications installed on mobile tablets and phones.

## Best practices for supply type targeting

Targeting is set to **ON** by default for all device and supply types. When configuring your targeting settings, adhere to these practices for best results when serving:

- To target in-app inventory, be sure that **Tablets** and **Phones** are set to **ON**.
- App targeting (set within Inventory Targeting) applies only to mobile app impressions. To target mobile app impressions exclusively, set **Apps Placements** to **ON** and **Web Placements** and **Mobile Web Placements** to **OFF**.
- Domain targeting (set within Inventory Targeting) applies only to web or mobile web impressions. To target domain impressions exclusively, set **Web Placements** and **Mobile Web Placements** to **ON** and **Apps Placements** to **OFF**.
  - To target PC-based web placements exclusively, set **Web Placements** to **ON** and **Mobile Web Placements** and **Apps Placements** to **OFF**.
  - To target mobile-based web placements exclusively, set **Mobile Web Placements** to **ON** and **Web Placements** and **App Placements** to **OFF**.

   > [!NOTE]
   > The choices you make here affect the targeting options configured further in the procedure. If mobile options are not listed, contact your Microsoft Advertising representative.

## Related topics

- [Augmented Line Items (ALI)](augmented-line-items-ali.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Object Hierarchy](object-hierarchy.md)
- [Set Up Line Item Inventory and Brand Safety](set-up-line-item-inventory-and-brand-safety.md)
- [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md)
