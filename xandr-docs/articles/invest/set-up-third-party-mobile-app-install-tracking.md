---
title: Microsoft Invest - Set Up Third-Party Mobile App Install Tracking
description: In this article, follow our step-by-step instructions to set up third-party mobile app install tracking with an external vendor and understand how the install tracking works.
---

# Microsoft Invest - Set up third-party mobile app install tracking

This page explains how to set up third-party mobile app install tracking with an external vendor; it also describes the process by which those installs are reported back to Xandr by the vendor. Finally, it covers how server-side conversion tracking works in general, as well as providing links to further documentation.

## App install tracking vendors

These are examples of partners that have integrated with Xandr for app install tracking. For any questions please reach out to these partners directly.

- [Flurry](https://www.flurry.com/)
- Sam4Mobile
- [Singular](https://www.singular.net/)
- [AppsFlyer](https://www.appsflyer.com/)
- [TapStream](https://tapstream.com/)
- MDotM
- [Google Ad Manager](https://admanager.google.com/home/)
- [Kochava](https://kochava.com/)
- [Epsilon Conversant](https://www.epsilon.com/)
- TapSense
- [Tune (formerly HasOffers)](https://www.tune.com/)
- [Adjust](https://www.adjust.com/)
  - [Adjust Network Integrations Page](https://docs.adjust.com/en/article/skadnetwork-partner-integrations/)
  - [Adjust Partner Page (Click URL Builder)](https://help.adjust.com/en/partner/encoding-tool/)

## Set up third-party mobile app install tracking

> [!NOTE]
> The instructions given here will only work with Xandr-hosted creatives at this time. Technically, our server-side conversion attribution requires the `${SSP_DATA}` macro to be populated by the creative's ad server, so any ad server that populates this macro will work. In practice, there are not any other ad servers that populate this macro at this time.

### Step 1. Create a conversion pixel

Follow the process described in [Create a Conversion Pixel](create-a-conversion-pixel.md) to set up a conversion tracker in our system. When this tracker fires, it informs Xandr that a conversion has taken place. You will provide this conversion pixel ID to the install tracking vendor so they can perform the server-side conversion call described below.

> [!NOTE]
> **Specific to AppsFlyer**: While creating a Conversion Pixel section, make sure that the SDK event names used in Appsflyer match the Conversion Event names in Xandr. Otherwise, the conversion will not be passed back to Xandr and won't be reflected in the Microsoft Invest UI.

### Step 2. Get the click URL from the install tracking vendor

The install tracking vendor should provide you with a URL template that they will use to track conversions. You may want to fill out the URL with other macros; Xandr will replace the text of these macros with relevant data when the data is provided. These macros are used to pass information back to Xandr so that it can be used with our systems. For more information about the macros we support and their meanings, see [Creative Macros](creative-macros.md).

Here's an example of what a click URL from an install tracking vendor could look like:

``` pre
https://wetrackinstalls.com/serve?action=click&publisher_id=[publisher_id]&site_id=[site_id]&offer_id=[offer_id] &odin=${DEVICE_ODIN}&open_udid=${DEVICE_OPENUDID}&ios_ifa=${DEVICE_APPLE_IDA}&ref_id=${SSP_DATA} 
```

> [!NOTE]
> The URL you get from the vendor **must** use the macro `${SSP_DATA}` as the click ID. This click ID will be used in the "post-back" call described below, which the vendor makes to report a successful app install. If this macro is not included in the URL, Xandr will not be able to record the conversion.

### Step 3. Set the creative's landing page URL to the provided install tracking vendor URL

Set the landing page of the creative (also known as the click URL) to the URL provided by your tracking vendor. This process is described in [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

> [!NOTE]
> Make sure you fill out the click URL with any desired [Creative Macros](creative-macros.md), as described in **Step 2** above.

### Step 4. The install tracking vendor reports conversions back to Xandr

When a creative with the install tracking click URL is clicked, the install tracking vendor will make a "post-back" call to Xandr that will report a successful conversion. Here's an example of a post-back URL:

``` pre
https://sspx-router.adnxs.com/sspx?id=[appnexus conversion pixel ID]&sspdata=[click id passed in ${SSP_DATA} on click]
```

You should never need to see this URL, since it's called by the install tracking vendor, not you, the client. However, this information could be useful to you in case any issues arise. For more information about how the server-side conversion tracking process works, see [Server-Side Conversion Pixels](server-side-conversion-pixels.md).

> [!NOTE]
> The sspx handler is supported over non-secure (`http://adnxs.com/sspx`) and secure (`https://secure.adnxs.com/sspx`) modes.

## How it works

When your creative's landing page URL is set up correctly, the install tracking process works as follows.

See the diagram below for a visualization of how this process works. The numbers in the diagram correspond to each of the bulleted points below.

1. The user clicks on the creative. The landing page for the creative is the URL provided by the app install tracker as described in    **Step 2** above.

1. Xandr logs the click and fills in the `${SSP_DATA{style="line-height: 1.6;"}}` token, as well as any device identifiers (such as `${DEVICE_APPLE_IDA{style="line-height: 1.6;"}}`) and other [Creative Macros](creative-macros.md) before redirecting to the install tracking vendor's server. The install tracking vendor also logs the click, along with the now filled-in contents of the `${SSP_DATA{style="line-height: 1.6;"}}` token and device IDs. The install tracker then redirects the user to the app download page.

1. The user installs the app from the app download page.

1. The app notifies the tracking vendor of an install and sends along its device ID.

1. The install tracking vendor matches the device ID provided by the app to the click it logged earlier, and then fires the Xandr server-side conversion pixel, passing the `${SSP_DATA{style="line-height: 1.6;"}}` token. This registers the conversion with Xandr.

    :::image type="content" source="media/third-party-app-install-tracking.png" alt-text="A diagram showing the install tracking process.":::
  
## Related topics

- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)
- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Add a Creative](add-a-creative.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
