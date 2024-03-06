---
title: Microsoft Monetize - Reporting on Conversions
description: This page gives an overview on concepts related to conversion pixels for troubleshooting, like time taken by pixel to load, Attributed URLs that displays the URL of the website on which a conversion pixel has been placed and Attributed conversions report.   
ms.date: 10/28/2023
---


# Microsoft Monetize - Reporting on conversions

You can use reports to troubleshoot your conversion pixels and thoroughly analyze conversion data.

## Pixel loads

The **Conversion Pixels** section displays how long ago your advertisers' conversion pixels loaded, as well as how many times each pixel loaded in the last 12 hours. This information is updated continuously, and helps you both verify the pixels that are loading properly and identify the pixels in need of troubleshooting. To view the health information associated with each pixel, navigate to the **Conversion Pixels** screen.

The **Loads Last 12 Hours** column displays the number of total loads on the pixel **ID** in the last 12 hours (including the twelfth hour).

The **Last Load** column displays how long ago any web page with the conversion pixel was last visited in the last 12 hours. If "Never" displays here for more than 10 minutes after a pixel was added, the pixel may not be placed correctly on any website.

> [!NOTE]
> Seeing a reasonable time in the **Last Load** column only indicates that the conversion pixel was fired on **at least one (but possibly not every)** website in the last 12 hours. It is recommended to check for individual sites statistics, in **Attributed URLs** below.

To view more information about the conversion pixel, mouse-over the icons in the **Status** column. The **Status** will display information regarding the health of the conversion pixel. For example, look at the **Status** message below. In this example, if your conversion pixel isn't associated with an active line item, then you might be missing out on tracking valuable conversions. Similarly, if your pixel has never loaded, then you might need to investigate with your advertiser to make sure the pixel is placed correctly.

:::image type="content" source="media/conversion-pixels-statuses.png" alt-text="Screenshot of health of the conversion pixel.":::

For details on using this report via the API, see [Conversion Pixel Last Fire](../digital-platform-api/conversion-pixel-last-fire.md).

## Attributed URLs

To view **Conversion Pixel Details** and the **Top 25 Attributed URLs in the Past Hour** section, select a conversion pixel from the **Conversion Pixels** section. **The Top 25 Attributed URLs** section displays the URL of the website on which a conversion pixel has been placed and the related load information.

The **URL** column displays the URL of the website on which the conversion pixel has been placed.

The **Loads** column displays the number times the conversion pixel has loaded in the past hour on the corresponding website.

The **Last Load** column displays how long ago the conversion pixel loaded on this particular website in the last 12 hours. If "Never" displays here for more than 10 minutes after a pixel was added, the pixel may not be placed correctly on this site.

## Attributed conversions

The Advertiser Attributed Conversions report allows you to view conversion pixel IDs, order IDs, times of attributed clicks or impressions, and other information related to your advertisers' attributed conversions. You can use this information to gain valuable insight into your conversions, for example, the times of day that users are most likely to convert.

This report can retrieve data for the last 33 days, but the timestamps will always be in the UTC timezone, so you'll need to translate the UTC time to your standard timezone. If you pull a report for "yesterday", however, the report will run for "yesterday" relative to your standard timezone.

To access this report directly from the **Conversion Pixels** screen, check the box for each pixel that you want to report on and then click **More Actions** \>  **Run Report**.

This takes you to the Advertiser Attributed Conversions report, where the pixels you selected are preset as filters and **Conversion Pixel** is preset as a dimension. Note that you can also access the report directly from the **Advertiser Reporting** screen (**Advertisers** \>  **Reporting**).

> [!NOTE]
> When exporting the Advertiser Attributed Conversions report to Excel, long numbers (including User ID and Auction ID) are converted to floating point format, and any digit after digit 15 will be converted to zero. For example, a User ID of 102083040601081716 will be converted to 102083040601081000 which is not a valid Microsoft Advertising User ID. If you need to pull valid User or Auction IDs, you can copy them manually or use the API version of this report.

For more information about this report, including a full list of dimensions, metrics, and filters, see [Advertiser Attributed Conversions Report](advertiser-attributed-conversions-report.md). For details on running this report via the API, click [here](../digital-platform-api/advertiser-attributed-conversions.md). You may also be interested in the [Network Attributed Conversions Report](member-attributed-conversions-report.md), which provides this information on a different level and includes Universal Pixel attribution information.

## Related topics

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Export Conversion Pixels](export-conversion-pixels.md)
- [Conversion Pixels Advanced](conversion-pixels-advanced.md)
- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)