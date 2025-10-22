---
title: Set IDFA usage for iOS
description: This page covers Identifier for Advertisers (**IDFA**) which is an Apple provided id to track the users for advertising purposes by the publishers who have an app on the Apple App Store.   
ms.custom: ios-sdk 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Set IDFA usage for iOS

Here is an overview of Identifier for Advertisers (**IDFA**).

## Overview

The Identifier for Advertisers (**IDFA**) is an Apple provided id to track the users for advertising purposes by the publishers who have an app on the Apple App Store (post getting consent from the users to do that). An API is introduced in Xandr mobile SDK to enable or disable IDFA usage by including or excluding the IDFA field in the ad request. By default, the value is set as **NO** for including the IDFA field in the AdRequests.

## Property

| Property | Type | Attribute | Description |
|--|--|--|--|
| `disableIDFAUsage` | BOOL | readwrite | To exclude the IDFA field in ad request. Default value is NO. |

``` 
@property (nonatomic, readwrite) BOOL disableIDFAUsage;
```

## Example

``` 
[ANSDKSettings sharedInstance].disableIDFAUsage  = YES;
```
