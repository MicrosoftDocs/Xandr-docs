---
title: Create and Customize a Video Placement Tag
description: In this article, find step-by-step instructions on how to create and customize a video placement tag.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create and customize a video placement tag

Tag customization requires you to build on the root tag by identifying the correct handler for your implementation, then adding a combination of required and optional parameters.

> [!NOTE]
> Microsoft Advertising now supports a domain, [adnxs-simple.com](http://adnxs-simple.com/), which does not send or read browser cookies on requests. Clients can leverage this cookie-free domain when there is no consent to use personal data. Relevant calls initiated by Microsoft Advertising will automatically use this domain when there is no consent or when cookies are not required for the function. For more information, see [Part of Service Policies](../policies-regulations/index.yml).

To customize a video placement tag for use in a tag implementation:

1. On the **Placement** screen in Monetize, click **Export Tag** to export the root of the tag.

    A typical root tag looks like this: `https://secure.adnxs.com/ptv?id=12345678`.

1. If the page is secure, update the endpoint to `https://`

1. The default tag uses the `ptv` handler. See the following table to determine whether you should replace the handler with a different one.

    | Placement type | Client-Side Handler | Server-Side Handler |
    |---|---|---|
    | single ad | `ptv` | `ssptv` |
    | ad pod | `vmap` | `ssvmap` |

    > [!NOTE]
    > Some video players don't support VMAP. If your player doesn't support it, you can implement ad pods using the `/ptv` or `/ssptv` handler.

1. Add the required parameters to your tag. For  more information, see:
    - [Required Tag Parameters for Desktop and Mobile Web Inventory](required-parameters-for-mobile-web-inventory.md)
    - [Required Tag Parameters for Android and iOS Inventory](required-parameters-for-android-and-ios-inventory.md)
    - [Required Tag Parameters for CTV Inventory](required-parameters-for-ctv-inventory.md)
