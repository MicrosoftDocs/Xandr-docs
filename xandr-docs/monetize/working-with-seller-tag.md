---
title: Working with Microsoft Advertising's Seller Tag (AST)
description: Explore Seller Tag (AST) consolidating ad slots for efficient auctions. Run this lightweight JavaScript SDK asynchronously.
ms.date: 10/28/2023
---

# Working with Microsoft Advertising's seller tag (AST)

Microsoft Advertising's Seller Tag (AST) is a lightweight JavaScript SDK that consolidates all ad slots on a publisher's web page to be auctioned and sends information about them in a single ad request whenever possible.

AST runs in the header or body of a web page in a user's browser and allows publishers to conduct auctions directly from the page. AST loads asynchronously, meaning that ad calls do not block the page content from loading. For more information on AST, see [Seller Tag](../seller-tag/seller-tag.md).

## AST features

AST provides the following features:

- **Competitive Exclusions** - allow you to prevent creatives with competitive brands or offer categories from serving alongside each other. Competitive exclusions settings are available at the Advertiser and Creative levels. For more information, see [Competitive Exclusions](competitive-exclusions.md).
- **Page Caps** - allow you to restrict brands, advertisers, line items, or campaigns from winning more than one ad slot per AST ad call. Sell-side page caps apply to brands, while buy-side page caps apply to advertisers, line items, and campaigns. For more information, see [Sell-Side Page Caps](sell-side-page-caps.md) and [Buy-Side Page Caps](buy-side-page-caps.md).
- **Roadblocks** - allow you to serve multiple creatives together on the same page. Roadblocks are only available on managed inventory, where you can control the settings on both the buy-side and the sell-side. For more information, see [Target Your Inventory with Roadblocking](target-your-inventory-with-roadblocking.md).

## Set up placements with AST

You'll need to set up AST on your publishers' placements before you can take advantage of its features. For more information on how to set up AST, see [Set Up Placements with AST](../seller-tag/set-up-placements-with-ast.md).

## Related topics

- [Seller Tag](../seller-tag/seller-tag.md)
- [Set Up Placements with AST](../seller-tag/set-up-placements-with-ast.md)
- [Sell-Side Page Caps](sell-side-page-caps.md)
- [Buy-Side Page Caps](buy-side-page-caps.md)
- [Competitive Exclusions](competitive-exclusions.md)
- [Target Your Inventory with Roadblocking](target-your-inventory-with-roadblocking.md)