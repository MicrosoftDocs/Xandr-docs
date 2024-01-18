---
title: Microsoft Monetize - Supported Viewability Standards for Guaranteed Outcomes
description: The article defines viewability standards for guaranteed outcomes—buyer-specific, including media type, viewability definition, and vendor.
ms.date: 10/28/2023
---

# Microsoft Monetize - Supported viewability standards for guaranteed outcomes

The definition for what constitutes a viewable impression varies from buyer to buyer. A chosen standard generally comprises three components: the media type, the viewability definition, and the measurement technology vendor. Guaranteed Outcomes has been built to support any standard made up of those three components, with each standard represented as a generic clearing event. The following clearing events are supported today for Guaranteed Views.

| Clearing Event Name | ID | Viewability Definition | Media Type | Measurement Technology Vendor |
|---|---|---|---|---|
| Views - Standard Display | 2 | IAB (50% of pixels in-view for 1 continuous second) | Display/Banner | Xandr |
| Views - Custom Display - 100pv1s | 6 | 100% of pixels in-view for 1 continuous second | Display/Banner | Xandr |
| Views - Standard Video | 8 | IAB (50% of pixels in-view for 2 continuous seconds) | Video | Xandr |
| Views - Custom Video - 100pv50pd | 9 | 100% of pixel in-view for 50% of the duration of the video, with audio on (if instream) or audio off (if outstream) | Video | Xandr |

## Related topic

[Guaranteed Outcomes](guaranteed-outcomes.md)
