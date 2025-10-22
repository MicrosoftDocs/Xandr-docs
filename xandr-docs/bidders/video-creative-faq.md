---
title: Video Creative FAQ
description: Learn about Xandr's video ad capabilities—supporting in-stream and in-banner videos. Understand VAST, VPAID, and technical specifications. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Video creative FAQ

## What types of video can I run on Xandr?

You can run in-stream and in-banner video on the Xandr platform.

## What is in-stream video?

In-stream video creatives are played in video players on web pages. They are played before, in the middle of, or after other video content, and use VAST XML to ensure proper rendering in the players.

Xandr supports video creatives served by a third-party video ad server that uses external VAST XML for rendering in players. Here Xandr returns a Wrapper VAST response with a URL to your external video ad server.

For video hosting support, reach out to your account managers to enable VAST creative transcoding and hosting functionality.

## What is in-banner video?

In-banner video creatives are played in banner placements rather than in video players. The video creative must be served along with the video player. Xandr uses JWPlayer as the default in-banner video player but you can use any player of your choosing depending on how you set up your in-banner media subtype creative templates. The banner placement may accommodate in-banner video creatives, if allowed by the publisher.

For the JW Player's technical specifications, see [https://www.longtailvideo.com/players/jw-player/tech-specs](https://www.longtailvideo.com/players/jw-player/tech-specs).

## What is VAST?

VAST stands for Video Ad Serving Template. It is an XML-based video ad serving protocol that provides a uniform way for video content to be transferred from ad servers to video players on web pages. For more
details about VAST, see the Interactive Advertising Bureau's VAST documentation at [https://www.iab.net/guidelines/508676/digitalvideo/vast](https://www.iab.net/guidelines/508676/digitalvideo/vast).

## What are the technical specifications for in-stream (VAST) and in-banner videos?

**Video creatives served by a third-party ad server:**

- Xandr supports all external VAST ad servers.
- There are no size or format restrictions on videos served by external ad servers.
- Companion banners will serve only if the video player on the page supports companions.

**Video creatives hosted on a third-party CDN but served by Xandr:**

Xandr supports third-party hosted VAST XML for in-stream video creatives. In-banner video creatives will also be required to have the actual creative file(s) hosted on a third-party CDN.

## What is Outstream video?

Outstream is a video format used by lots of clients and will be helpful to include so that users can understand what the expected usage of this format is compared to In-stream.

## Does Xandr support VPAID?

You can add VPAID-enabled in-stream video creatives to Xandr, but we cannot guarantee that they will work with all video players. Only certain video players can support the VPAID protocol; our supply has to indicate if their players can support it. For more information about VPAID (Video Player Ad-Serving Interface Definition), see the Interactive Advertising Bureau's VPAID documentation at [https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vpaid](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vpaid).

## Does Xandr support in-stream (VAST) videos on secure (https) inventory?

Yes. Xandr supports in-stream (VAST) videos on secure inventory. VAST creatives on secure inventory can be submitted for auditing using the regular auditing process.

## Will my in-stream (VAST) videos always run on suitable inventory?

Yes. In-stream video creatives will run only on placements that are explicitly enabled for VAST video. To get the widest reach for your in-stream video campaigns, we recommend setting only minimal inventory targeting.

## What inventory is available for in-stream (VAST) videos?

In-stream video inventory from StickyADS, SpotXchange, LiveRail, AdapTV, Rubicon and Google Ad Exchange is available on Xandr's platform.

## What are ad pods?

Ad pods are a way to specify multiple ad elements which are to be sequenced together and played back to back within a single ad break.
Sellers are able to indicate the duration they want for their ad pods and the maximum number of ads they want to play within a single pod.

## What is VMAP?

VMAP stands for Video Multiple ad Playlist. It is an IAB specification for an XML template that video content owners can use to describe the structure for ad inventory insertion when they don’t control the video
player or the content distribution. For ad pods, Xandr outputs our response in VMAP instead of VAST.

## What does the error message "Heavy ad intervention" mean?

This error message signifies that the resource use for a creative exceeds one or more threshold(s) set by [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) introduced by Chrome. Since September 2020, Chrome has introduced a new [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) that monitors ad iframes and may redirect them to an error page (Heavy ad intervention) if resource use exceeds specified criteria. Video advertisements, in particular, may be vulnerable to this intervention, which impacts iframes that load more than 4 MB of data.

If a creative satisfies any of the following criteria, it is considered heavy:

- The main thread is used for more than 60 seconds in total.
- In any 30 second window, the main thread is used for more than 15 seconds.
- More than 4 MB of network bandwidth is consumed

It is recommended that the creative is compliant with the technical specifications detailed above.
