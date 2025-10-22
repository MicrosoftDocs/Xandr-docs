---
title: Set Test Mode for Android
description: This page is an overview to set test mode for Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Set test mode for Android

Here is an overview on setting test mode for Android.

## Overview

An API is introduced in Xandr mobile SDK to set the mode of execution of AdRequests as test mode for debugging or testing purpose. By default, the mode of execution of AdRequests is set as **false** for test mode. To enable the test mode, the value of the API needs to be changed to **true**. However, the scope of setting the test mode for AdRequest execution as **true** is limited to debugging/development or testing purpose only,  and not to be used in a production environment. Enabling the test mode in a production environment leads to unintended consequences and impacts the Monetization of your app.

## Property

| Property | Type | Description |
|--|--|--|
| `enableTestMode` | boolean | Sets true or false for the AdRequests to be executed in the test mode. |

``` 
public static void enableTestMode(boolean enabled);
```

## Example

```
SDKSettings.enableTestMode(true);
```
