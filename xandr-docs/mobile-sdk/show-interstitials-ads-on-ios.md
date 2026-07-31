---
title: Show Interstitial Ads on iOS
description: This page gives an overview on the instructions and code samples that are required for showing interstitial ads on iOS.
ms.custom: ios-sdk
ms.date: 07/17/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Show interstitial ads on iOS

This page has instructions and code samples for showing interstitial ads on iOS.

## Overview

Showing interstitial ads requires a bit more work than banners. In addition to implementing `viewDidLoad` as you would for a banner, you must implement the `adDidReceiveAd` delegate method.

When the ad content is received from the ad server, your implementation of the `adDidReceiveAd` callback is fired. In the example below, `displayAdFromViewController` is called right away, but your implementation could wait until it's more convenient for your app to show the interstitial ad. The call to `displayAdFromViewController` needs to happen within approximately 4 minutes of the call to `loadAd` for the impression to be counted.

For more information, see the code sample below.

## Creative media types supported by the Interstitial ad unit

The `ANInterstitialAd` can render creatives of the following media types, which map to the media types Monetize categorizes creatives by (see [Create a Placement — Media types and subtypes](../monetize/create-a-placement.md#media-types-and-subtypes)):

| Media Type | Description |
|:---|:---|
| Banner (`1`) | Static or animated display banner creatives. |
| Interstitial (`3`) | Full-screen creatives, including MRAID, static image, and HTML responsive formats. For creative setup, see:<br><ul><li>[Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)</li><li>[Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)</li><li>[Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)</li></ul> |
| Video (`4`) | VAST video creatives. See [Configure video player options on iOS](configure-video-player-options-on-ios.md) to customize the video player UI. |

> [!IMPORTANT]
> Each media type must be **explicitly enabled** in the placement's **Allowed Media** configuration in Monetize to be eligible to serve. Configure **Allowed Media** in the Monetize UI or via the API to include every media type you want the interstitial to receive — if no compatible media type is allowed on the placement, no ads will serve. For details, see [Create a Placement — Limit the type and size of creatives that can serve](../monetize/create-a-placement.md#step-3-limit-the-type-and-size-of-creatives-that-can-serve).

## Basic integration

The code samples below show how to request an interstitial ad using a placement ID.

### [Swift](#tab/swift1)

```
// iOS: Swift code to show an interstitial ad
// Import ANInterstitialAd.h in the bridging header.
class ViewController: UIViewController, ANInterstitialAdDelegate {

    let interstitial = ANInterstitialAd(placementId: "1326299")

    override func viewDidLoad() {
        super.viewDidLoad()
        // Set ourselves as the delegate so we can respond to the required adDidReceiveAd
        // message of the ANAdDelegate protocol.
        interstitial.delegate = self
        // Load an ad!
        interstitial.loadAd()
    }

    // ANInterstitialAdDelegate
    func adDidReceiveAd(_ ad: Any) {
        interstitial.display(from: self)
    }

    func ad(_ ad: Any, requestFailedWithError error: Error) {
        NSLog("The ad request failed: \(error.localizedDescription)")
    }

    func adFailed(toDisplay ad: ANInterstitialAd) {
        NSLog("Uh oh, the ad failed to display!")
    }
}
```

### [Objective-C](#tab/objectivec1)

```
// iOS: Objective-C code to show an interstitial ad
#import "ViewController.h"
#import "ANInterstitialAd.h"

@interface ViewController () <ANInterstitialAdDelegate>
@property (nonatomic, strong) ANInterstitialAd *interstitial;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    self.interstitial = [[ANInterstitialAd alloc] initWithPlacementId:@"1326299"];
    // Set ourselves as the delegate so we can respond to the required adDidReceiveAd
    // message of the ANAdDelegate protocol.
    self.interstitial.delegate = self;
    // Load an ad!
    [self.interstitial loadAd];
}

- (void)adDidReceiveAd:(id<ANAdProtocol>)ad {
    [self.interstitial displayAdFromViewController:self];
}

- (void)adFailedToDisplay:(ANInterstitialAd *)ad {
    NSLog(@"Uh oh, the ad failed to display!");
}

@end
```

---

## Advanced settings

The following sections describe optional configuration and callbacks you can use to customize how your interstitial ad requests and displays creatives.

### Initialize with member ID and inventory code

As an alternative to a placement ID, you can request an interstitial ad using a member ID and an inventory code by initializing `ANInterstitialAd` with `-initWithMemberId:inventoryCode:`.

#### [Swift](#tab/swift2)

```
// iOS: Swift code to request an interstitial using member ID and inventory code
let interstitial = ANInterstitialAd(memberId: 123, inventoryCode: "your-inventory-code")
interstitial.delegate = self
interstitial.loadAd()
```

#### [Objective-C](#tab/objectivec2)

```
// iOS: Objective-C code to request an interstitial using member ID and inventory code
self.interstitial = [[ANInterstitialAd alloc] initWithMemberId:123 inventoryCode:@"your-inventory-code"];
self.interstitial.delegate = self;
[self.interstitial loadAd];
```

---

### Using custom interstitial sizes

By default, if you don't specify an ad size, the SDK will fetch ads in any of the sizes below that are less than or equal to the size of the device's screen.

- 1x1 (always sent)
- The detected size of the screen (always sent)
- 300x250
- 320x480
- 900x500
- 1024x1024

If you want to show interstitial ads in sizes other than the defaults, set the `allowedAdSizes` property on the `ANInterstitialAd`. Note that the detected size of the screen will still be passed as the main size. The sizes set using the `allowedAdSizes` property will be passed in as `promo_sizes` on the placement and will replace the defaults of 300x250 and 320x480.

#### [Swift](#tab/swift3)

```
// iOS: Swift code to show interstitial ads in sizes other than the defaults
let interstitial = ANInterstitialAd(placementId: "1326299")
interstitial.allowedAdSizes = NSMutableSet(array: [
    NSValue(cgSize: CGSize(width: 320, height: 480)),
    NSValue(cgSize: CGSize(width: 768, height: 1024))
])
```

#### [Objective-C](#tab/objectivec3)

```
// iOS: Objective-C code to show interstitial ads in sizes other than the defaults
self.interstitial = [[ANInterstitialAd alloc] initWithPlacementId:@"1326299"];
self.interstitial.allowedAdSizes = [NSMutableSet setWithArray:@[
    [NSValue valueWithCGSize:CGSizeMake(320, 480)],
    [NSValue valueWithCGSize:CGSizeMake(768, 1024)]
]];
```

---

### Set the close button delay

For **Banner** and **Interstitial** creatives, the close button appears on the interstitial ad ten seconds after it is displayed by default. To change the delay, set the `closeDelay` property on the `ANInterstitialAd`, passing the delay in **seconds**. The maximum is 10 seconds; values above that are ignored. Setting `0` allows the close button to appear immediately. This setting has no effect on **Video** creatives, which use the video's own skip/close controls.

#### [Swift](#tab/swift4)

```
// Show the close button after 5 seconds instead of the default 10.
self.interstitial.closeDelay = 5
```

#### [Objective-C](#tab/objectivec4)

```
// Show the close button after 5 seconds instead of the default 10.
self.interstitial.closeDelay = 5;
```

---

### Auto-close an interstitial

To auto-close a **Banner** or **Interstitial** creative after a specific timeout, do not call `displayAdFromViewController`. Instead, call `displayAdFromViewController:autoDismissDelay:` and specify how many seconds the ad should be displayed before it is closed. This setting has no effect on **Video** creatives, which run until they complete or are skipped.

#### [Swift](#tab/swift5)

```
// Show an interstitial ad, wait for 10 seconds, then auto-close it.
self.interstitial.display(from: self, autoDismissDelay: 10)
```

#### [Objective-C](#tab/objectivec5)

```
// Show an interstitial ad, wait for 10 seconds, then auto-close it.
[self.interstitial displayAdFromViewController:self autoDismissDelay:10];
```

---

### Customize video player options

To customize the video player UI — skip controls, mute, click-through text, and other playback controls — see [Configure video player options on iOS](configure-video-player-options-on-ios.md).

---

### Receive video completion callbacks

Assign a `videoDelegate` conforming to `ANInterstitialAdVideoDelegate` on your `ANInterstitialAd` to be notified how a **Video** interstitial ad ended via `-adDidCompleteVideo:withState:` — `ANInterstitialVideoCompletionStateCompleted`, `Skipped`, or `Error`. The callback fires only for RTB interstitial video ads (not mediated or CSR) and runs alongside the existing close callbacks.

#### [Swift](#tab/swift6)

```
// iOS: Swift code to receive interstitial video completion callbacks
// Import ANInterstitialAd.h in the bridging header.
class ViewController: UIViewController, ANInterstitialAdDelegate, ANInterstitialAdVideoDelegate {

    let interstitial = ANInterstitialAd(placementId: "1326299") // Create the interstitial ad

    override func viewDidLoad() {
        super.viewDidLoad()
        interstitial.delegate = self // Set the standard ad delegate
        interstitial.videoDelegate = self // Set the video completion delegate
        interstitial.loadAd() // Load the ad
    }

    func adDidReceiveAd(_ ad: Any) {
        interstitial.display(from: self)
    }

    // ANInterstitialAdVideoDelegate
    func adDidCompleteVideo(_ ad: ANInterstitialAd,
                            with state: ANInterstitialVideoCompletionState) {
        switch state {
        case .completed:
            // The video played to its natural end
            break
        case .skipped:
            // The user skipped the video before it ended
            break
        case .error:
            // Playback ended because of an error or timeout
            break
        @unknown default:
            break
        }
    }
}
```

#### [Objective-C](#tab/objectivec6)

```
// iOS: Objective-C code to receive interstitial video completion callbacks
#import "ViewController.h"
#import "ANInterstitialAd.h"

@interface ViewController () <ANInterstitialAdDelegate, ANInterstitialAdVideoDelegate>
@property (nonatomic, strong) ANInterstitialAd *interstitial;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    self.interstitial = [[ANInterstitialAd alloc] initWithPlacementId:@"1326299"]; // Create the interstitial ad
    self.interstitial.delegate = self; // Set the standard ad delegate
    self.interstitial.videoDelegate = self; // Set the video completion delegate
    [self.interstitial loadAd]; // Load the ad
}

- (void)adDidReceiveAd:(id<ANAdProtocol>)ad {
    [self.interstitial displayAdFromViewController:self];
}

// ANInterstitialAdVideoDelegate
- (void)adDidCompleteVideo:(nonnull ANInterstitialAd *)ad
                 withState:(ANInterstitialVideoCompletionState)state {
    switch (state) {
        case ANInterstitialVideoCompletionStateCompleted:
            // The video played to its natural end
            break;
        case ANInterstitialVideoCompletionStateSkipped:
            // The user skipped the video before it ended
            break;
        case ANInterstitialVideoCompletionStateError:
            // Playback ended because of an error or timeout
            break;
    }
}

@end
```

---
