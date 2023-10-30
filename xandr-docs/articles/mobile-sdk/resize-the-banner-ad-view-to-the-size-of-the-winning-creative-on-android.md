---
title: Resize the Banner Ad View to the Size of the Winning Creative on Android
description: Resize the banner ad view on Android to the size of the winning creative after winning a bid using methods for height and width retrieval.
ms.custom: android-sdk
---

# Resize the banner ad view to the size of the winning creative on Android

When you win a bid, you may want to resize the banner ad view to the size of the winning creative.

To retrieve the height and width of the winning creative, use the getCreativeHeight and getCreativeWidth methods.

## Methods

| Method | Description |
|:---|:---|
| `getCreativeWidth()` | Retrieve the width of the creative for the banner ad view. |
| `getCreativeHeight()` | Retrieve the height of the creative for the banner ad view. |

## Example

```
BannerAdView bav = new BannerAdView(this);
bav.getCreativeWidth();
bav.getCreativeHeight();
```
