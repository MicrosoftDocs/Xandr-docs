---
title: Publisher ID for Android
description: Use the publisher ID parameter of the Universal Tag service to indicate what action should occur when an ad request fails at the placement level.
ms.custom: android-sdk
---

# Publisher ID for Android

This page describes the `publisher_id` parameter of the Universal Tag service.  

## What is Publisher ID?

The Publisher ID parameter enables publishers to indicate what action should occur when an ad request fails at the placement level. Previously, if the request failed, the Member ID would be used to determine which default creative to return with the request. With the addition of the Publisher ID parameter publishers now have two options for resolving default placements when the request fails, the publisher and the member default placement.

## Publisher ID process

When an invalid placement code is called:

- If a `publisher_id` is present in the JSON request, the request will be rerouted to the publisher level default  placement.
- When there is no `publisher_id` in the JSON request, the request will be rerouted to the member level default placement.

## Ad unit

The [AdUnit](./android-sdk-ad-units.md) class has two methods for setting and retrieving `publisherId`.

**Setter**

```
public void setPublisherId(int publisherId)
```

**Getter**

```
public int getPublisherId() 
```

## Multi ad request changes

Users can select from one of three initialization methods. All require a `memberId` and a `delegate` object as arguments in order for `ANMultiAdRequest` be initialized, `publisherId` is an optional setting. The `memberId`, `delegate` and `publisherId` may only be set during initialization. All `AdUnits` must contain the same `memberId` as the one passed in the initialization process. See [ANMultiAdRequest](./multi-ad-request-for-android.md) for more details.

```
public ANMultiAdRequest(Context context, int memberId, int publisherId, MultiAdRequestListener multiAdRequestListener, boolean loadOnInit, Ad... ads)
public ANMultiAdRequest(Context context, int memberId, int publisherId, MultiAdRequestListener multiAdRequestListener)
```

> [!NOTE]
> The `addAdUnit` method of the `ANMultiAdRequest` will read the attached `publisher_id` of the `AdUnit`. If that value does not match the publisherId set to the `ANMultiAdRequest` instance, the `ANMultiAdRequest` instance will reject the `AdUnit`.
