---
title: Android SDK integration instructions
description: Learn how to integrate the current Android SDK into your app and configure its required dependencies and permissions.
ms.custom: android-sdk
ms.date: 09/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Android SDK integration instructions

This page describes how to integrate the Android SDK with your app.

For instructions on showing different ad types, see:

- [Show Banners on Android](show-banners-on-android.md)
- [Show Interstitials on Android](show-interstitials-on-android.md)

This section provides instructions to set up the Android SDK to display ads in your app.

## Requirements

- Your app's minimum SDK version must be Android 5.0 (API level 21) or later.
- To request ads, use a valid placement ID. For supported ad units, you can instead use a valid member ID and inventory code.

> [!TIP]
> - **Google Play services**
> To enable the Android Advertising ID (AAID) for frequency capping and mobile app targeting, include the Google Play services ads identifier library. The Android SDK functions without this optional dependency, but AAID-based features aren't available.

> - **Android Studio and Gradle**
> These instructions assume you are using Android Studio and Gradle. The Android SDK's required manifest entries and consumer ProGuard rules are automatically merged into your app. If you use another build system, the steps may vary.

## Installation

### Step 1. Get the SDK

Make sure Maven Central is included in your project's repositories. Then add the Android SDK and Google Play services ads identifier dependencies to your app module's `build.gradle` file:

```gradle
dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:9.14.0'
    implementation 'com.google.android.gms:play-services-ads-identifier:18.2.0'
}
```

The Google Play services dependency is optional. Omit it if your app doesn't use AAID-based frequency capping or mobile app targeting.

To add mediation adapters, see [Mediate with Android](mediate-with-android-sdk-instructions.md).

<!-- - Check out the source code from [Github](https://github.com/appnexus/mobile-sdk-android) and follow the instructions in [Build the Android SDK From Source](build-the-android-sdk-from-source.md). -->

### Step 2. Edit app permissions (optional)

Location access isn't required for the Android SDK to request ads. If your app chooses to provide location data, declare the permissions that match the level of access your app needs:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
</manifest>
```

- `ACCESS_COARSE_LOCATION` allows access to approximate location.
- `ACCESS_FINE_LOCATION` allows access to precise location. Declare and request it only if your app needs precise location.

On Android 6.0 (API level 23) and later, your app must request declared location permissions at runtime. The Android SDK accesses location only after the user grants permission.
>
For more information, see [Request runtime permissions](https://developer.android.com/training/permissions/requesting) in the Android documentation.

> [!NOTE]
> The Android SDK doesn't request location updates. When location is enabled, it uses a location supplied by your app or the device's available last-known location.

### Step 3. Configure code shrinking for AAID

The Android SDK accesses the Google Play services ads identifier library through reflection. If your app enables R8 or ProGuard and includes the optional AAID dependency, add the following rules to your app's ProGuard rules file:

```proguard
# Preserve Google Play services classes used to retrieve the AAID.
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient {
    public static com.google.android.gms.ads.identifier.AdvertisingIdClient$Info getAdvertisingIdInfo(android.content.Context);
}
-keep class com.google.android.gms.ads.identifier.AdvertisingIdClient$Info {
    public java.lang.String getId();
    public boolean isLimitAdTrackingEnabled();
}
```

### Step 4. Set up for mediation (optional)

For instructions on getting set up for mediation, see [Mediate with Android](mediate-with-android-sdk-instructions.md).

## Implementation note: Forwarding lifecycle callbacks

The SDK allows you to forward lifecycle callbacks for the subclasses of `AdView`: `BannerAdView` and `InterstitialAdView`.

Forwarding lifecycle callbacks is highly recommended for better performance. For anyone mediating AdMob/DFP banners, it is a requirement that they be called, as we need to forward the lifecycle callbacks to the AdMob/DFP banner as required by them. See the code sample below for information about which methods to call, and when.

The following example uses `BannerAdView`. Use the same lifecycle methods when working with `InterstitialAdView`.

For more information about activity lifecycles, see [Managing the Activity Lifecycle](https://developer.android.com/guide/components/activities/intro-activities) in the Android docs.

### [Kotlin](#tab/kotlin1)

```kotlin
class BannerActivity : AppCompatActivity() {
    private lateinit var banner: BannerAdView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        banner = BannerAdView(this) // Create the banner ad view
        banner.setPlacementID("123456") // Set placement ID
        setContentView(banner)
    }

    override fun onResume() {
        super.onResume()
        banner.activityOnResume() // Forward the resume callback
    }

    override fun onPause() {
        banner.activityOnPause() // Forward the pause callback
        super.onPause()
    }

    override fun onDestroy() {
        banner.activityOnDestroy() // Forward the destroy callback
        super.onDestroy()
    }
}
```

### [Java](#tab/java1)

```java
public class BannerActivity extends AppCompatActivity {
    private BannerAdView banner;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        banner = new BannerAdView(this); // Create the banner ad view
        banner.setPlacementID("123456"); // Set placement ID
        setContentView(banner);
    }

    @Override
    protected void onResume() {
        super.onResume();
        banner.activityOnResume(); // Forward the resume callback
    }

    @Override
    protected void onPause() {
        banner.activityOnPause(); // Forward the pause callback
        super.onPause();
    }

    @Override
    protected void onDestroy() {
        banner.activityOnDestroy(); // Forward the destroy callback
        super.onDestroy();
    }
}
```

---

## Related topics

- [Show Banners](show-banners-on-android.md)
- [Show Interstitials](show-interstitials-on-android.md)
