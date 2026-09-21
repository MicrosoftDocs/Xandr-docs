---
title: Get Facebook demand for native on iOS
description: Learn how to use the iOS SDK Facebook adapter to request, render, and track Facebook native ads.
ms.custom: ios-sdk
ms.date: 09/03/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Get Facebook demand for native on iOS

This article describes how to use the iOS SDK Facebook adapter to retrieve and display native ads from Meta Audience Network.

> [!NOTE]
> The Facebook adapter requires iOS 15.0 or later.

## SDK installation

Install the Facebook CSR adapter by using Swift Package Manager. The adapter package includes compatible versions of the iOS SDK and Meta Audience Network SDK as dependencies.

1. Open your project in Xcode.
1. Select the project in the Project navigator, and then select **Package Dependencies**.
1. Select the **+** button to add a package dependency.
1. Enter the following package URL in the search box, and then press **Return**:

   ```text
   https://github.com/appnexus/mobile-sdk-ios-mediation-facebook
   ```

1. Choose the version setting that fits your project. For new projects, select **Up to Next Major Version**. Then select **Add Package**.
1. Select the **ANFacebookCSRAdapter** product and your app target, and then select **Add Package**.
1. Verify that **ANFacebookCSRAdapter** appears under **Package Dependencies**.

## Initialize Facebook's Audience Network SDK

Early in your app lifecycle, initialize Meta Audience Network and pass the result to `ANFBSettings`.

### [Swift](#tab/swift1)

```swift
FBAudienceNetworkAds.initialize(with: nil) { results in
    ANFBSettings.setFBAudienceNetworkInitialize(results.isSuccess) // Store the initialization result
}
```

### [Objective-C](#tab/objectivec1)

```objectivec
[FBAudienceNetworkAds initializeWithSettings:nil
                           completionHandler:^(FBAdInitResults *results) {
    [ANFBSettings setFBAudienceNetworkInitialize:results.isSuccess]; // Store the initialization result
}];
```

---

When initialization succeeds, the adapter can retrieve the Meta bidder token. Otherwise, `getBidderToken` returns `nil`.

Set advertiser tracking according to the user's tracking choice before requesting ads. Replace the example value with the result from your consent flow.

### [Swift](#tab/swift2)

```swift
let userAllowedTracking = true
FBAdSettings.setAdvertiserTrackingEnabled(userAllowedTracking) // Set the user's tracking choice
```

### [Objective-C](#tab/objectivec2)

```objectivec
BOOL userAllowedTracking = YES;
[FBAdSettings setAdvertiserTrackingEnabled:userAllowedTracking]; // Set the user's tracking choice
```

---

## Request and render a native ad

> [!NOTE]
> Retain the request and response while the ad is loading or displayed. Releasing the response unregisters its view.

The following example assumes that your view controller has a native ad container with icon and call-to-action outlets. It registers the call-to-action control as the clickable view.

### [Swift](#tab/swift3)

```swift
final class FacebookNativeAdViewController: UIViewController, ANNativeAdRequestDelegate {
    @IBOutlet private weak var nativeAdView: UIView!
    @IBOutlet private weak var iconImageView: UIImageView!
    @IBOutlet private weak var callToActionButton: UIButton!

    private var nativeAdRequest: ANNativeAdRequest?
    private var nativeAdResponse: ANNativeAdResponse?

    override func viewDidLoad() {
        super.viewDidLoad()

        let request = ANNativeAdRequest()
        request.placementId = "18793423" // Set placement ID
        request.delegate = self // Set the request delegate
        nativeAdRequest = request
        request.loadAd() // Load the ad
    }

    func adRequest(_ request: ANNativeAdRequest, didReceive response: ANNativeAdResponse) {
        nativeAdResponse = response
        iconImageView.image = response.iconImage
        callToActionButton.setTitle(response.callToAction, for: .normal) // Render the call-to-action text

        if let facebookAdapter = response.customElements?[kANNativeCSRObject]
            as? ANAdAdapterCSRNativeBannerFacebook {
            facebookAdapter.registerView(
                forTracking: nativeAdView,
                withRootViewController: self,
                iconImageView: iconImageView,
                clickableViews: [callToActionButton]
            ) // Register the Facebook response
        } else {
            do {
                try response.registerView(
                    forTracking: nativeAdView,
                    withRootViewController: self,
                    clickableViews: [callToActionButton]
                ) // Register other native responses
            } catch {
                print("Unable to register the native ad view: \(error)")
            }
        }
    }

    func adRequest(
        _ request: ANNativeAdRequest,
        didFailToLoadWithError error: Error,
        with adResponseInfo: ANAdResponseInfo?
    ) {
        print("Native ad failed to load: \(error.localizedDescription)")
    }
}
```

### [Objective-C](#tab/objectivec3)

```objectivec
@interface FacebookNativeAdViewController () <ANNativeAdRequestDelegate>
@property (nonatomic, weak) IBOutlet UIView *nativeAdView;
@property (nonatomic, weak) IBOutlet UIImageView *iconImageView;
@property (nonatomic, weak) IBOutlet UIButton *callToActionButton;
@property (nonatomic, strong) ANNativeAdRequest *nativeAdRequest;
@property (nonatomic, strong) ANNativeAdResponse *nativeAdResponse;
@end

@implementation FacebookNativeAdViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.nativeAdRequest = [[ANNativeAdRequest alloc] init];
    self.nativeAdRequest.placementId = @"18793423"; // Set placement ID
    self.nativeAdRequest.delegate = self; // Set the request delegate
    [self.nativeAdRequest loadAd]; // Load the ad
}

- (void)adRequest:(ANNativeAdRequest *)request
        didReceiveResponse:(ANNativeAdResponse *)response {
    self.nativeAdResponse = response;
    self.iconImageView.image = response.iconImage;
    [self.callToActionButton setTitle:response.callToAction forState:UIControlStateNormal]; // Render the call-to-action text

    id csrObject = response.customElements[kANNativeCSRObject];
    if ([csrObject isKindOfClass:[ANAdAdapterCSRNativeBannerFacebook class]]) {
        ANAdAdapterCSRNativeBannerFacebook *facebookAdapter = csrObject;
        [facebookAdapter registerViewForTracking:self.nativeAdView
                          withRootViewController:self
                                   iconImageView:self.iconImageView
                                  clickableViews:@[self.callToActionButton]]; // Register the Facebook response
    } else {
        NSError *registrationError = nil;
        [response registerViewForTracking:self.nativeAdView
                   withRootViewController:self
                           clickableViews:@[self.callToActionButton]
                        error:&registrationError]; // Register other native responses
        if (registrationError != nil) {
            NSLog(@"Unable to register the native ad view: %@", registrationError);
        }
    }
}

- (void)adRequest:(ANNativeAdRequest *)request
        didFailToLoadWithError:(NSError *)error
        withAdResponseInfo:(ANAdResponseInfo *)adResponseInfo {
    NSLog(@"Native ad failed to load: %@", error.localizedDescription);
}

@end
```

---

The Facebook adapter provides registration overloads for these combinations:

| Icon view | Clickable views |
|:---|:---|
| `FBMediaView` | Entire native ad view |
| `FBMediaView` | Selected subviews |
| `UIImageView` | Entire native ad view |
| `UIImageView` | Selected subviews |

## Related

- [iOS SDK Integration Instructions](ios-sdk-integration-instructions.md)
- [Show Banner Native on iOS](show-banner-native-on-ios.md)
- [Show Native Ads on iOS](show-native-ads-on-ios.md)
