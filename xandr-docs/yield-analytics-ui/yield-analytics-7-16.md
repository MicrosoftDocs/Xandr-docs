---
title: Yield Analytics 7.16
description: Learn about different enhancements made in the Permissions page.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 7.16

## Product permission enhancements

- When selecting Parent Products to a User Group on the Permissions page, you have the ability to view current associated overlaps. This is helpful when considering a Permission Product. Select **View Overlaps**.
- Availability Lookup has additional analysis and result information when deducing Child/Twin Product relationships for Dynamic Availability Lookups. The (i) icon provides information for these cases:
  - Where there is no Capacity (0) and Availability (0), values are visible in the row.
  - Where the Dynamic Lookup expresses an Overlap Type which is not a Twin, Self or Child, information on the Overlaps analyzed is provided.

  :::image type="content" source="media/m.png" alt-text="Screenshot of Permissions page.":::

- There are two overrides provided, which will enable the visibility of Availability Lookup information and Product Creation regardless of the Availability Lookup outcome. Talk to your Account Manager about configuring.
  - A View override will display Availability Lookup Result data regardless of the Product Permission.
  - An Edit override will allow Product Creation on Availability Lookup, Product Creation, and Product Edit.

  :::image type="content" source="media/n.png" alt-text="Screenshot of Availability Lookup Result data.":::
