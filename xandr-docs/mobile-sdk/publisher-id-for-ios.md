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

- If `publisherId` is set, a failed request is rerouted to the publisher level default placement.
- If `publisherId` is not set, a failed request is rerouted to the member level default placement.

## Properties

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `publisherId` | NSInteger | readwrite, assign | The publisher ID associated with the ad unit. |

## Example

Set `publisherId` on any ad unit before calling `loadAd`.

### [Objective-C](#tab/objectivec1)

```objectivec
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"123456" adSize:size];
banner.publisherId = 12345;
[banner loadAd];
```

### [Swift](#tab/swift1)

```swift
let banner = ANBannerAdView(frame: rect, placementId: "123456", adSize: size)
banner.publisherId = 12345
banner.loadAd()
```

---

To retrieve the currently set publisher ID:

### [Objective-C](#tab/objectivec2)

```objectivec
NSInteger publisherId = banner.publisherId;
```

### [Swift](#tab/swift2)

```swift
let publisherId = banner.publisherId
```

---

## Multi ad request

`publisherId` can optionally be set when initializing `ANMultiAdRequest`. For initialization options and full usage, see [Multi Ad Request for iOS](./multi-ad-request-for-ios.md).
