---
title: Microsoft Monetize - Auto Macro Insertion
description: In this page, learn when and why Microsoft Advertising inserts the `${CLICK_URL}` and `${CACHEBUSTER}` macros into your creative third-party tags. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Auto macro insertion

When you add or edit third-party creative tags, Microsoft Advertising automatically inserts the `${CLICK_URL}` and `${CACHEBUSTER}` macros into your creative third-party tags if the third-party ad server's format is recognized, which will allow you to quickly traffic your creatives.

In some cases, Microsoft Advertising will replace an ad server macro with a macro specific to Microsoft Advertising.

> [!NOTE]
> You can also use the encoded version of the `${CLICK_URL}` macro, such as `${CLICK_URL_ENC}`. For more information, see [Click Tracking](click-tracking.md).

If the Microsoft Advertising auto-tagger fails to automatically insert the `${CLICK_URL}` and `${CACHEBUSTER}` macros into your third-party tag, you can manually insert them into the appropriate locations. For more information, see [Click Tracking](click-tracking.md). If you don't know which parameter to use when inserting the macro, contact your client.

## Inserting macros into Third-Party tags automatically

Microsoft Advertising can automatically insert the `${CLICK_URL}` and `${CACHEBUSTER}` macros into a variety of third-party tags such as Sizmek and Atlas.

> [!NOTE]
> Microsoft Advertising can't auto insert the `${CLICK_URL}` and `${CACHEBUSTER}` macros into Google's DDM tags. However, these third-party tags can still be manually inserted.

Feel free to submit a [support ticket](https://help.xandr.com/s/login/) if you'd like to have a specific tag type added to our supported list. When creating the support ticket, be sure to provide:

- the name of the ad server that these tags appear on.
- the exact parameters used to traffic the `${CLICK_URL}` and `${CACHEBUSTER}` macros.

## Related topics

- [Creative Macros](creative-macros.md)
- [Supported Creative Macros](supported-creative-macros.md)