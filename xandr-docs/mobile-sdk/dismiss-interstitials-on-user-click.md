---
title: Dismiss Interstitials on User Click
description: In this article, learn how to dismiss interstitial ads when users click, including instructions, methods, and examples.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Dismiss interstitials on user click

By default, when a user clicks an interstitial ad and is taken to the landing page in the device's native browser, when they return to the app the interstitial ad is still displayed. This article has instructions for dismissing the interstitial ad when the user clicks.

To change this behavior so that the interstitial ad view is dismissed when the user clicks on the ad, the following methods are available on the `InterstitialAdView`:

## Methods
The following methods are supported in this feature:

| Method | Description |
|:---|:---|
| `shouldDismissOnClick()` | Whether the interstitial ad view will be dismissed when the user clicks the ad. Defaults to `false`. |
| `setDismissOnClick(boolean)` | Pass `true` to dismiss the interstitial ad view when the user clicks the ad. |

## Example

``` 
InterstitialAdView iav = new InterstitialAdView(this);
iav.setPlacementID("1326299");
iav.setDismissOnClick(true);       
```

## Related topics

- [Show Interstitials](show-interstitials-on-android.md)
- [Xandr Mobile SDKs](xandr-mobile-sdks.md)
