---
title: Show Banner Video (Outstream) ads on iOS
description: The Mobile SDK supports serving multiple creative formats through a single banner entry point. This page talks about constraints in doing so. Also, learn steps to enable a mix of VAST Video and HTML Banner Ads.
ms.custom: ios-sdk
ms.date: 2/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Show Banner Video (Outstream) ads on iOS

> [!NOTE]
> This offering is currently in Alpha and is subject to change.

Some constraints:

- Video mediation is not yet supported.
- When a placement is integrated using the iOS SDK, video settings configured in the Monetize UI or API are not applied. Video player behavior—including playback method (auto-play, sound on or off), volume control visibility, player size, and controls such as skip—is managed entirely by the SDK through the `ANVideoPlayerSettings` class.
- Configure all video player options explicitly in `ANVideoPlayerSettings` within the app. For more information, see [Customize video player options on iOS](configure-video-player-options-on-ios.md).

## Show a mix of VAST Video and HTML Banner Ads

First, enable video ads in your app for ANBannerAdView.

### [Objective-C](#tab/objc1)

```objc
banner.shouldAllowVideoDemand = YES;
```

### [Swift](#tab/swift1)

```swift
banner.shouldAllowVideoDemand = true
```

---

If you have specified Video as a Media Type for your placement in your app, it is still necessary to use the preceding code to activate video ads. Without explicitly enabling video ads through the SDK, only banner ads will be served. On the other hand, if you haven't included Video as a Media Type for your placement in your app, you can still enable video ads to be served by calling the above commands to set **AllowVideoDemand** to true.

The selection of either VAST Video or regular HTML Banner Ads in the app is determined automatically by the SDK based on the creative with the highest bid.

## Video player size

Publishers have the option to set predetermined player sizes for different video orientations (portrait, landscape, and square) before loading the video ad using the **loadAd**() function. When the video assets are received, the SDK will automatically play the video ad in the appropriate pre-set player size based on its aspect ratio. If these pre-set values are not defined, the SDK will default to using the primary AdSize of **ANBannerAdView** as the player size.

**Set video player size for each ANBannerAdView instance:**

### [Objective-C](#tab/objc2)

```objc
banner.landscapeBannerVideoPlayerSize = CGSizeMake(300, 250);
banner.portraitBannerVideoPlayerSize = CGSizeMake(300, 400);
banner.squareBannerVideoPlayerSize = CGSizeMake(200, 200);
```

### [Swift](#tab/swift2)

```swift
banner.landscapeBannerVideoPlayerSize = CGSize(width: 300, height: 250)
banner.portraitBannerVideoPlayerSize = CGSize(width: 300, height: 400)
banner.squareBannerVideoPlayerSize = CGSize(width: 200, height: 200)
```

---

## Video creative's width and height

Publishers can query the size of the video ad using the below API. The value will only be populated after the **adDidReceiveAd** callback is triggered.

### [Objective-C](#tab/objc3)

```objc
[banner getVideoWidth];
[banner getVideoHeight];
```

### [Swift](#tab/swift3)

```swift
banner.getVideoWidth()
banner.getVideoHeight()
```

---

## Related topic

[Customize Video Player Options](configure-video-player-options-on-ios.md)
