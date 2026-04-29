---
title: Set GPID for Android
description: Learn how to set a Global Placement ID (GPID) in the Android SDK.
ms.custom: android-sdk
ms.date: 4/20/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Set GPID for Android

This article describes how to use `gpid` to assign a globally unique identifier to an ad placement.

## Overview

`gpid` (Global Placement ID) is a publisher-specified, distinct, and persistent identifier for an ad unit. The Mobile SDK's `placementId` identifies an ad slot in Monetize, but when buyers purchase inventory across multiple SSPs, they can't reliably tell which placement is being sold in a given auction. Set `gpid` to provide a consistent identifier for the same ad slot across SSPs and Prebid integrations. For the full specification, see the [IAB OpenRTB GPID community extension](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/main/extensions/community_extensions/gpid.md).

- If `gpid` is set, the identifier is included in every ad request from that unit.
- If `gpid` is not set, no global placement identifier is sent with the request.

## Methods

| Method | Description |
|:---|:---|
| `public void setGpid(String gpid)` | Sets the Global Placement ID on the ad unit. |
| `public String getGpid()` | Gets the currently set Global Placement ID. |

## Example

### [Java](#tab/java1)

```java
// Banner
BannerAdView banner = new BannerAdView(this, "123456");
banner.setGpid("Test_GlobalPlacementId"); // Set GPID
banner.loadAd(); // Load the ad
String gpid = banner.getGpid(); // Get GPID

// Native
NativeAdRequest nativeAdRequest = new NativeAdRequest(this, "123456");
nativeAdRequest.setGpid("Test_GlobalPlacementId"); // Set GPID
String nativeGpid = nativeAdRequest.getGpid(); // Get GPID
```

### [Kotlin](#tab/kotlin1)

```kotlin
// Banner
val banner = BannerAdView(this, "123456")
banner.gpid = "Test_GlobalPlacementId" // Set GPID
banner.loadAd() // Load the ad
val gpid = banner.gpid // Get GPID

// Native
val nativeAdRequest = NativeAdRequest(this, "123456")
nativeAdRequest.gpid = "Test_GlobalPlacementId" // Set GPID
val nativeGpid = nativeAdRequest.gpid // Get GPID
```
