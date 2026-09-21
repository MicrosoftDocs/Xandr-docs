---
title: Show native ads on iOS
description: Learn how to request, render, track, and release native ads in an iOS app.
ms.custom: ios-sdk
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Show native ads on iOS

This article describes how to use `ANNativeAdRequest` and `ANNativeAdResponse` to show native ads in your iOS app.

## Overview

Native ads let you render ad assets in views that match your app's design. To support this workflow, the iOS SDK exposes the following classes, protocols, and methods:

- `ANNativeAdRequest` loads an ad for a placement, and `ANNativeAdRequestDelegate` receives the result.
- `ANNativeAdResponse` provides the native assets returned by a successful request.
- `ANNativeAdResponse` provides methods for registering the rendered view for impression and click tracking, while the optional `ANNativeAdDelegate` receives impression and click events.

In the standard SDK flow, create and load a request, render the assets from the response, and then register the view for tracking.

- Keep references to the request, response, and rendered view while the ad is displayed.
- Release the request, response, and rendered view when they are no longer needed.

To customize the assets returned in a native ad response, see [Request specific assets with OpenRTB Native](#request-specific-assets-with-openrtb-native) or [Request specific assets with Native Assembly](#request-specific-assets-with-native-assembly).

> [!NOTE]
> For information about native impression counting, see [Impression counting methods](impression-counting-methods.md).

## Request a native ad

Use the following properties on `ANNativeAdRequest`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `placementId` | `NSString *` | readwrite, copy | Placement ID used for the native ad request. |
| `delegate` | `id<ANNativeAdRequestDelegate>` | readwrite, weak | Delegate that receives the request result. |

## Access standard native response data

To use the standard native flow, load an `ANNativeAdRequest` without setting `openRTBAssets`. `ANNativeAdResponse` contains the assets and related metadata available for the selected ad.

Use the following properties on `ANNativeAdResponse`:

| Property | Type | Attribute | Default | Description |
|:---|:---|:---|:---|:---|
| `title` | `NSString *` | readonly, strong | `nil` | Native ad title. |
| `sponsoredBy` | `NSString *` | readonly, strong | `nil` | Name of the advertiser or sponsor. |
| `body` | `NSString *` | readonly, strong | `nil` | Native ad body text. |
| `additionalDescription` | `NSString *` | readonly, strong | `nil` | Additional ad description. |
| `callToAction` | `NSString *` | readonly, strong | `nil` | Call-to-action text. |
| `mainImageURL` | `NSURL *` | readonly, strong | `nil` | URL for loading the main image. |
| `mainImageSize` | `CGSize` | readonly, assign | `CGSizeZero` | Main image dimensions. |
| `mainImage` | `UIImage *` | readonly, strong | `nil` | Preloaded main image. See [Configure image loading](#configure-image-loading). |
| `iconImageURL` | `NSURL *` | readonly, strong | `nil` | URL for loading the icon image. |
| `iconImageSize` | `CGSize` | readonly, assign | `CGSizeZero` | Icon image dimensions. |
| `iconImage` | `UIImage *` | readonly, strong | `nil` | Preloaded icon image. See [Configure image loading](#configure-image-loading). |
| `rating` | `ANNativeAdStarRating *` | readonly, strong | `nil` | Star rating for the advertised product or app. |
| `privacyLink` | `NSString *` | readwrite, strong | `nil` | Privacy information URL supplied for the ad, when available. |

## Register tracking

Use the following APIs on `ANNativeAdResponse` after rendering the native assets:

| API | Description |
|:---|:---|
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>error:</code> | Registers the rendered view for impression tracking and makes the entire view clickable. |
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>clickableViews:<wbr>error:</code> | Registers the rendered view for impression tracking and makes the listed views clickable. |
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>openMeasurementFriendlyObstructions:<wbr>error:</code> | Registers the rendered view for impression tracking, makes the entire view clickable, and identifies friendly obstructions. |
| <code>registerViewForTracking:<wbr>withRootViewController:<wbr>clickableViews:<wbr>openMeasurementFriendlyObstructions:<wbr>error:</code> | Registers tracking with specific clickable views and friendly obstructions. |
| `delegate` | Optional object that implements `ANNativeAdDelegate` to receive impression, click, presentation, and expiration events. |

For information about registering friendly obstructions, see [Viewability measurement on iOS](viewability-measurement-on-ios.md).

## Example

### [Swift](#tab/swift1)

```swift
final class NativeAdViewController: UIViewController, ANNativeAdRequestDelegate {
    @IBOutlet private weak var nativeAdView: UIView!
    @IBOutlet private weak var titleLabel: UILabel!
    @IBOutlet private weak var sponsoredByLabel: UILabel!
    @IBOutlet private weak var bodyLabel: UILabel!
    @IBOutlet private weak var ratingLabel: UILabel!
    @IBOutlet private weak var callToActionButton: UIButton!

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
        let mainImageURL = response.mainImageURL // Pass the main image URL to your app's image-loading implementation
        let iconImageURL = response.iconImageURL // Pass the icon image URL to your app's image-loading implementation
        titleLabel.text = response.title // Render the title
        sponsoredByLabel.text = response.sponsoredBy // Render the sponsor name
        bodyLabel.text = response.body // Render the body text
        if let rating = response.rating {
            ratingLabel.text = "\(rating.value)/\(rating.scale)" // Render the rating
        }
        let privacyURL = response.privacyLink // Get the privacy URL
        callToActionButton.setTitle(response.callToAction, for: .normal) // Render the call-to-action text
        nativeAdView.isHidden = false

        do {
            try response.registerView(
                forTracking: nativeAdView,
                withRootViewController: self,
                clickableViews: [callToActionButton]
            ) // Track impressions and CTA clicks
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
}
```

### [Objective-C](#tab/objectivec1)

```objectivec
@interface NativeAdViewController () <ANNativeAdRequestDelegate>
@property (nonatomic, weak) IBOutlet UIView *nativeAdView;
@property (nonatomic, weak) IBOutlet UILabel *titleLabel;
@property (nonatomic, weak) IBOutlet UILabel *sponsoredByLabel;
@property (nonatomic, weak) IBOutlet UILabel *bodyLabel;
@property (nonatomic, weak) IBOutlet UILabel *ratingLabel;
@property (nonatomic, weak) IBOutlet UIButton *callToActionButton;
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
    NSURL *mainImageURL = response.mainImageURL; // Pass the main image URL to your app's image-loading implementation
    NSURL *iconImageURL = response.iconImageURL; // Pass the icon image URL to your app's image-loading implementation
    self.titleLabel.text = response.title; // Render the title
    self.sponsoredByLabel.text = response.sponsoredBy; // Render the sponsor name
    self.bodyLabel.text = response.body; // Render the body text
    if (response.rating) {
        self.ratingLabel.text = [NSString stringWithFormat:@"%g/%ld",
            response.rating.value, (long)response.rating.scale]; // Render the rating
    }
    NSString *privacyURL = response.privacyLink; // Get the privacy URL
    [self.callToActionButton setTitle:response.callToAction forState:UIControlStateNormal]; // Render the call-to-action text
    self.nativeAdView.hidden = NO;

    NSError *registrationError = nil;
    BOOL registered = [response registerViewForTracking:self.nativeAdView
                                 withRootViewController:self
                                        clickableViews:@[self.callToActionButton]
                                                 error:&registrationError]; // Track impressions and CTA clicks
    if (!registered) {
        NSLog(@"Unable to register the native ad view: %@", registrationError);
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

## Extended Native Ad Assets

In addition to the standard native ad flow, your app can optionally access extended assets through OpenRTB Native or Native Assembly. If you set `openRTBAssets`, the OpenRTB Native request takes precedence over the Native Assembly configuration associated with the placement.

For either workflow, your app can parse the exposed asset object directly instead of using the normalized asset properties on `ANNativeAdResponse`. Keep the `ANNativeAdResponse` instance to register the rendered view for tracking and receive native ad events.

| Asset | [OpenRTB Native](#request-specific-assets-with-openrtb-native) access | [Native Assembly](#request-specific-assets-with-native-assembly) access | Description |
|:---|:---|:---|:---|
| VAST video | `vastXML` | `vastXML` | Returns the VAST video markup. |
| Likes | `openRTBNative` by request ID | `customElements` with `likes` | Returns the number of likes. |
| Downloads | `openRTBNative` by request ID | `customElements` with `downloads` | Returns the number of downloads. |
| Price | `openRTBNative` by request ID | `customElements` with `price` | Returns the product price. |
| Sale price | `openRTBNative` by request ID | `customElements` with `saleprice` | Returns the discounted product price. |
| Phone | `openRTBNative` by request ID | `customElements` with `phone` | Returns the advertiser phone number. |
| Address | `openRTBNative` by request ID | `customElements` with `address` | Returns the advertiser address. |
| Display URL | `openRTBNative` by request ID | `customElements` with `displayurl` | Returns the advertiser-facing display URL. |
| Click URL | `openRTBNative` with `link.url` | `customElements` with `link.url` | Returns the primary click destination. |
| Click fallback URL | `openRTBNative` with `link.fallback` | `customElements` with `link.fallback_url` | Returns the fallback click destination. |
| Custom extension | `openRTBNative` with `ext` | Not applicable | Returns response-level extension data defined by the demand partner. |

### Request specific assets with OpenRTB Native

> [!NOTE]
> OpenRTB Native isn't available for all members. Contact your account representative or Microsoft Advertising Support to confirm availability. Don't include `eventtrackers` in `openRTBAssets`; the iOS SDK adds the supported event trackers.

**`ANNativeAdRequest`:** Use `openRTBAssets` to describe the assets your app needs according to OpenRTB Native 1.2. You can specify image sizes, text lengths, video, and custom assets. Assign each asset an `id` so you can match it to the value returned in the response. You can also add custom data through `ext` using keys and values agreed with your demand partner. For available fields and values, see the [IAB OpenRTB Native Ads Specification 1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf). Set `openRTBAssets` before calling `loadAd()`.

Use the following property on `ANNativeAdRequest`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `openRTBAssets` | `NSDictionary<NSString *, id> *` | readwrite, strong | Sets the OpenRTB Native 1.2 request object that defines the requested assets and constraints. The property exposes `setOpenRTBAssets:` in Objective-C. |

**`ANNativeAdResponse`:** Whenever possible, the SDK maps standard assets to the corresponding properties. The complete OpenRTB Native response is also available through `openRTBNative`, where you can find returned assets by the IDs used in the request.

Use the following property on `ANNativeAdResponse`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `openRTBNative` | `NSDictionary<NSString *, id> *` | readonly, strong | Returns the complete OpenRTB Native response, or `nil` when unavailable. |

### [Swift](#tab/swift2)

```swift
private func loadOpenRTBNativeAd() {
    nativeAdRequest = ANNativeAdRequest() // Create a native ad request
    nativeAdRequest?.placementId = "123456" // Set placement ID
    nativeAdRequest?.delegate = self // Set the request delegate
    nativeAdRequest?.openRTBAssets = [
        "ver": "1.2", // Set the OpenRTB Native version
        "privacy": 1, // Request privacy information
        "ext": ["foo": "bar"], // Add a custom request extension
        "assets": [
            ["id": 1, "required": 1, "title": ["len": 300]], // Request title
            ["id": 2, "required": 1, "data": ["type": 2]], // Request body text
            ["id": 3, "required": 0, "data": ["type": 1]], // Request sponsor name
            ["id": 4, "required": 0, "img": ["type": 3]], // Request main image
            ["id": 5, "required": 0, "data": ["type": 12]], // Request CTA text
            ["id": 6, "required": 0, "img": ["type": 1, "hmin": 50, "wmin": 50]], // Request icon
            ["id": 7, "required": 0, "data": ["type": 4]], // Request likes
            ["id": 8, "required": 0, "data": ["type": 6]], // Request price
            ["id": 9, "required": 0, "data": ["type": 11]] // Request display URL
        ]
    ] // Set requested OpenRTB Native assets
    nativeAdRequest?.loadAd() // Load the ad
}

func adRequest(_ request: ANNativeAdRequest, didReceive response: ANNativeAdResponse) {
    let openRTBNative = response.openRTBNative
    let responseAssets = openRTBNative?["assets"] as? [[String: Any]]
    var assetsById: [Int: [String: Any]] = [:]
    responseAssets?.forEach { asset in
        if let assetId = asset["id"] as? Int {
            assetsById[assetId] = asset
        }
    }
    let title = response.title // Or: (assetsById[1]?["title"] as? [String: Any])?["text"] as? String
    let body = response.body // Or: (assetsById[2]?["data"] as? [String: Any])?["value"] as? String
    let mainImageURL = response.mainImageURL // Or: (assetsById[4]?["img"] as? [String: Any])?["url"] as? String
    let callToAction = response.callToAction // Or: (assetsById[5]?["data"] as? [String: Any])?["value"] as? String
    let iconImageURL = response.iconImageURL // Or: (assetsById[6]?["img"] as? [String: Any])?["url"] as? String
    let likesAsset = assetsById[7]
    let priceAsset = assetsById[8]
    let displayUrlAsset = assetsById[9]
    let likesData = likesAsset?["data"] as? [String: Any]
    let priceData = priceAsset?["data"] as? [String: Any]
    let displayUrlData = displayUrlAsset?["data"] as? [String: Any]
    let likes = likesData?["value"] as? String // Match request ID 7
    let price = priceData?["value"] as? String // Match request ID 8
    let displayUrl = displayUrlData?["value"] as? String // Match request ID 9
    let customExtension = openRTBNative?["ext"] as? [String: Any]
    let customValue = customExtension?["foo"] as? String // Read a custom response extension
    let link = openRTBNative?["link"] as? [String: Any]
    let clickUrl = link?["url"] as? String
    let clickFallbackUrl = link?["fallback"] as? String
}
```

### [Objective-C](#tab/objectivec2)

```objectivec
- (void)loadOpenRTBNativeAd {
    self.nativeAdRequest = [[ANNativeAdRequest alloc] init]; // Create a native ad request
    self.nativeAdRequest.placementId = @"123456"; // Set placement ID
    self.nativeAdRequest.delegate = self; // Set the request delegate
    [self.nativeAdRequest setOpenRTBAssets:@{
        @"ver": @"1.2",
        @"privacy": @1,
        @"ext": @{@"foo": @"bar"}, // Add a custom request extension
        @"assets": @[
            @{@"id": @1, @"required": @1, @"title": @{@"len": @300}}, // Request title
            @{@"id": @2, @"required": @1, @"data": @{@"type": @2}}, // Request body text
            @{@"id": @3, @"required": @0, @"data": @{@"type": @1}}, // Request sponsor name
            @{@"id": @4, @"required": @0, @"img": @{@"type": @3}}, // Request main image
            @{@"id": @5, @"required": @0, @"data": @{@"type": @12}}, // Request CTA text
            @{@"id": @6, @"required": @0, @"img": @{@"type": @1, @"hmin": @50, @"wmin": @50}}, // Request icon
            @{@"id": @7, @"required": @0, @"data": @{@"type": @4}}, // Request likes
            @{@"id": @8, @"required": @0, @"data": @{@"type": @6}}, // Request price
            @{@"id": @9, @"required": @0, @"data": @{@"type": @11}} // Request display URL
        ]
    }]; // Set requested OpenRTB Native assets
    [self.nativeAdRequest loadAd]; // Load the ad
}

- (void)adRequest:(ANNativeAdRequest *)request
        didReceiveResponse:(ANNativeAdResponse *)response {
    NSDictionary *openRTBNative = response.openRTBNative;
    NSArray<NSDictionary *> *responseAssets = openRTBNative[@"assets"];
    NSMutableDictionary<NSNumber *, NSDictionary *> *assetsById = [NSMutableDictionary dictionary];
    for (NSDictionary *asset in responseAssets) {
        NSNumber *assetId = asset[@"id"];
        if (assetId) {
            assetsById[assetId] = asset;
        }
    }
    NSString *title = response.title; // Or: assetsById[@1][@"title"][@"text"]
    NSString *body = response.body; // Or: assetsById[@2][@"data"][@"value"]
    NSURL *mainImageURL = response.mainImageURL; // Or: assetsById[@4][@"img"][@"url"]
    NSString *callToAction = response.callToAction; // Or: assetsById[@5][@"data"][@"value"]
    NSURL *iconImageURL = response.iconImageURL; // Or: assetsById[@6][@"img"][@"url"]
    NSDictionary *likesAsset = assetsById[@7];
    NSDictionary *priceAsset = assetsById[@8];
    NSDictionary *displayUrlAsset = assetsById[@9];
    NSString *likes = likesAsset[@"data"][@"value"]; // Match request ID 7
    NSString *price = priceAsset[@"data"][@"value"]; // Match request ID 8
    NSString *displayUrl = displayUrlAsset[@"data"][@"value"]; // Match request ID 9
    NSDictionary *customExtension = openRTBNative[@"ext"];
    NSString *customValue = customExtension[@"foo"]; // Read a custom response extension
    NSDictionary *link = openRTBNative[@"link"];
    NSString *clickUrl = link[@"url"];
    NSString *clickFallbackUrl = link[@"fallback"];
}
```

---

### Request specific assets with Native Assembly

**`ANNativeAdRequest`:** No Native Assembly-specific request configuration is required in your app. Native Assembly is configured for the placement in Microsoft Monetize and is used when `openRTBAssets` isn't set. For this workflow, the SDK uses only the **Creative Asset Specifications** from the Native Assembly associated with the placement. The HTML, CSS, and JavaScript from the **Renderer** tab aren't used; your app renders the returned assets. Renderer code applies only to the Banner Native rendering workflow. For more information, see [Native Assembly Renderer on iOS](native-assembly-renderer-on-ios.md). We recommend using OpenRTB Native when it's available. For setup instructions, see [Configuring a Native Assembly](../monetize/configuring-a-native-assembly.md).

**`ANNativeAdResponse`:** Get the value for `kANNativeElementObject` from `customElements`, cast it to a dictionary, and then read each asset by its field name. Check that a field exists before using it because the creative might omit it.

Use the following property on `ANNativeAdResponse`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `customElements` | `NSDictionary *` | readonly, strong | Returns all elements in the native ad response, or `nil` when unavailable. |

### [Swift](#tab/swift3)

```swift
let nativeElements = response.customElements?[kANNativeElementObject] as? [String: Any]
let title = response.title // Or: nativeElements?["title"] as? String
let body = response.body // Or: nativeElements?["desc"] as? String
let mainImageURL = response.mainImageURL // Or: (nativeElements?["main_img"] as? [String: Any])?["url"] as? String
let iconImageURL = response.iconImageURL // Or: (nativeElements?["icon"] as? [String: Any])?["url"] as? String
let callToAction = response.callToAction // Or: nativeElements?["ctatext"] as? String
let likes = nativeElements?["likes"] as? String
let price = nativeElements?["price"] as? String
let link = nativeElements?["link"] as? [String: Any]
let clickUrl = link?["url"] as? String
let clickFallbackUrl = link?["fallback_url"] as? String
```

### [Objective-C](#tab/objectivec3)

```objectivec
NSDictionary *nativeElements = response.customElements[kANNativeElementObject];
NSString *title = response.title; // Or: nativeElements[@"title"]
NSString *body = response.body; // Or: nativeElements[@"desc"]
NSURL *mainImageURL = response.mainImageURL; // Or: nativeElements[@"main_img"][@"url"]
NSURL *iconImageURL = response.iconImageURL; // Or: nativeElements[@"icon"][@"url"]
NSString *callToAction = response.callToAction; // Or: nativeElements[@"ctatext"]
NSString *likes = nativeElements[@"likes"];
NSString *price = nativeElements[@"price"];
NSDictionary *link = nativeElements[@"link"];
NSString *clickUrl = link[@"url"];
NSString *clickFallbackUrl = link[@"fallback_url"];
```

---

## Configure image loading

Native ad responses can include URLs for a main image and an icon. Use these URLs with your app's image-loading implementation, or enable SDK preloading before calling `loadAd()` to receive downloaded `UIImage` objects. Preloading is disabled by default.

Use the following properties on `ANNativeAdRequest`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `shouldLoadMainImage` | `BOOL` | readwrite, assign | Whether the SDK preloads the main image. |
| `shouldLoadIconImage` | `BOOL` | readwrite, assign | Whether the SDK preloads the icon image. |

### [Swift](#tab/swift4)

```swift
nativeAdRequest.shouldLoadMainImage = true // Preload the main image
nativeAdRequest.shouldLoadIconImage = true // Preload the icon image
nativeAdRequest.loadAd() // Load the ad

let mainImage = response.mainImage // Get the preloaded main image
let iconImage = response.iconImage // Get the preloaded icon image
```

### [Objective-C](#tab/objectivec4)

```objectivec
self.nativeAdRequest.shouldLoadMainImage = YES; // Preload the main image
self.nativeAdRequest.shouldLoadIconImage = YES; // Preload the icon image
[self.nativeAdRequest loadAd]; // Load the ad

UIImage *mainImage = response.mainImage; // Get the preloaded main image
UIImage *iconImage = response.iconImage; // Get the preloaded icon image
```

---

## Related

- [iOS SDK integration instructions](ios-sdk-integration-instructions.md)
- [Get Facebook demand for native on iOS](get-facebook-demand-for-native-on-ios.md)
- [Mediate with iOS](mediate-with-ios.md)
