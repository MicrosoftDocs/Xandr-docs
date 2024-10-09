---
title: Location Controls on iOS
description: This article provides instructions to control location data accuracy and HTML5 location access for advertisers to improve monetization of ads.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Location controls on iOS

On this page you'll find instructions for controlling the accuracy of the location data the SDK sends to the ad server, as well as for controlling the HTML5 location access for creatives rendered in a WebView. Improving location accuracy can be useful for advertisers as better location data may lead to better monetization of your ads.

## Location accuracy

Use the ANAdProtocol `setLocationWithLatitude` method to control how accurate the location data is that you pass to the ad server:

```
CLLocation *location = [locationManager location];
NSDate *now = [NSDate date];
[banner.setLocationWithLatitude:location.coordinate.latitude
  longitude:location.coordinate.longitude
  timestamp: now
  horizontalAccuracy: location.horizontal_accuracy
  precision: 4];
```

The `precision` parameter will cause all location information to be internally rounded to the specified number of digits after the decimal before being passed to the ad server. The correlation between the value of `precision` and location accuracy distance is as follows:

| Precision (Integer) | Resolution Accuracy |
|:---|:---|
| 2 | Approx. 1 kilometer |
| 3 | Approx. 100 meters |
| 4 | Approx. 10 meters |
| -1 | Full resolution is passed |

## Location access

Creatives rendered in a WebView can access a user's location through HTML5 location API's. By default, when a creative asks for location, a popup is displayed to the users asking for explicit consent/permission to use the location. App developers can control this behavior and disable location access for creatives using the APIs describe below. When location access is disabled, popups won't be shown to the users and the creative will receive a PERMISSION_DENIED error for HTML5 location API calls.

Use the `ANSDKSettings.sharedInstance.locationEnabledForCreative` property to control the location access for creatives. Default is `YES`.

The following code disables location for the creative:

```
ANSDKSettings.sharedInstance.locationEnabledForCreative = NO
```
