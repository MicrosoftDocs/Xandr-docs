---
title: Integrate Vungle Demand for Interstitial Video Ads on Android
description: Learn how to integrate and display interstitial video ads using Vungle on Android.
ms.custom: android-sdk
ms.date: 10/28/2023
---

# Integrate Vungle demand for interstitial video ads on Android

This page provides steps to integrate and display interstitial video ads using Vungle on Android. Follow these steps to configure and display interstitial video ads using Vungle on Android.

## Step 1: Install the SDK

To integrate Vungle demand, include the **AppNexus Mobile SDK** and the **Vungle Demand Adapter** in your project.  Include the following dependencies in the `build.gradle` file under the `dependencies` section:

```gradle


dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:[9,10)'
    implementation 'com.appnexus.opensdk.csr:appnexus-vungle-csr:[9,10)'
}
```

## Step 2: Initialize the Vungle SDK

Initialize the Vungle SDK early in your app's lifecycle to ensure it is ready to use. Replace `YOUR_APP_ID` with the app ID provided by Vungle.

```java

VungleAds.init(this, "YOUR_APP_ID", new InitializationListener() {
    @Override
    public void onSuccess() {
        Log.d("vunglecsr", "Vungle SDK initialized successfully");
    }

    @Override
    public void onError(@NonNull VungleError vungleError) {
        Log.d("vunglecsr", "Initialization failed: " + vungleError.getErrorMessage());
    }
});
```

On successful initialization of the Vungle SDK, the `ANVungleSettings.setVungleInitialize` method is set to `true`. If initialization fails, the value is set to `false`.

- If the flag is `true` (Vungle SDK is initialized), the `getBidderToken` method will return the Vungle Bidder Token, allowing you to proceed with further steps.
- If the flag is `false`, the `getBidderToken` method will return `nil`, indicating that the SDK initialization has failed.

### Step 3: Initialize an interstitial ad and set the required keyword

After successfully initializing the Vungle SDK, the bidder token is captured by the AppNexus SDK during the ad request and forwarded to the primary supply platform (PSP).

To load an interstitial ad, create an instance of the `InterstitialAdView` object. Ensure you retain a reference to this object appropriately.

Set a custom keyword before calling the loadAd() method. Use the following specifications:

- **Key**: `"VUNGLE_PLACEMENT_ID_FOR_CSR"`
- **Value**: Your Vungle placement ID mapped to the Monetize placement.

Here’s an example:

```java
// Create and configure the interstitial ad object
interstitialAdView = new InterstitialAdView(this);

// Set the Monetize placement ID
interstitialAdView.setPlacementID("32380589");

// Add the custom keyword for Vungle placement
interstitialAdView.addCustomKeywords("VUNGLE_PLACEMENT_ID_FOR_CSR", "VUNGLE_PLACEMENT_123");

// Set the ad listener to handle ad events
interstitialAdView.setAdListener(adListener);

// Load the ad
interstitialAdView.loadAd();
```

> [!NOTE]
>
> - Replace "32380589" with your Monetize placement ID.
> - Replace "VUNGLE_PLACEMENT_123" with the Vungle placement ID mapped to your ad configuration.

By following this process, you ensure the ad request includes the necessary bidder token and configuration for displaying interstitial ads.

### Step 4: Render the ad

After successfully loading the interstitial ad, render the creative when it fits your app's flow. In this example, the ad is displayed immediately.

```java
public void onAdLoaded(AdView iav) {
    // Display the interstitial ad
    interstitialAdView.show();
}
```
