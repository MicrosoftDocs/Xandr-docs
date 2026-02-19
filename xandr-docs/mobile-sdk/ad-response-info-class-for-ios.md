---
title: adResponseInfo Class for iOS
description: In this article, understand what the adResponseInfo class is, its properties, and find code samples of this class for iOS Mobile SDK.
ms.custom: ios-sdk
ms.date: 2/19/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# adResponseInfo class for iOS

This article explains about the `adResponseInfo` class in iOS Mobile SDK.

The [ANAdResponseInfo class](https://github.com/appnexus/mobile-sdk-ios/blob/master/sdk/sourcefiles/public-headers/ANAdResponseInfo.h) is a read-only public convenience class created to hold Universal Tag response properties that are relevant to publishers. When an `AdUnit` is returned from the `loadAd` method without an error, either as a fully defined `adObject` or as a no bid response, an `ANAdResponseInfo` is instantiated as a `adResponseInfo` property of the returned Ad Unit.

To retrieve the `adResponseInfo` object from the ad response, use the following properties:

``` 
@property (nonatomic, readwrite, strong, nullable) ANAdResponseInfo *adResponseInfo;
```

## Properties

| Property | Type | Description |
|---|---|---|
| `contentSource` | String | An Xandr contentSource. A contentSource can be RTB, CSM, or SSM. |
| `creativeId` | String | A unique identifier for the creative associated with the response. |
| `memberID` | Integer | A unique identifier for the member associated with the response. |
| `networkName` |  String | The name of the network associated with the response.   |
| `placementId` |  String | A unique identifier for the placement tag associated with the response. |
| `auctionId` | String | A unique identifier generated for the current bid. |
| `cpm` | NSNumber | The bid price of the current auction expressed as Cost per mille, or thousand (mille = thousand in Latin). A pricing model in which advertisers pay for every 1000 impressions of their advertisement served. This is the standard basic pricing model for online advertising. |
| `cpmPublisherCurrency` | NSNumber | The cpm expressed in publishers' currency. |
| `publisherCurrencyCode` | NSString | The currency code of the publishers' currency. For example, USD |
| `isSov`            | BOOL       | Indicates whether the ad is sold on an exclusive basis. Exclusive (also known as Share of Voice (SOV)) means the advertiser has purchased 100% of the placement’s inventory for a given time period. |
| `mediaTypeId `     | NSInteger  | Media Type ID associated with the response. |
| `mediaSubtypeId`  | NSInteger  | Media Subtype ID associated with the response. |
| `brandCategoryId` | NSInteger  | Brand Category ID associated with the response. |
| `dealId`         | NSInteger  | Deal ID associated with the response. |
| `isRoadblock`      | BOOL       | Indicates whether this is a roadblock ad. |


> [!NOTE]
> AdResponseInfo can be retrieved using VideoAd instance, Interstitial Ad View instance and Native Ad Response also apart from Banner Ad View.

#### Code sample (Objective C)

> ```
> // For interstitialAd once adDidReceiveAd is callback
>   NSString* interstitialAdCreativeId = self.interstitialAd.adResponseInfo.creativeId; // same will be followed to get other adResponseInfo from interstitialAd
>  // For videoAd once adDidReceiveAd is callback
>   NSString* videoAdCreativeId = self.videoAd.adResponseInfo.creativeId; // same will be followed to get other adResponseInfo from videoAd
>  // For nativeAd once didReceiveResponse is callback
>   ANAdResponseInfo nativeAdResponseInfo = nativeAdResponse;
>    NSString* nativeAdCreativeId = nativeAdResponseInfo.creativeId; // same will be followed to get other adResponseInfo from videoAd
> BOOL bannerISOValue = self.banner.adResponseInfo.isSov;
> NSInteger bannerMediaTypeIdValue = self.banner.adResponseInfo.mediaTypeId;
> NSInteger bannerMediaSubtypeIdValue = self.banner.adResponseInfo.mediaSubtypeId;
> NSInteger bannerBrandCategoryIdValue = self.banner.adResponseInfo.brandCategoryId;
> NSInteger bannerDealIdValue = self.banner.adResponseInfo.dealId;
> BOOL bannerIsRoadblockValue = self.banner.adResponseInfo.isRoadblock;
> ```

#### Code sample (Swift)

> ```
> // For interstitialAd once adDidReceiveAd is callback
>   let interstitialAdCreativeId : String = (self.interstitialAd.?.adResponseInfo?.creativeId)! // same will be followed to get other adResponseInfo from interstitialAd
>  // For videoAd once adDidReceiveAd is callback
>   let videoAdCreativeId : String = (self.videoAd.?.adResponseInfo?.creativeId)!  // same will be followed to get other adResponseInfo from videoAd
>  // For nativeAd once didReceiveResponse is callback
>   let nativeAdCreativeId : String = (self.nativeAdResponse.?.adResponseInfo?.creativeId)!  // same will be followed to get other adResponseInfo from nativeAd
> let bannerISOValue: Bool = (self.banner?.adResponseInfo?.isSov)!
> let bannerMediaTypeIdValue: Int = (self.banner?.adResponseInfo?.mediaTypeId)!
> let bannerMediaSubtypeIdValue: Int = (self.banner?.adResponseInfo?.mediaSubtypeId)!
> let bannerBrandCategoryIdValue: Int = (self.banner?.adResponseInfo?.brandCategoryId)!
> let bannerDealIdValue: Int = (self.banner?.adResponseInfo?.dealId)!
> let bannerIsRoadblockValue: Bool = (self.banner?.adResponseInfo?.isRoadblock)!
> ```



### Example
#### [Objective C](#tab/objectivec1)

```
- (void)requestBannerAd
{
  // Make a banner ad view.
  self.banner = [ANBannerAdView adViewWithFrame:CGRectMake(0, 0, 300, 250) placementId:@“1” adSize:CGSizeMake(300,250)];
  self.banner.delegate = self;
  //... Add required configurations
  [self.banner loadAd];
}
// On Ad Loaded
- (void)adDidReceiveAd:(id)ad {
  NSLog(@“Ad did receive ad”);
  NSString* bannerCreativeId = self.banner.adResponseInfo.creativeId;
  NSString* bannerPlacementId = self.banner.adResponseInfo.placementId;
  NSString* bannerAuctionId = self.banner.adResponseInfo.auctionId;
  NSNumber* bannerCPM = self.banner.adResponseInfo.cpm;
  NSNumber* bannerCPMPublisherCurrency = self.banner.adResponseInfo.cpmPublisherCurrency;
  NSString* bannerPublisherCurrencyCode = self.banner.adResponseInfo.publisherCurrencyCode;
}
```

#### [Swift](#tab/swift1)

```
func requestBannerAd() {
       // Make a banner ad view.
       self.banner = ANBannerAdView(frame: CGRect(origin: CGPoint(x: 0,y :0), size: CGSize(width: 300, height: 250)), placementId: “1”, adSize: CGSize(width: 300, height: 250))
       self.banner!.rootViewController = self
       self.banner!.delegate = self
       //... Add required configurations
       self.banner!.loadAd()
   }
  // On Ad Loaded
   func adDidReceiveAd(_ ad: Any) {
       print(“Ad did receive ad”)
       let bannerCreativeId : String = (self.banner?.adResponseInfo?.creativeId)!
       let bannerPlacementId : String = (self.banner?.adResponseInfo?.placementId)!
       let bannerAuctionId : String = (self.banner?.adResponseInfo?.auctionId)!
       let bannerCPM = (self.banner?.adResponseInfo?.cpm)!
       let bannerCPMPublisherCurrency = (self.banner?.adResponseInfo?.cpmPublisherCurrency)!
       let bannerPublisherCurrencyCode = (self.banner?.adResponseInfo?.publisherCurrencyCode)!
}
```
