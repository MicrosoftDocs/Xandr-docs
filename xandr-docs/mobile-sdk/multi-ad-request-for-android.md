---
title: Multi Ad Request for Android
description: This article has instructions and code samples for initiating and configuring multi ad reqguest for Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Multi ad request for Android

## Overview

This page has instructions and code samples for initiating and configuring a `ANMultiAdRequest`. `ANMultiAdRequest` enables the user to use a single universal tag (UTv3) request to initiate multiple auctions, the results of which are returned in a single server response.

`ANMultiAdRequest` is a concrete class and does not implement any interface. The class adopts the type and behavior of different `AdUnits` ([banner](./show-banners-on-android.md), [native](./show-native-ads-on-android.md), [video](./show-instream-video-ads-on-android.md), etc.) using the same specifications of each `AdUnit` type. Custom keywords can be assigned to a `ANMultiAdRequest` and will be inherited by the contained `AdUnits`. An `ANMultiAdRequest` has a public facing listener which observes for `onMultiAdRequestCompleted()` or `onMultiAdRequestFailed()`.

## Initialization

Users can select from one of two initialization methods. Both require a memberId and a `multiAdRequestListener` object as arguments in order for `ANMultiAdRequest` to be initialized. The `memberId` and `multiAdRequestListener` may only be set once per instance. An optional [Publisher ID parameter](./publisher-id-for-android.md) can be set at this time. All `AdUnits` must contain the same `memberId` as the one passed in the initialization process `AdUnits` containing `placementIds` will use the associated `memberId` of that placement. Upon successful initialization, a `ANMultiAdRequest` class instance is returned.

> [!NOTE]
> The `MultiAdRequest` instance will reject `AdUnits` with `memberId` values different from their own.

### Initialization methods
The following methods are supported in this feature:


#### Initialize with a list of `AdUnits` and call the `load` method

Enables initialization and calls the `load` method with a single line of code. The instance is initialized with a list of one or more `AdUnits`. If a failure occurs during the `load` lifecycle, the class is not initialized and a nil object is returned. When a successful `load` process occurs, a class instance is returned.

**Without publisher ID**

```
anMultiAdRequest = new ANMultiAdRequest(context, memberId, multiAdRequestListener, loadOnInit, ads);
```

**With publisher ID**

```
public ANMultiAdRequest(Context context, int memberId, int publisherId, MultiAdRequestListener multiAdRequestListener, boolean loadOnInit, Ad...ads)
```

#### Simple Initialization

This basic initialization returns an instance of the class but takes no action. Configuration can be completed by using class properties and methods. The initialized delegate is set on the `AdUnits` as they are added.

**Without publisher ID**

```
anMultiAdRequest = new ANMultiAdRequest(context, memberId, multiAdRequestListener);
```

**With publisher ID**

```
public ANMultiAdRequest(Context context, int memberId, int publisherId, MultiAdRequestListener multiAdRequestListener)
```

## Arguments

| Variable | Type | Scope | Description |
|:---|:---|:---|:---|
| `memberId` | int | Required | A member ID. Any `AdUnits` contained within the `ANMultiAdRequest` must have identical `memberIds` or the `ANMultiAdRequest` will be rejected. The `memberId` can also be attained by passing in a `placementId`. |
| `multiAdRequestListener` | MultiAdRequestListener | Required | Used to share information about the response whether it is success or failure. |
| `loadOnInit` | boolean | Optional | Boolean value to decide whether to load the `ANMultiAdRequest` during its initialization. |
| `ads` | Ad | Optional | Variable-length argument for taking in a list of Ads. |

## Configuration

All `ANMultiAdRequest` configuration properties and methods are the same in type and usage as those used by `AdUnits`. If properties are set in the `ANMultiAdRequest`, the `AdUnits` inherit those properties. They are not permanent, once the `ANMultiAdRequest` has completed its lifecycle `AdUnits` revert back to their previous property values.

| Parameter | Type | Description |
|:---|:---|:---|
| `memberId` | int | A member ID. Any `AdUnits` contained within the `ANMultiAdRequest` must have identical `memberIds` or the `ANMultiAdRequest` will be rejected by Xandr's Impression Bus. The `memberId` can also be attained by passing in a `placementId`. |
| `age` | String | The user's age. |
| `gender` | AdView.GENDER | The user's gender. |
| `externalUid` | String | User generated ID that can be mapped with Xandr's internal IDs and that mapping shared amongst the members of clients with multiple seats. |
| `customKeyword` | ArrayList<Pair<String, String>> | Custom keywords applied to the `ANMultiAdRequest`. These keywords will be inherited by the attached AdUnits. This list can be supplemented within each `AdUnit` with additional custom keywords. |
| `AdUnit` | Ad | An AdUnit item to add to the `ANMultiAdRequest`. |

## `ANMultiAdRequest` methods

### `load()`

Loads all contained `AdUnits` by sending a `multi-tag UTv3` request to Xandr's Impression Bus. For each `ANMultiAdRequest` instance, only one load may be active at a time. Loads are complete when one of the `Listner` methods is fired. Returns `true` on success and `false` on failure.

```
public boolean load()
```

### `addAdUnit(Ad adUnit)`

Adds an `AdUnit` to the `ANMultiAdRequest`. `AdUnits` will be rejected if their `memberId` does not match the `memberId` assigned to the `ANMultiAdRequest` or does not match the `memberId` of the other `AdUnits` contained within the `ANMultiAdRequest`. Returns `true` on success and `false` on failure.

```
public boolean addAdUnit(Ad adUnit)
```

#### Arguments

| Parameter | Type | Scope | Description |
|:---|:---|:---|:---|
| `AdUnit` | Ad | Required | An `AdUnit` item to add to the `ANMultiAdRequest`. |

### `removeAdUnit(Ad adUnit)`

Removes an `AdUnit` from the `ANMultiAdRequest` Returns `true` on success and `false` on failure.

```
public void removeAdUnit(Ad adUnit)
```

#### Arguments

| Parameter | Type | Scope | Description |
|:---|:---|:---|:---|
| `AdUnit` | Ad | Required | An `AdUnit` item to remove from the `ANMultiAdRequest`. |

### `addCustomKeywordWithKey`

Adds a custom keyword to the `ANMultiAdRequest`. Stored as a pair of keys and value, custom keywords are inherited by the `AdUnits` contained within the `ANMultiAdRequest`.

```
public void addCustomKeywords(String key, String value)
```

#### Arguments

| Parameter | Type | Scope | Description |
|:---|:---|:---|:---|
| `key` | String | Required | The key identifier for the custom keyword. |
| `value` | String | Required | The value of the custom keyword. |

### `removeCustomKeywordWithKey`

Removes a custom keyword from the `MultiAdRequest`. The remove keyword will no longer be inherited by the `AdUnits` contained within the `ANMultiAdRequest`.

```
public void removeCustomKeyword(String key)
```

#### Arguments

| Parameter | Type | Scope | Description |
|:---|:---|:---|:---|
| `key` | String | Required | The key identifier for the custom keyword to be removed. |

### `clearCustomKeywords`

Removes all custom keywords from the `MultiAdRequest`. The cleared keywords will no longer be inherited by the `AdUnits` contained within the `ANMultiAdRequest`. 

```
public void clearCustomKeywords()
```

### `stop()`

Stops the `MultiAdRequest`, before the request is completed.

```
public void stop()
```

### `activityOnDestroy()`

Destroys the ad-unit after activity is completed to prevent memory leaks.

```
adUnit.activityOnDestroy()
```
> [!NOTE]
> As best practices:
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the attached AdUnits when they are expected to be destroyed.

#### Example

```
if (anMultiAdRequest != null) {
            for (WeakReference<Ad> adRef: anMultiAdRequest.getAdUnitList()) {
                Ad ad  = adRef.get();
                if (ad instanceof BannerAdView) {
                    ((BannerAdView) ad).activityOnDestroy();
                } else if (ad instanceof InterstitialAdView){
                    ((InterstitialAdView) ad).activityOnDestroy();
                } else if (ad instanceof VideoAd) {
                    ((VideoAd) ad).activityOnDestroy();
                }
            }
        }
```

## `MultiAdRequestListener` methods

### `onMultiAdRequestCompleted()`

Returns success of `ANMultiAdRequest`. Success indicates that all contained `AdUnits` have loaded and have a clear outcome.

```
void onMultiAdRequestCompleted()
```

### `onMultiAdRequestFailed(ResultCode code)`

Returns an error message if the `UT Request` generated by an `ANMultiAdRequest` instance fails, for any reason.

```
void onMultiAdRequestFailed(ResultCode code)
```

## Related topics

- [Show Banners on Android](./show-banners-on-android.md)
- [Show Interstitials Ads on Android](./show-interstitials-ads-on-ios.md)
- [Show an Instream Video Ads on Android](./show-instream-video-ads-on-android.md)
