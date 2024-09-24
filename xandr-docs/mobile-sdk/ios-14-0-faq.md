---
title: iOS 14.0 FAQ(s)
description: In this article, explore the frequently asked questions (FAQs) about Apple's iOS 14.0 release in relation to the iOS SDK.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# iOS 14.0 FAQ(s)

This document provides an FAQ in regards to the release of Apple's iOS 14.0 in relation to the Xandr iOS SDK. Specific questions on iOS 14.0 should be researched on the [Apple release site](https://www.apple.com/ios/ios-14-preview/).

> [!WARNING]
> This document is written from the perspective of Xandr Mobile SDK, other parts of our Platform were not considered when creating this FAQ. If you have a specific question about Xandr's support for SKAdNetwork/iOS14, reach out to our support team.

## What is Xandr mobile SDK doing to support AppTrackingTransparency?

Xandr's support for AppTrackingTransparency comes from two distinct point-of-views, what we expect the Publisher App to do and what we are changing in the Xandr Mobile SDK.

- As per the requirements by Apple in iOS14 and above, our expectations are that the Publisher App will
  - use the [App Tracking Transparency Framework](https://developer.apple.com/documentation/apptrackingtransparency?language=objc).
  - present an app-tracking authorization request to the user.
  - request the user's consent as described in the [requestTrackingAuthorizationWithCompletionHandler](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547037-requesttrackingauthorizationwith?language=objc).
- If publishers decide not to show the app-tracking authorization request to users, then the authorization status will either be *ATTrackingManagerAuthorizationStatusNotDetermined* or *ATTrackingManagerAuthorizationStatusRestricted*. These cases will be treated the same way as *ATTrackingManagerAuthorizationStatusDenied*.
- The below table describes how the SDK will treat [ATTrackingManagerAuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanagerauthorizationstatus?language=objc) value.

| ATTrackingManagerAuthorizationStatus | Xandr SDK's treatment of limit_ad_tracking field in AdRequest |
|:---|:---|
| ATTrackingManagerAuthorizationStatusAuthorized | - IDFA is supported. <br> - Publisher 1st party data is supported and optional [iOS user ID doc publisher first party ID](user-id-s-mapping-on-ios.md).<br> - Industry IDs are supported (Liveramp IDL, NetID, etc) and optional [iOS user id doc external user ID](user-id-s-mapping-on-ios.md). |
| ATTrackingManagerAuthorizationStatusDenied | - IDFA is not supported.<br> - Publisher 1st party data is supported [iOS user ID doc publisher ID](user-id-s-mapping-on-ios.md).<br> - Industry IDs are not supported (Liveramp IDL, NetID, etc) [iOS user ID doc external user ID](user-id-s-mapping-on-ios.md). |
| ATTrackingManagerAuthorizationStatusNotDetermined | - IDFA is not supported.<br> - Publisher 1st party data is supported [iOS user ID doc publisher ID](user-id-s-mapping-on-ios.md).<br> - Industry IDs are not supported (Liveramp IDL, NetID, etc) [iOS user ID doc external user ID](user-id-s-mapping-on-ios.md). |
| ATTrackingManagerAuthorizationStatusRestricted | - IDFA is not supported.<br> - Publisher 1st party data is supported [iOS user ID doc publisher ID](user-id-s-mapping-on-ios.md).<br> - Industry IDs are not supported (Liveramp IDL, NetID, etc) [iOS user ID doc external user ID](user-id-s-mapping-on-ios.md). |

> [!NOTE]
> It is the responsibility of the publisher to present the authorization requests. Xandr SDKs will not perform this task.

## What is happening to IDFA in iOS14?

Xandr SDK will fetch and send valid IDFA in ad request only if the authorization status is *ATTrackingManagerAuthorizationStatusAuthorized*.

> [!NOTE]
> If you are concerned with a high volume of users opting out of tracking in iOS14 and above and what options Xandr will use to replace IDFA, reach out to the mobile SDK team. We will pass your concerns on to the correct team responsible for IDFA.

## What happens if App's do not update to v7.6 of SDK release?

If the user is in iOS14 and the app has not updated to v7.6.2+ of the SDK, AdRequest will be sent with limit_ad_tracking:true (This is because Xandr SDK will still be using deprecated iOS13 [API](https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614148-advertisingtrackingenabled?language=objc) in this case).

## What is Xandr Mobile SDK doing to support SKAdNetwork?

[SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork) and related changes in iOS14 are specific for attributing app installations. Xandr Mobile SDK has traditionally relied on third parties such as [Appflyer](https://www.appsflyer.com/blog/aggregated-attribution-solution-ios14/) and [Kochava](https://www.kochava.com/getting-prepared-for-ios-14/) for attributing app installs and they continue to support app install attribution in iOS14 and above. In addition to Appflyer and Kochava, we are associated with the following app install tracking vendors.

- [Flurry](https://www.flurry.com/)
- [AppsFlyer](https://www.appsflyer.com/)
- [TapStream](https://tapstream.com/)
- Google Ad Manager
- Apsalar
- [Kochava](https://kochava.com/)
- [Conversant](https://www.conversantmedia.com/)
- [Tune (formerly HasOffers)](https://www.tune.com/)
- [Adjust](https://www.adjust.com/)
  - [Adjust Network Integrations Page](https://help.adjust.com/en/article/integrated-partners)
  - [Adjust Partner Page (Click URL Builder)](https://partners.adjust.com/index.md)

Go [here](../monetize/set-up-third-party-mobile-app-install-tracking) (log in required) for instructions to integrate these vendors with your app and have them report back to your Xandr account.
