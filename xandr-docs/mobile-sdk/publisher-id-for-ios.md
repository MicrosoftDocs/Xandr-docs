---
title: Publisher ID for iOS
description: The publisher_id parameter provides publishers two options for resolving default placements when an ad request fails at the placement level.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Publisher ID for iOS

This article explains about the `publisher_id` parameter of the Universal Tag service.  

## Overview

The `publisher_id` parameter enables publishers to indicate what action should occur when an ad request fails at the placement level. In older versions of mobile SDK, if the request failed, the member ID was be used to determine which default creative to return with the request. With the addition of the `publisher_id` parameter, publishers now have two following options to resolve default placements when the request fails:

1. publisher level default placement
1. member level default placement

### Process

When an invalid placement code is called:

- If a `publisher_id` is present in the JSON request, the request will be rerouted to the publisher level default placement.
- When there is no `publisher_id` in the JSON request, the request will be rerouted to the member level default placement.

## Ad unit methods for publisher ID

The [AdUnit](./ios-sdk-ad-units.md) class has following two methods for setting and retrieving `publisherId`:

### Setter method

#### [Swift](#tab/swift1)

```
public func setPublisherId (publisherId:Int)
```

#### [Objective C](#tab/objectivec1)

 ```
- (void)setPublisherId:(NSInteger)publisherId;
 ```

### Getter method

#### [Swift](#tab/swift2)

```
publisherId:Int
```

#### [Objective C](#tab/objectivec2)

```
(NSInteger) publisherId;
```

## Multi ad request changes

Users can select from one of three initialization methods. All require a `memberId` and a `delegate` object as arguments in order for `ANMultiAdRequest` be initialized, `publisherId` is an optional setting. The `memberId`, `delegate` and `publisherId` may only be set during initialization. All `AdUnits` must contain the same `memberId` as the one passed in the initialization process. See [ANMultiAdRequest](./multi-ad-request-for-ios.md) for more details.

### Code Sample (Objective C)

```
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
            delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
             adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                     ... NS_REQUIRES_NIL_TERMINATION;
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
         publisherId:(NSInteger)publisherId
            delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
             adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                     ... NS_REQUIRES_NIL_TERMINATION;
- (nullable instancetype)
    initAndLoadWithMemberId:(NSInteger)memberId
                   delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
                    adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                            ... NS_REQUIRES_NIL_TERMINATION;
- (nullable instancetype)
    initAndLoadWithMemberId:(NSInteger)memberId
                publisherId:(NSInteger)publisherId
                   delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
                    adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                            ... NS_REQUIRES_NIL_TERMINATION;
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
         andDelegate:(nullable id<ANMultiAdRequestDelegate>)delegate;
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
         publisherId:(NSInteger)publisherId
         andDelegate:(nullable id<ANMultiAdRequestDelegate>)delegate;
```

> [!NOTE]
> The `addAdUnit` method of the `ANMultiAdRequest` will read the attached `publisherId` of the `AdUnit`. If that value does not match the `publisherId` set to the `ANMultiAdRequest` instance, the `ANMultiAdRequest` instance will reject the `AdUnit`.
