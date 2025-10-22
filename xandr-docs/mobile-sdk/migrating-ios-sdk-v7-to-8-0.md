---
title: Migrating iOS SDK v7 to 8.0
description: Publishers using iOS SDK v8.0 must initialize Xandr SDK before making an ad request to avoid exceptions.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Migrating iOS SDK v7 to 8.0

Publishers with SDK v8.0, are required to initialize Xandr SDK before making an ad request. When using Xandr Mobile Ads SDK for iOS SDK v8, the `init()` method must be called prior to any other SDK operations. Without this initialization no Ad request would go through and the SDK would throw an exception. For more information, see [iOS - SDK Initialization (v8.0)](./ios-sdk-initialization-v8-0.md).

```
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
     
    // ideally initialize Xandr SDK inside AppDelegate before calling any other SDK methods
    [[XandrAd sharedInstance] initWithMemberID:1234 preCacheRequestObjects:YES completionHandler:^(BOOL success) {
            if(success){
                NSLog(@"XandrAd init Complete");
            }
    }];
    return YES;
    }
```

## Removed APIs and their alternatives

Some of the APIs listed below has been removed in the Xandr SDK v8.0. If the below listed APIs are being used, we request the APIs to be migrated to their equivalent or alternative APIs.

| Class | Removed Property(s) and Method(s) | Alternative Property(s) and Method(s) |
|:---|:---|:---|
| `ANBannerAdView`<br><br><br> | **Property**: `externalUid`  | `ANSDKSettings.publisherUserId` |
| `ANBannerAdView` | **Property**: `adType` | `ANAdResponseInfo.adType` |
| `ANBannerAdView` | **Property**:  `creativeId` | `ANAdResponseInfo.creativeId` |
| `ANBannerAdView` | **Property**: `countImpressionOnAdReceived` | N/A |
| `ANBannerAdView` | **Method**: ` - (void)setAllowNativeDemand:(BOOL)nativeDemand withRendererId:(NSInteger)rendererId;` | `ANBannerAdView.shouldAllowNativeDemand<br>ANBannerAdView.nativeAdRendererId` |
| `ANInterstitialAd`<br> | **Property**: `externalUid`  | `ANSDKSettings.publisherUserId` |
| `ANInterstitialAd` | **Property**: `adType` | `ANAdResponseInfo.adType` |
| `ANInterstitialAd` | **Property**:  `creativeId` | `ANAdResponseInfo.creativeId` |
| `ANInstreamVideoAd`<br> | **Property**: `externalUid`  | `ANSDKSettings.publisherUserId` |
| `ANInstreamVideoAd` | **Property**: `adType` | `ANAdResponseInfo.adType` |
| `ANInstreamVideoAd` | **Property**:  `creativeId` | `ANAdResponseInfo.creativeId` |
| `ANMultiAdRequest`<br> | **Property**: `externalUid`  | `ANSDKSettings.publisherUserId` |
| `ANMultiAdRequest` | **Property**: `adType` | `ANAdResponseInfo.adType` |
| `ANMultiAdRequest` | **Property**:  `creativeId` | `ANAdResponseInfo.creativeId` |
| `ANExternalUserId`<br> | **Property**: `source` | `ANUserId.source` |
| `ANExternalUserId` | **Property**:  `userId` | `ANUserId.userId` |
| `ANExternalUserId` | **Method**: `- (nullable instancetype)initWithSource:(ANExternalUserIdSource)source userId:(nonnull NSString *)userId;` | ```ANUserId.initWithANUserIdSource:(ANUserIdSource)source userId:(nonnull NSString *)userId;``` |
| `ANNativeAdRequest` | **Property**: `adType` | `ANAdResponseInfo.adType` |
| `ANNativeAdRequest` | **Property**: `externalUid` | `ANSDKSettings.publisherUserId` |
| `ANNativeAdResponse` | **Property**: `creativeId` | `ANAdResponseInfo.creativeId` |
| `ANSDKSettings`<br><br> | **Property**: `HTTPSEnabled` | N/A  |
| `ANSDKSettings` | **Property**: `externalUserIdArray` | `ANSDKSettings.userIdArray` |
| `ANSDKSettings` | **Property**:  `useAdnxsSimpleDomain` | N/A |
| `ANSDKSettings` | **Property**: `countImpressionOn1PxRendering` | N/A |
| `ANTargetingParameters` | **Property**: `externalUid` | N/A |
