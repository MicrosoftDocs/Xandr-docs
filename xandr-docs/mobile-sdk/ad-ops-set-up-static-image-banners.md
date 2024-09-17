---
title: Ad Ops - Set up Static Image Banners
description: In this article, find Ad Ops setup instructions for serving banners on Xandr mobile SDKs.
ms.custom: android-sdk
ms.date : 10/28/2023
ms.author: shsrinivasan
---

# Ad Ops - Set up static image banners

This page has Ad Ops setup instructions for serving banners on our Xandr [Mobile SDKs](xandr-mobile-sdks.md). The configuration matches the placement in our SDK's demo app.

For developer-focused banner documentation, see [Show Banners](show-banners-on-ios.md).

## Set up creatives

Use the following settings to set up your creative (see “Add Interstitial Creatives” in the UI documentation for more information):

1. Under **Creative Content**, choose a **Third-party creative** type.
1. Choose a **Creative format** of **Third Party URL**.
1. Choose an **Output Type** of **Image**.
1. Choose a **Media Type of Banner**: **Standard Banner**.
1. In the **Template** field, choose **AppNexus: Standard**.

## Set up placements

Use the following settings to set up your placement (see "Create a Placement" in the UI documentation for more information):

1. Set the **Supply Type** to **Mobile Application**.
1. Set the **Media Type** to **Banner**.
1. Choose a placement size that matches the size of your desired banner ad view in the SDK (as described in the [Show Banners](show-banners-on-ios.md) developer docs).

## Set up SDK 

Follow the developer documentation in [Show Banners](show-banners-on-ios.md).

## Related topics

- [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
- [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)
