---
title: Banner Video / OutStream Ads on iOS
description: The AppNexus mobile SDK supports serving multiple creative formats through a single banner entry point. This page talks about constraints in doing so. Also learn steps to enable a mix of VAST video and HTML banner Ads.  
ms.custom: ios-sdk
ms.date: 10/28/2023
---


# Banner Video / OutStream ads on iOS

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

As of version 4.5 for iOS, the mobile SDK supports serving multiple creative formats (RTB VAST outstream videos and regular banner ads) through a single banner entry point.

Some constraints:

- Video mediation is not yet supported.
- You cannot currently configure video player options, such as starting video with audio on/off or the presence of a volume button, for a mobile placement with the application UI.

## Show a mix of VAST video and HTML banner Ads

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
