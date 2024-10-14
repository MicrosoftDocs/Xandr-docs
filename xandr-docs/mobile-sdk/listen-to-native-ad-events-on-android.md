---
title: Listen to Native Ad Events on Android
description: In this article, learn about the NativeAdEventListener feature in Android, including its scope, methods, and examples.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Listen to native ad events on Android

## Overview

A publisher can opt for the SDK to handle various ad events such as AdClick, occurrence of impressions etc., by registering into **NativeAdEventListener** API. Using the API, SDK handles all the mentioned events and notify the publishers whether the impression trackers are fired or not for the creatives. To listen to the Ad events, publishers need to register first using **registerTracking**, after which SDK uses **NativeAdEventListener** to track the ad events. Publishers need to unregister using **unregisterTracking** when they are finished with the views for the response or wish to reuse the view object(s) for a new **NativeAdResponse**.

## Scope of listen to native ad events

The scope of this feature is limited to native creatives only.

## Methods
The following methods are supported in this feature:


### Register for tracking of ad events - registerTracking

Method that registers a single or a list of the developer views that will track impressions and respond to clicks for the native ad.

```
public static void registerTracking(final NativeAdResponse response, final View view, final NativeAdEventListener listener)
public static void registerTracking(final NativeAdResponse response, final View container, final List<View> views, final NativeAdEventListener listener)
```

You can pass friendly obstruction list also in this method. For more information about Friendly Obstructions, see [OMID Friendly Obstruction for Android](omid-friendly-obstruction-for-android.md).

```
public static void registerTracking(final NativeAdResponse response, final View view, final NativeAdEventListener listener, final List<View> friendlyObstructionsList)
public static void registerTracking(final NativeAdResponse response, final View container, final List<View> views, final NativeAdEventListener listener, final List<View> friendlyObstructionsList)
```

You can pass a boolean indicating whether to enable OMID optimization. Set to true to enable OMID optimization, which triggers visibility checks and manages the OMID ad session.

```
public static void registerTracking(final NativeAdResponse response, final View view, final NativeAdEventListener listener, final List friendlyObstructionsList, final boolean enableOMIDOptimization)

public static void registerTracking(final NativeAdResponse response, final View container, final List views, final NativeAdEventListener listener, final List friendlyObstructionsList, final boolean enableOMIDOptimization)

public static void registerTracking(final NativeAdResponse response, final View view, final NativeAdEventListener listener, final boolean enableOMIDOptimization)

public static void registerTracking(final NativeAdResponse response, final View container, final List views, final NativeAdEventListener listener, final boolean enableOMIDOptimization)
```


### Tracking of ad events - NativeAdEventListener

API with methods to track the ad events such as:

- when ad click is set to be handled by the app or SDK.
- when the ad takes the user away from the application.
- when an impression is recorded for a native creative.

  ```
  /**
   * Called when the developer sets the ad click to be handled by the SDK
   */
  public void onAdWasClicked();
   
  /**
   * Called when the ad takes the user away from the application
   */
  public void onAdWillLeaveApplication();
   
  /**
   * Called when the developer sets the ad click to be handled by the app
   * @param clickUrl the click url
   * @param fallbackURL the fallback url
   */
  public void onAdWasClicked(String clickUrl,String fallbackURL);
   
  /**
   * Called when an impression is recorded for an native ad
   */
  public void onAdImpression();
  ```

### Unregister for tracking of ad events - unregisterTracking

Method to unregister a native creative from tracking.

```
public static void unRegisterTracking(final View view)
```

## Example

```
// Register the Native Ad to listen to the Ad events
NativeAdSDK.registerTracking(response, nativeAdContainer, nativeAdEventListener);
// Initialise NativeAdEventListener
NativeAdEventListener nativeAdEventListener = new NativeAdEventListener() {
        @Override
        public void onAdWasClicked() {
            Log.d(LOG_TAG, "Native  onAdWasClicked");
        }
 
        @Override
        public void onAdWillLeaveApplication() {
            Log.d(LOG_TAG, "Native onAdWillLeaveApplication");
        }
 
        @Override
        public void onAdWasClicked(String clickUrl, String fallbackURL) {
            Log.d(LOG_TAG, "onAdWasClicked::clickUrl" + clickUrl + "::fallbackURL::" + fallbackURL);
        }
 
        @Override
        public void onAdImpression() {
            Log.d(LOG_TAG, "Native  onAdImpression");
        }
    };
```
