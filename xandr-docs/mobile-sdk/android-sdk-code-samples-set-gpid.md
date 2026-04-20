---
title: Set GPID for Android (Global Placement ID)
description: Learn how to set a Global Placement ID (GPID) for Android platform, with code samples to assist in your app development.
ms.custom: android-sdk
ms.date: 4/20/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Set GPID for Android

This article describes how to use `gpid` to assign a globally unique identifier to an ad placement.

## Overview

`gpid` (Global Placement ID) is a publisher-specified, distinct, and persistent identifier for an ad unit. The Mobile SDK's `placementId` identifies an ad slot within Monetize, but buyers purchasing inventory across multiple SSPs have no way of knowing which placement is being transacted in a given auction. Setting `gpid` gives buyers a consistent identifier for the same ad slot across all SSPs and Prebid integrations. For the full specification, see the [IAB OpenRTB GPID community extension](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/main/extensions/community_extensions/gpid.md).

- If `gpid` is set, the identifier is included in every ad request from that unit.
- If `gpid` is not set, no global placement identifier is sent with the request.

## Methods

| Method | Description |
|:---|:---|
| `public void setGpid(String gpid)` | Sets the Global Placement ID on the ad unit. |
| `public String getGpid()` | Returns the currently set Global Placement ID. |

## Example

### [Java](#tab/java1)

```java
// Banner
BannerAdView banner = new BannerAdView(this, "123456");
banner.setGpid("Test_GlobalPlacementId"); // Set Global Placement ID
banner.loadAd(); // Load the ad
String gpid = banner.getGpid(); // Get Global Placement ID

// Native
NativeAdRequest nativeAdRequest = new NativeAdRequest(this, "123456");
nativeAdRequest.setGpid("Test_GlobalPlacementId"); // Set Global Placement ID
String nativeGpid = nativeAdRequest.getGpid(); // Get Global Placement ID
```

### [Kotlin](#tab/kotlin1)

```kotlin
// Banner
val banner = BannerAdView(this, "123456")
banner.gpid = "Test_GlobalPlacementId" // Set Global Placement ID
banner.loadAd() // Load the ad
val gpid = banner.gpid // Get Global Placement ID

// Native
val nativeAdRequest = NativeAdRequest(this, "123456")
nativeAdRequest.gpid = "Test_GlobalPlacementId" // Set Global Placement ID
val nativeGpid = nativeAdRequest.gpid // Get Global Placement ID
```
