---
title: Mediate with iOS
description: Learn how to add and set up mediation adapters for the iOS SDK.
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Mediate with iOS

This article describes how to install and configure mediation adapters for the iOS SDK.

## Overview

Mediation enables your app to request ads from multiple ad networks through the iOS SDK. Each adapter connects the iOS SDK to a network SDK. During an ad request, mediation checks the configured demand sources until one fills the request or no demand remains.

## Supported networks and media types

The following mediation adapters and media types are supported:

| Demand source | Network SDK version | Banner | Interstitial | Native | Docs |
|:---|:---|:---|:---|:---|:---|
| Google AdMob | 12.8.0 | Yes | Yes | Yes | [AdMob mediation](https://developers.google.com/admob/ios/mediation) |
| Google Ad Manager | 12.8.0 | Yes | Yes | No | [Google Ad Manager mediation](https://developers.google.com/ad-manager/mobile-ads-sdk/ios/mediation) |
| SmartAdServer | 7.24.2 | Yes | Yes | No | [SmartAdServer SDK documentation](https://documentation.smartadserver.com/displaySDK/) |

## Requirements

- Your app must target iOS 15.0 or later.
- Install a supported iOS SDK release. For instructions, see [iOS SDK integration instructions](ios-sdk-integration-instructions.md).
- Add an adapter for each network you want to mediate.

## Install mediation adapters

Use Swift Package Manager to add one or both mediation adapter packages. Each package declares compatible iOS SDK and third-party network SDK dependencies, which Swift Package Manager resolves automatically.

For Google AdMob or Google Ad Manager, add the following package and select the `ANGoogleAdapter` product:

```text
https://github.com/appnexus/mobile-sdk-ios-mediation-google
```

For SmartAdServer, add the following package and select the `ANSmartAdapter` product:

```text
https://github.com/appnexus/mobile-sdk-ios-mediation-smartadserver
```

For each adapter:

1. Open your project in Xcode.
1. Select the project in the Project navigator, and then select **Package Dependencies**.
1. Select the **+** button, enter one of the package URLs shown above, and then press **Return**.
1. Choose the version setting that fits your project. For new projects, select **Up to Next Major Version**. Then select **Add Package**.
1. Select the adapter product identified above and your app target, and then select **Add Package**.
1. Verify that the adapter appears under **Package Dependencies**.

After installing the adapters, complete the configuration for each adapter before loading ads.

## Google Mobile Ads SDK

The `ANGoogleAdapter` package supports Google AdMob and Google Ad Manager demand. Both demand sources support banner and interstitial ads. Native mediation is available only for AdMob.

***Add the Google app ID (AdMob and Google Ad Manager)***

Add the `GADApplicationIdentifier` key to your app's `Info.plist`. Set its value to your AdMob or Google Ad Manager app ID. This app-level setting applies to all Google ad formats:

```xml
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-################~##########</string>
```

***Pass a content URL (AdMob and Google Ad Manager)***

To pass the URL of the content surrounding an ad to Google, add `content_url` as a custom keyword to the ad unit. This applies to banner and interstitial requests for AdMob and Google Ad Manager, and native requests for AdMob. The following example uses `ANBannerAdView`:

#### [Swift](#tab/swift1)

```swift
let size = CGSize(width: 320, height: 50)
let banner = ANBannerAdView(frame: CGRect(origin: .zero, size: size), placementId: "123456", adSize: size) // Create the banner ad view
banner.addCustomKeywords(withKey: "content_url", values: ["https://www.example.com"]) // Set the content URL
```

#### [Objective-C](#tab/objectivec1)

```objectivec
CGSize size = CGSizeMake(320, 50);
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:CGRectMake(0, 0, 320, 50) placementId:@"123456" adSize:size]; // Create the banner ad view
[banner addCustomKeywordsWithKey:@"content_url" values:@[@"https://www.example.com"]]; // Set the content URL
```

---

***Support multiple iPad windows (AdMob and Google Ad Manager)***

To load Google-mediated banner ads in an iPad app that supports multiple windows, enable multi-scene support before loading ads. Load the banner from `viewDidAppear(_:)` instead of `viewDidLoad()`. This configuration applies only to Google-mediated banner ads in multi-window iPad apps:

#### [Swift](#tab/swift2)

```swift
ANGoogleMediationSettings.setIPadMultiSceneSupport(true) // Enable iPad multi-scene support
```

#### [Objective-C](#tab/objectivec2)

```objectivec
[ANGoogleMediationSettings setIPadMultiSceneSupport:YES]; // Enable iPad multi-scene support
```

---

***Set a Publisher Provided ID (Google Ad Manager only)***

To pass a publisher-defined identifier to Google Ad Manager for ad targeting and reporting, set a **Publisher Provided ID (PPID)** before making ad requests. This applies only to Google Ad Manager demand:

#### [Swift](#tab/swift3)

```swift
ANGoogleMediationSettings.setGooglePublisherProvidedId("example-ppid-123") // Set the Google PPID
```

#### [Objective-C](#tab/objectivec3)

```objectivec
[ANGoogleMediationSettings setGooglePublisherProvidedId:@"example-ppid-123"]; // Set the Google PPID
```

---

***Set up native mediation (AdMob only)***

To render an AdMob native response, load the native ad view from a XIB. Set the XIB's root view to `NativeAdView` in Swift or `GADNativeAdView` in Objective-C. The following example verifies that AdMob filled the request, renders the title, and registers the view for tracking:

#### [Swift](#tab/swift4)

```swift
func adRequest(_ request: ANNativeAdRequest, didReceive response: ANNativeAdResponse) {
  guard response.networkCode == .adMob else { return }

  let adNib = UINib(nibName: "NativeAdView", bundle: .main)
  guard let nativeAdView = adNib.instantiate(withOwner: self).first as? NativeAdView else { return }
  (nativeAdView.headlineView as? UILabel)?.text = response.title // Render the native ad title

  do {
    try response.registerView(
      forTracking: nativeAdView,
      withRootViewController: self,
      clickableViews: [nativeAdView.callToActionView as Any]
    ) // Register the AdMob native view
  } catch {
    print("Unable to register the AdMob native view: \(error)")
  }
}
```

#### [Objective-C](#tab/objectivec4)

```objectivec
- (void)adRequest:(ANNativeAdRequest *)request
    didReceiveResponse:(ANNativeAdResponse *)response {
  if (response.networkCode != ANNativeAdNetworkCodeAdMob) {
    return;
  }

  NSArray *objects = [[NSBundle mainBundle] loadNibNamed:@"NativeAdView"
                           owner:self
                           options:nil];
  GADNativeAdView *nativeAdView = objects.firstObject;
  ((UILabel *)nativeAdView.headlineView).text = response.title; // Render the native ad title

  NSError *registrationError = nil;
  [response registerViewForTracking:nativeAdView
         withRootViewController:self
             clickableViews:@[nativeAdView.callToActionView]
                error:&registrationError]; // Register the AdMob native view
}
```

---

## SmartAdServer

The SmartAdServer adapter doesn't require additional configuration after you add its package dependency.

## Custom mediation networks

Microsoft Monetize provides built-in support for several mobile ad networks. To mediate another network:

- Write a [custom mediation adaptor](./ios-custom-adaptors.md) that enables the iOS SDK to receive events from the network SDK.
- Follow the instructions in [Add a Network](../digital-platform-api/mediated-network-service.md) to create a **Custom Mobile Network**.

## Related topics

- [iOS SDK integration instructions](ios-sdk-integration-instructions.md)
- [iOS Custom Adaptors](./ios-custom-adaptors.md)
