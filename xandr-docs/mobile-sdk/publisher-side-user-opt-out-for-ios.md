---
title: Publisher-side User Opt-Out for iOS
description: The publisher-side user opt-out feature allows publishers to set users' choice of opt-in/out for iOS from tracking in ad requests.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Publisher side user opt-out for iOS

The publisher-side user opt-out feature provides a new API call in Mobile SDK that enables the publishers to set the information of users' choice of opt-in/out from tracking in the `AdRequests`. For any `AdRequest`, Xandr Mobile SDK checks in the device or OS environment level and populates the value for `limitAdTracking` (LMT) in the background automatically (If `LMT=true`, it indicates that the user opts out from tracking at the device or OS settings). However, the publishers retain information about their users' opt-in/out of tracking and thus are required to pass that information if their user has opted out in order to comply with their privacy regulations. To facilitate this, publisher side user opt-out feature has been introduced to the Mobile SDK.

## Property

The publisher side user opt-out feature enhances the MobileSDK API with a property which indicates whether the feature is enabled or not and if not enable the same.

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `doNotTrack` | BOOL | readwrite | Indicates if you have information in the app about user opt-out. If set to `YES`, tracking cookies and IDFA will be disabled for all future auctions.<br>Default value is `NO`. |

```
/**
 Do not track flag. Set this to YES/NO if you have information in the app about user opt-out. If set to YES, tracking cookies and IDF will be disabled for all future auctions. Default value is NO.
*/
@property (nonatomic, readwrite) BOOL doNotTrack;
```

## Example

```
//Swift
ANSDKSettings.sharedInstance().doNotTrack = true
//Objective-C
[ANSDKSettings sharedInstance].doNotTrack = YES;
```
