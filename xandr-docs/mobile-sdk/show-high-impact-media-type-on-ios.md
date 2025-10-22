---
title: Show High Impact Media type on iOS
description: This page has instructions and code samples for showing a high impact media as banner ad view in Xandr Mobile SDK for iOS.
ms.custom: ios-sdk 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Show high impact media type on iOS

> [!NOTE]
> This feature is available in Xandr Mobile SDK version 8.1.0 for iOS.

## Overview

This page has instructions and code samples for showing a high impact media as banner ad view in Xandr Mobile SDK for iOS.

## Property

This feature enhances the MobileSDK API with a property that indicates whether high impact media can serve on an Ad object.

| Property | Type | Attribute | Description |
|--|--|--|--|
| `shouldAllowHighImpactDemand` | BOOL | readwrite | Indicates whether high impact media can serve on the Ad object.<br>Default value is NO. |

``` 
/**
 * Sets whether or not High Impact Media(AppNexus Media Type:11) can serve on this Ad object.
 *
*/
@property (nonatomic, readwrite) BOOL shouldAllowHighImpactDemand;
```

## Example

``` 
// Allow High Impact Media for ANBannerAdView 
bannerAdView.shouldAllowHighImpactDemand = YES;
```
