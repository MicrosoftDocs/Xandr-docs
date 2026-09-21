---
title: Vungle Demand for iOS
description: Learn how to integrate Vungle demand for interstitial video ads on iOS using the AppNexus SDK and ANVungleAdapter.
ms.custom: ios-sdk
ms.date: 09/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Vungle demand for iOS

This page provides detailed steps for integrating and displaying Interstitial Video Ads using the Vungle SDK in your iOS application.

## Prerequisites

Before integrating Vungle demand, ensure that you have the following:

- An app that targets iOS 15.0 or later.
- A Vungle app ID and placement ID.

## SDK installation

Install the Vungle adapter by using Swift Package Manager. The adapter package includes compatible versions of the iOS SDK and Vungle Ads SDK as dependencies.

1. Open your project in Xcode.
1. Select the project in the Project navigator, and then select **Package Dependencies**.
1. Select the **+** button to add a package dependency.
1. Enter the following package URL in the search box, and then press **Return**:

   ```text
   https://github.com/appnexus/mobile-sdk-ios-mediation-vungle
   ```

1. Choose the version setting that fits your project. For new projects, select **Up to Next Major Version**. Then select **Add Package**.
1. Select the **ANVungleAdapter** product and your app target, and then select **Add Package**.
1. Verify that **ANVungleAdapter** appears under **Package Dependencies**.

## Initialize the Vungle SDK

To initialize the Vungle SDK, add the following code to the early lifecycle of your app.
Replace "YOUR_APP_ID" with the App ID provided by Vungle.

### Example

#### [Swift](#tab/swift1)

```swift

VungleAds.initWithAppId("YOUR_APP_ID") { error in
    if let error = error {
        print("VUNGLE - Error initializing SDK: \(error.localizedDescription)")
        ANVungleSettings.setVungleInitialize(false)
    } else {
        print("VUNGLE - SDK initialization successful")
        ANVungleSettings.setVungleInitialize(true)
    }
}
```

#### [Objective-C](#tab/objectivec1)

```objectivec

[VungleAds initWithAppId:@"YOUR_APP_ID" completion:^(NSError * _Nullable error) {
    if (error) {
        NSLog(@"Error initializing SDK");
        [ANVungleSettings setVungleInitialize:NO];
    } else {
        NSLog(@"Init is complete");
        [ANVungleSettings setVungleInitialize:YES];
    }
}];
```
---

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

#### [Swift](#tab/swift2)

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

#### [Objective-C](#tab/objectivec2)

```objectivec

@property (nonatomic, strong)ANInterstitialAd *interstitialAd;

    self.interstitialAd = [[ANInterstitialAd alloc] initWithPlacementId:@"12345"];
    self.interstitialAd.delegate = self;
    [self.interstitialAd addCustomKeywordWithKey:@"VUNGLE_PLACEMENT_ID_FOR_CSR" value: @"VUNGLE_PLACEMENT_123"];
    [self.interstitialAd loadAd];
```

---

## Render creative

After the interstitial ad is successfully loaded, you can display it to users based on your app's logic. In the example below, the ad is shown immediately upon loading.

### Example

#### [Swift](#tab/swift3)

```swift

func adDidReceiveAd(_ ad: Any) {
    self.interstitialAd.display(from: self)
}
```

#### [Objective-C](#tab/objectivec3)

```objectivec


- (void)adDidReceiveAd:(id<ANAdProtocol>)ad {
    [self.interstitialAd displayAdFromViewController: self];
}
```

---
