---
title: Seller Tag
description: In this page, learn about Microsoft's seller tag (AST), how to implement it, an API refernce, and using AST in specific conditions. 
ms.custom: seller-tag
ms.date: 10/28/2023
---


# Seller Tag

Microsoft Advertising's seller tag (AST) is a lightweight JavaScript SDK that runs in the header or body of a web page in a user's browser and allows publishers to conduct auctions directly from the page. AST consolidates all ad slots on a page to be auctioned and sends information about them in a single ad request whenever possible. AST loads asynchronously, meaning that ad calls do not block the page content from loading.

The following pages provide an overview of AST, how to implement it, an API reference and using AST in specific situations.

> [!NOTE]
> - AST will work with AMP HTML markup. The library currently only supports banner ads. Click here for detailed information: [AmpProject](https://github.com/ampproject/amphtml/blob/main/ads/vendors/appnexus.md)
> - AST uses the "count on begin to render" methodology to track impressions.

| Sections | Description |
|--|--|
| [AST Browser Support](ast-browser-support.md) | List of browsers that are supported by Xandr's seller tag (AST). |
| [AST Release History](ast-release-history.md) | A listing of current and past releases and changes occurring in each realease. |
| [AST Video Capabilities](ast-video-capabilities.md) | Instructions on using AST with different video formats. |
| [AST API Reference](ast-api-reference.md) | A reference guide for the functions and properties of of Xandr's seller tag (AST) JavaScript library. |
| [Benefits of AST](benefits-of-ast.md) | The benefits of using AST. |
| [Breaking Changes in the API](breaking-changes-ast-api.md) | A description of what is considered a breaking change. |
| [SafeFrame API Reference](safeframe-api-reference.md) | Instructions on implementing SafeFrames and an SafeFrames API reference. |
| [Set Up Placements with AST](set-up-placements-with-ast.md) | Instructions for implementing the AST tag on a webpage. |
