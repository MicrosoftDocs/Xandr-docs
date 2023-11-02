---
title : Show Interstitials Ads on iOS
description : This page has instructions and code samples for showing interstitial ads on iOS.
ms.custom : ios-sdk
---


# Show Interstitials Ads on iOS

This page has instructions and code samples for showing interstitial ads
on iOS.

## iOS - interstitial overview

Showing interstitial ads is a little more work. In addition to
implementing `viewDidLoad` as we did in the banner example, we must
implement the `adDidReceiveAd` delegate method. See the example below
for details.

Furthermore, actually showing interstitial ads to users is a two-step
process:

1. Call `loadAd` to fetch the ad contents from our server and cache
    them locally. Note that any ad content is rendered in a WebView at
    the time it is fetched from the ad server and cached. This means
    that any third-party tracking pixels that are part of the ad content
    will be fired at the time of the call to `loadAd`, not when the call
    to `displayAdFromViewController` is made at a later time.
1. When the ad content is actually received from the ad server, your
    implementation of the `adDidReceiveAd` callback is fired. In the
    example below, we call `displayAdFromViewController` right away, but
    your implementation could wait until it's more convenient for your
    app to show the interstitial ad. Note that the call
    to `displayAdFromViewController` needs to happen within
    approximately 4 minutes of the call to `loadAd` in order for the
    impression to be counted by Xandr. (For the
    exact timing in milliseconds, see the value
    of `kANInterstitialAdTimeout` in the source code.)

  > [!NOTE]
  > The close button appears after ten seconds by default. You can set the delay using `ANInterstitialAd.setCloseDelay`.

For more information, see the code sample below.

## iOS - interstitial code sample

> [!NOTE]
> The interstitial code sample below shows how to request ads using the placement ID. Beginning with version RC2.8, you can initialize interstitials using a combination of member ID and inventory code instead (placement ID is still supported). Here is the method:

``` 
// iOS: ObjC code that uses inventory code and member ID instead of placement ID (optional)
-(instancetype)initWithMemberId:(NSInteger)memberId inventoryCode:(NSString *)inventoryCode;
```

**Objective C**

``` 
// iOS: ObjC code to show an interstitial ad
#import "ViewController.h"
#import "ANInterstitialAd.h"
@interface ViewController () <ANInterstitialAdDelegate>
@property (nonatomic, strong)ANInterstitialAd *inter;
@end
@implementation ViewController : UIViewController
- (void)viewDidLoad {
    self.inter = [[ANInterstitialAd alloc] initWithPlacementId:@"1326299"];
    
    // set ourselves as the delegate so we can respond to the required adDidReceiveAd
    // message of the `ANAdDelegate protocol' (see implementation below)
    self.inter.delegate = self;
    
    // Load an ad!
    [self.inter loadAd];
}
- (void)adDidReceiveAd:(id<ANAdProtocol>)ad {
    [self.inter displayAdFromViewController:self];
}
- (void)adFailedToDisplay:(ANInterstitialAd *)ad {
    NSLog(@"Uh oh, the ad failed to display!");
}
@end
```

**Swift:**

``` 

// iOS: Swift code to show an interstitial ad
// Import ANInterstitialAd.h in the bridging header.
class ViewController: UIViewController, ANInterstitialAdDelegate {
  let inter = ANInterstitialAd.init(placementId: "1326299")
  override func viewDidLoad() {
    super.viewDidLoad()
    // Set ourselves as the delegate so we can respond to the required adDidReceiveAd
    // message of the ANAdDelegate protocol (see implementation below).
    inter.delegate = self
    // Load an ad!
    inter.loadAd()
  }
  // ANInterstitialAdDelegate
  extension InterstitialViewController: ANInterstitialAdDelegate {
    // - (void)adDidReceiveAd:(nonnull id)ad;
    func adDidReceiveAd(_ ad: Any) {
      appNexusIntersitial?.display(from: self)
    }
    // - (void)ad:(nonnull id)loadInstance didReceiveNativeAd:(nonnull id)responseInstance;
    func ad(_ ad: Any, requestFailedWithError error: Error) {
    }
  }
}
```

## Using custom interstitial sizes

By default, if you don't specify an ad size, the SDK will fetch ads in
any of the sizes below that are less than or equal to the size of the
device's screen.

- 1x1 (always sent)
- The detected size of the screen (always sent)
- 300x250
- 320x480
- 900x500
- 1024x1024

If you want to show interstitial ads in sizes other than the defaults,
set the `allowedAdSizes` property on the `ANInterstitialAd`. Note that
the detected size of the screen will still be passed as the main size.
The sizes set using the `allowedAdSizes` property will be passed in
as `promo_sizes` on the placement and will replace the defaults of
300x250 and 320x480.

## Auto-Close an interstitial

If you want to auto-close an interstitial ad after a specific timeout
period, do not call `displayAdFromViewController` as described in the
above sections. Instead,
call `displayAdFromViewController:(UIViewController *)controller autoDismissDelay:(NSTimeInterval)delay`.
The following examples sets the number of seconds the interstitial is
displayed before it is closed to 10 seconds.

``` 
// This will show an interstitial ad, wait for 10 seconds, then auto close it.
 [self.interstitial displayAdFromViewController:self autoDismissDelay:10];
```
