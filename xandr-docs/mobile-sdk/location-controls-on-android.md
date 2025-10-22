---
title: Location Controls on Android
description: This article provides instructions to control the accuracy of location data sent to the ad server and HTML5 location access for creatives in a WebView.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Location controls on Android

On this page you'll find instructions for controlling the accuracy of the location data the SDK sends to the ad server as well as for controlling the HTML5 location access for creatives rendered in a WebView.

<!--## Overview

### Location accuracy

Improving location accuracy can be useful for advertisers, as better location data may lead to better monetization of your ads.

### Location access

Creatives rendered in a WebView can access a user's location through HTML5 location API's. By default, when a creative asks for location, a popup is displayed to the users asking for explicit consent/permission to use the location. App developers can control this behavior and disable location access for creatives using the APIs describe below. When location access is disabled, popups won't be shown to the users and the creative will receive a PERMISSION_DENIED error for HTML5 location API calls.-->

## Location accuracy

Improving location accuracy can be useful for advertisers, as better location data may lead to better monetization of your ads.

Use the `SDKSettings.setLocationDecimalDigits(int digitsAfterDecimal)` method to control how accurate the location data is that you pass to the ad server:

```
SDKSettings.setLocationDecimalDigits(2);
```

The `digitsAfterDecimal` argument will cause all location information to be internally rounded to the specified number of digits after the decimal before being passed to the ad server. The correlation between the value of `digitsAfterDecimal` and location accuracy distance is as follows:

| Digits after Decimal | Resolution Accuracy |
|:---|:---|
| 2 | Approx. 1 kilometer |
| 3 | Approx. 100 meters |
| 4 | Approx. 10 meters |
| -1 | Full resolution is passed |

## Location access

Creatives rendered in a WebView can access a user's location through HTML5 location API's. By default, when a creative asks for location, a popup is displayed to the users asking for explicit consent/permission to use the location. App developers can control this behavior and disable location access for creatives using the APIs describe below. When location access is disabled, popups won't be shown to the users and the creative will receive a PERMISSION_DENIED error for HTML5 location API calls.

Use the SDKSettings.setLocationEnabledForCreative(boolean enabled) method to control the location access for creatives. Default is `true`. The following code disables the location pop-up from the creative:

```
SDKSettings.setLocationEnabledForCreative(false);
```
