---
title: Microsoft Monetize - What to Check if You Suspect a Discrepancy?
description: Explore common causes of reporting discrepancies, investigate time frames, zone differences, measurement units, configuration errors, and ad server variations.
ms.date: 10/28/2023
---

# Microsoft Monetize - What to check if You suspect a discrepancy?

Report discrepancies have a number of common causes. Before you begin a fuller investigation, consider common potential causes like time frames, time zone differences, measurement units, macro configuration errors, and differences in how ad servers count impressions.

Before you file a case, consider the following situations that can create an apparent discrepancy, but are actually the expected result of either a misconfiguration, or of unlike things being compared.

| Potential Cause | Explanation/Resolution |
|---|---|
| The time zone for the two reports is different.<br>**Note**: Be careful: Daylight Savings can cause confusion about time zones. | The advertiser report was pulled in EST, but the network pulled theirs in GMT. This isn't a true discrepancy. |
| The reports don't use the same time frame. | Example: one report is weekly: the other is monthly. This isn't a true discrepancy. |
| Tracking pixels are not in the correct format | Example: a pixel pasted into a browser shows up as an image, but in the Microsoft Advertising UI it is marked as an HTML URL. |
| The third-party impression tracker counts impressions differently than Microsoft Advertising does. | Microsoft Advertising counts an impression when the creative begins to render, but the third-party report counts impressions using an imp tracker placed at the bottom of the placement or page. If the creative doesn't load completely, or the user navigates away before it's fully loaded, the third-party report will show fewer impressions. |
| The `${CACHEBUSTER}` macro isn't implemented or is implemented incorrectly, so ads are being cached and retrieved from the local cache on viewing. | Because cached ad impressions aren't tracked, Microsoft Advertising-reported impressions in this case are significantly higher than impressions recorded in the advertiser's system.<br>You can resolve this problem by ensuring that the `${CACHEBUSTER}` macro is added to all third-party creatives. This ensures that ads are always pulled from an ad server, rather than the user's browser cache. For examples of properly inserted macros for various tag providers, see [Click Tracking](click-tracking.md). If your tag provider is not listed, please reach out to them for assistance. |
| Conversion numbers don't match due to conversion pixel configuration. | Any modification can affect pixel functionality. Double check your pixel implementation, and only use tag managers that do not alter the original pixel code, such as Google Tag Manager. |
| Page drop-offs or slow load times on specific publishers or placements. | Page drop-offs occur when:<br> - a viewer leaves a page before a creative being loaded<br> - something prevents the creative from loading completely (such as a loss of network connection or a crashed browser). <br><br>Discrepancies caused by these problems typically occur when a creative is loaded into a placement at the bottom of a page: in other words, at the end of the normal chain of page load events. When pages load slowly, users are more likely to navigate away before the ad tag loads. Mobile campaigns have a higher likelihood of page drop-off, especially when served over a carrier connection over a wifi connection. |
| "Unknown" domains. | Not all publishers expose their domains in reports. If you see lots of "Unknown" impressions in a Site Domain Report, you can run an [Advertiser Analytics Report](advertiser-analytics-report.md) grouped by seller, publisher, and placement, and compare Microsoft Advertising and third-party reports by publisher and placement. |
| Click numbers don't match due to the `${CLICK_URL}` implementation. | Double-check your `${CLICK_URL}` macro. It’s also very important to insert click macros to both `<script>` and `<noscript>` parts in third-party ad server tags. For more information, see [Click Tracking](click-tracking.md). |
