---
title: Support for External Inventory Code and Traffic Source Code on Android
description: Learn how an external inventory code provides publishers the ability to break out data on their inventory more granularly than the placement level.    
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Support for external enventory code and traffic source code on Android

## Overview - External inventory code

An external inventory code provides publishers the ability to break out data on their inventory more granularly than the placement level. The value can be passed via the `ext_inv_code` field of the request body using the `extInvCode` property, but must be entered into the system before it is logged and available as a dimension in relevant reporting. For more information, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). In short, this property allows you to pass the predefined external inventory codes on ad calls and then report on them.

### Scope of extInvCode

You need to set the External Inventory Code using the `extInvCode` property of `BannerAdView`, `InterstitialAdView`, `NativeAdRequest` and `VideoAd`. However, the scope of use of this property depends on your reporting requirement. You can omit the call to this property if you don't want to use this feature.

**Property**

| Property | Type | Description |
|--|--|--|
| `extInvCode` | String | Sets the external inventory code and indicates predefined value passed on the query string that can be used in reporting. |

``` 
/**
 * Passes the external inventory code to the Ad Request
 * @param extInvCode passed as String, specifies predefined value passed on the query string that can be used in reporting.
 * */
public void setExtInvCode(String extInvCode)
 
 
/**
 * Returns the external inventory code, initially added using {@link #setExtInvCode(String)}
 * @@return extInvCode as String, specifies predefined value passed on the query string that can be used in reporting.
 * */
public String getExtInvCode()
```

**Example**

``` 
//Banner
bannerAdView.setExtInvCode("Xandr-extInvCode");
bannerAdView.getExtInvCode();
//Native
nativeAdRequest.setExtInvCode("Xandr-extInvCode");
nativeAdRequest.getExtInvCode();
```

## Overview - Traffic source code

A traffic source code provides the ability to check the third-party traffic source of a particular impression. If the traffic source code is pre-registered with Xandr, and is passed via the query string using the `trafficSourceCode` property, then it would let you know the sources for the third party traffic occurred for an impression.

### Scope of trafficSourceCode

You need to set the Traffic Source Code using the `trafficSourceCode` property of `ANBannerAdView`, `InterstitialAdView`, `ANNativeAdRequest` and `ANInstreamVideoAd`.  

**Property**

| Property | Type | Description |
|--|--|--|
| `trafficSourceCode` | String | Indicates predefined source code values for third party traffic passed on the query string. |

``` 
/**
 * Passes the traffic source code to the Ad Request
 * @param trafficSourceCode passed as String, specifies the third-party source of this impression.
 * */
public void setTrafficSourceCode(String trafficSourceCode) {
    requestParameters.setTrafficSourceCode(trafficSourceCode);
}
 
/**
 * Returns the traffic source code, initially added using {@link #setTrafficSourceCode(String)}
 * @return trafficSourceCode as String, specifies the third-party source of this impression.
 * */
public String getTrafficSourceCode() {
    return requestParameters.getTrafficSourceCode();
}
```

**Example**

``` 
//Banner
bannerAdView.setTrafficSourceCode("Xandr-trafficSourceCode");
bannerAdView.getTrafficSourceCode();
 
//Native
nativeAdRequest.setTrafficSourceCode("Xandr-trafficSourceCode");
nativeAdRequest.getTrafficSourceCode();
```
