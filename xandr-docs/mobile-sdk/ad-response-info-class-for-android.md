---
title: adResponseInfo Class for Android
description: In this article, understand what the adResponseInfo class is, its properties, and find code samples of this class for Android Mobile SDK.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# adResponseInfo class for Android

## Overview

The `adResponseInfo` class is a convenience class created to hold Universal Tag response properties that are relevant to publishers. When an `AdUnit` is returned from the `loadAd` method without an error, either as a fully defined `adObject` or as a no bid response, an `ANAdResponseInfo` is instantiated as an `adResponseInfo` property of the returned Ad Unit.

To retrieve the adResponseInfo object from the ad response:

```
public ANAdResponseInfo getAdResponseInfo()
```

## Properties

| Property | Type | Description |
|---|---|---|
| `adType` | AdType | The Ad Type of the returned ad object. |
| `contentSource` | String | An AppNexus contentSource. A contentSource can be RTB, CSM, or SSM. |
| `memberID` | Integer | A unique identifier for the member associated with the response. |
| `networkName` | String | The name of the network associated with the response.   |
| `tagId` | String | A unique identifier for the placement tag associated with the response. <br><br> **Note**: This may also be referred to as placementId in some instances of code. |
| `auctionId` | String | A unique identifier generated for the current bid. |
| `cpm` | Double | The bid price of the current auction expressed as Cost per mille, or thousand (mille = thousand in Latin). A pricing model in which advertisers pay for every 1000 impressions of their advertisement served. This is the standard basic pricing model for online advertising. |
| `cpmPublisherCurrency` | Double | The cpm expressed in publishers' currency. |
| `publisherCurrencyCode` | String | The currency code of the publishers' currency. For example, USD |

> [!NOTE]
> `AdResponseInfo` can be retrieved using Video Ad instance, Interstitial Ad View instance, and Native Ad Response also apart from Banner Ad View.
>
> #### Code sample (Java)
>
> ```
> //Video Ad
> AdResponseInfo adResponseInfo = videoAd.getAdResponseInfo()
> //Native Ad
> AdResponseInfo adResponseInfo = nativeAdResponse.getAdResponseInfo()
> //Insterstitial Ad View
> AdResponseInfo adResponseInfo = interstitial.getAdResponseInfo()
> ```
>
> #### Code sample (Kotlin)
>
> ```
> //Video Ad
> val adResponseInfo = videoAd.adResponseInfo
> //Native Ad
> val adResponseInfo = nativeAdResponse.adResponseInfo
> //Insterstitial Ad View
> val adResponseInfo = interstitial.adResponseInfo
> ```


### Example

#### [Java](#tab/java1)

```
// Request Banner Ad
bav = new BannerAdView(this);
bav.setPlacementID("1"); // Placement ID
bav.setAdSize(300, 250); // Size
bav.setAdListener(this) // AdListener
// On Ad Loaded
@Override
public void onAdLoaded(AdView bav) {
    log("Banner Ad Loaded");
    
    AdType adType = bav.getAdResponseInfo().getAdType();
    String tagId = bav.getAdResponseInfo().getTagId();
    String auctionId = bav.getAdResponseInfo().getAuctionId();
    Double cpm = bav.getAdResponseInfo().getCpm();
    Double cpmpublisherCurrency = bav.getAdResponseInfo().getCpmPublisherCurrency();
    String publishercurrencyCode = bav.getAdResponseInfo().getPublisherCurrencyCode();
}
```

#### [Kotlin](#tab/kotlin1)

```
// Request Banner Ad
banner = BannerAdView(this)
banner.placementID = "1" // PlacementID
banner.setAdSize(300, 250) // Size
banner.adListener = this // AdListener
banner.loadAd()
// On Ad Loaded
override fun onAdLoaded(ad: AdView?) {
    log("Banner Ad Loaded")
    val creativeId = banner.adResponseInfo.creativeId
    val adType = banner.adResponseInfo.adType
    val tagId = banner.adResponseInfo.tagId
    val auctionId = banner.adResponseInfo.auctionId
    val cpm = banner.adResponseInfo.cpm
    val cpmPublisherCurrency = banner.adResponseInfo.cpmPublisherCurrency
    val publisherCurrencyCode = banner.adResponseInfo.publisherCurrencyCode
}
```

> 