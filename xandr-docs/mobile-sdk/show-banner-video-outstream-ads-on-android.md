---
title: Show Banner Video / OutStream Ads on Android
description: This page explains steps by which Xandr mobile SDK supports serving multiple creative formats through a single banner entry point. 
ms.custom: android-sdk
ms.date: 10/28/2023
---


# Show Banner Video / OutStream Ads on Android

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

As of Version 4.6 the Xandr mobile SDK supports serving multiple creative formats (RTB VAST outstream videos and regular banner ads) through a single banner entry point.

Some constraints:

- Video mediation is not yet supported.
- You cannot currently configure video player options, such as starting video with audio on/off or the presence of a volume button, for a mobile placement with the Console UI.

## Show a mix of VAST Video and HTML Banner Ads

Before you begin, you must [integrate the SDK](android-sdk-integration-instructions.md) with your project.

Next, enable Video Ads in your App for BannerAdView.

``` 
banner.shouldAllowVideoDemand = true;
```

The selection of either VAST video or regular HTML banner ads in the app is determined automatically by the SDK based on the creative with the highest bid.

> [!NOTE]
> If you have specified Video as a Media Type for your placement in Console, it is still necessary to use the aforementioned commands to activate video ads. Without explicitly enabling video ads through the SDK, only banner ads will be served. On the other hand, if you haven't included Video as a Media Type for your placement in Console, you can still enable video ads to be served by calling the above commands to set **AllowVideoDemand** to true.

## Video orientation

**Video Player Size:**

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
