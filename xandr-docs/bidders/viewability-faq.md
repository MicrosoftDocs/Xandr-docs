---
title: Bidders - Viewability FAQ
description: Explore FAQs on viewability metrics, methods, troubleshooting. Check Console reporting for reliable data. Ensure optimal creative functionality.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Viewability FAQ

This page answers frequently asked questions you might have about viewability.

## Viewability data from Xandr

### How many impressions does Xandr's viewability measure per day?

Xandr measures viewability on over 10 billion impressions per day.

### Where can I see viewability data?

Viewability metrics are available from the [Report Service](report-service.md).

### In Xandr reporting, what is the definition used for viewable impressions?

Our reporting is based on the IAB standard definition: 50% of the area of the creative (30% of the area of a large size creative) in view for 1 continuous second.

### Has viewability reporting always been available?

We were not measuring all impressions prior to April 15, 2015. Therefore if you run a report that includes data from before that date, you may see a lower-than-expected Measurement Rate.

### Are other viewability metrics available, such as "viewable for less than 5 seconds"?

While our measurement script is capable of collecting more granular metrics such as duration, we have not yet built this functionality in reporting. Although more granular metrics can be useful for gaining deeper insights, we are focused on making the most actionable viewability data widely and easily available.

Stay tuned for updates as we continue to develop viewability reporting.

## Xandr viewability script functionality

### What methods does Xandr use to measure viewability?

Our viewability employs a best-in-class hybrid measurement methodology combining Page Geometry and Browser Optimization. When used in tandem, this hybrid method allows us to reliably measure viewability of most impressions.

### In reporting, how does the Xandr view-measurement rate compare to other measurement vendors?

**View-Measurement Rate** from Xandr is not directly comparable to third-party measurement vendors. The rate is calculated as the percentage of impressions measured for viewability out of the total number of impressions (View-measured Impressions / Total Impressions). The discrepancy arises from the Total Impressions metric.

Due to the native integration of Xandr viewability, the number of total impressions reported is the number of **ALL** transacted impressions; whereas, a third-party will only count impressions when their script is successfully loaded. The third-party impressions count will almost always be lower that the Xandr impression count.

The **View-Measured Impressions metric**, on the other hand, is comparable to the methodology used by other measurement vendors as it is calculated based on impressions where the viewability script loaded successfully.

The result is that the View-Measurement Rate will typically be lower from Xandr, due to the higher Total Impression count. The lower rate is a result of using different methods for counting total impressions and is not an indicator of the technical quality of the measurement.

### Does Xandr's viewability use projection-based methods to report on viewable impressions?

No, all reporting data is based on direct measurement.

### What types of inventory are supported by Xandr viewability?

The Xandr viewability script is currently enabled for web, mobile web inventory and in-app inventory on Xandr's SDK. Viewability measurement on the following native inventory is also supported:

- Sellers on AST v0.11 and above
- Sellers supporting OpenRTB 'jstracker' field (Integration is required with Xandr to enable measurement)

In addition to the supported inventory supply types, the script is continuously tested (over 300,000 tests run every day!) on the following platforms and browsers:

- Windows platform
  - Internet Explorer
  - Firefox
  - Chrome
  - Safari
  - Opera
- Mac OS platform
  - Safari
  - Firefox
  - Chrome
  - Opera
- iOS platform
  - Safari
- Android platform
  - Chrome
  - Android browser

### What types of creatives are supported in Xandr viewability?

The Xandr viewability script is currently enabled for all creatives with Media Type = Banner and Native. Xandr also supports Video creatives.

### Why isn't the Xandr viewability script able to measure an impression on supported inventory and creative formats?

The possible causes could be:

- **JavaScript is not enabled in the internet browser of the user.** If JavaScript is not enabled, the impression will not be considered 'view-measured'.
- **The script is unable to locate the creative within five seconds.** If JavaScript is enabled, the first action the script takes is to locate the creative. If the script is unable to locate the creative, and at least 5 seconds have passed, the impression is not considered 'view-measured'. It is therefore important to ensure that the script  is served close to the actual creative content. This should be the normal case, though some custom implementations of Xandr's tags could prevent the script from being able to locate the creative.
- **Flash is disabled.** In certain scenarios, Flash must be enabled. In cross-domain (aka "unfriendly") IFrames on Webkit browsers (Chrome and Safari), the script requires Flash to measure if the creative is in-view. This is particularly a limitation on mobile-web inventory, since Flash is generally not available on mobile devices.

### What impression types are not measured by Xandr?

Our viewability script does not measure impression type blank, and default.

### What can I do to improve measurement rates?

Publishers should use javascript tags or "friendly" IFrames wherever possible. When the viewability script is served into "unfriendly" iFrames, the requirement for Flash (particular on mobile) will decrease measurement success.

### At what point does Xandr's viewability script start measuring? Will the script wait for the creative to load before measuring?

Our viewability script waits for the creative content to load before measuring for viewability. This may be a source of discrepancies with other measurement vendors, in particular when the creative content is a large file.

### Will Xandr's viewability script slow down my page load or otherwise impact my page content?

No. The size of the script is approximately 20KB, and it is served from a globally distributed CDN, optimized for speed and reliability. All calls made by the script are made asynchronously.

The script is tested continuously across all major browsers and operating systems to ensure, among other things, that it does not impact the page content. The script has been in use for many years, and we have drawn on all of that experience to ensure that we do not interfere with the user's experience.

### What does Xandr's viewability script monitor for in order to measure viewability?

Our viewability script continuously monitors system events and browser statuses to determine whether an ad is in-view. Some of these events and statuses include:

- Window focus / unfocus
- Tab switches
- Page scroll
- Page resize
- Browser zoom
- Screen saver start
- Banner object load / unload
- Mouse / keyboard activity / inactivity

### How does Xandr's viewability script determine whether a human is viewing the ad?

Xandr's platform has robust policy and filtering for non-human and other invalid traffic. See [Inventory Auditing](inventory-auditing.md) for more details.

These checks are applied to all platform inventory before an impression is auctioned, so the viewability script itself does not need to monitor or check for non-human or invalid traffic.

The script will however check for inactive users. If there is no keyboard, mouse, scroll or other activity for 60 seconds, then the script considers the user to be inactive. Any ads served, for example by an auto-refresh placement, will be considered non-viewable until an activity event is detected.

## Viewability rate results

### Why do I get a low viewability rate on placement X?

Xandr's ad-viewability technology has been extensively tested for several years, so you can trust the viewability data that is provided.

When a placement is below the fold, after the content, or at the bottom of the page, the banner is unlikely to be viewable.

When a placement is above the fold, it is not always viewable, because:

- Some users leave the page within the first seconds after the page is loaded. If the ad is in-view for less   than one second, it is not viewable.
- Some users scroll quickly to the content, so the top of the page  becomes non-viewable and the 1 second threshold is not reached.
- Tall banners are often partially viewable (like 300x600), but if fewer than 50% of pixels are viewable, the banner is not viewable.
- The page is automatically refreshed while it is opened in a hidden tab or window.

### Why is my viewability rate with vendor X higher than with Xandr?

- What is the vendor's measurement rate for this campaign / site?
  - Compare it with our view-measurement rate in the Console reporting. High measurement rates are usually more reliable.
- Does vendor X measure the banner object or the placement?
  - The IAB's recommendation is to measure the banner object, not the placement.
  - We measure the object, the banner is not viewable if the object is not loaded.

### Why do I get a low viewability rate on creative X?

It could be any of the following:

- Is the creative working correctly?
- Is it rendering ?
- Do you have a backup image for flash creatives on mobile?

## Related topic

[Introduction to Viewability](../monetize/introduction-to-viewability.md)
  