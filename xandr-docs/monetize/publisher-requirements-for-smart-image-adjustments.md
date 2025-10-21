---
title: Publisher Requirements for Smart Image Adjustments
description: In this article, learn the publisher requirements to be met before using smart image adjustments.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Publisher requirements for smart image adjustments

Buyers can use Smart Image Adjustments to automatically resize their main native creative image and icon, giving publishers the ability to easily fill their placements with these native creative assets at a much higher capacity. However, publishers must first ensure that they are meeting the neccesary placement dimension criteria to ensure that they will be able to fulfill the buyers' demand.

DSPs such as Oath, TTD, and DBM all require publishers to meet the minimum placement width and height dimension criteria before a bid can be submitted. For resizing to work, these DSPs require that the publisher provide the exact width and height of the placement. For the ad tag to work, the publisher must meet both the minimum and exact width and height criteria.

Typically, the publisher also defines the native creative image requirements using either the exact size of the image or a ratio. The size of the image is defined by the exact height and width such as 500 x 400. The ratio consists of a `min_width` (in pixels), `ratio_height`, and `ratio_width`. For more information, see [Native Layout Service](../digital-platform-api/native-layout-service.md) and [Seller Tag (AST)](../seller-tag/seller-tag.md).

The publisher's required native creative image sizes and dimensions can be defined in real time using our various supply integration endpoints, which includes AST, OpenRTB, and our SDK, as well as the Native Assemebly feature that is available in Monetize. For more information, see [Configuring a Native Assembly](configuring-a-native-assembly.md).

To keep to our recommended native best practices, see [Native Sell-Side Best Practices](https://download.microsoft.com/download/e/e/5/ee544211-092a-45c4-8076-57b5c5aaceb3/28%20Dec%202023/Sell-Side-Native-Best-Practices.pdf).

## Related topics

- [Add a Creative](add-a-creative.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
