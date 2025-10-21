---
title: Microsoft Monetize - Companions
description: Explore how companions, often in standard banners or rich media, enhance video ad experiences, making them more creative. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Companions

A companion is a creative that is commonly displayed in the form of a standard banner or rich media. It can also wrap the video ad experience. Companions are supported on VAST version 2.0 and higher.

Companions are typically served with linear or non-linear creatives. The following rendering modes can be used to indicate when and where the companion should display:

| Rendering Mode | Description |
|--|--|
| End-Card | The companion is rendered after the video playback has stopped. The companion's dimensions should match the dimensions of the video or audio creative. |
| Concurrent | The companion is rendered alongside the video or audio creative for the entire duration of the video playback. |
| Default | Depending upon the player's default behavior, the companion will either be rendered after the video playback has stopped (end-card) or alongside the video or audio creative for the entire duration of the video playback (concurrent). |

> [!NOTE]
> Rendering modes are only supported on VAST versions 4.1 and 4.2.

## Related topics

- [Video Creatives](video-creatives.md)
- [Audio Creatives](audio-creatives.md)
- [Add a Creative](add-a-creative.md)
