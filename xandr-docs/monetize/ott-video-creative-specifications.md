---
title: Microsoft Monetize - OTT Video Creative Specifications
description: Explore technical specifications of Over-the-Top (OTT) videos, focusing on the requirements for premium digital content.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - OTT video creative specifications

An OTT (Over-the-Top video) creative is designed to be displayed before, after, or during in-stream video content delivered over the internet. Typically, OTT video content is played on a Connected TV (CTV). CTV can include a TV that is connected to the internet via an external device (for example a Blu-Ray player or a gaming console), or a Smart Television. OTT content is generally viewed by engaged users watching high-quality video content in a full-screen mode. OTT advertising is considered premium digital video inventory. It's the highest-quality format you can purchase programmatically, with completion rates as high as 90%. To uphold the quality of the viewing experience, creative requirements for OTT inventory are stricter than standard web-based video supply.

## Recommended OTT video creative specifications

- Creative Type: VAST
- Media Type: MP4
- Minimum Bitrate: 2,000 kbps
- Minimum Resolution: 1280x720 (sometimes notated as 720p)
- Duration: 15 or 30 seconds

VPAID is not supported for OTT placements, and FLV, WebM and VPAID media types will not be eligible to serve on OTT inventory.

## OTT video creative limitations

- Viewability reporting is not supported for OTT creatives. However, impression, quartile, and completion tracking are available. For more information, see [Measurement of Video Viewability using VPAID Wrapper](video-viewability.md).
- Do not include segment pixels in your inline VAST code, because they will not load in the SDK.
- To use creatives of a different duration than 15 or 30 seconds, reach out to the publisher.

## Checking your creative's specifications

To view the specifications of a particular creative in the XML code, paste its third-party VAST URL or the Microsoft Advertising hosting URL (`https://ib.adnxs.com/cr?id=CREATIVE_ID&format=vast` where CREATIVE_ID is the identifier for your creative) into a browser. The VAST Check functionality in Monetize will also verify that all creatives meet the requirements for duration, format, OTT bitrate, and resolution.

## Publisher-specific OTT creative requirements

Some publishers, such as Hulu and ESPN, have specific requirements and processes. Your creatives should meet the specific requirements for those publishers as well as the base requirements described in this topic.

## Related topics

- [Buying ESPN Inventory](buying-espn-inventory.md)
- [Buying Hulu Inventory](buying-hulu-inventory.md)
