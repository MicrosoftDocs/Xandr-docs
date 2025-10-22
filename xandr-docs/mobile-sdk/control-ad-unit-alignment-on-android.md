---
title: Control Ad Unit Alignment on Android
description: In this article, explore detailed instructions on how to control ad unit alignment on Android devices.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Control ad unit alignment on Android

This article has instructions on how to control the alignment of banner ads.

Use the `BannerView.setAdAlignment(enum AdAlignment)` method to override the alignment of the ad unit within the banner ad view:

```
bav.setAdAlignment(BOTTOM_CENTER);
```

However, this works only in the cases where the banner ad view's frame is larger than the ad. The default alignment is `CENTER`. The ad can be aligned in one of the following ways:

- center
- top left
- top center
- top right
- center left
- center right
- bottom left
- bottom center
- bottom right
