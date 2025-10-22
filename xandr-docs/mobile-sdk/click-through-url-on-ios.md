---
title: Click-Through URL on iOS
description: In this article, learn what click-through refers to and the methods used to implement it on iOS with examples.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Click-through URL on iOS

The term click-through refers to the capability of our Mobile SDK to handle what happens when the user clicks on an ad. This document describes how click-through works and provides examples on ways to implement this feature for iOS.

Xandr's Mobile SDK allows you to determine how the value of the `click_url` string in the bid response will be handled when the user clicks on an ad.

There are three possibilities:

- Open the click-through URL in the SDK browser.
- Open the click-through URL in the external device browser.
- Return the URL to the calling environment without opening any browser.

Cases that open a browser will notify the caller via `onAdClicked` in Android and `adWasClicked:withURL:` in iOS.

In the case of a native ad request:

- Two URLs are returned: `click_url` and `click_url_fallback`.

    It is assumed that the caller will handle click-through URL(s) appropriately by displaying their contents to the user. The `click_url_fallback`, if defined, is used only if `click_url` cannot be resolved, for whatever reason, by the browser display system.
- The listener/delegate callback method is: `onAdWasClicked(clickUrl, fallbackURL)` for Android; `adWasClickedWithURL:fallbackURL:` for iOS.

## Mobile SDK structure

- For Banner, Interstitial and Video, ANAdProtocol defines a delegate method, `adWasClicked:withURL:`. 
- For Native, ANNativeAdDelegate defines a delegate method, `adWasClickedWithURL:fallbackURL:`.

## Examples

If you do not want to fetch ClickURL, there is no need to implement the method `adWasClicked:withURL:` that returns `clickURL`.

If you do want to fetch ClickURL, you can use the following code example to get started:

```
// Enable RETURN_URL API
adObject.clickThroughAction = ANClickThroughActionReturnURL;
```

Then add `adWasClicked:withURL:` to get `urlString`.

```
// iOS: ObjC to show a banner ad
 
#import "MyViewController.h"
#import "ANBannerAdView.h"
 
@interface MyViewController ()
@property (nonatomic, strong)  ANBannerAdView      *banner;
@end
@implementation MyViewController
ANBannerAdView  *banner  = nil;
- (void) viewDidLoad
 
{
 
    CGSize  size      = CGSizeMake(300, 250);  // NOTE  Setting size is necessary only for fetching banner and video ad objects.
    //       This field is ignored when the placement returns a native ad object.
    CGRect  someRect  = CGRectMake(...);  
    // Create the banner ad view here, but wait until the delegate fires before displaying.
    //
    ANBannerAdView  *banner  = [ANBannerAdView adViewWithFrame:someRect placementId:@"13572468" adSize:size];
    banner.rootViewController = self;
    banner.clickThroughAction = ANClickThroughActionReturnURL;
    // Load an ad!
    [banner loadAd];
 
}
 
 
// Display all multi-format ads in success method from ANMultiFormatAdDelegate.
//
- (void) adDidReceiveAd:(id)adObject
{
       [self.view addSubview:banner];
}
// optional method
- (void)adWasClicked:(id)ad withURL:(NSString *)urlString{   
   // the caller can handle it appropriately, displaying its content to the user.
}
 
@end
```
