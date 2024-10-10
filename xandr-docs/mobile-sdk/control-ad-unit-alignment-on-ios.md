---
title: Control Ad Unit Alignment on iOS
description: In this article, explore detailed instructions on how to control ad unit alignment on iOS devices.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Control ad unit alignment on iOS

This page has instructions on how to control the alignment of banner ads.

Use the `ANBannerViewAdAlignment` property of banner ad views to override the alignment of the ad unit within the banner ad view:

```
banner.alignment = ANBannerViewAdAlignmentBottomCenter;
```

This will only work in cases where the banner ad view's frame is larger than the ad. The default alignment is `ANBannerViewAdAlignmentCenter`. The ad can be aligned in one of the following ways:

- center
- top left
- top center
- top right
- center left
- center right
- bottom left
- bottom center
- bottom right
