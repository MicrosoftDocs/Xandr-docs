---
title: Set Test Mode for iOS
description: This page is an overview to set test mode for IOS.
ms.custom: ios-sdk 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Set test mode for iOS

Here is an overview on setting test mode for IOS.

## Overview

An API is introduced in Xandr mobile SDK to set the mode of execution of AdRequests as test mode for debugging or testing purpose. By default, the mode of execution of AdRequests is set as **No** for test mode. To enable the test mode, the value of the API needs to be changed to **Yes**. However, the scope of setting the test mode for AdRequest execution as **Yes** is limited to debugging/development or testing purpose only,  and not to be used in a production environment. Enabling the test mode in a production environment leads to unintended consequences and impacts the Monetization of your app.

## Property

| Property | Type | Attribute | Description |
|--|--|--|--|
| `enableTestMode` | BOOL | readwrite | Sets YES or NO for the AdRequests to be executed in the test mode. |

``` 
@property (nonatomic) BOOL enableTestMode;
```

## Example

``` 
ANSDKSettings.sharedInstance.enableTestMode = YES;
```
