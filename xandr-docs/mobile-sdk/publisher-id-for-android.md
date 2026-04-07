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

- If `publisherId` is set, a failed request is rerouted to the publisher level default placement.
- If `publisherId` is not set, a failed request is rerouted to the member level default placement.

## Methods

| Method | Description |
|:---|:---|
| `public void setPublisherId(int publisherId)` | Sets the publisher ID on the ad unit. |
| `public int getPublisherId()` | Returns the currently set publisher ID. |

## Example

Set `publisherId` on any ad unit before calling `loadAd`.

### [Java](#tab/java1)

```java
BannerAdView adView = new BannerAdView(this);
adView.setPlacementID("123456");
adView.setPublisherId(12345);
adView.loadAd();
```

### [Kotlin](#tab/kotlin1)

```kotlin
val adView = BannerAdView(this)
adView.setPlacementID("123456")
adView.publisherId = 12345
adView.loadAd()
```

---

To retrieve the currently set publisher ID:

### [Java](#tab/java2)

```java
int publisherId = adView.getPublisherId();
```

### [Kotlin](#tab/kotlin2)

```kotlin
val publisherId = adView.publisherId
```

---

## Multi ad request

`publisherId` can optionally be set when initializing `ANMultiAdRequest`. For initialization options and full usage, see [Multi Ad Request for Android](./multi-ad-request-for-android.md).
