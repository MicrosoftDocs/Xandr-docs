---
title: Viewability measurement on Android
description: Learn how the Android SDK supports ad viewability measurement.
ms.custom: android-sdk
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Viewability measurement on Android

This article describes how the Android SDK supports ad viewability measurement.

## Overview

The Android SDK uses the IAB Tech Lab's industry-standard Open Measurement SDK (OM SDK) to measure viewability and support third-party verification. Viewability measurement starts automatically during normal SDK operation; no separate integration is required.

For more information about the industry standard, see the [IAB Tech Lab Open Measurement SDK](https://iabtechlab.com/standards/open-measurement-sdk/).

## Manage friendly obstructions

Viewability measurement determines how much of an ad is visible. App UI that overlaps an ad can reduce the measured visible area. Register an overlapping view as a friendly obstruction only when it is an intentional part of the ad experience, such as a close button or logo. The measurement process excludes registered friendly obstructions from obstruction calculations while continuing to measure the ad.

Keep the following points in mind:

- Views contained within the ad are already treated as part of the ad and do not need to be registered.
- Do not register unrelated app content or controls as friendly obstructions.
- Friendly obstructions affect viewability calculations; they do not hide or remove the registered views.

Use the following methods on `BannerAdView`, `InterstitialAdView`, and `VideoAd`:

| Method | Description |
|:---|:---|
| `void addFriendlyObstruction(View view)` | Adds a view as a friendly obstruction. |
| `void removeFriendlyObstruction(View view)` | Removes a view from the friendly obstruction list. |
| `void removeAllFriendlyObstructions()` | Removes all views from the friendly obstruction list. |

### Example

The following example uses a banner ad. The same methods are available on `InterstitialAdView` and `VideoAd`.

#### [Kotlin](#tab/kotlin1)

```kotlin
val banner = BannerAdView(this)
banner.setPlacementID("123456") // Set placement ID
banner.addFriendlyObstruction(friendlyObstructionView) // Add a friendly obstruction
banner.removeFriendlyObstruction(friendlyObstructionView) // Remove a friendly obstruction
banner.removeAllFriendlyObstructions() // Remove all friendly obstructions
```

#### [Java](#tab/java1)

```java
BannerAdView banner = new BannerAdView(this);
banner.setPlacementID("123456"); // Set placement ID
banner.addFriendlyObstruction(friendlyObstructionView); // Add a friendly obstruction
banner.removeFriendlyObstruction(friendlyObstructionView); // Remove a friendly obstruction
banner.removeAllFriendlyObstructions(); // Remove all friendly obstructions
```

---

### Register native ad friendly obstructions

Use one of the following methods on `NativeAdSDK`:

| Method | Description |
|:---|:---|
| <code>public static void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>NativeAdEventListener listener, <wbr>List&lt;View&gt; friendlyObstructionsList)</code> | Registers the native ad container for impression tracking, makes the entire container clickable, and identifies its friendly obstructions. |
| <code>public static void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>List&lt;View&gt; clickableViews, <wbr>NativeAdEventListener listener, <wbr>List&lt;View&gt; friendlyObstructionsList)</code> | Registers the native ad container for impression tracking, makes the listed views clickable, and identifies its friendly obstructions. |

Pass the friendly obstruction views when registering the native ad response. Native ads do not support removing individual friendly obstructions after registration.

#### [Kotlin](#tab/kotlin2)

```kotlin
NativeAdSDK.registerTracking(
    nativeAdResponse,
    nativeView,
    nativeAdEventListener,
    listOf(friendlyObstructionView)
) // Register the native view and its friendly obstructions
```

#### [Java](#tab/java2)

```java
NativeAdSDK.registerTracking(
    nativeAdResponse,
    nativeView,
    nativeAdEventListener,
    Arrays.asList(friendlyObstructionView)
); // Register the native view and its friendly obstructions
```

---

## Enable OMID optimization

OMID optimization reduces ongoing OM SDK session work for native ads. When enabled, the Android SDK periodically checks a registered native ad container and finishes its OMID session after the container becomes fully visible. This setting does not enable or disable viewability measurement, change click handling, or change when impression URLs are fired. It is disabled by default.

Configure the setting before registering native ad views. It applies to native ads that use the SDK impression tracker. It does not apply to banner ads or native CSR and mediation integrations that manage impression tracking outside the SDK impression tracker.

Use the following methods on `SDKSettings`:

| Method | Description |
|:---|:---|
| `public static void setOMIDOptimizationEnabled(boolean enabled)` | Enables or disables OMID session-lifecycle optimization for native ads. |
| `public static boolean isOMIDOptimizationEnabled()` | Returns whether OMID session-lifecycle optimization is enabled. |

Set OMID optimization through `SDKSettings` before calling `NativeAdSDK.registerTracking()`.

### [Kotlin](#tab/kotlin3)

```kotlin
SDKSettings.setOMIDOptimizationEnabled(true) // Enable OMID optimization
val omidOptimizationEnabled = SDKSettings.isOMIDOptimizationEnabled() // Get the current setting
```

### [Java](#tab/java3)

```java
SDKSettings.setOMIDOptimizationEnabled(true); // Enable OMID optimization
boolean omidOptimizationEnabled = SDKSettings.isOMIDOptimizationEnabled(); // Get the current setting
```

---

## Related topics

- [Introduction to viewability](../monetize/introduction-to-viewability.md)
- [Reporting on viewability](../monetize/reporting-on-viewability.md)
