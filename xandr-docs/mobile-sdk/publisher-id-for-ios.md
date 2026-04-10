---
title: Publisher ID for iOS
description: Learn how to use publisherId to control which default creative is served when an ad request fails at the placement level on iOS.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Publisher ID for iOS

This article describes how to use `publisherId` to control which default creative is served when an ad request fails.

## Overview

Setting `publisherId` on an ad unit determines which default creative is served when an ad request fails at the placement level:

- If `publisherId` is set, a failed request is rerouted to the publisher-level default creative.
- If `publisherId` is not set, a failed request is rerouted to the member-level default creative.

## Properties

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `publisherId` | NSInteger | readwrite, assign | The publisher ID associated with the ad unit. |

## Example

Set `publisherId` on any ad unit before calling `loadAd`.

### [Objective-C](#tab/objectivec1)

```objectivec
// Banner
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"123456" adSize:size];
banner.publisherId = 12345; // Set publisher ID
[banner loadAd]; // Load the ad
// Native
ANNativeAdRequest *nativeAdRequest = [[ANNativeAdRequest alloc] init];
nativeAdRequest.publisherId = 12345; // Set publisher ID
```

### [Swift](#tab/swift1)

```swift
// Banner
let banner = ANBannerAdView(frame: rect, placementId: "123456", adSize: size)
banner.publisherId = 12345 // Set publisher ID
banner.loadAd() // Load the ad
// Native
let nativeAdRequest = ANNativeAdRequest()
nativeAdRequest.publisherId = 12345 // Set publisher ID
```

---

To retrieve the currently set publisher ID:

### [Objective-C](#tab/objectivec2)

```objectivec
// Banner
NSInteger publisherId = banner.publisherId; // Get publisher ID
// Native
NSInteger nativePublisherId = nativeAdRequest.publisherId; // Get publisher ID
```

### [Swift](#tab/swift2)

```swift
// Banner
let publisherId = banner.publisherId // Get publisher ID
// Native
let nativePublisherId = nativeAdRequest.publisherId // Get publisher ID
```

---

## Multi ad request

`publisherId` can optionally be set when initializing `ANMultiAdRequest`. For initialization options and full usage, see [Multi Ad Request for iOS](./multi-ad-request-for-ios.md).
