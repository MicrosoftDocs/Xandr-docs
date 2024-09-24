---
title: Ad Ops - Set Up Static Image Full Screen Interstitials
description: In this article, find Ad Ops setup instructions for serving static image full-screen interstitials on Xandr mobile SDKs.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Ad Ops - Set up static image full screen interstitials

This page has Ad Ops setup instructions for serving static image "full-screen" interstitials on our Xandr [Mobile SDKs](xandr-mobile-sdks.md). By "full-screen", we mean that the static image will be resized to fit the device's screen by JavaScript running in the creative template used in the instructions below.

For developer-focused interstitial documentation, see [Show Interstitials](show-interstitials-ads-on-ios.md).

## Set up creatives

To set up your creative, first create a creative and then configure the settings listed below:

1. Under **Creative Content**, choose to **Upload a file**.
1. Choose a **Media Type** of **Interstitial: Interstitial**.
1. In the **Template** field, choose **Xandr: Mobile SDK Static Images** (ID 38934).
1. If you have a landscape image you want to traffic when the user changes the orientation of their device, you can add it in the **Template** tab.

:::image type="content" source="media/ad-ops-set-up-static-image.png" alt-text="A screenshot of the Template tab with the Template Option Details settings.":::

## Set up placements

To set up your placement,

1. Create a placement
1. Configure the settings listed below.

In the **Allowed Media** section, select the **Other** button and include the **Interstitial: Interstitial** media type.

## Set up SDK

Make sure the SDK is sending the 1x1 ad size on the ad call (it does send this size by default).

If you have changed the allowed sizes for interstitials in your app from the defaults, check to make sure you're sending the 1x1 ad size. For instructions on sending ad sizes explicitly, see the **Using Custom Interstitial Sizes** section of [Show Interstitials](show-interstitials-ads-on-ios.md).

You can use the following Xandr placement ID in your app for testing: `8571059`.

## Related topics

- [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
- [Ad Ops - Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)
