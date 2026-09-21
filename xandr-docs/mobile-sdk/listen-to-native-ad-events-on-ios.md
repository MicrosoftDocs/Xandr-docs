---
title: Listen to native ad events on iOS
description: Learn how to use ANNativeAdDelegate to receive impression, click, navigation, presentation, and expiration events on iOS.
ms.custom: ios-sdk
ms.date: 09/17/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Listen to native ad events on iOS

This article describes how to use `ANNativeAdDelegate` to receive events for native ads.

## Overview

`ANNativeAdDelegate` notifies your app about native ad impressions, clicks, navigation away from the app, presentation changes, and expiration. After rendering the assets from `ANNativeAdResponse`, set its delegate and register the native ad view for tracking. For registration options, see [Show native ads on iOS](show-native-ads-on-ios.md#register-tracking).

## Properties

Use the following property on `ANNativeAdResponse`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `delegate` | `id<ANNativeAdDelegate>` | readwrite, weak | Assigns the delegate that receives impression, click, presentation, navigation, and expiration events for the registered native ad view. |

## Methods

Use the following methods on `ANNativeAdDelegate`:

| Method | Description |
|:---|:---|
| `adWasClicked:` | Called after a native ad click when `clickThroughAction` is `ANClickThroughActionOpenSDKBrowser` or `ANClickThroughActionOpenDeviceBrowser`. The SDK opens the click-through destination. |
| `adWasClicked:withURL:fallbackURL:` | Called after a native ad click when `clickThroughAction` is `ANClickThroughActionReturnURL`. Your app is responsible for handling the returned click-through URL or fallback URL. |
| `adWillPresent:` | Called before the SDK presents the click-through destination in the in-app browser. |
| `adDidPresent:` | Called after the in-app browser is presented and takes control from your app. |
| `adWillClose:` | Called before the in-app browser closes and returns control to your app. |
| `adDidClose:` | Called after the in-app browser closes and control returns to your app. |
| `adWillLeaveApplication:` | Called before the click-through action moves the user from your app to another app, such as the device browser. |
| `adDidLogImpression:` | Called after the SDK records the native ad impression and fires its impression trackers. |
| `adWillExpire:` | Called shortly before the native ad response expires, allowing your app to prepare a replacement ad. |
| `adDidExpire:` | Called when the native ad response expires and can no longer be registered for tracking. |

## Example

### [Swift](#tab/swift1)

```swift
final class NativeAdViewController: UIViewController, ANNativeAdRequestDelegate, ANNativeAdDelegate {
    @IBOutlet private weak var nativeAdView: UIView!
    @IBOutlet private weak var titleLabel: UILabel!

    private var nativeAdRequest: ANNativeAdRequest?
    private var nativeAdResponse: ANNativeAdResponse?

    override func viewDidLoad() {
        super.viewDidLoad()

        let request = ANNativeAdRequest()
        request.placementId = "123456" // Set placement ID
        request.delegate = self // Set the request delegate
        nativeAdRequest = request
        request.loadAd() // Load the ad
    }

    func adRequest(_ request: ANNativeAdRequest, didReceive response: ANNativeAdResponse) {
        nativeAdResponse = response
        titleLabel.text = response.title // Render the native ad title
        response.delegate = self // Set the native ad event delegate

        do {
            try response.registerView(
                forTracking: nativeAdView,
                withRootViewController: self
            ) // Register tracking and event callbacks
        } catch {
            print("Unable to register the native ad view: \(error)")
        }
    }

    func adRequest(
        _ request: ANNativeAdRequest,
        didFailToLoadWithError error: Error,
        with adResponseInfo: ANAdResponseInfo?
    ) {
        print("Native ad failed to load: \(error.localizedDescription)")
    }

    func adWasClicked(_ response: Any) {
        print("Native ad clicked")
    }

    func adWasClicked(_ response: Any, withURL clickURL: String, fallbackURL: String) {
        print("Native ad clicked: \(clickURL)")
    }

    func adWillPresent(_ response: Any) {
        print("In-app browser will open")
    }

    func adDidPresent(_ response: Any) {
        print("In-app browser opened")
    }

    func adWillClose(_ response: Any) {
        print("In-app browser will close")
    }

    func adDidClose(_ response: Any) {
        print("In-app browser closed")
    }

    func adWillLeaveApplication(_ response: Any) {
        print("Native ad will leave the app")
    }

    func adDidLogImpression(_ response: Any) {
        print("Native ad impression recorded")
    }

    func adWillExpire(_ response: Any) {
        print("Native ad is about to expire")
    }

    func adDidExpire(_ response: Any) {
        print("Native ad expired")
    }
}
```

### [Objective-C](#tab/objectivec1)

```objectivec
@interface NativeAdViewController () <ANNativeAdRequestDelegate, ANNativeAdDelegate>
@property (nonatomic, weak) IBOutlet UIView *nativeAdView;
@property (nonatomic, weak) IBOutlet UILabel *titleLabel;
@property (nonatomic, strong) ANNativeAdRequest *nativeAdRequest;
@property (nonatomic, strong) ANNativeAdResponse *nativeAdResponse;
@end

@implementation NativeAdViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.nativeAdRequest = [[ANNativeAdRequest alloc] init];
    self.nativeAdRequest.placementId = @"123456"; // Set placement ID
    self.nativeAdRequest.delegate = self; // Set the request delegate
    [self.nativeAdRequest loadAd]; // Load the ad
}

- (void)adRequest:(ANNativeAdRequest *)request
        didReceiveResponse:(ANNativeAdResponse *)response {
    self.nativeAdResponse = response;
    self.titleLabel.text = response.title; // Render the native ad title
    response.delegate = self; // Set the native ad event delegate

    NSError *registrationError = nil;
    BOOL registered = [response registerViewForTracking:self.nativeAdView
                                 withRootViewController:self
                                                  error:&registrationError]; // Register tracking and event callbacks
    if (!registered) {
        NSLog(@"Unable to register the native ad view: %@", registrationError);
    }
}

- (void)adRequest:(ANNativeAdRequest *)request
        didFailToLoadWithError:(NSError *)error
        withAdResponseInfo:(ANAdResponseInfo *)adResponseInfo {
    NSLog(@"Native ad failed to load: %@", error.localizedDescription);
}

- (void)adWasClicked:(id)response {
    NSLog(@"Native ad clicked");
}

- (void)adWasClicked:(id)response
             withURL:(NSString *)clickURL
         fallbackURL:(NSString *)fallbackURL {
    NSLog(@"Native ad clicked: %@", clickURL);
}

- (void)adWillPresent:(id)response {
    NSLog(@"In-app browser will open");
}

- (void)adDidPresent:(id)response {
    NSLog(@"In-app browser opened");
}

- (void)adWillClose:(id)response {
    NSLog(@"In-app browser will close");
}

- (void)adDidClose:(id)response {
    NSLog(@"In-app browser closed");
}

- (void)adWillLeaveApplication:(id)response {
    NSLog(@"Native ad will leave the app");
}

- (void)adDidLogImpression:(id)response {
    NSLog(@"Native ad impression recorded");
}

- (void)adWillExpire:(id)response {
    NSLog(@"Native ad is about to expire");
}

- (void)adDidExpire:(id)response {
    NSLog(@"Native ad expired");
}

@end
```

---

## Related

- [Show native ads on iOS](show-native-ads-on-ios.md)
- [Listener for adWillExpire on iOS](listener-for-adabouttoexpire-on-ios.md)
- [Viewability measurement on iOS](viewability-measurement-on-ios.md)
