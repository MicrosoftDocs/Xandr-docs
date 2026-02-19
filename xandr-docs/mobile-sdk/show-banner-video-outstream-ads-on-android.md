---
title: Show Banner Video / OutStream Ads on Android
description: This page explains the steps by which Xandr mobile SDK supports serving multiple creative formats through a single banner entry point. 
ms.custom: android-sdk
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Show banner video/OutStream ads on Android

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

As of Version 4.6 the mobile SDK supports serving multiple creative formats (RTB VAST outstream videos and regular banner ads) through a single banner entry point.

Some constraints:

- Video mediation is not yet supported.
- When a placement is integrated using the Android SDK, video settings configured in the Monetize UI or API are not applied. Video player behavior—including playback method (auto-play, sound on or off), volume control visibility, player size, and controls such as skip—is managed entirely by the SDK through the `ANVideoPlayerSettings` class.
<br>Configure all video player options explicitly in `ANVideoPlayerSettings` within the app. For more information, see [Customize video player options on Android](https://learn.microsoft.com/en-us/xandr/mobile-sdk/customize-video-player-options-on-android?tabs=java1).

## Show a mix of VAST Video and HTML banner ads

Before you begin, you must [integrate the SDK](android-sdk-integration-instructions.md) with your project.

Next, enable video ads in your App for BannerAdView.

``` 
banner.shouldAllowVideoDemand = true;
```

The selection of either VAST video or regular HTML banner ads in the app is determined automatically by the SDK based on the creative with the highest bid.

> [!NOTE]
> If you have specified Video as a Media Type for your placement in Console, it is still necessary to use the aforementioned commands to activate video ads. Without explicitly enabling video ads through the SDK, only banner ads will be served. On the other hand, if you haven't included Video as a Media Type for your placement in Console, you can still enable video ads to be served by calling the above commands to set **AllowVideoDemand** to true.

## Video orientation

**Video player size:**

Publishers have the option to set predetermined player sizes for different video orientations (portrait, landscape, and square) before loading the video ad using the **loadAd**() function. When the video assets are received, the SDK will automatically play the video ad in the appropriate pre-set player size based on its aspect ratio. If these pre-set values are not defined, the SDK will default to using the primary AdSize of **BannerAdview** as the player size.

**Set video player zize for each BannerAdView instance:**

``` 
bav.setPortraitBannerVideoPlayerSize(new AdSize(300,400));
bav.setLandscapeBannerVideoPlayerSize(new AdSize(300,250));
bav.setSquareBannerVideoPlayerSize(new AdSize(200,200));
```

**Video creative's width and height:**

Publishers can query the size of the video ad using the below API.

> [!NOTE]
> The values will only be populated after the **onAdLoaded** callback is triggered.

``` 
((BannerAdView) bav).getBannerVideoCreativeWidth();
((BannerAdView) bav).getBannerVideoCreativeHeight();
```

## Related topic

[Customize Video Player Options](customize-video-player-options-on-android.md)
