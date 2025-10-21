---
title: Microsoft Monetize - Video Creative Best Practices
description: This page provides a list of best practices to ensure maximum delivery and success for your VAST creatives on the Microsoft Advertising platform. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Video creative best practices

This page provides you with a list of best practices, in a question-answer format, to ensure maximum delivery and success for your VAST creatives on the Microsoft Advertising platform.

## Has the creative passed the Microsoft Advertising platform audit?

If not, the creative will be ineligible to serve on any SSP inventory. See [Creative Standards](creative-standards.md) for more information about audit.

## Has the creative passed SSL audit?

If not, the creative will not serve on Google Ad Manager inventory and will see limited delivery other SSP inventory. See  [Creative Standards](creative-standards.md) for more information about audit.

## Is the creative duration longer than 60 seconds?

This can limit reach because most supply sources will cap at 30 or 60 seconds. However, if your creative must be longer than 60 seconds, please reach out to your Microsoft Advertising representative.

## Are you using the correct tags?

Make sure to use a **ptv** tag instead of a **tt** tag while running a debug auction for video creatives. For more information regarding debug auctions, see [Understanding the Debug Auction](understanding-the-debug-auction.md).

``` 
https://secure.adnxs.com/ptv?id=[TAG_ID]&debug_member=[BUYER_MEMBER_ID]&dongle=[PASSWORD] 
```

## Are your video files transcoded into a variety of bitrates?

It is recommended that you transcode video files into a variety of bitrates to ensure there is no latency in uploading the file. Some exchanges (for example, Google Ad Manager) have latency requirements and will fail creatives that are too large to support slower internet connections. For more information, see [Video Creative Guidelines and Specifications](video-creative-guidelines-and-specifications.md).

## Is your creative VPAID?

Microsoft Advertising will only match VPAID creatives to VPAID-enabled placements, limiting reach.

## Are you using both VAST and in-banner creatives in the same line item or campaign?

Avoid using both VAST creatives and in-banner or interstitial video creatives within the same video line item or campaign. An in-banner or interstitial video creative will not serve when you target by position: Pre-Roll, Mid-Roll, or Post-Roll.

## Have you included all the recommended formats in your VAST XML file?

Ensure that any VAST XML includes at least three formats -- FLV, MP4, and WebM. Not including the recommended formats will limit delivery.

## Does your ad server allow Microsoft Advertising VAST check domains?

Ensure that your ad server allows Microsoft Advertising VAST check domains. VAST check may fail otherwise. Please reach out to your Microsoft Advertising representative for additional domain detail if necessary.

## Have you included all necessary query string macros in your VAST tag?

Microsoft Advertising automatically inserts the click URL into the XML wrapper of all VAST creatives. You are not required to add the click macro and click testing is not required. However, you should manually insert the Microsoft Advertising CACHEBUSTER macro.

## What does the error message "Heavy ad intervention" mean?

This error message signifies that the resource use for a creative exceeds one or more threshold(s) set by [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) introduced by Chrome. Since September 2020, Chrome has introduced a new [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) that monitors ad iframes and may redirect them to an error page (Heavy ad intervention)if resource use exceeds specified criteria. Video advertisements, in particular, may be vulnerable to this intervention, which impacts iframes that load more than 4 MB of data.

If a creative satisfies any of the following criteria, it is considered heavy:

- The main thread is used for more than 60 seconds in total.
- In any 30 second window, the main thread is used for more than 15 seconds.
- More than 4 MB of network bandwidth is consumed.

It is recommended that the creative is compliant with the technical specifications detailed above.
