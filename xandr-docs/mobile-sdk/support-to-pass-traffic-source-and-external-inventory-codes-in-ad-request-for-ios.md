---
title: Support to Pass Traffic Source and External Inventory Codes in Ad Request for iOS
description: Learn what is an external inventory code and how it provides publishers the ability to break out data on their inventory more granularly than the placement level.  
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Support to pass traffic source and external inventory codes in Ad request for iOS

## Overview - External inventory code

An external inventory code provides publishers the ability to break out data on their inventory more granularly than the placement level. The value can be passed via the `ext_inv_code` field of the request body using the `extInvCode` property, but must be entered into the system before it is logged and available as a dimension in relevant reporting. For more information, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). In short, this property allows you to pass the predefined external inventory codes on ad calls and then report on them.

## Scope of extInvCode

You need to set the External Inventory Code using the `extInvCode` property of `ANBannerAdView`, `InterstitialAdView`, `ANNativeAdRequest` and `ANInstreamVideoAd` However, the scope of use of this property depends on your reporting requirement. You can omit the call to this property if you don't want to use this feature.

**Property**

| Property | Type | Attribute | Description |
|--|--|--|--|
| `extInvCode` | String | readwrite | Indicates predefined value passed on the query string that can be used in reporting. |

``` 
/**
 Set the extInvCode, Specifies predefined value passed on the query string that can be used in reporting. The value must be entered into the system before it is logged.
*/
@property (nonatomic, readwrite, strong, nullable) NSString *extInvCode;
```

 **Example**

``` 
//Banner
ANBannerAdView *  banner = [[ANBannerAdView alloc] initWithFrame: CGRectMake(0, 0, 320, 50)];
.............
[banner setExtInvCode:@"Xandr-extInvCode"];
 
//Native
ANNativeAdRequest *  nativeAdRequest = [[ANNativeAdRequest alloc] init];
 ...........
[nativeAdRequest setExtInvCode:@"Xandr-extInvCode"];
```

**Overview - Traffic source code**

A traffic source code provides the ability to check the third-party traffic source of a particular impression. If the traffic source code is pre-registered with Xandr, and is passed via the query string using the `trafficSourceCode` property, then it would let you know the sources for the third party traffic occurred for an impression.

## Scope of trafficSourceCode

You need to set the Traffic Source Code using the `trafficSourceCode` property of `ANBannerAdView`, `InterstitialAdView`, `ANNativeAdRequest` and `ANInstreamVideoAd`.  

**Property**

| Property | Type | Attribute | Description |
|--|--|--|--|
| `trafficSourceCode` | String | readwrite | Indicates predefined source code values for third party traffic passed on the query string. |

``` 
/**
Set the trafficSourceCode,  Specifies the third-party source of this impression.
*/
@property (nonatomic, readwrite, strong, nullable) NSString *trafficSourceCode;
```

**Example**

``` 
//Banner
ANBannerAdView *  banner = [[ANBannerAdView alloc] initWithFrame: CGRectMake(0, 0, 320, 50)];
.............
[banner setTrafficSourceCode:@"Xandr-trafficSourceCode"];
 
//Native
ANNativeAdRequest *  nativeAdRequest = [[ANNativeAdRequest alloc] init];
 ...........
[nativeAdRequest setTrafficSourceCode:@"Xandr-trafficSourceCode"];
```
