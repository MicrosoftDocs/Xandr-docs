---
title: Get Vungle Demand for Interstitial Video on Android
description: Learn how to integrate and display interstitial video ads using Vungle on Android, including SDK setup, initialization, and ad rendering.
ms.custom: android-sdk
ms.date: 10/28/2023
---

# Get Vungle demand for interstitial video on Android

This page provides steps to integrate and display interstitial video ads using Vungle on Android. Follow these steps to configure and display interstitial video ads using Vungle on Android.

## Step 1: Install the SDK

To integrate Vungle demand, include the **AppNexus Mobile SDK** and the **Vungle Demand Adapter** in your project. Add the following lines to the `dependencies` section of your `build.gradle` file:

```
dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:[9,10)'
    implementation 'com.appnexus.opensdk.csr:appnexus-vungle-csr:[9,10)'
}
```

## Step 2: Initialize the Vungle SDK

Initialize the Vungle SDK early in your app's lifecycle to ensure it is ready to use. Replace `YOUR_APP_ID` with the app ID provided by Vungle.

```
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

In the onSuccess() callback, confirm that the SDK has been initialized successfully. Use the onError() callback to log any initialization errors.

### Step 3: Initialize an interstitial ad and set the required keyword

After successfully initializing the Vungle SDK, the bidder token is captured by the AppNexus SDK during the ad request and forwarded to the primary supply platform (PSP).

To load an interstitial ad, create an instance of the `InterstitialAdView` object. Ensure you retain a reference to this object appropriately.

Before calling the `loadAd()` method, set a custom keyword with the following specifications:

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

Once the interstitial ad has successfully loaded, display the ad at the appropriate moment. In this example, the ad is shown immediately after it is successfully received.

```java
public void onAdLoaded(AdView iav) {
    // Display the interstitial ad
    interstitialAdView.show();
}
```
