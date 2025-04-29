---
title: Android SDK Ad Units Overview
description: In this article, find links to resources that describe how to implement the various ad units available within the Android SDK.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Android SDK ad units overview

This section describes how to implement the various ad units available within the Android SDK.

## Android ad units

> [!IMPORTANT]
> Native impression counting methodology follows the count-on-render methodology that is used for banner creatives - an impression will fire as soon as the native advertisement renders, regardless of its length of time on the screen. This will ensure greater accuracy and better deliverability, thus improving overall yield.

| AdUnits | Description |
|---|---|
| [Banner Ads](show-banners-on-android.md) | Enables the display of a banner ad. |
| [Banner Native](show-banner-native-on-android.md) | Enables the configuration of a banner ad to return native demand. |
| [High Impact Media](show-high-impact-media-type-on-android.md) | Enables the display of high impact media as banner ad. |
| [Instream Video](show-instream-video-ads-on-android.md) | Enables the display of in-stream video ads. |
| [Interstitials Ads](show-interstitials-on-android.md) | Enables the display of an interstitial ad, an interactive, full-screen ad that covers the interface of the app. |
| [Native Ads](show-native-ads-on-android.md) | Enables the return of native ad demand. Native advertising is the use of ads that match the look, feel and function of the media format in which they appear. |

## Interfaces

| Interfaces | Description |
|---|---|
| [Multi Ad Request](multi-ad-request-for-android.md) | ANMultiAdRequest enables the user to use a single universal tag (UTv3) request to initiate multiple auctions. |
| [Native Assembly Renderer](native-assembly-renderer-for-android.md) | The native assembly renderer simplifies the use of Banner Native so that it behaves like Banner. |
| [Publisher Id](publisher-id-for-android.md) | Provides publishers with options to what action should occur when an ad request fails at the placement level. |
