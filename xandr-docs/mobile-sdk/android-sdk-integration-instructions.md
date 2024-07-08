---
title: Android SDK Integration Instructions
description: In this article, find step-by-step instructions on how to integrate our Android SDK with your project.
ms.custom: android-sdk
ms.date : 10/28/2023
---

# Android SDK integration instructions

This page describes how to integrate our SDK with your project.

For instructions on showing different ad types, see:

- [Show Banners on Android](show-banners-on-android.md)
- [Show Interstitials on Android](show-interstitials-on-android.md)

Follow the instructions in this section to set up our SDK to show ads in your app.

## Requirements

This SDK requires Android 4 or later, and Android SDK version 14 or higher.

In order to show ads, you must have a valid Xandr placement ID. This is a numeric ID that represents a context in an application where ads can be shown.

> [!TIP]
>
> - **Google Play**
>
>     In order to enable the Android Advertising ID (AAID) for frequency capping and mobile app targeting, you must include Google Play Services as a dependency of your app. Xandr's SDK will still function without Google Play Services, but you won't have access to those features.
> - **Android Studio and Gradle**
>
>     These instructions assume you are using Android Studio and Gradle. Most of the required `AndroidManifest.xml` entries (except the Location permissions) and ProGuard changes are automatically added to your app. If you are using other build systems, the steps may vary.

## Installation

### Step 1. Get the SDK

Install via Maven from your `build.gradle` file as shown below. Note that the `[9,10)` notation means that when your app is compiled, the latest version of the SDK in the 9.x release series will be included. When we release a new version of the SDK, all you have to do to get the new version is recompile your app. If you want to include mediation adaptors for other SDKs in your `build.gradle`, see the section **Let us Mediate other Networks** of [Mediate with Android](mediate-with-android-sdk-instructions.md).
  
  > [!NOTE]
  > These are top-level blocks, not part of the buildscript block.

> [!WARNING]
> The compile command is no longer supported by Gradle, it has been replaced with the implementation command.
>
> ```
> // Android: Gradle config to install the SDK
> repositories {
>     mavenCentral()
> }
> 
> dependencies {
>     implementation 'com.appnexus.opensdk:appnexus-sdk:[9,10)'
> }
>    
> ```
>

<!-- - Check out the source code from [Github](https://github.com/appnexus/mobile-sdk-android) and follow the instructions in [Build the Android SDK From Source](build-the-android-sdk-from-source.md). -->

### Step 2. Edit app permissions (optional)

Edit your Android manifest to include the following (optional but recommended) permissions:

```
<!-- Android: XML to include recommended permissions -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

<!-- Add the permissions here... -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

- `ACCESS_COARSE_LOCATION` (recommended) - Grants the SDK permission to access approximate location based on cell tower.
- `ACCESS_FINE_LOCATION` (recommended) - Grants the SDK permission to access a more accurate location based on GPS.

> [!TIP]
> Location permissions must prompt the user:
>
> In API Level 23 (Marshmallow) and above, you must prompt the user with a dialog at app runtime for either of the location permissions listed above. The SDK can only access location permissions with the user's consent.
>
> For more information, see [Request Permissions](https://developer.android.com/training/permissions/requesting#perm-request) from the Android documentation.

Although not technically required, the location permissions make it possible for the SDK to send location-based data to advertisers. Sending better location data generally leads to better monetization.

> [!NOTE]
> The SDK will never wake up the phone to request the location to be updated; this would take time and battery. Instead, it will use these permissions to access the last known location of the device.

### Step 3. Edit ProGuard settings

If your app uses ProGuard, you must edit your ProGuard settings to avoid stripping Google Play out of your app. The SDK doesn't require Google Play to function, but you will lose access to the Android Advertiser ID (AAID), which is used for app targeting and frequency capping. Edit your project's `proguard-project.txt` file to add the following:

```
### Proguard settings to support Android Advertiser ID
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient {
    com.google.android.gms.ads.identifier.AdvertisingIdClient$Info getAdvertisingIdInfo(android.content.Context);
}
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient$Info {
    java.lang.String getId();
    boolean isLimitAdTrackingEnabled();
}     
```

### Step 4. Set up for mediation (optional)

For instructions on getting set up for mediation, see [Mediate with Android](mediate-with-android-sdk-instructions.md).

## Implementation note: Forwarding lifecycle callbacks

The SDK allows you to forward lifecycle callbacks for the subclasses of `AdView`: `BannerAdView` and `InterstitialAdView`.

Forwarding lifecycle callbacks is highly recommended for better performance. For anyone mediating AdMob/DFP banners, it is a requirement that they be called, as we need to forward the lifecycle callbacks to the AdMob/DFP banner as required by them. See the code sample below for information about which methods to call, and when.

For more information about activity lifecycles, see [Managing the Activity Lifecycle](https://developer.android.com/guide/components/activities/intro-activities) in the Android docs.

```
    /**
     * To be called by the developer when the fragment/activity's onDestroy() function is called.
     */
    abstract public void activityOnDestroy();

    /**
     * To be called by the developer when the fragment/activity's onPause() function is called.
     */
    abstract public void activityOnPause();

    /**
     * To be called by the developer when the fragment/activity's onResume() function is called.
     */
    abstract public void activityOnResume(); 
```

## Related topics

- [Show Banners](show-banners-on-android.md)
- [Show Interstitials](show-interstitials-on-android.md)
