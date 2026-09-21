---
title: Mediate with Android
description: Learn how to add and set up mediation adapters for the Android SDK.
ms.custom: android-sdk
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Mediate with Android

This article describes how to install and configure mediation adapters for the Android SDK.

## Overview

Mediation enables your app to request ads from multiple ad networks through the Android SDK. Each adapter connects the Android SDK to a network SDK. During an ad request, mediation checks the configured demand sources until one fills the request or no demand remains.

## Supported networks and media types

The following mediation adapters and media types are supported:

| Demand source | Network SDK version | Banner | Interstitial | Native | Docs |
|:---|:---|:---|:---|:---|:---|
| Google AdMob | 24.5.0 | Yes | Yes | Yes | [AdMob mediation](https://developers.google.com/admob/android/mediation) |
| Google Ad Manager | 24.5.0 | Yes | Yes | No | [Google Ad Manager mediation](https://developers.google.com/ad-manager/mobile-ads-sdk/android/mediation) |
| SmartAdServer | 7.23.0 | Yes | Yes | No | [SmartAdServer SDK documentation](https://documentation.smartadserver.com/displaySDK/) |

## Requirements

- Your app must use Android 6.0 (API level 23) or later when integrating Google Mobile Ads SDK (Legacy) 24.5.0.
- These instructions assume that you use Android Studio and Gradle.
- Install a supported Android SDK release. For instructions, see [Android SDK integration instructions](./android-sdk-integration-instructions.md).

Gradle automatically merges each adapter's required manifest entries and consumer ProGuard rules into your app.

## Install mediation adapters

Make sure Maven Central is included in your project's repositories. Then add the Android SDK and the required mediation adapters to your app module's `build.gradle` file:

```gradle
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:[9,10)'
    implementation 'com.appnexus.opensdk.mediatedviews:appnexus-googleplay-mediation:[9,10)'
    implementation 'com.appnexus.opensdk.mediatedviews:appnexus-smartadserver-mediation:[9,10)'
}
```

Each adapter dependency includes a compatible version of its network SDK.

After installing the adapters, complete the configuration for each adapter before loading ads.

## Google Mobile Ads SDK (Legacy)

The Google adapter supports Google AdMob and Google Ad Manager demand. Both demand sources support banner and interstitial ads. Native mediation is available only for AdMob.

***Add the Google app ID (AdMob and Google Ad Manager)***

Add the `com.google.android.gms.ads.APPLICATION_ID` metadata key to your app's `AndroidManifest.xml`. Set its value to your AdMob or Google Ad Manager app ID. This app-level setting applies to all Google ad formats:

```xml
<application>
    <meta-data
        android:name="com.google.android.gms.ads.APPLICATION_ID"
        android:value="ca-app-pub-################~##########" />
</application>
```

***Forward lifecycle callbacks (AdMob and Google Ad Manager)***

Google banner mediation requires forwarding the host activity's lifecycle callbacks to `BannerAdView`. For interstitial ads, the callbacks prevent late responses after the activity is paused or destroyed. For implementation examples, see [Forwarding lifecycle callbacks](./android-sdk-integration-instructions.md#implementation-note-forwarding-lifecycle-callbacks).

***Pass a content URL (AdMob and Google Ad Manager)***

To pass the URL of the content surrounding an ad to Google, add `content_url` as a custom keyword to the ad unit. This applies to banner and interstitial requests for AdMob and Google Ad Manager, and native requests for AdMob. The following example uses `BannerAdView`:

#### [Kotlin](#tab/kotlin1)

```kotlin
// Banner
val banner = BannerAdView(this) // Create the banner ad view
banner.addCustomKeywords("content_url", "https://www.example.com") // Set the content URL
```

#### [Java](#tab/java1)

```java
// Banner
BannerAdView banner = new BannerAdView(this); // Create the banner ad view
banner.addCustomKeywords("content_url", "https://www.example.com"); // Set the content URL
```

---

***Set a Publisher Provided ID (Google Ad Manager only)***

To pass a publisher-defined identifier to Google Ad Manager for ad targeting and reporting, set a **Publisher Provided ID (PPID)** before making ad requests. This applies only to Google Ad Manager demand:

#### [Kotlin](#tab/kotlin2)

```kotlin
GooglePlayAdsSettings.setGooglePublisherProvidedId("example-ppid-123") // Set the Google PPID
```

#### [Java](#tab/java2)

```java
GooglePlayAdsSettings.setGooglePublisherProvidedId("example-ppid-123"); // Set the Google PPID
```

---

***Configure native media rendering (AdMob only)***

Choose how your app renders media in AdMob native ads:

- **Default rendering:** The adapter returns image asset URLs and doesn't populate Google's `MediaView`.
- **Google media rendering:** To let `MediaView` render the image or video asset, call `AdMobNativeSettings.setEnableMediaView(true)` before making the native ad request. The view used to render the response must extend `com.google.android.gms.ads.nativead.NativeAdView`.
- **Video playback:** Optionally, use `VideoOptions` to configure how native video plays.

The following example enables `MediaView` and starts native video muted:

#### [Kotlin](#tab/kotlin3)

```kotlin
val videoOptions = VideoOptions.Builder().setStartMuted(true).build() // Start native video muted
AdMobNativeSettings.setVideoOptions(videoOptions) // Configure native video playback
AdMobNativeSettings.setEnableMediaView(true) // Enable Google MediaView rendering
val nativeAdRequest = NativeAdRequest(this, "123456") // Create the native ad request
nativeAdRequest.loadAd() // Load the native ad
```

#### [Java](#tab/java3)

```java
VideoOptions videoOptions = new VideoOptions.Builder().setStartMuted(true).build(); // Start native video muted
AdMobNativeSettings.setVideoOptions(videoOptions); // Configure native video playback
AdMobNativeSettings.setEnableMediaView(true); // Enable Google MediaView rendering
NativeAdRequest nativeAdRequest = new NativeAdRequest(this, "123456"); // Create the native ad request
nativeAdRequest.loadAd(); // Load the native ad
```

---

## SmartAdServer

The SmartAdServer adapter doesn't require additional configuration after you add its dependency.

## Custom mediation networks

Microsoft Monetize provides built-in support for several mobile ad networks. To mediate another network:

- Write a [custom mediation adaptor](./android-custom-adaptors.md) that enables the Android SDK to receive events from the network SDK.
- Follow the instructions in [Add a Network](../digital-platform-api/mediated-network-service.md) to create a **Custom Mobile Network**.

## Related topics

- [Android SDK integration instructions](./android-sdk-integration-instructions.md)
- [Android Custom Adaptors](./android-custom-adaptors.md)
