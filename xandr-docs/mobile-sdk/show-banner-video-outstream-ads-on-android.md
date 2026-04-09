---
title: Show Banner Video (Outstream) ads on Android
description: This page explains the steps by which the Mobile SDK supports serving multiple creative formats through a single banner entry point.
ms.custom: android-sdk
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Show Banner Video (Outstream) ads on Android

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

Some constraints:

- Video mediation is not yet supported.
- When a placement is integrated using the Android SDK, video settings configured in the Monetize UI or API are not applied. Video player behavior—including playback method (auto-play, sound on or off), volume control visibility, player size, and controls such as skip—is managed entirely by the SDK through the `ANVideoPlayerSettings` class.
- Configure all video player options explicitly in `ANVideoPlayerSettings` within the app. For more information, see [Customize video player options on Android](customize-video-player-options-on-android.md).

## Show a mix of VAST Video and HTML Banner Ads

First, enable video ads in your app for BannerAdView.

### [Java](#tab/java1)

```java
banner.setAllowVideoDemand(true);
```

### [Kotlin](#tab/kotlin1)

```kotlin
banner.allowVideoDemand = true
```

---

If you have specified Video as a Media Type for your placement in Console, it is still necessary to use the preceding code to activate video ads. Without explicitly enabling video ads through the SDK, only banner ads will be served. On the other hand, if you haven't included Video as a Media Type for your placement in Console, you can still enable video ads to be served by using the preceding code to set **AllowVideoDemand** to `true`.

The selection of either VAST Video or regular HTML Banner Ads in the app is determined automatically by the SDK based on the creative with the highest bid.


## Video player size

Publishers have the option to set predetermined player sizes for different video orientations (portrait, landscape, and square) before loading the video ad using the **loadAd**() function. When the video assets are received, the SDK will automatically play the video ad in the appropriate pre-set player size based on its aspect ratio. If these pre-set values are not defined, the SDK will default to using the primary AdSize of **BannerAdview** as the player size.

**Set video player size for each BannerAdView instance:**

### [Java](#tab/java2)

```java
banner.setPortraitBannerVideoPlayerSize(new AdSize(300, 400));
banner.setLandscapeBannerVideoPlayerSize(new AdSize(300, 250));
banner.setSquareBannerVideoPlayerSize(new AdSize(200, 200));
```

### [Kotlin](#tab/kotlin2)

```kotlin
banner.setPortraitBannerVideoPlayerSize(AdSize(300, 400))
banner.setLandscapeBannerVideoPlayerSize(AdSize(300, 250))
banner.setSquareBannerVideoPlayerSize(AdSize(200, 200))
```

---

## Video creative's width and height

Publishers can query the size of the video ad using the below API. The value will only be populated after the **onAdLoaded** callback is triggered.

### [Java](#tab/java3)

```java
banner.getBannerVideoCreativeWidth();
banner.getBannerVideoCreativeHeight();
```

### [Kotlin](#tab/kotlin3)

```kotlin
banner.getBannerVideoCreativeWidth()
banner.getBannerVideoCreativeHeight()
```

---

## Related topic

[Customize Video Player Options](customize-video-player-options-on-android.md)
