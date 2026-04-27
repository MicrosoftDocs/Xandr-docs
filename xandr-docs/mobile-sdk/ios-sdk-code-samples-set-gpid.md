---
title: Set GPID for iOS
description: Learn how to set a Global Placement ID (GPID) in the iOS SDK.
ms.custom: ios-sdk
ms.date: 4/20/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Set GPID for iOS

This article describes how to use `gpid` to assign a globally unique identifier to an ad placement.

## Overview

`gpid` (Global Placement ID) is a publisher-specified, distinct, and persistent identifier for an ad unit. The Mobile SDK's `placementId` identifies an ad slot in Monetize, but when buyers purchase inventory across multiple SSPs, they can't reliably tell which placement is being sold in a given auction. Set `gpid` to provide a consistent identifier for the same ad slot across SSPs and Prebid integrations. For the full specification, see the [IAB OpenRTB GPID community extension](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/main/extensions/community_extensions/gpid.md).

- If `gpid` is set, the identifier is included in every ad request from that unit.
- If `gpid` is not set, no global placement identifier is sent with the request.

## Properties

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `gpid` | NSString | readwrite, copy | The Global Placement ID associated with the ad unit. |

## Example

### [Objective-C](#tab/objectivec1)

```objectivec
// Banner
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"123456" adSize:size];
banner.gpid = @"Test_GlobalPlacementId"; // Set GPID
[banner loadAd]; // Load the ad
NSString *gpid = banner.gpid; // Get GPID

// Native
ANNativeAdRequest *nativeAdRequest = [[ANNativeAdRequest alloc] init];
nativeAdRequest.placementId = @"123456"; // Set Monetize placement ID
nativeAdRequest.gpid = @"Test_GlobalPlacementId"; // Set GPID
NSString *nativeGpid = nativeAdRequest.gpid; // Get GPID
```

### [Swift](#tab/swift1)

```swift
// Banner
let banner = ANBannerAdView(frame: rect, placementId: "123456", adSize: size)
banner.gpid = "Test_GlobalPlacementId" // Set GPID
banner.loadAd() // Load the ad
let gpid = banner.gpid // Get GPID

// Native
let nativeAdRequest = ANNativeAdRequest()
nativeAdRequest.placementId = "123456" // Set Monetize placement ID
nativeAdRequest.gpid = "Test_GlobalPlacementId" // Set GPID
let nativeGpid = nativeAdRequest.gpid // Get GPID
```
