---
title: Resize Ads to Fit Screen or Banner Ad View on Android
description: Learn how to expand ad creative to fit banner ad view, device screen width, and container view with instructions provided in this article.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Resize ads to fit screen or banner ad view on Android

Depending on where advertising fits into your application, you might want to expand the ad creative to fill the banner ad view in which it is displayed, or to fit the device's screen width.

This page has instructions for:

- Resizing the ad to fill the banner ad view
- Resizing the ad to fit the device's screen width
- Constraining the ad to the container view (superview)

## Resize ad to fit banner ad view

### Methods
The following methods are supported in this feature:

| Method | Description |
|:---|:---|
| `setResizeAdToFitContainer(boolean)` | Whether the creative should resize to fill the banner ad view in which it is displayed. This feature will cause ad creatives that are smaller than the view size to 'stretch' to the current size. This may cause image quality degradation for the benefit of having an ad occupy the entire ad view. Defaults to `false`. |
| `getResizeAdToFitContainer()` | Check whether the creative will resize to fill the banner ad view in which it is displayed. |

### Example

```
BannerAdView bav = new BannerAdView(this);
bav.setPlacementID("1326299");
bav.setAdSize(300, 50);
bav.setResizeAdToFitContainer(true);
bav.getResizeAdToFitContainer();  // true
```

## Resize ad to fit screen's width

### Methods

| Method | Description |
|:---|:---|
| `setExpandsToFitScreenWidth(boolean)` | Causes the banner ad view to resize to fit the width of the device's screen. This feature will cause ad creatives that are smaller than the screen width to 'stretch' to fit. This may cause image quality degradation for the benefit of having an ad occupy the entire screen. Defaults to `false`. |
| `getExpandsToFitScreenWidth()` | Check whether the banner ad view will resize to fit the width of the device's screen. |

### Example

```
BannerAdView bav = new BannerAdView(this);
bav.setPlacementID("1326299");
bav.setAdSize(300, 50);
bav.setExpandsToFitScreenWidth(true);
bav.getExpandsToFitScreenWidth(); // true
```

### Put them together

If you call both `setExpandsToFitScreenWidth(true)` and `setResizeAdToFitContainer(true)`, the SDK will try to expand the banner ad view to the screen width first, and then adjust the ad to fit the container size.
