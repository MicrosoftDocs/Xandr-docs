---
title: forceCreativeId for Android
description: In this article, discover how to use forceCreativeId on Android devices. Learn about its scope, method, and an example for better understanding.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# forceCreativeId for Android

A forceCreativeId specifies the ID of a creative that should be forced to appear in a placement. It is used to request for the desired creative to display. Forcing a creative allows you to preview an ad on a site, perform testing or certification, and create tear sheets. This API is available for banner, interstitial, native and InstreamVideo creatives.

## Scope of forceCreativeId

The scope of the forceCreativeId is limited to debug or testing purpose only and not to be used in a production environment.

## Method
The following methods are supported in this feature:

### setForceCreativeId

Setter method which assigns the creative ID for display in a placement. It will pass the forceCreateveId as the argument in the method.

``` 
public void setForceCreativeId(int forceCreativeId)
```

## Example

``` 
//Banner
BannerAdView banner = new BannerAdView(this);
banner.setForceCreativeId(135482485);
 
//Interstitial
InterstitialAdView interstitialAd = new InterstitialAdView(this);
interstitialAd.setForceCreativeId(135482485);
 
//Native
NativeAdRequest adRequest = new NativeAdRequest(this, "123456");
adRequest.setForceCreativeId(135482485);
 
//InstreamVideo
VideoAd instreamVideoAd = new VideoAd( this , "9924002" );
instreamVideoAd.setForceCreativeId(135482485);   
```
