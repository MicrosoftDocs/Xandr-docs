---
title: Microsoft Monetize - Smart Image Adjustments for Native Creatives
description: Explore easy resizing with Smart Image Adjustments, adapting to diverse publisher criteria swiftly for native creatives.
ms.date: 10/28/2023
---

# Microsoft Monetize - Smart image adjustments for native creatives

Buyers can use Smart Image Adjustments to automatically resize their main native creative image and icon with a few clicks of the mouse so that they can quickly meet the publisher's placement criteria.

## Accessing smart image adjustments for native creatives

By default, the **Allow Smart Image Adjustments** toggle is enabled for all buyers that have access to Invest or Monetize. To keep to our recommended native best practices, see [Native Buy-Side Best Practices](https://download.microsoft.com/download/e/e/5/ee544211-092a-45c4-8076-57b5c5aaceb3/28%20Dec%202023/Buy-Side-Native-Best-Practices.pdf).

## How smart image adjustments works?

If buyers bid with a native creative image that doesn't exactly match the dimensions of a publisher's placement, Microsoft Advertising will automatically resize the image by adding white bars to fill the placement when the **Allow Smart Image Adjustments** toggle is enabled. If the buyer doesn't want white bars added, they should select the **Crop image to fit placement** radio button after clicking the **Allow Smart Image Adjustments** toggle so that the image is cropped and centered without white bars. For more information, see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

When using Smart Image Adjustments within Invest and Monetize, the main native creative image and icon can only be resized up to 200% and down to 50% of the original aspect ratio. Smart Image Adjustments can also convert native creative images vertically and horizontally. This can be done with our Creative Service API , which gives you more control over the max scale factor and aspect ratio bounds. For more information, see [Creative Service API](../digital-platform-api/creative-service.md). The original dimensions of the native creative ultimately determine what is possible.

## Related topic

[Native Creatives](native-creatives.md)
