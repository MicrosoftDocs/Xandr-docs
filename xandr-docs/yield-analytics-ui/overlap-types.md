---
title: Overlap Types
description: In this article, explore the various types of overlaps through a detailed example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Overlap types

Overlap types represent the hierarchical relationship between two products as follows:

- Parent – Product that entirely contains (i.e., is a full superset of) another product.
- Child – Product that is entirely contained within (i.e., is a full subset of) another product.
- Sibling – Product that partially overlaps with another product.
- Twin – Two products that contain/describe the exact same set of inventory.

## Example of an overlap

The following example shows these overlap types in action:

- Parent: Section=Sports – The Section=Sports product is a parent to the Section=Football product because Section=Football product is entirely contained within it.
- Child: Section=Football – The Section=Football product is a child of the Section=Sports product because it's entirely contained within Section=Sports.
- Sibling: Geo=NY – The Geo=NY product is a sibling to the Section=Sports product because the two products partially overlap.
- Twin: Content Category=Sports – The Content Category=Sports product is a twin to the Section=Sports product because they both contain exactly the same set of inventory.

:::image type="content" source="media/gg.png" alt-text="Diagram of an overlap example.":::

## Related topics

- [Analyze Product Overlaps](analyze-product-overlaps.md)
- [Products Overview](products-overview.md)
