---
title: Multi Ad Request for iOS
description: This article provides instructions and code samples for using ANMultiAdRequest to initiate multiple auctions in a single server response. 
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Multi ad request for iOS

## Overview

This article provides instructions and code samples for initiating and configuring a multi ad request (`ANMultiAdRequest`). `ANMultiAdRequest` enables you to use a single universal tag (UTv3) request to initiate multiple auctions, the results of which are returned in a single server response.

`ANMultiAdRequest`, like an `AdUnit`, implements a subset of `ANAdProtocol`. This enables a `ANMultiAdRequest` to adopt the type and behavior of different `AdUnits` ([banner](./show-banners-on-ios.md), [native](./show-banner-native-on-ios.md), [video](./show-instream-video-ads-on-ios.md), etc.) using the same specifications of each `AdUnit` type. Custom keywords can be assigned to a `ANMultiAdRequest` and will be inherited by the contained `AdUnits`.

## Initialization

Users can select from one of three initialization methods. All require a `memberId` and a `delegate` object as arguments in order for `ANMultiAdRequest` be initialized. The `memberId` and `delegate` may only be set once per instance. An optional [Publisher ID parameter](./publisher-id-for-ios.md) can be set at this time. All `AdUnits` must contain the same `memberId` as the one passed in the initialization process. `AdUnits` containing `placementIds` will use the associated `memberId` of that placement. Upon successful initialization, an `ANMultiAdRequest` class instance is returned.

> [!NOTE]
> The `ANMultiAdRequest` instance will reject `AdUnits` with `memberId` values different from their own.

### Initialization methods
The following methods are supported in this feature:

#### Initialize with a list of one or more `AdUnits`

Initializes an instance of `ANMultiAdRequest` with a list of one or more `AdUnits`. For example,

**Without publisher ID**

```
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
            delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
             adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit, ...;
```

**With publisher ID**

```
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
         publisherId:(NSInteger)publisherId
            delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
             adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                     ... NS_REQUIRES_NIL_TERMINATION;
```

#### Initialize with a list of `AdUnits` and call the `load` method

Enables initialization and calls the `load` method with a single line of code. Like the process above, the instance is initialized with a list of one or more `AdUnits`. If a failure occurs during the `load` lifecycle, the class is not initialized and a null object is returned. When a successful `load` process occurs, a class instance is returned, after which the success or failure of the instance is communicated to the caller via `ANMultiAdRequestDelegate`. For example,

**Without publisher ID**

```
- (nullable instancetype)
    initAndLoadWithMemberId:(NSInteger)memberId
                   delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
                    adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                            ...;
```

**With publisher ID**

```
- (nullable instancetype)
    initAndLoadWithMemberId:(NSInteger)memberId
                publisherId:(NSInteger)publisherId
                   delegate:(nullable id<ANMultiAdRequestDelegate>)delegate
                    adUnits:(nonnull id<ANAdProtocolFoundationCore>)firstAdUnit,
                            ... NS_REQUIRES_NIL_TERMINATION;
```

#### Simple initialization

This basic initialization returns an instance of the class but takes no action. Configuration can be completed by using class properties and methods. The initialized delegate is set on the `AdUnits` as they are added.

**Without publisher ID**

```
- (nullable instancetype)initWithMemberId:(NSInteger)memberId
                              andDelegate:(nonnull id<ANMultiAdRequestDelegate>)
```

**Without publisher ID**

```
- (nullable instancetype)
    initWithMemberId:(NSInteger)memberId
         publisherId:(NSInteger)publisherId
         andDelegate:(nullable id<ANMultiAdRequestDelegate>)delegate;
```

### Arguments

| Variable | Type | Attributes | Scope | Description |
|:---|:---|:---|:---|:---|
| `memberId` | NSInteger | nonatomic, readonly, assign | `Required` | A member ID. Any `AdUnits` contained within the `ANMultiAdRequest` must have identical `memberIds` or the `ANMultiAdRequest` will be rejected. The `memberId` can also be attained by passing in a `placementId`. |
| `delegate` | ANMultiAdRequestDelegate | nonnull | Required | An object to be notified with relevant callbacks and information. |
| `adUnits` | List of adUnits | nonnull | Optional | A list of `AdUnits` for initialization of a `ANMultiAdRequest`. |

> [!NOTE]
> If initialization is successful, SDK returns `YES`, otherwise returns `NO`.

## Configuration

All `ANMultiAdRequest` configuration properties and methods are the same in type and usage as those used by `AdUnits`. If properties are set in the `ANMultiAdRequest`, the `AdUnits` inherit those properties. They are not permanent. Once the `ANMultiAdRequest` has completed its lifecycle, `AdUnits` will access their local property values after being removed from the list of `AdUnits` encapsulated by the `ANMultiAdRequest` instance.

### Parameters

| Parameter | Type | Attributes | Description |
|:---|:---|:---|:---|
| `memberId` | NSInteger | readonly | A member ID. Any `AdUnits` contained within the `MultiAdRequest` must have identical `memberIds` or the `MultiAdRequest` will be rejected by Xandr's Impression Bus. The `memberId` can also be attained by passing in a `placementId`. |
| `location` | ANLocation | readwrite | The user location. `Location` can be set with `horizontalAccuracy` and a `precision` level. See [Location Methods](#location-methods) below. |
| `age` | NSString | readwrite | The user's age. |
| `gender` | ANGender | readwrite | The user's gender. |
| `customKeyword` | Array | readwrite | Custom keywords applied to the `MultiAdRequest`. These keywords will be inherited by the attached `AdUnits`. This list can be supplemented within each `AdUnit` with additional custom keywords. |
| `AdUnit` | Object | readwrite | An `AdUnit` item to add to the `MultiAdRequest` |
| `countOfAdUnits` | NSUintetger | readonly | Returns the number of `AdUnits` contained by the `MultiAdRequest` instance. |

### Location methods

`setLocationWithLatitude` sets the value of the `location` property of a `MultiAdRequest` object. It can be called with an additional `precision` parameter. For example,

**Without precision parameter**

```
- (void)setLocationWithLatitude:(CGFloat)latitude
                      longitude:(CGFloat)longitude
                      timestamp:(nullable NSDate *)timestamp
             horizontalAccuracy:(CGFloat)horizontalAccuracy;
```

**With precision parameter**

```
- (void)setLocationWithLatitude:(CGFloat)latitude
                      longitude:(CGFloat)longitude
                      timestamp:(nullable NSDate *)timestamp
             horizontalAccuracy:(CGFloat)horizontalAccuracy
                      precision:(NSInteger)precision;
```

#### Parameters

| Parameter | Type | Scope | Description |
|:---|:---|:---|:---|
| `latitude` | CGFloat | Required | The latitude of the location. |
| `longitude` | CGFloat | Required | The longitude of the location. |
| `timestamp` | NSDate | Optional | The timestamp that the location was set. |
| `horizontalAccuracy` | CGFloat | Required | The radius of uncertainty for the location. |
| `precision` | NSInteger | Optional | Determines the decimal degree precision for the location. |

#### Methods

- **`load`**  

  Loads all contained `AdUnits` by sending a `multi-tag UTv3` request to Xandr's Impression Bus. For each `ANMultiAdRequest` instance, only one load may be active at a time. Loads are complete when one of the `MultiAdRequestDelegate` methods is fired. Returns `YES` on success and `NO` on failure.

  ```
  - (BOOL)load;
  ```

- **`addAdUnit`**  

  Adds an `AdUnit` to the ANMultiAdRequest. `AdUnits` will be rejected if their `memberId` does not match the `memberId` assigned to the `MultiAdRequest` or does not match the `memberId` of the other `AdUnits` contained within the `ANMultiAdRequest`. Returns `YES` on success and `NO` on failure.

  ```
  - (BOOL)addAdUnit:(nonnull id<ANAdProtocolFoundation>)adunit;
  ```

  **Arguments**  
   
  | Parameter | Type | Scope | Description |
  |:---|:---|:---|:---|
  | `AdUnit` | Object | Required | An `AdUnit` item to add to the `MultiAdRequest` |  
  
- **`removeAdUnit`**

  Removes an `AdUnit` from the `ANMultiAdRequest`. Returns `YES` on success and `NO` on failure.

  ```
  - (BOOL)removeAdUnit:(nonnull id<ANAdProtocolFoundation>)adunit;
  ```

  **Arguments**  

  | Parameter | Type | Scope | Description |
  |---|---|---|---|
  | `AdUnit` | Object | Required | An `AdUnit` item to add to the `MultiAdRequest` |

- **`addCustomKeywordWithKey`**  

  Adds a custom keyword to the `ANMultiAdRequest`. Stored as a pair of keys and value, custom keywords are inherited by the `AdUnits` contained within the `ANMultiAdRequest`.

  ```
  - (void)addCustomKeywordWithKey:(nonnull NSString *)key
                            value:(nonnull NSString *)value;
  ```

  **Arguments**  

  | Parameter | Type | Scope | Description |
  |---|---|---|---|
  | `key` | NSString | Required | The key identifier for the custom keyword. |
  | `value` | NSString | Required | The value of the custom keyword. |

- **`removeCustomKeywordWithKey`**  

  Removes a custom keyword from the `ANMultiAdRequest`. The removed keyword will no longer be inherited by the `AdUnits` contained within the `ANMultiAdRequest`.

  ```
  - (void)removeCustomKeywordWithKey:(nonnull NSString *)key;
  ```

  **Arguments**  

  | Parameter | Type | Scope | Description |
  |---|---|---|---|
  | `key` | NSString | Required | The key identifier for the custom keyword to be removed. |
  
- **`clearCustomKeywords`**  

  Removes all custom keywords from the `ANMultiAdRequest`. The removed keywords will no longer be inherited by the `AdUnits` contained within the `ANMultiAdRequest`.

  ```
  - (void)clearCustomKeywords;
  ```

- **`stop`**  

  Stops the `ANMultiAdRequest`, before the request is completed.

  ```
  - (void)stop;
  ```

### ANMultiAdRequestDelegate methods

- **`multiAdRequestDidComplete`**

  Returns success of `ANMultiAdRequest`. Success indicates that all contained `AdUnits` have loaded and have a clear outcome  

  ```
  - (void)multiAdRequestDidComplete:(nonnull ANMultiAdRequest *)MultiAdRequest;
  ```

- **`multiAdRequestDidFailWithError`**  

  Returns an error message if the `UT Request` generated by an `ANMultiAdRequest` instance fails, for any reason.

  ```
  - (void)multiAdRequestDidFailWithError:(nonnull NSError *)error;
  ```

> [!NOTE]
> `[ANMultiAdRequest load]` can also fail by returning `NO` even prior to sending a `UT Request`. If load returns `YES` that means the `UT Request` was initiated, and all further errors will come through the delegate method.

## Related topics

- [Show Banners on iOS](./show-banners-on-ios.md)
- [Show Interstitials Ads on iOS](./show-interstitials-ads-on-ios.md)
- [Show Instream Video Ads on iOS](./show-instream-video-ads-on-ios.md)
