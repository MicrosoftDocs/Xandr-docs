---
title: Microsoft Monetize - Viewability FAQ
description: Explore Microsoft Advertising Viewability for insights, optimize strategies, and boost digital visibility by locating essential metrics.
ms.date: 10/28/2023
---

# Microsoft Monetize - Viewability FAQ

## Viewability data

The following questions address where to find Microsoft Advertising viewability data and the key metrics associated with it.

### In reporting, what is the definition used for viewable impressions?

Our reporting is based on the IAB standard definition: 50% of the area of the creative (30% of the area of a large size creative) in view for 1 continuous second.

### Are other viewability metrics available, such as "viewable for less than 5 seconds"?

Adserver clients can now use the Engagement Metrics report to access a wide variety of metrics. We are focused on making the most actionable viewability data widely and easily available.

### Microsoft Advertising Viewability Script Functionality

The following questions address the Microsoft Advertising viewability script, how it works, what it measures, and its limitations.

### What methods does Microsoft Advertising use to measure viewability?

Microsoft Advertising viewability employs a best-in-class hybrid measurement methodology combining Page Geometry and Browser Optimization. When used in tandem, this hybrid method allows us to reliably measure viewability of most impressions.

### Does Microsoft Advertising viewability use projection-based methods to report on viewable impressions?

No, all reporting data is based on direct measurement.

### What types of inventory are supported by Microsoft Advertising viewability?

The Microsoft Advertising viewability script is currently enabled for web, mobile web, and in-app (SDK) inventory. In addition to our SDK, we support viewability for the Microsoft SDK and OMSDK.

OMSDK in-app viewability measurement is supported as follows:

- Microsoft Advertising's Mobile SDK version 4.9 and above supports OMSDK display
- Microsoft Advertising's Mobile SDK version 5.0 and above supports OMSDK native
- Microsoft Advertising's iOS Mobile SDK version 6.1 and above supports OMSDK video
- Microsoft Advertising's Android Mobile SDK version 6.1.1 and above supports OMSDK video

Viewability measurement on the following native inventory is supported:

- Sellers on AST v0.11 and above
- Sellers supporting OpenRTB 'jstracker' field. (Integration is required with Microsoft Advertising to enable measurement)

### What types of creatives does Microsoft Advertising viewability support?

The Microsoft Advertising viewability script is currently enabled for all banner, native, and video creatives. For more information about how viewability works for video, see [Video Viewability](video-viewability.md).

### Why would some supported inventory not be measurable?

The possible causes could be:

- If JavaScript is not enabled in a user's browser, the viewability script can't measure the impression.
- The viewability script may not be able to locate the creative. If the creative cannot be located within 5 seconds, the impression is not considered view-measured. To avoid this problem, make sure the script is served close to the actual creative content, particularly if you have a custom tag implementation.
- In rare cases, some very old browsers won't support viewability measurement, for example if the ad is loaded in a cross-domain iFrame configuration.
- Finally, network latency or the user simply closing the browser too quickly can prevent the script from capturing data required for measurement.

### What impression types are not measured by Microsoft Advertising?

"blank" and "default"

### When does the Microsoft Advertising viewability script start measuring? Will the script wait for the creative to load before measuring?

The Microsoft Advertising viewability script waits for the creative content to load before measuring for viewability. This may be a source of discrepancies with other measurement vendors, in particular when the creative content is a large file.

### Will the Microsoft Advertising viewability script slow down my page load or otherwise impact my page content?

No. The script, which is approximately 20KB, is served from a globally distributed CDN that is optimized for speed and reliability. All script calls are made asynchronously.

The viewability script is tested continuously across all major browsers and operating systems to ensure, among other things, that it does not impact the page content. The script has been in use since 2007, and extensive real-world usage confirms the ad viewer’s experience is not impacted.

### How does the Microsoft Advertising viewability script determine whether a human is viewing the ad?

The Microsoft Advertising Platform has robust policy and filtering for non-human and other invalid traffic.

Checks are applied to all platform inventory before an impression is auctioned, so the viewability script itself does not need to monitor or check for non-human or invalid traffic.

The script will however check for inactive users. If there is no keyboard, mouse, scroll or other activity for 60 seconds, then the script considers the user to be inactive. Any ads served, for example by an auto-refresh placement, will be considered non-viewable until an activity event is detected.

## Viewability rate results

The following questions address how to interpret your reported viewability rates in Microsoft Monetize.

### Why do I get a low viewability rate on placement X?

The Microsoft Advertising ad-viewability technology has been intensively tested for several years, so you can trust the viewability data that is provided.

When a placement is below the fold, after the content, or at the bottom of the page, the banner is unlikely to be viewable.

When a placement is above the fold, it is not always viewable, because:

- Some users leave the page within the first seconds after the page is loaded. If the ad is in-view for less than one second, it is not viewable.
- Some users scroll quickly to the content, so the top of the page becomes non-viewable and the 1 second threshold is not reached.
- High banners are often partially viewable (like 300x600), but in case fewer than 50% of pixels are viewable, the banner is not viewable.
- The page is automatically refreshed, while it is opened in a hidden tab or window.

### Why is my viewability rate with vendor X higher than with Microsoft Advertising?

- What is the vendor's measurement rate?
  - Compare it with our view-measurement rate in reporting. High measurement rates are usually more reliable.
- Does vendor X measure the banner object or the placement?
  - The IAB's recommendation is to measure the banner object, not the placement.
  - We measure the object: the banner is not viewable if the object is not loaded.

### Why do I get a low viewability rate on creative X?

It could be any of the following:

- Is the creative working correctly?
- Is it rendering?

### Related topics

- [Introduction to Viewability](introduction-to-viewability.md)
- [Reporting on Viewability](reporting-on-viewability.md)
