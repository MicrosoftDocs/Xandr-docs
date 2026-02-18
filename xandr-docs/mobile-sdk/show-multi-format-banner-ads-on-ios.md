---
title: Banner Video / OutStream Ads on iOS
description: The AppNexus mobile SDK supports serving multiple creative formats through a single banner entry point. This page talks about constraints in doing so. Also, learn steps to enable a mix of VAST video and HTML banner Ads.  
ms.custom: ios-sdk
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Banner video/OutStream ads on iOS

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

As of version 4.5 for iOS, the mobile SDK supports serving multiple creative formats (RTB VAST outstream videos and regular banner ads) through a single banner entry point.

Some constraints:

- Video mediation is not yet supported.
- When a placement is integrated using the iOS SDK, video settings configured in the Monetize UI or API are not applied. Video player behavior—including playback method (auto-play, sound on or off), volume control visibility, player size, and controls such as skip—is managed entirely by the SDK through the `ANVideoPlayerSettings` class.
<br>Configure all video player options explicitly in `ANVideoPlayerSettings` within the app. For more information, see [Customize video player options on iOS](https://learn.microsoft.com/en-us/xandr/mobile-sdk/configure-video-player-options-on-ios?tabs=objectivec1).

## Show a mix of VAST video and HTML banner ads

1. Before you begin, you must [integrate the iOS SDK](ios-sdk-integration.md) with your project.
2. Next, enable Video Ads in your App for ANBannerAdView.

``` 
banner.shouldAllowVideoDemand = true;
```

The selection of either VAST video or regular HTML banner ads in the app is determined automatically by the SDK based on the creative with the highest bid.

> [!NOTE]
> If you have specified Video as a Media Type for your placement in the application, it is still necessary to use the aforementioned commands to activate video ads. Without explicitly enabling video ads through the SDK, only banner ads will be served. On the other hand, if you haven't included Video as a Media Type for your placement in the application, you can still enable video ads to be served by calling the above commands to set **AllowVideoDemand** to true.

## Video orientation

### Set video player size

Publishers have the option to set predetermined player sizes for different video orientations (portrait, landscape, and square) before loading the video ad using the **loadAd**() function. When the video assets are received, the SDK will automatically play the video ad in the appropriate pre-set player size based on its aspect ratio. If these pre-set values are not defined, the SDK will default to using the primary AdSize of **ANBannerAdView** as the player size.

**Code sample to set video player size for each ANBannerAdView instance:**

``` 
banner!.landscapeBannerVideoPlayerSize = CGSize(width: 300, height: 250)
banner!.portraitBannerVideoPlayerSize = CGSize(width: 300, height: 400)
banner!.squareBannerVideoPlayerSize = CGSize(width: 200, height: 200)
```

### Query video creative's width and height

Publishers can query the size of the video ad using the below API.

``` 
banner?.getVideoWidth()
banner?.getVideoHeight()
```

> [!NOTE]
> The values will only be populated after the adDidReceiveAd callback is triggered.

## Related topic

[Customize Video Player Options](configure-video-player-options-on-ios.md)
