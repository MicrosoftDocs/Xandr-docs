---
title: Native Assembly Renderer on iOS
description: The native assembly renderer simplifies the use of Banner Native, allowing users to implement native advertising without requiring developers to rebuild their apps.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Native assembly renderer on iOS

The native assembly renderer simplifies the use of [Banner Native](./show-banner-native-on-ios.md) so that it behaves like [Banner](./show-banners-on-ios.md). That is, you can set Native banners to act like web display banners. The renderer simplifies the process of generating Native display and allows Xandr users to implement Native advertising without requiring developers to rebuild their apps with changes or new formats.
Previously, developers had to manage native assets in the UT response by using the AN Native Response class in the Mobile SDK. Now the `renderer_url` in the UT response can be processed and combined with the resources necessary to display native assets in a web view. This generates an AN MRAID container view that is ready to display the moment it is loaded.

> [!NOTE]
> This feature is only available in [Banner Native](./show-banner-native-on-ios.md).

<!--## EntryPoint

Currently, this feature is available only in [Banner Native](./show-banner-native-on-ios.md).-->

## Request API for native assembly renderer

Since renderer is only available in `BannerNativeAd`, you can enable `enableNativeRendering` by setting the `Allow Native` to `YES` in the `BannerAdRequest`. The response will be processed in the same manner as a `BannerAd`.

The following fields must be set:

| Field | Value |
|:---|:---|
| `AllowNativeDemand` | `YES/true` |
| `enableNativeRendering` | `YES/true` |

```
@property (nonatomic, readwrite) BOOL enableNativeRendering;
```

### Example

```
bannerAdObject.enableNativeRendering = YES;
```

## Response API for native assembly renderer

Banner's Delegate is being used to handle Banner-Native `RendererAd`.

```
- (void)adDidReceiveAd:(id)ad
```

### Example

```
- (void)adDidReceiveAd:(id)ad
{
        //Ad Received Successfully
}
```

## Tracker management

Impression trackers are automatically handled by the SDK in the same manner as HTML banner ads. Click trackers should be setup via the renderer console and be managed in the renderer itself.
