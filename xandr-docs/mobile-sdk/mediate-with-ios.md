---
title: Mediate with iOS
description: This article provides information on mediation with iOS. Mediation lets you sell ad impressions through multiple networks to generate more revenue.
ms.custom: ios-sdk
---

# Mediate with iOS

<!--Mediation lets you sell ad impressions through multiple networks to generate more revenue. This is initiated by your main (mediating) SDK which calls out to one or more mediated SDKs in a "waterfall"-like process. If your main SDK can't show an ad for some reason, it can iterate over the list of mediated SDKs and contact them in the order you specify. This will continue until the impression is filled or you've run out of mediated SDKs.

Reasons to mediate to another SDK include the following:

- To provide better monetization under specific circumstances
- To provide access to information such as a unique user ID or the device's operating system, location, or ID
- Some networks only accept requests from their own SDKs, forcing you to use their SDK to access their demand -->

## Supported networks and media types

This section lists the networks that we provide mediation adaptors for, and the media types that each adaptor supports. For each adaptor, we show whether it supports banners, interstitials, native, or all three.

| Adaptor | Version | Banner | Interstitial | Native | Docs |
|:---|:---|:---|:---|:---|:---|
| AdMob and DFP | 10.10.0  | Yes | Yes | Yes | [Google Mobile Ads - iOS Document](https://developers.google.com/admob/ios/mediation) |
| SmartAdServer | 7.24.2  | Yes | Yes | No | [SmartAdServer Documentation](https://documentation.smartadserver.com/displaySDK/) |

## Prerequisites

To mediate these networks, you'll need the following:

- A supported release of our SDK. For instructions on installing our SDK, see [Integrate with iOS](./ios-sdk-integration.md).
- The SDK of the network you want to mediate.
- A mediation adaptor that allows our SDK to communicate with the network's SDK. If you use [CocoaPods](https://cocoapods.org/), use the code below in your project directory's PodFile. You can include as many or as few adaptors as you like from this list:

    ```
    platform :ios, '12.0'
       
    target 'SimpleBanner' do
      pod 'AppNexusSDK/GoogleAdapter'
      pod 'AppNexusSDK/SmartAdAdapter'
    end   
    ```

<!-- - There are two ways to get our mediation adaptors:
  - You can install the binary builds of the adaptors that are included with our [official releases](https://github.com/appnexus/mobile-sdk-ios/releases). You can also build the adaptors yourself from [source](https://github.com/appnexus/mobile-sdk-ios/tree/master/mediation/mediatedviews).
  - If you use [CocoaPods](https://cocoapods.org/), use the code below in your project directory's PodFile. You can include as many or as few adaptors as you like from this list: -->

## Instantiating mediation adaptors

If you use the following adaptor, you need to initialize the adaptor's SDK as early as possible in the lifecycle of the application. A perfect place to do this is in the app delegate. The code samples below show how to do this.

### AdMob native mediation

> [!NOTE]
> The instructions in this section are only needed if you are doing native mediation. Mediating banners and interstitials should not require any initialization code or further work.

To handle AdMob native ads, you need to:

1. Create a native ad view that inherits from `GADNativeAdView`:

    ```
    #pragma mark - ANNativeAdRequestDelegate
    - (void)adRequest:(ANNativeAdRequest *)request didReceiveResponse:(ANNativeAdResponse *)response
    {
       ...
       if (self.nativeAdResponse.networkCode == ANNativeAdNetworkCodeAdMob) {
        // If ANNativeAdNetworkCodeAdMob, special Steps are there for creating a View which supports Google's MediaView Requirements.
            
        GADNativeAdView *nativeAdView = // Pass your Google Admob View(Step 2)for rendering Native Ad response ;
        ...
        // All the native components will be set as regular Ad  
        // Main Image is automatically added by GoogleSDK in the MediaView
       }else{
         ...
          // If not ANNativeAdNetworkCodeAdMob, create a regular View for all others.
       }
    }
    ```

    > [!NOTE]
    > For SDK v5.3 and higher, you need to specify the `GADIsADManagerApp` key in the app's `info.plist` with a boolean `YES` value.
    >
    > ```
    > <key>GADIsAdManagerApp</key>
    >  <true/>
    > ```

1. Set up the custom keyword.

    For passing the content URL to the Google SDK, the content URL needs to be passed as a custom keyword with the requester ad object (`BannerAdView`, `InterstitialAdView`, `NativeAdRequest`). The key to be used is `content_url`. Here is an example:

    ```
    // Add key content_url with a value (www.appnexus.com).
    [adView addCustomKeywordWithKey:@"content_url" value:@"www.appnexus.com"];
    ```

### AdMob banner mediation  

> [!NOTE]
> The instructions in this section are only needed to load AdMob banner ads in iPads for the apps that support multi-window capability.

To handle AdMob banner ads for the apps that support multi-window capability in iPads, Xandr Mobile SDK provides a public class `ANGoogleMediationSettings`. This class contains:

- Boolean method `setIPadMultiSceneSupport` that needs to be set as `YES`, if the app supports multi-screen in iPads.
- Getter method `getIPadMultiSceneSupport` to fetch the value set for the apps.

  **Code Sample (Objective C)**

  ```
  /**
   Set setIPadMultiScreenSupport to YES if the application will support multiscene in iPad.
   */
  + (void)setIPadMultiSceneSupport:(BOOL)setIPadMultiSceneSupport;
  + (BOOL)getIPadMultiSceneSupport;
  ```

Additionally, publishers should load the ad from `viewDidAppear` method instead of `viewDidLoad` in the app.

#### Example of use (Objective C)

```
/**
 Set setIPadMultiScreenSupport to YES if the application will support multiscene in iPad.
 */
[ANGoogleMediationSettings setIPadMultiSceneSupport:YES];
```

## Custom mobile networks

Microsoft Monetize has built-in support for a number of popular mobile ad networks. If you want to mediate a network it doesn't support, you must:

- Write a [custom mediation adaptor](./ios-custom-adaptors.md) that lets our SDK receive events from the SDK you want to mediate.
- Set up a **Custom Mobile Network** using the instructions in [Add a Network](../digital-platform-api/mediated-network-service.md).

## Related topics

- [Integrate with iOS](./ios-sdk-integration.md)
- [iOS Custom Adaptors](./ios-custom-adaptors.md)
