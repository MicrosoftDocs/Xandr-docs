---
title: forceCreativeId for iOS
description: In this article, discover how to use forceCreativeId on iOS devices. Learn about its scope, method, and an example for better understanding.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# forceCreativeId for iOS

A forceCreativeId specifies the ID of a creative that should be forced to appear in a placement. It is used to request for the desired creative to display. Forcing a creative allows you to preview an ad on a site, perform testing or certification, and create tear sheets. This API is available for banner, interstitial, native and InstreamVideo creatives.

> [!NOTE]
> The scope of the forceCreativeId is limited to debug or testing purposes. You should never use it in a production environment.

## Properties

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `forceCreativeId` | Integer | readwrite, assign | Indicates the id of creative that is to be assigned to appear in a placement. |

``` 
@property (nonatomic, readwrite, assign) NSInteger forceCreativeId;
```

## Example

``` 
//Banner
ANBannerAdView *banner = [[ANBannerAdView alloc] initWithFrame:CGRectMake(0, 0, 320, 50) placementId:@"1" adSize:CGSizeMake(320, 50)];
banner.forceCreativeId = 135482485;
 
//Interstitial
ANInterstitialAd *interstitialAd = [[ANInterstitialAd alloc] initWithPlacementId:@"1"];
interstitialAd.forceCreativeId = 135482485;
 
//Native
ANNativeAdRequest *adRequest = [[ANNativeAdRequest alloc] init];
adRequest.forceCreativeId = 135482485;
 
//InstreamVideo
ANInstreamVideoAd  *instreamVideoAd  = [[ANInstreamVideoAd alloc] initWithPlacementId:placementID];
instreamVideoAd.forceCreativeId = 135482485; 
```
