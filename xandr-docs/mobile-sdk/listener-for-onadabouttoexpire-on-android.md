---
title: Listener for onAdAboutToExpire on Android
description: In this article, learn about the Listener for onAdAboutToExpire in Android, including its properties, methods, and examples.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Listener for onAdAboutToExpire on Android

## Overview

A set of two callback methods are introduced under **NativeAdEventListener** API to notify the publisher when an ad is about to expire and when an ad is actually expired. When an ad is expired then the impression doesn't get counted for that ad. Additionally, if ad impression is logged before expiry then both the callback methods are invalidated.

Once **onAdLoaded** method is called, the user needs to set the **NativeAdEventListener** to get following callback methods:

- **public void onAdAboutToExpire();**

  This callback method is used to notify the publisher when an ad is about to expire.

- **public void onAdExpired();**

  This callback method is used to notify that an ad is expired.

The time interval for about to expire of an ad can be set using the variable **Settings.NATIVE_AD_ABOUT_TO_EXPIRE_INTERVAL**. The default value of about to expire time interval is 60\*1000 milliseconds. This interval denotes the time period in milliseconds on the basis of which **onAdAboutToExpire()** callback is triggered. This method gets triggered at the number of milliseconds prior to actual expiry interval of the ad. Apart from the callbacks, an additional API has been exposed to register the **NativeAdEventListener** known as **registerNativeAdEventListener**.

For example:

```
Settings.NATIVE_AD_ABOUT_TO_EXPIRE_INTERVAL = <time in ms>; // Example: 2 * 60 * 1000
```

> [!NOTE]
> The variable for about to expire time interval must be set before making a Native Ad request, so that the response can adapt to the values set in this variable. If it is not set explicitly, default value (60\*1000 milliseconds) will be considered.

## Methods
The following methods are supported in this feature:


### Register with NativeAdEventListener

Registering the **NativeAdEventListener** is achieved using overloaded methods of **NativeAdSDK.registerTracking()**.

```
final NativeAdEventListener nativeAdEventListener = new NativeAdEventListener() {
    @Override
    public void onAdWasClicked() {
    }
 
    @Override
    public void onAdWillLeaveApplication() {
    }
 
    @Override
    public void onAdWasClicked(String clickUrl, String fallbackURL) {
    }
 
    @Override
    public void onAdImpression() {
    }
 
    @Override
    public void onAdAboutToExpire() {
    }
 
    @Override
    public void onAdExpired() {
    }
}; 
NativeAdSDK.registerTracking(response, nativeContainer, nativeAdEventListener);
```

### registerNativeAdEventListener

```
/**
 * Register the NativeAdResponse to listen to Native Ad events
 *
 * @param response  that contains the meta data of native ad
 * @param listener  called when Ad event happens, can be null
 */
public static void registerNativeAdEventListener(final NativeAdResponse response, final NativeAdEventListener listener);
NativeAdSDK.registerNativeAdEventListener(response, nativeAdEventListener);
```
