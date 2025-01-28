---
title: Integrate Vungle Demand for Interstitial Video Ads on iOS
description: Learn how to integrate Vungle demand for interstitial video ads on iOS using the AppNexus SDK and ANVungleAdapter.
ms.custom: ios-sdk
ms.date: 10/28/2023
---

# Integrate Vungle demand for interstitial video ads on iOS

This page provides detailed steps for integrating and displaying Interstitial Video Ads using the Vungle SDK in your iOS application.

## Prerequisites

Before integrating Vungle Demand, ensure that you have the following SDK versions installed:

- **Microsoft Ads SDK**: version 9.3.0
- **ANVungleAdapter**: required for Vungle integration
- **VungleAds SDK**: version 7.3.2

## SDK installation

To integrate the Vungle Demand, you will need to install the **Mobile SDK** and the **ANVungleAdapter** package. Follow the steps below to install the required dependencies using CocoaPods.

### Step 1: Install CocoaPods

If CocoaPods is not installed on your system, follow the instructions at [CocoaPods.org](https://cocoapods.org/) to install it.

### Step 2: Create and configure the Podfile

1. Open Terminal or your preferred command line editor.
1. Navigate to your project directory.
1. Run the following command to create a **Podfile**:

   ```bash
   pod init
   ```

1. Open the **Podfile** using a text editor.
1. Set the platform version to **iOS 12.0** (AppNexus supports two iOS releases back from the current release).
1. Add the following dependencies to the target section.

#### Example Podfile configuration

```ruby


    
    platform :ios, '12.0'
    project 'SampleApp'

    target 'SampleApp' do
        pod 'AppNexusSDK'
        pod 'AppNexusSDK/ANVungleAdapter'
    end
```

### Step 3: Install the Pods

1. Save the changes to the **Podfile**, then proceed to install the dependencies.
1. In Terminal, run the following command to install the pods.

## Initialize the Vungle SDK

To initialize the Vungle SDK, add the following code to the early lifecycle of your app.
Replace "YOUR_APP_ID" with the App ID provided by Vungle.

```

VungleAds.initWithAppId("YOUR_APP_ID") { error in
    if let error = error {
        print("VUNGLE - Error initializing SDK: \(error.localizedDescription)")
    } else {
        print("VUNGLE - SDK initialization successful")
        ANVungleSettings.setVungleInitialize(true)
    }
}
```

- On successful initialization, `ANVungleSettings.setVungleInitialize(true)` will be set.
- If initialization fails, `ANVungleSettings.setVungleInitialize(false)` will be set.
- When initialized successfully, the `getBidderToken` method returns a valid bidder token, while if initialization fails, it returns `nil`.

## Initialize an interstitial object and set required keyword

After successfully initializing Vungle’s SDK, our SDK will automatically capture Vungle’s bidder token and include it in the ad request, which is then passed to PSP. Follow these steps to initialize an interstitial object and set the required keyword:

1. Initialize an **`ANInterstitialAd`** object.
2. Retain a reference to this instance appropriately.
3. Set a custom keyword in the request **before calling the `load()` method**:
   - The key must be the string: **`VUNGLE_PLACEMENT_ID_FOR_CSR`**.
   - The value should be your Vungle placement, mapped to the Monetize placement.

### Example code

```swift

import VungleAdsSDK
import AppNexusSDK
import ANVungleAdapter

var interstitialAd = ANInterstitialAd()

// Initialize the interstitial ad object
interstitialAd = ANInterstitialAd(placementId: "1234567")

// Set the required keyword
interstitialAd.addCustomKeyword(withKey: "VUNGLE_PLACEMENT_ID_FOR_CSR", value: "VUNGLE_PLACEMENT_123")

// Assign a delegate
interstitialAd.delegate = self

// Make a request to load the ad
interstitialAd.load()
```

## Render creative

After the interstitial ad is successfully loaded, you can display it to users based on your app's logic. In the example below, the ad is shown immediately upon loading.

```swift

func adDidReceiveAd(_ ad: Any) {
    self.interstitialAd.display(from: self)
}
```
