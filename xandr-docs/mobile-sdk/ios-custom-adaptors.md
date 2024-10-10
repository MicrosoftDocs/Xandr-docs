---
title: iOS Custom Adaptors
description: In this article, learn about iOS custom adaptors and the code you must write to create your own custom adaptors.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# iOS custom adaptors

Custom adaptors allow our SDK to call out to another SDK installed on the same device, usually for mediation. This document describes the code you must write to create your own custom adaptors.

> [!NOTE]
> The protocols described here are exactly what we used to implement our own mediation adaptors.

## Banners

In order to make mediation calls to another SDK to show banners, you must implement the `ANCustomAdapterBanner` protocol. There is only one method specified by this protocol: `requestBannerAdWithSize`. This method handles instantiating the mediated SDK and using it to make ad requests. It should fire events from the mediated SDK by calling delegate methods like `didLoadBannerAd`. See the examples below for details.

`requestBannerWithAdSize` takes the following arguments:

- `size`: The size of the mediated ad view.
- `rootViewController`: The controller for the mediated ad view.
- `parameterString`: An optional opaque string passed from the server, this can be used to define SDK-specific parameters such as additional targeting information. The encoding of the contents of this string are entirely up to the implementation of the third-party SDK adaptor. In other words, the parameter must be populated with values understood by the third-party SDK’s ad server.
- `idString`: The ID of the ad unit as understood by the third-party SDK’s ad server. It refers to a specific place where an advertiser can show ads in a mobile app. This ID is opaque to our mobile SDK; the ID’s contents and their encoding are up to the implementation of the third-party SDK.
- `targetingParameters`: Any ad targeting parameters such as age, gender, or location that you would like to send to the mediated SDK. You are responsible for sending the mediated SDK parameters that it can understand.

Below is an example adaptor that mediates a fictional “Godzilla” SDK to show banner ads. For more information on the callbacks in this example, see the [Required Callbacks](#required-callbacks) and [Optional Callbacks](#optional-callbacks) sections below.

``` 
@implementation GodzillaBannerAdaptor
@synthesize delegate;
#pragma mark GodzillaCustomAdapterBanner
- (void)requestBannerAdWithSize:(CGSize)size
             rootViewController:(UIViewController *)rootViewController
                serverParameter:(NSString *)parameterString
                       adUnitId:(NSString *)idString
            targetingParameters:(ANTargetingParameters *)targetingParameters
{
    // Here is where you are responsible for (1) instantiating the mediated SDK,
    // (2) building a request object using the elements of `targetingParameters`.
    // Note that you are responsible for ensuring that the targeting
    // parameters can be understood by the mediated SDK.  We also assume that (3)
    // you create a view in the mediated SDK that you can use to make the ad request.
    // Next, we tell the mediated SDK's ad view to request a banner ad from their ad
    // server.  If it works, we call the `didLoadBannerAd` method on our delegate to
    // notify it that we've successfully loaded an ad.
    [self.gzAdView getAdWithRequest:request onCompletion:^(BOOL success, NSError *error) {
        if (success) {
            [self.delegate didLoadBannerAd:self.gzAdView];
        } else {
    // If the mediated SDK was not able to load an ad successfully, we are responsible 
    // for translating the mediated SDK's error codes into something that we can 
    // understand and report to our delegate using `didFailToLoadAd`.
            ANAdResponseCode code = ANAdResponseInternalError;
            switch (error.code) {
                case GodzillaAdUnknownError:
                    code = ANAdResponseInternalError;
                    break;
                case GodzillaAdServerError:
                    code = ANAdResponseNetworkError;
                    break;
                case GodzillaAdUnavailable:
                    code = ANAdResponseUnableToFill;
                    break;
                case GodzillaAdDisabled:
                    code = ANAdResponseInvalidRequest;
                    break;
                default:
                    code = ANAdResponseInternalError;
                    break;
            }
            [self.delegate didFailToLoadAd:code];
        }
    }];
}
#pragma mark GodzillaBannerDelegate
// Implement the required callbacks that allow the mediated SDK to
// communicate with ours.
- (void)GodzillaAdWillPresent:(GodzillaBanner *)bannerAd {
    [self.delegate willPresentAd];
}
- (void)GodzillaAdDidPresent:(GodzillaBanner *)bannerAd {
    [self.delegate didPresentAd];
}
- (void)GodzillaAdWillDismiss:(GodzillaBanner *)bannerAd {
    [self.delegate willCloseAd];
}
- (void)GodzillaAdDidDismiss:(GodzillaBanner *)bannerAd {
    [self.delegate didCloseAd];
}
- (void)GodzillaAdDidInteract:(GodzillaBanner *)bannerAd {
    [self.delegate adWasClicked];
}
- (void)GodzillaAdWillLeaveApplication:(GodzillaBanner *)bannerAd {
    [self.delegate willLeaveApplication];
}
```

## Interstitials

In order to make mediation calls to another SDK to show interstitials, you must implement the `ANCustomAdapterInterstitial` protocol. There are three methods specified by this protocol:

- `requestInterstitialAdWithParameter`: Requests the interstitial ads from the mediated SDK. It takes three arguments:
  - `parameterString`: An optional opaque string passed from the server, this can be used to define SDK-specific parameters such as additional targeting information. The encoding of the contents of this string are entirely up to the implementation of the third-party SDK adaptor. In other words, the parameter must be populated with values understood by the third-party SDK’s ad server.
  - `idString`: The ID of the ad unit as understood by the third-party SDK’s ad server. It refers to a specific place where an advertiser can show ads in a mobile app. This ID is opaque to our mobile SDK; the ID’s contents and their encoding are up to the implementation of the third-party SDK.
  - `targetingParameters`: Any ad targeting parameters such as age, gender, or location that you would like to send to the mediated SDK. You are responsible for sending the mediated SDK parameters that it can understand.
- `isReady`: Whether or not there is an interstitial ad loaded and ready to show to the user.
- `presentFromViewController`: Displays the interstitial ad to the user. Should include a check to `isReady` to see if it can operate. Takes one argument, `viewController`, which is the view controller used to display the interstitial.

In this example code, we mediate a fictional “Godzilla” SDK and have it show an interstitial ad:

``` 
@implementation GodzillaInterstitialAdaptor
@synthesize delegate;
#pragma mark GodzillaCustomAdapterInterstitial
- (void)requestInterstitialAdWithParameter:(NSString *)parameterString
                                  adUnitId:(NSString *)idString
                       targetingParameters:(ANTargetingParameters *)targetingParameters
{
    // Here is where you are responsible for (1) instantiating the mediated SDK,
    // (2) building a request object using the elements of `targetingParameters`.
    // Note that you are responsible for ensuring that the targeting
    // parameters can be understood by the mediated SDK.  We also assume that (3)
    // you create a view in the mediated SDK that you can use to make the ad request.
    // Next, we tell the mediated SDK's ad view to request an interstitial ad from their
    // ad server.  If it works, we call the `didLoadInterstitialAd` method on our 
    // delegate to notify it that we've successfully loaded the ad.
    [GodzillaInterstitial fetchWithRequest:request
                          UUID:idString
                          onCompletion:^(BOOL success, NSError *error) {
                          if (success) {
                            [self.delegate didLoadInterstitialAd:self];
                          }
                          else {
    // If the mediated SDK was not able to load an ad successfully, we are responsible 
    // for translating the mediated SDK's error codes into something that we can 
    // understand and report to our delegate using `didFailToLoadAd`.
    ANAdResponseCode code = ANAdResponseInternalError;
    switch (error.code) {
                    case GodzillaAdUnknownError:
                        code = ANAdResponseInternalError;
                        break;
                    case GodzillaAdServerError:
                        code = ANAdResponseNetworkError;
                        break;
                    case GodzillaAdUnavailable:
                        code = ANAdResponseUnableToFill;
                        break;
                    case GodzillaAdDisabled:
                        code = ANAdResponseInvalidRequest;
                        break;
                    default:
                        code = ANAdResponseInternalError;
                        break;
                }
                [self.delegate didFailToLoadAd:code];
            }
        }];
}
- (void)presentFromViewController:(UIViewController *)viewController {
    // First, we check if the ad is not ready to show.  If true, we
    // fire the `failedToDisplayAd` event and exit.
    if (![self isReady]) {
        [self.delegate failedToDisplayAd];
        return;
    }
    // At this point, we know that an ad is ready.  We tell the
    // mediated interstitial view to show the ad, and if it fails,
    // we fire the `failedToDisplayAd` method.
    [GodzillaInterstitial displayfromViewController:viewController
                          onCompletion:^(BOOL success, NSError *error) {
                          if (!success) {
                              NSLog(@"Godzilla interstitial call to display ad failed");
                              [self.delegate failedToDisplayAd];
                          }
                      }];
}
- (BOOL)isReady {
    // Check whether the mediated SDK has an ad available to show.
    return [GodzillaInterstitial isReady];
}
#pragma mark GodzillaInterstitialDelegate
// Implement the required callbacks that allow the mediated SDK to
// communicate with ours.
- (void)GodzillaAdWillPresent:(GodzillaInterstitial *)interstitialAd {
    [self.delegate willPresentAd];
}
- (void)GodzillaAdDidPresent:(GodzillaInterstitial *)interstitialAd {
    [self.delegate didPresentAd];
}
- (void)GodzillaAdWillDismiss:(GodzillaInterstitial *)interstitialAd {
    [self.delegate willCloseAd];
}
- (void)GodzillaAdDidDismiss:(GodzillaInterstitial *)interstitialAd {
    [self.delegate didCloseAd];
}
- (void)GodzillaAdDidInteract:(GodzillaInterstitial *)interstitialAd {
    [self.delegate adWasClicked];
}
- (void)GodzillaAdWillLeaveApplication:(GodzillaInterstitial *)interstitialAd {
    [self.delegate willLeaveApplication];
}
```

## Required callbacks

The callbacks listed below must be implemented in your custom adaptor. You can see examples of their use in the code samples elsewhere on this page.

To indicate a successful ad request, call one of the following depending on whether the ad is a banner or interstitial:

- `- (void)didLoadBannerAd:(UIView *)view`: The mediated SDK’s ad request completed and returned a banner successfully.
- `- (void)didLoadInterstitialAd:(id<ANCustomAdapterInterstitial>)adaptor`: The mediated SDK’s ad request completed and returned an interstitial. Pass a reference to the current adaptor.

To indicate an unsuccessful ad request whether the ad is a banner or interstitial, call:

- `- (void)didFailToLoadAd:(ANAdResponseCode)errorCode`: The mediated SDK’s ad request failed to return a valid ad.

Furthermore, for interstitial adaptors, a failed attempt to show() should call:

- `- (void)failedToDisplayAd`: The mediated SDK received a call to present an interstitial, but no ad was available or the SDK failed to present.

## Optional callbacks

The callbacks listed below should be implemented in custom adaptors for both banners and interstitials. Note that they are not strictly required.

- `- (void)adWasClicked`: The ad was clicked by the user while being displayed by the mediated SDK.
- `- (void)willPresentAd`: The user interacts with the ad and the mediated SDK is about to present a modal view.
- `- (void)didPresentAd`: The mediated SDK has presented the modal view.
- `- (void)willCloseAd`: The mediated SDK is about to close the modal view.
- `- (void)didCloseAd`: The mediated SDK closes the modal view.
- `- (void)willLeaveApplication`: The mediated SDK will launch an external application.

## Related topics

- [Integrate with iOS](ios-sdk-integration.md)
- [Mediate with iOS](mediate-with-ios.md)
- [ANJAM User Guide](anjam-user-guide.md)
