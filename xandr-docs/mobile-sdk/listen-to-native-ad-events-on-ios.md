---
title: Listen to Native Ad Events on iOS
description: In this article, learn about the NativeAdEventListener feature in iOS, including its scope, methods, and examples.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Listen to native ad events on iOS

## Overview

A publisher can opt for the SDK to handle various ad events such as AdClick, occurrence of impressions etc., by registering into **NativeAdEventListener** API. Using the API, SDK handles all the mentioned events and notify the publishers whether the impression trackers are fired or not for the creatives. To listen to the Ad events, publishers need to register first using **registerViewForTracking**, after which SDK uses **NativeAdEventListener** to track the ad events. Publishers need to unregister using **NativeAdResponse** when they are finished with the views for the response or wish to reuse the vieww object(s) for a new **NativeAdResponse**.

## Scope of listen to native ad events

The scope of this feature is limited to native creatives only.

## Methods
The following methods are supported in this feature:


### Register for tracking of ad events - registerViewForTracking

Method that registers a single or a list of the developer views that will track impressions and respond to clicks for the native ad.

```
- (BOOL)registerViewForTracking:(nonnull UIView *)view
         withRootViewController:(nonnull UIViewController *)rvc
                 clickableViews:(nullable NSArray *)views
                          error:(NSError *__nullable*__nullable)error
```

You can pass friendly obstruction list also in this method. For more information about Friendly Obstructions, see [OMID-Friendly Obstruction for iOS](omid-friendly-obstruction-for-ios.md).

```
- (BOOL)registerViewForTracking:(nonnull UIView *)view
         withRootViewController:(nonnull UIViewController *)rvc
                 clickableViews:(nullable NSArray<UIView *> *)views
                 openMeasurementFriendlyObstructions:(nonnull NSArray<UIView *> *)obstructionViews
                          error:(NSError *__nullable*__nullable)error;
```

### Tracking of ad events - NativeAdEventListener

API with methods to track the ad events such as:

- when the native view is clicked by the user.
- when native view returns the click-through URL and click-through fallback URL.
- when the native view was clicked, and the click through destination is about to open in the in-app browser.
- when the in-app browser has finished presenting and taken control from the application.
- when the in-app browser will close and control will be returned to the application.
- when the in-app browser has closed and control has been returned to the application.
- when the ad is about to leave the app or when an impression is recorded for a native creative.

  ```
  /*!
   * Sent when the native view is clicked by the user.
   */
  - (void)adWasClicked:(nonnull id)response;
   
   
  /*!
   * Sent when the native view returns the click-through URL and click-through fallback URL
   *   to the user instead of opening it in a browser.
   */
  - (void)adWasClicked: (nonnull id)response
               withURL: (nonnull NSString *)clickURLString
           fallbackURL: (nonnull NSString *)clickFallbackURLString;
   
   
  /*!
   * Sent when the native view was clicked, and the click through
   * destination is about to open in the in-app browser.
   *
   * @note If it is preferred that the destination open in the
   * native browser instead, then set clickThroughAction to ANClickThroughActionOpenDeviceBrowser.
   */
  - (void)adWillPresent:(nonnull id)response;
   
   
  /*!
   * Sent when the in-app browser has finished presenting and taken
   * control from your application.
   */
  - (void)adDidPresent:(nonnull id)response;
   
   
  /*!
   * Sent when the in-app browser will close and before
   * control has been returned to your application.
   */
  - (void)adWillClose:(nonnull id)response;
   
   
  /*!
   * Sent when the in-app browser has closed and control
   * has been returned to your application.
   */
  - (void)adDidClose:(nonnull id)response;
   
   
  /*!
   * Sent when the ad is about to leave the app.
   * This will happen in a number of cases, including when
   *   clickThroughAction is set to ANClickThroughActionOpenDeviceBrowser.
   */
  - (void)adWillLeaveApplication:(nonnull id)response;
   
   
   
  /*!
  * Sent when  an impression is recorded for an native ad
  */
  - (void)adDidLogImpression:(nonnull id)response;
  ```

### Unregister for tracking of ad events - unregisterTracking

Method to unregister a native creative from tracking.

```
self.nativeAdResponse = nil
```

## Example

```
- (void)adWasClicked: (nonnull id)response
             withURL: (nonnull NSString *)clickURLString
         fallbackURL: (nonnull NSString *)clickFallbackURLString
{
    NSLog(@"adWasClicked callback called wadWillExpireithURLString");
}
- (void)adWasClicked:(nonnull id)response {
    NSLog(@"adWasClicked callback called");
}
 
 
- (void)adWillPresent:(nonnull id)response {
    NSLog(@"adWillPresent callback called");
}
 
 
- (void)adDidPresent:(nonnull id)response {
    NSLog(@"adDidPresent callback called");
}
 
 
- (void)adWillClose:(nonnull id)response {
    NSLog(@"adWillClose callback called");
}
 
 
- (void)adDidClose:(nonnull id)response {
    NSLog(@"adDidClose callback called");
}
 
 
- (void)adWillLeaveApplication:(nonnull id)response {
    NSLog(@"adWillLeaveApplication callback called");
}
 
 
- (void)adDidLogImpression:(id)ad {
    NSLog(@"adDidLogImpression callback called");
}
```
