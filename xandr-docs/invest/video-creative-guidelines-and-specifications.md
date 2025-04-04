---
title: Microsoft Invest - Video Creative Guidelines and Specifications
description: This article provides guidelines and specifications for video creatives.
ms.date: 10/28/2023
---

# Microsoft Invest - Video creative guidelines and specifications

To serve on the Microsoft Advertising platform and other third-party platforms, all video creatives must adhere to the guidelines and specifications listed here, our creative standards, and any other guidelines that may apply.

Adhere to these general specifications when creating video creatives:

- The file size limit is 1.8 GB for hosted video creatives.
- The recommended minimum bit rate is 2500kbps.
- The recommended minimum video dimensions are 1280px x 720px.
- The video creative must be created using one of the following file types: 3G2 (3GPP2), 3GP (3GPP), Advanced Systems Format (ASF), Audio Video Interactive (AVI), F4A, F4B, F4P, F4V, FLV, M2V, M4V, MKV, MOV, M4P, MPE, MPEG, MPEG-2 (MP2), MPEG-4 (MP4), MPG, MPV, OGG, OGV, QuickTime (QT), RM, SWF, TS, VOB, WebM, and Windows Media Video (WMV).
- VAST version 2.0 and higher is supported.

## Specifications for hosted video creatives

Adhere to these specifications when creating hosted video creatives:

| Size (px) | Bit Rate (kbps) |
|:---|:---|
| 2160 | 30000 |
| 1280 | 8000 |
| 1080 | 7000 |
| 720 | 2500, 2000, 1700, 1100, and 600 |
| 432 | 1700, 1500, 1000, and 500 |

## Guidelines and specifications for third-party video creatives

Adhere to these guidelines and specifications when creating video creatives that will be trafficked through a third-party ad server:

- External VAST ad servers must submit content to our VAST Check functionality before it can be saved.
- There are no size or format restrictions on video creatives served by external ad servers.
- If serving VAST video creatives on Google inventory, their duration should be a maximum of 15 or 30 seconds. If you want to serve video creatives over 15 seconds in duration, we recommend that your creative contain the skippable element.
- Make sure that the video creatives included in your VAST document are transcoded using the FLV, MP4, and WebM file types.
- Multiple bitrates should be provided for in-stream video creatives that have been transcoded using the FLV, MP4, and WebM file types. The following bitrates are recommended:
  - 500kbps (optimized for mobile devices on cellular connection and required by many mobile SSPs)
  - 1200kbps
  - 2500kbps (optimized for high speed connections)
- Use secure tags in all cases. If you are trafficking VPAID creatives, make sure to properly secure every referenced file.
- Ensure that there is no invalid or unsupported character present in the VAST URL as well as in the 3rd party segments attached to the creative. For example,
  - This is the set of valid VAST characters: `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-._~:/?#[]@!$&'()*+,;=.`
  - This is a set of common invalid characters: `|, <, >, ^, {,}.`
- Additionally:
  - If there are curly brackets `{ }` present in the VAST URL or segment, then they **must** have `$` in front of the bracket.
  - Ensure that there is no double `%` present in the VAST URL or segment.

> [!IMPORTANT]
> Since September 2020, Chrome has introduced a new [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) that monitors ad iframes and may redirect them to an error page (Heavy ad intervention) if resource use exceeds specified criteria. Video advertisements, in particular, may be vulnerable to this intervention, which impacts iframes that load more than 4 MB of data.
>
> If a creative satisfies any of the following criteria, it is considered heavy:
>
> - The main thread is used for more than 60 seconds in total.
> - In any 30 second window, the main thread is used for more than 15 seconds.
> - More than 4 MB of network bandwidth is consumed
>
> It is recommended that the creative is compliant with the technical specifications detailed above.

## Related topics

- [Video Creatives](./video-creatives.md)
- [Add a Creative](./add-a-creative.md)
- [Add Creatives in Bulk](./add-creatives-in-bulk.md)
- [Supported VAST Features](./supported-vast-features.md)
