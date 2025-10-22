---
title: Receive Ad View Status Events on iOS
description: Learn how to receive ad view status events from the SDK using the ANAdDelegate protocol.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Receive ad view status events on iOS

This page has instructions on how to receive ad view status events from our SDK. You can use these events to determine from your app when an ad has been clicked, whether it's in an expanded state, and more.

In order to receive status events during the life cycle of the ad view, you must implement the `ANAdDelegate` protocol. Its methods are:

- `(void)adDidReceiveAd:(id)ad;`: Sent when Banner or Video ad content has been successfully retrieved from the server.
- `(void)ad:(id)loadInstance didReceiveNativeAd:(id)nativeAdResponse;`: Sent when Native ad content has been successfully retrieved from the server.
- `(void)ad:(id)ad requestFailedWithError:(NSError *)error`: Sent when the ad request to the server has failed.
- `(void)adWasClicked:(id)ad`: Sent when the ad is clicked by the user.
- `(void)adWasClicked:(id)ad withURL:(NSString *)urlString`: Sent when the ad is clicked by the user and allows you to determine how the value of the `click_url` string in the bid response will be handled.
- `(void)adWillClose:(id)ad`: Sent when the ad view is about to close.
- `(void)adDidClose:(id)ad`: Sent when the ad view has finished closing.
- `(void)adWillPresent:(id)ad`: Sent when the ad is clicked, and the SDK is about to open inside the in-SDK browser (a WebView). If you would prefer that ad clicks open the native browser instead, set `opensInNativeBrowser` to `true`.
- `(void)adDidPresent:(id)ad`: Sent when the ad has finished being viewed using the in-SDK browser.
- `(void)adWillLeaveApplication:(id)ad`: Sent when the ad is about to leave the app; this can happen if you have `opensInNativeBrowser` set to `true`, for example.
- `(void)adDidLogImpression:(nonnull id)ad`: Sent when an ad impression is observed during a banner or interstitial ad event.

The example below implements this protocol:

```
#import "FunViewController.h"
#import "ANInterstitialAd.h"
@interface FunViewController () <ANInterstitialAdDelegate>
@property (nonatomic, strong)ANInterstitialAd *inter;
@end
@implementation FunViewController : UIViewController
- (void)viewDidLoad {
    self.inter = [[ANInterstitialAd alloc] initWithPlacementId:@"1326299"];
    
    // set ourselves as the delegate so we can respond to the required adDidReceiveAd
    // message of the `ANAdDelegate protocol' (see implementation below)
    self.inter.delegate = self;
    
    // Load an ad!
    [self.inter loadAd];
}
- (void)adDidReceiveAd:(id)ad {
    [self.inter displayAdFromViewController:self];
}    
- (void)adDidLogImpression:(id)ad {
    NSLog(@"This ad is log the impression.");
} 
- (void)adFailedToDisplay:(ANInterstitialAd *)ad {
    NSLog(@"Uh oh, the ad failed to display!");
}
- (void)adWasClicked:(ANInterstitialAd *)ad {
    NSLog(@"Sweet, the ad was clicked!");
}
- (void)adWillClose:(ANInterstitialAd *)ad {
    NSLog(@"This ad is about to close.");
}
- (void)adDidClose:(ANInterstitialAd *)ad {
    NSLog(@"The ad just closed.");
}
- (void)adWillPresent:(ANInterstitialAd *)ad {
    NSLog(@"About to open an in-SDK WebView.");
}
- (void)adDidPresent:(ANInterstitialAd *)ad {
    NSLog(@"User finished viewing ad in in-SDK WebView.");
}
- (void)adWillLeaveApplication:(ANInterstitialAd *)ad {
    NSLog(@"About to leave this app (maybe opening an external browser?).");
}
@end
```
