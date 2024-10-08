---
title: Get Facebook Demand for Native on iOS
description: In this article, learn how to retrieve native ad assets for display in Facebook's Audience Network SDK on iOS devices.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Get Facebook demand for native on iOS

This document describes the process for retrieving native ad assets to display in Facebook's Audience Network SDK.

> [!NOTE]
> This SDK requires Xcode version 15.0 or higher and your app should target iOS version 12.0 or higher.

## SDK installation

The Xandr SDK and Xandr-FAN-Demand Package will need to be installed. Use [CocoaPods](https://cocoapods.org/).
<!-- There are two ways to install our SDK:

1. Download and unzip the latest release of our SDK from our [Github Releases](https://github.com/appnexus/mobile-sdk-ios/releases/latest) page. If you don't want the binary release, you can clone the source code from our [Github repo](https://github.com/appnexus/mobile-sdk-ios) and build it yourself. Drag and drop the FacebookCSRAdapter folder into Xcode Project.
1. Use [CocoaPods](https://cocoapods.org/). -->

Once you have CocoaPods installed.

1. Use Terminal or your command line editor of choice and navigate to the project directory and create a podfile.

    ``` 
    pod init
    ```

1. Using a text editor, open the newly created podfile. Set the platform to 12.0 (AppNexus always supports two iOS releases back from the current release) and add pod 'AppNexusSDX' to the target.

    ``` 
    # iOS: Podfile config to include our SDK
    platform :ios, '12.0'
         
    project 'SampleApp'
         
    target 'SampleApp' do
        
      pod 'AppNexusSDK'
      pod 'AppNexusSDK/FacebookCSRAdapter'
        
    end 
    ```

1. Save your changes and return to Terminal and enter:

    ``` 
    pod install
    ```

1. Cocoapods will download both the AppNexus SDK and FacebookCRSAdapter and also create a workspace in the project directory. If your project is currently open, close it and open the workspace.

## Initialize Facebook's Audience Network SDK

Early in the lifecycle of your app, initialize Facebook's Audience Network SDK (`FBAudienceNetworkAds`) as shown in the code-block below.

``` 
[FBAudienceNetworkAds 
  initializeWithSettings:fbAdSettingObject  
  completionHandler:^(FBAdInitResults *results) {
         if (results.success) {
             [ANFBSettings setFBAudienceNetworkInitialize:YES];
             complete(nil);
         } else {
             [ANFBSettings setFBAudienceNetworkInitialize:NO];
             complete(error); 
        }
     }];
```

On successful initialization of `FBAudienceNetworkAds`, `setFBAudienceNetworkInitialize` is set to `YES`, otherwise it is set as `NO`. If the value is set as `YES` i.e. Audience Network SDK is initialized, `getBidderToken` method of Audience Network SDK would return the Facebook Bidder Token to proceed further. For values set as `NO`, `getBidderToken` method will return nil.

Starting with iOS 14, Publisher App need to set a new API **setAdvertiserTrackingEnabled**  to fulfil the iOS policy obligations for using the Audience Network SDK. A new API **setAdvertiserTrackingEnabled** was added to **FBAdSettings** that is functional on only iOS 14 (and later) with FacebookAd SDK 6.0.0.

``` 
// Set the flag as true if a user provides consent
 [FBAdSettings setAdvertiserTrackingEnabled:YES];
 // Set the flag as false if a user disallows tracking
 [FBAdSettings setAdvertiserTrackingEnabled:NO];
```

## Create native ad request and load ad

> [!NOTE]
> Retain a reference to the request until a response has been returned.

``` 
self.nativeAdRequest= [[ANNativeAdRequest alloc] init];
self.nativeAdRequest.placementId = @"18793423";
self.nativeAdRequest.delegate = self;
[self.nativeAdRequest loadAd];
```

## Handle response for FBNativeBanner

Create a layout for FBNativeBanner. You can follow the example provided by [Facebook](https://developers.facebook.com/docs/audience-network/guides/initialize-sdk).

If a successful response is returned:

``` 
- (void)adRequest:(ANNativeAdRequest *)request didReceiveResponse:(ANNativeAdResponse *)response {
    // (code which loads the view)
    self.nativeAdResponse = response;
    self.adTitleLabel.text = self.nativeAdResponse.title;
    self.bodyLabel.text = self.nativeAdResponse.body;
    self.adSponsoredLabel.text = self.nativeAdResponse.sponsoredBy;
 
 
     if(self.nativeAdResponse.customElements[kANNativeCSRObject] && self.nativeAdResponse.customElements[kANNativeCSRObject] isKindOfClass:[ANAdAdapterCSRNativeBannerFacebook class]) {
        ANAdAdapterCSRNativeBannerFacebook *fbNativeBanner = (ANAdAdapterCSRNativeBannerFacebook *)response.customElements[kANNativeCSRObject];
        // CSR registerViewForTracking (see example below)
    }else {
        //  Non CSR registerViewForTracking
            //  See native ad examples here: show-native-ads-on-ios.md
    }
}
```

On a response error:

``` 
- (void)adRequest:(ANNativeAdRequest *)request didFailToLoadWithError:(NSError *)error withAdResponseInfo:(ANAdResponseInfo *)adResponseInfo{
    NSLog(@"didFailToLoadWithError");
}
```

## Register the view for tracking

Call the registerViewForTracking method of the ANAdAdapterCSRNativeBannerFacebook object.

### For MediaView with clickableViews

``` 
/*registerViewForTracking using MediaView with Click Tracker */
[fbNativeBanner registerViewForTracking:self.adUIView
                 withRootViewController:self
                          iconView:self.adIconView
                         clickableViews:@[self.adUIView]];          
```

### For MediaView with no clickableViews

``` 
/*registerViewForTracking using MediaView without Click Tracker */
[fbNativeBanner registerViewForTracking:self.adUIView
                 withRootViewController:self
                          iconView:self.adIconView];          
```

### For ImageView with clickableViews (no MediaView)

``` 
/* registerViewForTracking using Image View with Click Tracker */
  [fbNativeBanner registerViewForTracking:self.adUIView
                   withRootViewController:self
                            iconImageView:self.imageView
                           clickableViews:@[self.adUIView]];     
```

### For ImageView with no clickableViews (no MediaView)

``` 
/*registerViewForTracking using Image View without Click Tracker */
[fbNativeBanner registerViewForTracking:self.adUIView
                     withRootViewController:self
                              iconImageView:self.imageView];
```

## Unregister the view

When the ad is finished being displayed, the view must be unregistered.

``` 
self.nativeAdResponse = nil; // It will handle ad unregister views
```

## Related topics

- [iOS SDK Integration Instructions](ios-sdk-integration-instructions.md)
- [Show Banner Native on iOS](show-banner-native-on-ios.md)
- [Show Native Ads on iOS](show-native-ads-on-ios.md)
