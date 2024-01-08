---
title: Microsoft Monetize - Supported VAST Features
description: Xandr supports VAST features, including skipoffset and ad verification, with compatibility across VAST versions 2.0 through 4.0, but implementation depends on the publisher's support for the specific VAST version.
ms.date: 10/28/2023
---

# Microsoft Monetize - Supported VAST Features

The Xandr platform supports a variety of VAST features such as skipoffset and ad verification. Our VAST features are compatible with certain VAST versions. VAST versions 2.0 through 4.0 support backwards feature compatibility. However, if a publisher doesn't support a particular VAST version, then implementation of certain features on that publisher's player won't be possible.

The following table provides feature descriptions and indicates the VAST versions that are supported:

| VAST Feature | Description | VAST 2.0 | VAST 3.0 | VAST 4.0 | VAST 4.1 | VAST 4.2 |
|---|---|---|---|---|---|---|
| Ad Verification | Enables the video player to provide requested details about ad interaction and playback using JavaScript and Flash resources. At least one JavaScript resource or executable resource must be provided. | Not Supported | Not Supported | Not Supported | Supported | Supported |
| SkipOffset | Sets the number of seconds that a video or audio creative is allowed to play before it can be skipped. The default value is null. | Not Supported<br><br>**Note**: VPAID can be used as a workaround. | Supported | Supported | Supported | Supported |
| Universal Ad ID | Unique creative identifiers registered with AD-ID®, Clearcast, or a similar program. | Not Supported | Not Supported | Not Supported | Supported<br><br>**Note**: Only one universal ad ID is supported. | Supported<br><br>**Note**: Multiple universal ad IDs are supported. |
| Viewable Impression Tracker | Tracks viewable impressions. | Not Supported | Not Supported | Not Supported | Supported | Supported |

## Related topics

- [Video Creatives](video-creatives.md)
- [Audio Creatives](audio-creatives.md)
- [Add a Creative](add-a-creative.md)
