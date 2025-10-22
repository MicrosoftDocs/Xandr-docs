---
title: Listener for AdAboutToExpire on iOS
description: In this article, learn about the Listener for AdAboutToExpire in iOS, including its properties, methods, and examples.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Listener for AdAboutToExpire on iOS

A set of two callback methods is introduced under **ANNativeAdDelegate** API to notify the publisher when an ad is about to expire and when an ad is actually expired. When an ad is expired, the impression doesn't get counted for that ad. Additionally, if the ad impression is logged before expiry, both callback methods are invalidated.

After **didReceiveResponse** method is called, the user needs to set delegate to get following callback methods:

- **(void)adWillExpire:(nonnull id)response;**

  This callback method is used to notify the publisher when an ad is about to expire.

- **(void)adDidExpire:(nonnull id)response;**

  This callback method is used to notify that an ad is expired.

## Properties

The time interval for about to expire of an ad can be set using the property **nativeAdAboutToExpireInterval**. The default value of about to expire time interval is 60 seconds. This interval denotes the time period in seconds on the basis of which **adWillExpire()** callback is triggered.

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `nativeAdAboutToExpireInterval` | `NSInteger` | readwrite | Indicates the time interval of ad expiry in seconds. |

```
/**
   An AppNexus nativeAdAboutToExpireInterval. A nativeAdAboutToExpireInterval is a numeric value that is used to notify before ad is about to expire. Default value of aboutToExpireTimeInterval is 60(second).
 * nativeAdAboutToExpireInterval accept value in second.
 */
@property (nonatomic, readwrite, assign) NSInteger nativeAdAboutToExpireInterval;
```

> [!NOTE]
> The property for about to expire time interval must be set before making a Native Ad request, so that the response can adapt to the values set in this variable. If it is not set explicitly, default value (60 seconds) will be considered.

## Delegate callbacks

```
self.adRequest= [[ANNativeAdRequest alloc] init];
[self.adRequest setPlacementId:@"1"];
self.adRequest.delegate = self;
```

## Methods
The following methods are supported in this feature:

### (void)adWillExpire and (void)adDidExpire

```
- (void)adRequest:(ANNativeAdRequest *)request didReceiveResponse:(ANNativeAdResponse *)response
{
    response.delegate = self; // required to set for adWillExpire & adDidExpire callbacks
}
 
- (void)adDidExpire:(nonnull id)response {
    NSLog(@"adDidExpire");
}
 
- (void)adWillExpire:(nonnull id)response {
    NSLog(@"adWillExpire");
}
```
