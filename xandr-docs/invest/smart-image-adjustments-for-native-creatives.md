---
title: Microsoft Invest - Smart Image Adjustments for Native Creatives
description: In this article, learn what Smart Image Adjustments is, how to access it, and how it works.
ms.date: 10/28/2023
---

# Microsoft Invest - Smart Image Adjustments for native creatives

Buyers can use Smart Image Adjustments to automatically resize their main native creative image and icon with a few clicks of the mouse so that they can quickly meet the publisher's placement criteria.

## Access Smart Image Adjustments for native creatives

By default, the **Allow Smart Image Adjustments** toggle is enabled for all buyers that have access to Microsoft Invest or Microsoft Monetize. To keep to our recommended native best practices, see [Native Buy-Side Best Practices](https://download.microsoft.com/download/6/f/7/6f755603-e9af-4148-9e52-02e1fb7262b0/Xandr/Buy-Side-Native-Best-Practices.pdf).

## Smart Image Adjustments workflow

If buyers bid with a native creative image that doesn't exactly match the dimensions of a publisher's placement, Microsoft Advertising will automatically resize the image by adding white bars to fill the placement when the **Allow Smart Image Adjustments** toggle is enabled. If the buyer doesn't want white bars added, they should select the **Crop image to fit placement** radio button after selecting the **Allow Smart Image Adjustments** toggle so that the image is cropped and centered without white bars. For more information, see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

When using Smart Image Adjustments within Microsoft Invest and Microsoft Monetize, the main native creative image and icon can only be resized up to 200% and down to 50% of the original aspect ratio. Smart Image Adjustments can also convert native creative images vertically and horizontally. This can be done with our Creative Service API , which gives you more control over the max scale factor and aspect ratio bounds. For more information, see [Creative Service API](../digital-platform-api/creative-service.md). The original dimensions of the native creative ultimately determine what is possible.

## Related topic

[Native Creatives](native-creatives.md)
