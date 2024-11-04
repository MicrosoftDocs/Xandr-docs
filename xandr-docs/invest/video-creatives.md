---
title: Microsoft Invest - Video Creatives
description: Host or traffic video creatives through third-party ad servers. Video creatives have higher conversion rates and can be configured in various ways. 
ms.date: 10/28/2023
---

# Microsoft Invest - Video creatives

You can host video creatives with Microsoft Advertising or traffic them through third-party ad servers. Non-linear creatives, such as a non-video overlay creative that is served on top of the player, are not supported.

Video creatives can provide:

- **Higher conversion rates**: Video creatives are capable of gaining the user's attention from start to finish as they are very interactive and engaging compared to display creatives. Additionally, video creatives can be configured in various ways, which only increases their viewability.
- **Flexibility**: Video creatives can be created using various rich media formats.

## Types of video inventory

We support the following video inventory types on our platform, which publishers manage directly:

- **In-Stream Video**: It is played in video players on web pages, as well as CTVs. It can play before, in the middle of, or after other video content. In-stream video creatives can be served by a third-party ad server or hosted on a third-party ad server and served by Microsoft Advertising.
- **Out-Stream Video**: It is played in smart video players that expand when the container is in view as the consumer scrolls through the other content on the web page. Out-stream video is highly flexible and supports a variety of features such as skippability and autoplay. Some of these features can be set on the creative, and some are determined by the player settings. Out-stream can also be configured to play video and/or audio based on the criteria that the publisher has set. It supports HTML5 and works on desktop and mobile inventory.

## VAST and VPAID support

Microsoft Advertising supports Video Ad Serving Template (VAST) and Video Player-Ad Interface Definition (VPAID). Here are some key differences to note between VAST and VPAID:

| Category  | VAST | VPAID |
|:---|:-----|-------|
| **Purpose** | An XML-based video ad serving protocol that provides a uniform way for video content to be transferred from ad servers to video players on web pages. The interaction between the creative and player is unidirectional. Therefore, once the player receives the VAST tag, no other interactions are possible except for the activation of select tracking beacons at appropriate times during creative playback. Metadata is transferred from the ad server to the video player, which includes information about: <br> - which creative should play <br> - the duration of the creative <br> - whether the viewer should skip the creative <br> - the actual URL <br> - how the creative should be rendered <br><br> When a VAST video creative is played, Microsoft Advertising returns a Wrapper VAST response with a URL to the external video ad server. <br>VAST version 2.0 and higher is supported. For more information about VAST, see [IAB VAST Guidelines](https://www.iab.com/guidelines/vast/). <br><br> **Note**: Out-stream video demand can only be delivered with VAST for real-time bids (RTB). | Makes it possible for video creatives and video players to communicate with each other so that advertisers can serve rich, interactive creatives. VPAID is more suited for interactive environments. Examples include: <br> - Selecting different tabs in the creative to see information <br> - Expanding the view and zoom in/out <br> - Filling out a form <br> - Taking a survey <br> - Interacting with elements <br> - Playing games within the creative <br> - VPAID expands the capability of VAST, giving advertisers the ability to leverage the tracking features that VAST offers in conjunction with VPAID's rich media support. For more information about VPAID, see [IAB VPAID Standards](https://iabtechlab.com/standards/video-player-ad-interface-definition-vpaid/).<br><br> **Note**: You can add VPAID-enabled in-stream video creatives on the Microsoft Advertising platform, but we cannot guarantee that they will work with all video players. |
| **Prerequisites** | Video player that supports VAST | Video player that supports VPAID |
| **Ad Format Support** | Supports relatively simple, in-stream video formats that are not executable | Supports interactive, in-stream video formats that are executable such as requiring software logic to be executed |

## Related topics

- [Video Creative Guidelines and Specifications](./video-creative-guidelines-and-specifications.md)
- [Add Creatives in Bulk](./add-creatives-in-bulk.md)
- [Add a Creative](./add-a-creative.md)
- [Supported VAST Features](./supported-vast-features.md)
