---
title: Viewability measurement on iOS
description: Learn how the iOS SDK supports ad viewability measurement.
ms.custom: ios-sdk
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Viewability measurement on iOS

This article describes how the iOS SDK supports ad viewability measurement.

## Overview

The iOS SDK uses the IAB Tech Lab's industry-standard Open Measurement SDK (OM SDK) to measure viewability and support third-party verification. Viewability measurement starts automatically during normal SDK operation; no separate integration is required.

For more information about the industry standard, see the [IAB Tech Lab Open Measurement SDK](https://iabtechlab.com/standards/open-measurement-sdk/).

## Manage friendly obstructions

Viewability measurement determines how much of an ad is visible. App UI that overlaps an ad can reduce the measured visible area. Register an overlapping view as a friendly obstruction only when it is an intentional part of the ad experience, such as a close button or logo. The measurement process excludes registered friendly obstructions from obstruction calculations while continuing to measure the ad.

Keep the following points in mind:

- Views contained within the ad are already treated as part of the ad and do not need to be registered.
- Do not register unrelated app content or controls as friendly obstructions.
- Friendly obstructions affect viewability calculations; they do not hide or remove the registered views.

Use the following methods on `ANBannerAdView`, `ANInterstitialAd`, and `ANInstreamVideoAd`:

| Method | Description |
|:---|:---|
| `addOpenMeasurementFriendlyObstruction:` | Adds a view as a friendly obstruction. |
| `removeOpenMeasurementFriendlyObstruction:` | Removes a view from the friendly obstruction list. |
| `removeAllOpenMeasurementFriendlyObstructions` | Removes all views from the friendly obstruction list. |

### Example

The following example uses a banner ad. The same methods are available on `ANInterstitialAd` and `ANInstreamVideoAd`.

#### [Swift](#tab/swift1)

```swift
let banner = ANBannerAdView(frame: rect, placementId: "123456", adSize: size)
banner.addOpenMeasurementFriendlyObstruction(friendlyObstructionView) // Add a friendly obstruction
banner.removeOpenMeasurementFriendlyObstruction(friendlyObstructionView) // Remove a friendly obstruction
banner.removeAllOpenMeasurementFriendlyObstructions() // Remove all friendly obstructions
```

#### [Objective-C](#tab/objectivec1)

```objectivec
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"123456" adSize:size];
[banner addOpenMeasurementFriendlyObstruction:friendlyObstructionView]; // Add a friendly obstruction
[banner removeOpenMeasurementFriendlyObstruction:friendlyObstructionView]; // Remove a friendly obstruction
[banner removeAllOpenMeasurementFriendlyObstructions]; // Remove all friendly obstructions
```

---

### Register native ad friendly obstructions

Use one of the following methods on `ANNativeAdResponse`:

| Method | Description |
|:---|:---|
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>openMeasurementFriendlyObstructions:<wbr>error:</code> | Registers a native ad view for tracking, makes the entire view clickable, and identifies its friendly obstructions. |
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>clickableViews:<wbr>openMeasurementFriendlyObstructions:<wbr>error:</code> | Registers a native ad view for tracking, makes the listed views clickable, and identifies its friendly obstructions. |

Pass the friendly obstruction views when registering the native ad response. Native ads do not support removing individual friendly obstructions after registration.

#### [Swift](#tab/swift2)

```swift
try nativeAdResponse.registerView(
    forTracking: nativeView,
    withRootViewController: self,
    openMeasurementFriendlyObstructions: [friendlyObstructionView]
) // Register the native view and its friendly obstructions
```

#### [Objective-C](#tab/objectivec2)

```objectivec
[nativeAdResponse registerViewForTracking:nativeView
                   withRootViewController:self
           openMeasurementFriendlyObstructions:@[friendlyObstructionView]
                                    error:nil]; // Register the native view and its friendly obstructions
```

---

## Enable OMID optimization

OMID optimization reduces ongoing OM SDK session work based on ad visibility. Consider enabling it if your app experiences performance overhead from continued viewability tracking and a shorter verification measurement window is acceptable. Leave it disabled when maintaining the full measurement duration is more important. This setting does not turn viewability measurement on or off; it only controls how long the measurement session remains active.

Set the property before loading banner ads or registering native ad views so the setting applies consistently. The property supports banner and native ads only; it does not apply to interstitial or instream video ads.

Use the following property on `ANSDKSettings`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `enableOMIDOptimization` | BOOL | readwrite, assign | Controls whether the SDK shortens OMID session tracking for banner and native ads. The default is `NO`. |

#### [Swift](#tab/swift3)

```swift
ANSDKSettings.sharedInstance().enableOMIDOptimization = true // Enable OMID optimization
```

#### [Objective-C](#tab/objectivec3)

```objectivec
[ANSDKSettings sharedInstance].enableOMIDOptimization = YES; // Enable OMID optimization
```

---

## Related topics

- [Introduction to viewability](../monetize/introduction-to-viewability.md)
- [Reporting on viewability](../monetize/reporting-on-viewability.md)