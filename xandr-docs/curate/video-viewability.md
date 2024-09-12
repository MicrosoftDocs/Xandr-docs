---
title: Microsoft Curate - Measurement of Video Viewability using VPAID Wrapper
description: In this page, learn what is Video viewability and how you can measure it. This page also covers FAQs on video viewability.  
ms.date: 11/16/2023

---


# Microsoft Curate - Measurement of video viewability using VPAID Wrapper

This page explains the technology behind our video viewability measurement.

> [!IMPORTANT]
> Viewability for video creatives on Microsoft Advertising is measured using OMSDK for Web and App, and if it's not available we fall back to the VPAID wrapper measurement which is avalable for Web only but not for App.

## Video viewability

The Microsoft Advertising video viewability measurement is based on the IAB guidelines, which state that 50% of the surface of a video ad must be in-view for a minimum of 2 seconds.

**The Microsoft Advertising Video Viewability Measurement**

To enable viewability measurement, Microsoft Advertising wraps video ads with a VPAID component which is responsible for loading and playing the ad. In addition, the VPAID wrapper manages, tracks and measures viewability by dropping the viewability measurement script on the page. The VPAID component then notifies the measurement script of any ad related events such as starts, pauses, resumes, etc.

The VPAID wrapper requires that the player supports VPAID creatives. If the publisher does not support VPAID, the creative is considered non-measurable.The following is a list of all the supported and non-supported formats:

**Supported formats:**

- Any version of VAST
- Any version of VPAID
- Instream, outstream
- javascript VPAID
- Display Inventory

## AdServing

When viewability is enabled, the VPAID wrapper is served by default. If the player does not support VPAID, and the original third party creative was VAST, the VAST XML will serve without the VPAID component, and viewability will not be measured. Creatives that already include VPAID components will not serve on players that do not support VPAID.

The Microsoft Advertising VPAID wrapper will always serve when the player is able to play VPAID creatives. At present, only desktop web and mobile web are supported. Viewability measurement on both instream and outstream positions is supported.

**The AdServing Lifecycle**

1. A **video tag** is embedded within a video player on a publisher's website.
1. Consumer loads the website and the video ad tag makes a **bid request** to Microsoft Advertising servers.
1. The Microsoft Advertising server generates a **VAST document** that links to the Microsoft Advertising VPAID wrapper URL, and from the VAST to the player via a URL.
1. The VAST document is **sent** to the **Video player**.
1. The player loads, initializes, and **runs** the Microsoft Advertising **VPAID viewability wrapper**.
1. The VPAID wrapper injects the **viewability measurement javascript** on the page.
1. The VPAID wrapper makes a call to a **third party ad server**.
1. Third party ad server generates a **VAST document** (the original VAST creative uploaded within Curate).
1. The third party VAST document is **sent** to the **VPAID wrapper**.
1. The VPAID wrapper **loads** the video creative.
1. The **creative** **(ad) is displayed** in the player while the viewability javascript on the page **measures the viewability** of the creative.

:::image type="content" source="media/viewability.png" alt-text="Screenshot of AdServing Lifecycle.":::

**VPAID Wrapper Functions**

In addition to viewability measurement, the VPAID wrapper is responsible for loading and parsing the VAST document by identifying creatives and collecting tracking pixels. While the video ad is being played, the wrapper calls tracking events that are specified in the VAST document, such as pause, resume, pause on click etc. The VPAID wrapper is also responsible for managing click-through URLs and adjusting the volume of the video ad according to the volume set on the player.

**VPAID Wrapper specifications**

The VPAID wrapper has the following specifications:

- Hosted by Microsoft Advertising CDN
- Injects JavaScript code in the page to measure viewability
- Receives the URL of the VAST document to play as a parameter
- Downloads the VAST document, selects the media file to play, manages
  tracking events, forwards VPAID Events
- Desktop web and mobile web measurement

## Reporting - UI

The following metrics are now available in the Advertiser Video Analytics Report, Publisher Video Analytics Report, and Member Video Analytics Report. (See [Analytics Reporting](../invest/network-analytics-report.md) for more information.)

**Viewability Measurement Metrics**

| Viewability Metrics | Definition |
|--|--|
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |

> [!NOTE]
> Viewability Measurement Rate is not directly comparable to other measurement vendors since our total impression count is higher. Our measurement rate is not an indicator of the technical quality of the measurement. For more information, see the [Viewability FAQ](viewability-faq.md).

**Viewability metrics**

| Viewability Metrics | Definition |
|--|--|
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that 50% of the pixels of a video creative are in-view during 2 consecutive seconds. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |

## Reporting - API

The following Video viewability metrics are available via the API in the [Network Video Analytics](../digital-platform-api/network-video-analytics.md), [Network Publisher Video Analytics](../digital-platform-api/network-publisher-video-analytics.md) and [Network Advertiser Video Analytics](../digital-platform-api/network-advertiser-analytics.md) reports:

| Column | Description |
|--|--|
| imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that a video impression is viewable if 50% of the pixels are in-view during 2 consecutive seconds. |
| view_measured_imps | The total number of impressions that were measured for viewability. |
| view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |

The [Video Events Feed](../log-level-data/video-events-feed.md) now has the the following columns for video viewability:

|  |  |
|--|--|
| `view_result` | The Microsoft Advertising viewability measurement result of the impression. Possible values: <br>  1 = VIEW_MEASURED_VIEWABLE <br> 2 = VIEW_MEASURED_NON_VIEWABLE <br> 3 = VIEW_NON_MEASURED <br>For non-impression events, this will be NULL. |
| `view_non_measurable_reason` | The reason an impression could not be measured for viewability. Possible values: <br> 0 = N/A. The impression was measured for viewability <br> 1 = SCRIPT_NOT_SERVED. The viewability script was not served with the creative. For example, on mobile-app inventory. <br> 2 = NO_SCRIPT_CALLBACK. The viewability script was served with the creative, but no callback/event was received. For example, the user left the page before the creative was served. <br> 3 = TECHNICAL_LIMITATION. The viewability script was served and loaded, but was unable to measure for a technical reason. For example, a cross-domain iframe with Flash disabled. |

## FAQ

This section lists out frequently asked questions regarding video viewability.

**Will viewability work on both Microsoft Advertising hosted creatives and third-party hosted creatives?**

Yes, Microsoft Advertising provides viewability measurement across all video creatives for free.

**What happens if I upload a VAST creative?**

Microsoft Advertising adds a VPAID viewability wrapper and will deliver the viewability measurement across players that accept VPAID. The video creative is served as a VAST creative with no viewability measurement to players that only accept VAST.

**Will viewability measurement work on mobile web and mobile app supply?**

Desktop, mobile web and mobile app supply are supported.

**What happens if I upload a VPAID creative?**

Microsoft Advertising includes the VPAID viewability wrapper, thus increasing the number of wrappers on the creative, and the creative will measure viewability across players that allow for VPAID.

**Will it cause latency?**

Using a VPAID wrapper generates some additional latency since the player must first download the VPAID wrapper from Microsoft Advertising CDN (\\150ms). Once the wrapper is downloaded, the time taken to load a video ad with a wrapper will be the same as one loaded without. Viewability components are run asynchronously and do not affect the ad.

**Do I have to do anything to enable viewability for my creatives?**

No, your video creatives are enabled for viewability measurement by default.

**Will viewability restrict reach?**

No, it will not. Microsoft Advertising will serve the viewability script where applicable and the VAST only version of the creative where VPAID is not allowed, to ensure maximum reach.

**How can I optimize to more highly viewable inventory?**

Viewability measurement is included in the [Advertiser Video Analytics Report](../invest/advertiser-video-analytics-report.md) and [Member Video Analytics Report](network-video-analytics-report.md), which provide reporting down to the individual tag/placement or site domain. This enables clients to update targeting to either include or exclude high or poor performing placements.

**How does Microsoft Advertising viewability compare with other third party viewability vendors such as Integral Ad Science, and DoubleVerify?**

The Microsoft Advertising viewability measurement aligns closely with third party vendors and should be used as a helpful proxy to help optimize for higher viewability.
