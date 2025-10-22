---
title: AST API Reference
description: In this article, find information about the usage of the functions and variables of Microsoft Advertising's Seller Tag (AST) JavaScript library.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# AST API reference

This page describes the usage of the functions and variables of Microsoft Advertising's Seller Tag (AST) JavaScript library. For an example of a page with these functions implemented, see [Set Up Placements with AST](set-up-placements-with-ast.md).

> [!WARNING]
> You cannot load ads from HTML hosted in `localhost`.

## Public variables

- `apntag`: Primary AST object class.
- `apntag.anq`: Command queue for AST functions. Allows commands to be queued during page load time and executed when the `ast.js` script loads asynchronously.

## Debug mode

The AST library suppresses its `console.log` statements by default unless debug mode is enabled. In debug mode, developer console output is available.

To enable debug mode for the page you are viewing, add `?ast_debug=true` to the end of the URL of the page. For example,

`www.site.com/page.html?ast_debug=true`

You can also enable debug mode on a tag by adding  `apntag.debug = true;`

## Debug auction

To run a debug auction, add `?ast_debug=true&ast_dongle=ABC&ast_debug_member=1234` to the end of the URL of the page you are viewing (where `ABC` is your dongle used for debugs and `1234` is your debug member ID). For example, `http://www.site.com/page.html?ast_debug=true&ast_dongle=ABC&ast_debug_member=1234`

Alternatively, debug mode can be enabled on the tag using:

```
apntag.debug = true;
apntag.dongle = 'ABC';
apntag.debug_member = '1234';
```

## AST Toolkit

Publishers desire a way to quickly identify the source of particular ads on their page so they can make decisions about allowing them to serve in the future.  The AST Toolkit allows them to easily identify and block a creative that they see on their page.

To turn on AST Toolkit, add `?ast_toolkit=true&ast_dongle=ABC` to the end of the URL of the page you are viewing (where `ABC` is your dongle used for debugs). For example, `http://www.site.com/page.html?ast_toolkit=true&ast_dongle=ABC`

The AST Toolkit will provide the following data for each ad slot to the user:

- Creative ID
- Buyer Member ID
- Creative size served
- Available sizes on the auction
- Winning bid (CPM)
- Demand source
- Ad type (Banner, Video, Native)
- Media Type ID
- Link to UI Ad Quality screen for profile
- Link to Creative Preview

  AST Toolkit requires that `member` is set in `setPageOpts()` or `defineTag()`.

## Functions

- [Ad Object API](ad-object-api.md)
- [Attach Click Trackers](attach-click-trackers.md)
- [Clear Request](clear-request.md)
- [Define Tag](define-tag.md)
- [Enable Cookie Set](enable-cookie-set.md)
- [Fire Impression Trackers](fire-impression-trackers.md)
- [Get AST Version](get-ast-version.md)
- [Get Tag](get-tag.md)
- [Load Tags](load-tags.md)
- [Modify Tag](modify-tag.md)
- [Notify](notify.md)
- [Off Event](off-event.md)
- [On Event](on-event.md)
- [Push](push.md)
- [Refresh](refresh.md)
- [Resize Ad](resize-ad.md)
- [Set Endpoint](set-endpoint.md)
- [Set Keywords](set-keywords.md)
- [Set Page Options](set-page-options.md)
- [Set SafeFrame Configuration](set-safeframe-configuration.md)
- [Show Tag](show-tag.md)
