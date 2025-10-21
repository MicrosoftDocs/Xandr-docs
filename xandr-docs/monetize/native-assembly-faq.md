---
title: Native Assembly FAQ
description: In this article, find answers to frequently asked questions regarding Native Assembly.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Native Assembly FAQ

## What is Native Assembly?

Native Assembly is Microsoft Advertising’s native inventory management feature, allowing you to create new native inventory or enable native capabilities on an existing display placement.

## If I’m adding native capabilities to existing display inventory, is it really native inventory?

Yes! Native inventory created using Native Assembly is native inventory—be it new native placements or adding native capabilities to existing display placements. It will be bid on by native DSPs and show up as native inventory in reporting. Most importantly, publishers control the look of their rendered ads.

## When a display placement is enabled for native assembly, which ad format will be prioritized in an ad request? Banner or Native, both?

We do not prioritize formats in our marketplace and the highest bid will win. Please note that some DSPs don’t request all formats or prioritize certain formats. For this reason, multi-format requests don’t include all possible banner and native demand. That said, top DSPs like DV360, TTD, and Microsoft Invest will request both formats.

## What is a renderer?

The renderer is the layout or style that the native assets will be rendered in on page. You can use templated, ‘out-of-the-box’ renderers or fully customize them.

## What size should the renderer be?

The size rendered will be the primary size listed for your placement—either as defined by you or position [0] of the size array in the ad call.

## Do I have to edit page code to enable native capabilities?

No, with Native Assembly, there is no need to edit page code to implement multi-format native on existing display inventory. All inventory creation and management can be done directly from the Microsoft Monetize UI by associating your native renderer to your placement. Creating new native-specific placements is just as easy.

## Can I apply multiple renderers to a placement?

Each placement must be associated with one renderer. This is because the renderer is what defines the assets requested. Please note that rendered size does not affect native demand.

## Do I have to activate placements individually?

No, bulk activation is possible for scaled native inventory enablement. Please contact your Microsoft Advertising team for more details.

## What requirements should I set for my native assets?

We recommend adjusting asset requirements to the following character limits. This will maximize the amount of demand eligible for your placement.

- **Title**: 60 characters
- **Body**: 150 characters
- **Icon**: 300px x 300px
- **Main image**: 1200px x 627px

> [!TIP]
> We recommend thinking about the creative layout that aligns best with your content experience, such as ‘stacked image’ or ‘horizontal banner’, when deciding on which renderer template to use.
