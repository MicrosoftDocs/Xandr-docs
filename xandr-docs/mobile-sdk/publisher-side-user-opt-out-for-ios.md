---
title: Publisher-side User Opt-Out for iOS
description: The publisher-side user opt-out feature allows publishers to set users' choice of opt-in/out for iOS from tracking in ad requests.
ms.custom: ios-sdk
ms.date: 07/17/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Publisher side user opt-out for iOS

The publisher-side user opt-out feature exposes an API in the iOS SDK that lets publishers pass the users' opt-in/out tracking choice with every `AdRequest`. For any `AdRequest`, the iOS SDK populates `limitAdTracking` (LMT), read from [`AppTrackingTransparency`](https://developer.apple.com/documentation/apptrackingtransparency). However, the publishers retain information about their users' opt-in/out of tracking and thus are required to pass that information if their user has opted out in order to comply with applicable privacy regulations. Use the `doNotTrack` property to pass this opt-out choice to the iOS SDK.

## Property

Use the following property on `ANSDKSettings`:

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `doNotTrack` | BOOL | readwrite | Set to `YES` to indicate opt-out from tracking, or `NO` to indicate opt-in. When set to `YES`, tracking cookies and IDFA are disabled for all future auctions.<br>Default value is `NO`. |

## Example

### [Swift](#tab/swift1)

```
ANSDKSettings.sharedInstance().doNotTrack = true
```

### [Objective-C](#tab/objectivec1)

```
[ANSDKSettings sharedInstance].doNotTrack = YES;
```

---

## Related

- [SDK privacy for iOS](sdk-privacy-for-ios.md)
