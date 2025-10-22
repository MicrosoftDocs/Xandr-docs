---
title: Show Banner Native on iOS
description: Banner Native is the capability of Mobile SDK Banner class to return native demand. This page talks about banner object (ANBannerAdView) and how it is used.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Show banner native on iOS

## Overview
> [!NOTE]
> This offering is currently in Alpha and is subject to change.

The term *Banner Native* refers to the capability of Mobile SDK Banner class to return native demand. The banner object (ANBannerAdView) is multi-format, returning demand for banner ads and, if enabled via the APIs as described in the examples below, video and native ads. This means that you can instantiate a single Banner class object and pass it a single Member ID and Code (or Placement ID) and access demand across any or all of banner, video and native Media Type formats.

If you decide not to use the Banner Native capability you won't notice any significant changes in the manner in which your existing implementations function. There are minor changes to the standard MobileSDK headers (including one iOS header, which has been removed). But other than minor, one-time changes to satisfy the compilation process, there should be no impact on any existing code that uses the Banner class.

## Assumption

The assumption of this document is that you're already familiar with both the Banner and Native classes. To use Banner Native there are a number of significant changes both structurally and procedurally that you must manage.  The Banner class with Banner Native behaves like the traditional Native Request class.  When the Banner class returns with a native ad object, like traditional Native Request, it returns a Native Response object. This Native Response object can then be used in the traditional manner to display and track the ad content of a native ad object.

## Process changes

As of Mobile SDK Version 4.8, there is a change in the procedure of handling banner and video ad objects via the Banner class. Before the introduction of Banner Native,it was possible to add the Banner class instance view to a view hierarchy, even before the class instance returned the ad object. This made it possible to finalize the display setup of the class even before the lifecycle of loading and fetching the ad object had completed. Although this convenient short-cut meant potentially ignoring the callback that indicates the ad has loaded, it is a common pattern with the Mobile SDK.

If the Banner class is used to fetch native ads, the display step MUST wait until after the callback has fired. This is because the callback provides the delivery point for the native ad object, if it is returned, and because it is the only place to distinguish between the return of a native ad object versus a banner or video ad object.

## Mobile SDK structure

- The `ANAdDelegate` method returns an ad object handler that is defined only by id.  (Previous to Version 4.8 the handler was defined as id\<ANAdProtocol\>.)
- The `ANAdDelegate` protocol includes the new method `ad:didReceivNativeAd:`

## Use of multi-format Native Banner Ad View

Following steps explain how the multi-format `ANBannerAdView` is used:

- Enable Native demand for your `ANBannerAdView` using `setAllowNativeDemand `method as well as `shouldAllowNativeDemand` & `enableNativeRendering` properties. For enabling Video demand, use the property `shouldAllowVideoDemand.`

  ``` 
  /**
   * Sets whether or not Native Ads(AppNexus Media Type:12) can serve on this Ad object.
   *
  */
  @property (nonatomic, readwrite) BOOL shouldAllowNativeDemand;
  /**
   *  If enableNativeRendering is not set, the default is false.
   *  Rendering NativeAd to behave as BannerAd
   */
  @property (nonatomic, readwrite) BOOL enableNativeRendering;
  /**
   * Sets whether or not Video Ads(AppNexus Media Type:4) can serve on this Ad object.
   */
   @property (nonatomic, readwrite) BOOL shouldAllowVideoDemand;
  ```

  > [!NOTE]
  > As per new enhancements, the `RendererId` is set from the Console instead of it passing from the SDK. Hence, the deprecated message to use `shouldAllowNativeDemand`property is shown in the code block.

- By default these values are set to NO, in which case your `ANBannerAdView` will deliver only traditional HTML banner ads. You must explicitly enabled native and video in the app.

- Whereas `loadAd` can be called as soon as possible, the banner (or video) ad cannot be put into a subview until the delegate `adDidReceiveAd:` or `ad:didReceiveNativeAd:` has been called.

- A native ad object is returned as an instance of `ANNativeAdResponse` which can then be handled like any other traditional native response class.  In this case, `ANBannerAdView` effectively plays the same role as ANNativeAdRequest. (See [Show Native Ads on iOS](show-native-ads-on-ios.md) for more on ANNativeAdResponse.)

- By default, the mainImage and iconImage are not loaded. You can manually download these images via the properties mainImageURL and iconImageURL, in the class ANNativeAdResponse.

## Example

Usage of the multi-format ANBannerAdView class is simply a combination of the usage for banner and traditional native classes.

If you want to fetch native or a combination of banner, video, and/or native, you can use the following code example to get started:

```
/**
 This view displays ads from placements that return banner, video and/or native ads.
 Note the implementation requires delaying the point where the ad is displayed,
   because native ads are displayed with ANNativeAdResponse and because the type of ad must be
   tested after load in order to determine the proper means for display.
*/
 @code
    ANBannerAdView  *banner  = nil;
    - (void) loadMultiFormatAd
    {
        CGSize  size      = CGSizeMake(300, 250);  // NOTE  Setting size is necessary only for fetching banner and video ad objects.
                                                   //       This field is ignored when the placement returns a native ad object.
        CGRect  someRect  = CGRectMake(...);
        // Create the banner ad view here, but wait until the delegate fires before displaying.
        //
        ANBannerAdView  *banner  = [ANBannerAdView adViewWithFrame:someRect placementId:@"<YOUR_PLACEMENT_ID>" adSize:size];
        banner.rootViewController = self;
        // Load an ad!
        [banner loadAd];
    }
    // Display all multi-format ads in success method from ANBannerAdViewDelegate.
    //
    - (void) adDidReceiveAd:(id)adObject
    {
        if ([adObject isKindOfClass:[ANNativeAdResponse class]])
        {
            ANNativeAdResponse  *nativeAdResponse  = (ANNativeAdResponse *)ad;
            MyNativeView        *nativeView        = [[MyNativeView alloc] init];
            nativeView.title.text            = nativeAdResponse.title;
            nativeView.text.text             = nativeAdResponse.body;
            nativeView.iconImageView.image   = nativeAdResponse.iconImage;
            nativeView.mainImageView.image   = nativeAdResponse.mainImage;
            [nativeView.callToActionButton setTitle:response.callToAction forState:UIControlStateNormal];
            nativeAdResponse.delegate = self;
            [nativeAdResponse registerViewForTracking: nativeView
                              withRootViewController: self
                                      clickableViews: @[nativeView.callToActionButton, nativeView.mainImageView]
                                               error: nil
              ];
            [self.view addSubview:nativeView];
        } else {
            [self.view addSubview:banner];
        }
    }
 @endcode
 If this view will be displaying placements that include only banner and/or video ads,
   then display can be (optimistically) handled without using ANBannerAdViewDelegate:
 @code
    - (void) loadMultiFormatAdThatDoesNotIncludeNative
    {
        CGSize size = CGSizeMake(300, 250);
        // Create the banner ad view and add it as a subview.
        //
        ANBannerAdView  *banner  = [ANBannerAdView adViewWithFrame:rect placementId:@"13572468" adSize:size];
        banner.rootViewController = self;
        [self.view addSubview:banner];
        // Load an ad!
        // NOTE  Upon loadAd failure, the view impression simply remains blank.
        //
        [banner loadAd];
    }
 @endcode
```

If the ANBannerAdView will be displaying placements that include only banner and/or video ads, then display can be (optimistically) handled without using the adDidReceiveAd : delegate method:

``` 
@implementation MyViewController
 
- (void) loadMultiFormatAdThatDoesNotIncludeNative
{
    CGSize size = CGSizeMake(300, 250);
 
    // Create the banner ad view and add it as a subview.
    //
    ANBannerAdView  *banner  = [ANBannerAdView adViewWithFrame:rect placementId:@"13572468" adSize:size];
    banner.rootViewController = self;
 
    [self.view addSubview:banner];
 
    // Load an ad!
    // NOTE  Upon loadAd failure, the view impression simply remains blank.
    //
    [banner loadAd];
}
 
@end
```

## Related topics:

- [Show Banners on iOS](show-banners-on-ios.md)
- [Native Assembly Renderer on iOS](native-assembly-renderer-on-ios.md)
