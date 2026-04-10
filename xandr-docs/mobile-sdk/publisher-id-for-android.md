---
title: Publisher ID for Android
description: Learn how to use publisherId to control which default creative is served when an ad request fails at the placement level on Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Publisher ID for Android

This article describes how to use `publisherId` to control which default creative is served when an ad request fails.

## Overview

Setting `publisherId` on an ad unit determines which default creative is served when an ad request fails at the placement level:

- If `publisherId` is set, a failed request is rerouted to the publisher-level default creative.
- If `publisherId` is not set, a failed request is rerouted to the member-level default creative.

## Methods

| Method | Description |
|:---|:---|
| `public void setPublisherId(int publisherId)` | Sets the publisher ID on the ad unit. |
| `public int getPublisherId()` | Returns the currently set publisher ID. |

## Example

Set `publisherId` on any ad unit before calling `loadAd`.

### [Java](#tab/java1)

```java
// Banner
BannerAdView banner = new BannerAdView(this);
banner.setPlacementID("123456"); // Set placement ID
banner.setPublisherId(12345); // Set publisher ID
banner.loadAd(); // Load the ad
// Native
NativeAdRequest nativeAdRequest = new NativeAdRequest(this, "123456");
nativeAdRequest.setPublisherId(12345); // Set publisher ID
```

### [Kotlin](#tab/kotlin1)

```kotlin
// Banner
val banner = BannerAdView(this)
banner.setPlacementID("123456") // Set placement ID
banner.publisherId = 12345 // Set publisher ID
banner.loadAd() // Load the ad
// Native
val nativeAdRequest = NativeAdRequest(this, "123456")
nativeAdRequest.publisherId = 12345 // Set publisher ID
```

---

To retrieve the currently set publisher ID:

### [Java](#tab/java2)

```java
// Banner
int publisherId = banner.getPublisherId(); // Get publisher ID
// Native
int nativePublisherId = nativeAdRequest.getPublisherId(); // Get publisher ID
```

### [Kotlin](#tab/kotlin2)

```kotlin
// Banner
val publisherId = banner.publisherId // Get publisher ID
// Native
val nativePublisherId = nativeAdRequest.publisherId // Get publisher ID
```

---

## Multi ad request

`publisherId` can optionally be set when initializing `ANMultiAdRequest`. For initialization options and full usage, see [Multi Ad Request for Android](./multi-ad-request-for-android.md).
