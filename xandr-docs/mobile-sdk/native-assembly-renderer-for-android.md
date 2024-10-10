---
title: Native Assembly Renderer for Android
description: The native assembly renderer simplifies the use of Banner Native, allowing it to behave like web display banners. It simplifies generating Native display.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Native assembly renderer for Android

The native assembly renderer simplifies the use of [Banner Native](./show-banner-native-on-android.md) so that it behaves like a [Banner](./show-banners-on-android.md). That is, you can set Native banners to act like web display banners. The renderer simplifies the process of generating Native display and allows Xandr users to implement Native advertising without requiring developers to rebuild their apps with changes or new formats.

Previously, developers had to manage native assets in the UT response by using the AN Native Response class in the Mobile SDK. Now the `renderer_url` in the UT response can be processed and combined with the resources necessary to display native assets in a web view. This generates an AN MRAID container view that is ready to display the moment it is loaded.

## EntryPoint

Currently this feature is available only in [Banner Native](./show-banner-native-on-android.md).

## Request API for native assembly renderer

Renderer is only available in `BannerNative`. For a `BannerNativeAd`, a Client Developer can enable `enableNativeRendering` by setting the `Allow Native` to `YES` in the `BannerAdRequest`. The response will be processed in the same manner as a `BannerAd`.

The following fields must be set:

| Field | Value |
|:---|:---|
| `AllowNativeDemand` | `YES/true` |
| `enableNativeRendering` | `YES/true` |

```
public void enableNativeRendering(boolean enabled);
```

### Example

```
bannerAdView.enableNativeRendering(true);
```

## Response API for native assembly renderer

Banner's Delegate is being used to handle Banner-Native `RendererAd`

```
public void onAdLoaded(AdView adView)
```

### Example

```
public void onAdLoaded(AdView adView){
        //Ad Received Successfully
        }
```

## Tracker management

Impression trackers are automatically handled by the SDK in the same manner as HTML banner ads. Click trackers should be setup via the renderer console and be managed in the renderer itself.
