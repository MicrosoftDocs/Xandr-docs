---
title: Ad Ops - Set Up HTML Responsive Interstitials (non-MRAID)
description: In this article, find Ad Ops setup instructions for serving responsive HTML interstitials (non-MRAID) on Xandr mobile SDKs.
ms.custom: android-sdk
---

# Ad ops - Set up HTML responsive interstitials (non-MRAID)

This page has Ad Ops setup instructions for serving responsive HTML interstitials (non-MRAID) on our Xandr [Mobile SDKs](xandr-mobile-sdks.md).

For developer-focused interstitial documentation, see [Show Interstitials](show-interstitials-ads-on-ios.md).

## Creative settings

To set up your creative, follow the general instructions in the UI documentation for adding interstitial creatives and include the following settings:

- Under **Creative Content**, choose a **Third-party** creative type.
- Choose a **Creative format** of **Third Party URL**.
- Choose an **Output Type** of **HTML**.
- Choose a **Media Type** of **Interstitial: Interstitial**.
- In the **Template** field, choose **Xandr: Mobile SDK** (ID 38895).

## Placement settings

To set up your placement, follow the general instructions under "Create a Placement" in the UI documentation and include the following settings:

In the **Allowed Media** section, select the **Other** button and include the **Interstitial: Interstitial** media type.

## SDK settings

Make sure the SDK is sending the 1x1 ad size on the ad call (it does send this size by default).

If you have changed the allowed sizes for interstitials in your app from the defaults, check to make sure you're sending the 1x1 ad size. For instructions on sending ad sizes explicitly, see the **Using Custom Interstitial Sizes** section of [Show Interstitials](show-interstitials-ads-on-ios.md).

You can use the following Xandr placement ID in your app for testing: `8522187`.

## Related topics

- [Ad Ops - Set Up MRAID Full Screen Interstitials](ad-ops-set-up-mraid-full-screen-interstitials.md)
- [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)
