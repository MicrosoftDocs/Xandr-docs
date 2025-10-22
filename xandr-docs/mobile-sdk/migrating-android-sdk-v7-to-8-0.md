---
title: Migrating Android SDK v7 to 8.0
description: Publishers using SDK v8.0 must initialize Xandr SDK before making an ad request to avoid exceptions.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Migrating Android SDK v7 to 8.0

Publishers with SDK v8.0, are required to initialize Xandr SDK before making an ad request. When using Xandr Mobile Ads SDK for Android SDK v8, the `init()` method must be called prior to any other SDK operations. Without this initialization no Ad request would go through and the SDK would throw an exception. For more information, see [Android - SDK Initialization (v8.0)](./android-sdk-initialization-v8-0.md).

## Removed APIs and their alternatives

Some of the APIs listed below has been removed in the Xandr SDK v8.0. If the below listed APIs are being used, we request the APIs to be migrated to their equivalent or alternative APIs.

| Class | Removed API | Alternate API |
|:---|:---|:---|
| `ANNativeAdResponse` | `isOpenNativeBrowser()` | `getClickThroughAction()` |
| `ANNativeAdResponse` | `openNativeBrowser(boolean openNativeBrowser)` | `setClickThroughAction(ANClickThroughAction clickThroughAction)` |
| `VideoAd` | `getOpensNativeBrowser()` | `getClickThroughAction()` |
| `VideoAd` | `setOpensNativeBrowser(boolean opensNativeBrowser)` | `setClickThroughAction(ANClickThroughAction clickThroughAction)` |
| `VideoAd` | `setExternalUid(String externalUid)` | `SDKSettings.setPublisherUserId(String publisherUserId)` |
| `VideoAd` | `getExternalUid()` | `SDKSettings.getPublisherUserId()` |
| `VideoAd` | `getCreativeId()` | `ANAdResponseInfo.getCreativeId()` |
| `ANMultiAdRequest` | `getExternalUid()` | `SDKSettings.setPublisherUserId(String publisherUserId)` |
| `ANMultiAdRequest` | `setExternalUid(String externalUid)` | `SDKSettings.getPublisherUserId()` |
| `BannerAdView` | `loadAdOffscreen()` | `loadAd()` |
| `BannerAdView` | `getOpensNativeBrowser()` | `getClickThroughAction()` |
| `BannerAdView` | `setOpensNativeBrowser(boolean opensNativeBrowser)` | `setClickThroughAction(ANClickThroughAction clickThroughAction)` |
| `BannerAdView` | `setExternalUid(String externalUid)` | `SDKSettings.setPublisherUserId(String publisherUserId)` |
| `BannerAdView` | `getExternalUid()` | `SDKSettings.getPublisherUserId()` |
| `BannerAdView` | `getCreativeId()` | `ANAdResponseInfo.getCreativeId()` |
| `BannerAdView` | `getAdType()` | `ANAdResponseInfo.getAdType()` |
| `BannerAdView` | `setAllowNativeDemand(boolean enabled, int rendererId)` | `setAllowNativeDemand(boolean)` <br>`setRendererId(int rendererId)` |
| `BannerAdView` | `setCountImpressionOnAdLoad(boolean enabled)` | N/A |
| `BannerAdView` | `getCountImpressionOnAdLoad()` | N/A |
| `InterstitialAdView` | `loadAdOffscreen()` | `loadAd()` |
| `InterstitialAdView` | `getOpensNativeBrowser()` | `getClickThroughAction()` |
| `InterstitialAdView` | `setOpensNativeBrowser(boolean opensNativeBrowser)` | `setClickThroughAction(ANClickThroughAction clickThroughAction)` |
| `InterstitialAdView` | `setExternalUid(String externalUid)` | `SDKSettings.setPublisherUserId(String publisherUserId)` |
| `InterstitialAdView` | `getExternalUid()` | `SDKSettings.getPublisherUserId()` |
| `InterstitialAdView` | `getCreativeId()` | `ANAdResponseInfo.getCreativeId()` |
| `InterstitialAdView` | `getAdType()` | `ANAdResponseInfo.getAdType()` |
| `NativeAdRequest` | `getOpensNativeBrowser()` | `getClickThroughAction()` |
| `NativeAdRequest` | `setOpensNativeBrowser(boolean opensNativeBrowser)` | `setClickThroughAction(ANClickThroughAction clickThroughAction)` |
| `NativeAdRequest` | `setExternalUid(String externalUid)` | `SDKSettings.setPublisherUserId(String publisherUserId)` |
| `NativeAdRequest` | `getExternalUid()` | `SDKSettings.getPublisherUserId()` |
| `NativeAdResponse` | `getCreativeId()` | `ANAdResponseInfo.getCreativeId()` |
| `SDKSettings` | `useHttps(boolean useHttps)` | N/A. HTTPS is used by default. |
| `SDKSettings` | `isHttpsEnabled()` | N/A |
| `SDKSettings` | `setExternalUserIds(Map<ANExternalUserIdSource,String> externalUserIds)` | `setUserIds(List<ANUserId> userIdList)` |
| `SDKSettings` | `getExternalUserIds()` | `getUserIds()` |
| `SDKSettings` | `setAllowUsingSimpleDomain(boolean allow)` | N/A |
| `SDKSettings` | `setCountImpressionOn1pxRendering(boolean enable)` | N/A |
| `SDKSettings` | `getCountImpressionOn1pxRendering()` | N/A |
| `Clog` | `clogged (Variable)` | N/A |
| `ANExternalUserIdSource (enum)` |  | `ANUserId.Source` |
