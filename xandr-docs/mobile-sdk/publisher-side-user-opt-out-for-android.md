---
title: Publisher-side User Opt-Out for Android
description: The publisher side user opt-out feature in Android SDK allows publishers to set users' choice of opt-in/out for Android from tracking in the ad requests.
ms.custom: android-sdk
ms.date: 07/17/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Publisher side user opt-out for Android

## Overview

The publisher side user opt-out feature exposes an API in the Android SDK that lets publishers pass the users' opt-in/out tracking choice with every `AdRequest`. For any `AdRequest`, the Android SDK populates `limitAdTracking` (LMT), read from [`AdvertisingIdClient`](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient). However, the publishers retain information about their users' opt-in/out of tracking and thus required to pass that information if their user has opted out to comply with applicable privacy regulations. Use the `setDoNotTrack` method to pass this opt-out choice to the Android SDK.

## Methods

Use the following methods on `SDKSettings`:

| Method | Description |
|:---|:---|
| `public static void setDoNotTrack(boolean dnt)` | Setter method which enables the publisher side user opt-out feature. Set to `true` to indicate opt-out from tracking, or `false` to indicate opt-in. When set to `true`, tracking cookies and AAID are disabled for all future auctions. Default value is `false`. |
| `public static boolean getDoNotTrack()` | Getter method which indicates whether the tracking is enabled or not. Returns `true` if Do not track is enabled, `false` otherwise. |

## Example

### [Kotlin](#tab/kotlin1)

```
// Setter
SDKSettings.setDoNotTrack(true)
// Getter
SDKSettings.getDoNotTrack()
```

### [Java](#tab/java1)

```
// Setter
SDKSettings.setDoNotTrack(true);
// Getter
SDKSettings.getDoNotTrack();
```

---

## Related

- [SDK privacy for Android](sdk-privacy-for-android.md)
