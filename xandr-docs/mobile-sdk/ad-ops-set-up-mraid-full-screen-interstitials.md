---
title: Ad Ops - Set Up MRAID Full Screen Interstitials
description: In this article, find Ad Ops setup instructions for serving MRAID full screen interstitials on Xandr mobile SDKs.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Ad Ops - Set up MRAID full screen interstitials

This page has Ad Ops setup instructions for serving MRAID full screen interstitials on our Xandr [Mobile SDKs](xandr-mobile-sdks.md).

For developer-focused interstitial documentation, see [Show Interstitials](show-interstitials-ads-on-ios.md).

## Set up Creatives

To set up your MRAID creative, first create a creative and then configure the settings listed below:

1. Under **Creative Content**, choose the **Third-party** creative type.
1. Choose a **Creative format** of **Third-party tag**. Make sure to uncheck **Serve in iFrame**.
1. When entering the MRAID creative text in the **Tag** field, make sure to reference the `mraid.js` file in the first line of your creative:

    ```
    <script src="mraid.js"></script>
    ```

1. Choose a **Media Type** of **Interstitial: Interstitial**.
1. In the **Template** field, choose **Xandr: Mobile SDK** (ID 38896).

Then, in the **Template** tab:

- Check the **Delay Tag Load** checkbox to delay third-party tags from loading until the WebView displaying the ad occupies the full screen. This may be necessary to prevent discrepancies, since some third-party tags don't load properly offscreen in a 1x1 pixel WebView.
- Use the **Restrict To Orientation** dropdown to control how the ad will be shown on the device's screen:
  - **none**: The ad can appear in either landscape (horizontal) or portrait (vertical) orientation
  - **landscape**: The ad will only appear in landscape (horizontal) orientation
  - **portrait**: The ad will only appear in portrait (vertical) orientation

:::image type="content" source="media/ad-ops-set-up-mraid.png" alt-text="A screenshot of the Template tab with the Template Option Details settings.":::

## Set up placements

To set up your placement,

1. Create a placement.
1. Configure the settings listed below.

In the **Allowed Media** section, select the **Other** button and include the **Interstitial: Interstitial** media type.

## Set up ad size

Make sure the SDK is sending the 1x1 ad size on the ad call (it does send this size by default).

If you have changed the allowed sizes for interstitials in your app from the defaults, check to make sure you're sending the 1x1 ad size. For instructions on sending ad sizes explicitly, see the **Using Custom Interstitial Sizes** section of [Show Interstitials](show-interstitials-ads-on-ios.md).

You can use the following Xandr placement ID in your app for testing: `8522131`.

## Related topics

- [Ad Ops - Set Up Static Image Full Screen Interstitials](ad-ops-set-up-static-image-full-screen-interstitials.md)
- [Ad Ops - Set Up HTML Responsive Interstitials (non-MRAID)](ad-ops-set-up-html-responsive-interstitials-non-mraid.md)
