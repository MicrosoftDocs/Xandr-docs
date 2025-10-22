---
title: Introduction to Video Inventory and Formats
description: Learn about different types of creatives like In-stream video, out-stream video, in-banner video, VAST, VPAID, MRAID and VMAP in this module.     
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---


# Introduction to video inventory and formats

This article explains about different types of creatives, VAST protocol, VPAID and two types of VPAID modules, API application like MRAID, and VMAP which is a form of “ad podding.”

## In-stream video

In-stream video creatives are played in video players on web pages. They are played before, in the middle of, or after other video content, and use VAST XML to ensure proper rendering in the players.

## Out-stream video

Out-stream video ads are those that are embedded within the body of an article, mostly set to auto-play when the reader reaches the part of the page that contains the ad. The sound is usually not activated unless the reader hovers over the ads with their mouse.

## In-banner video

In-banner video creatives are played in banner placements rather than in video players. The ad buyer must serve the video player code and the VAST video creative together.

## VAST

VAST stands for Video Ad Serving Template. It is an XML-based video ad serving protocol that provides a uniform way for video content to be transferred from ad servers to video players on web pages. VAST allows for linear video creatives to be served without interactivity. VPAID modules can be included within a VAST document to facilitate interactivity.

Pure linear VAST (without VPAID modules) do not allow the buyer to measure viewability, but do allow the measurement of starts, quartile completions, and completed views. Pure linear VAST is common in mobile video. For more details about VAST, see the Interactive Advertising Bureau's VAST documentation at [IAB Guidelines for VAS](https://www.iab.com/).

## VPAID

VPAID stands for Video Player Ad-Serving Interface Definition. There are two types of VPAID modules, JavaScript (.js) and Flash (.swf). A VPAID module  allows a buyer to render JavaScript or Flash on the page in order to:

- create highly interactive video ad creatives

- measure viewability and verify player attributes

For more information about VPAID, see the [IAB Guidelines for VPAID](https://www.iab.com/).

## MRAID

Mobile Rich Media Ad Interface Definitions (MRAID) is a common API (Application Programming Interface) that allows advertisers to create HTML5 and JavaScript ads that function seamlessly with the app in which they are running. It allows users to expand and resize ads, and access the device’s other features, thus creating a rich, more interactive environment in which to display ads, instead of siloing static banners in small areas of the screen.

For more information regarding MRAID, see our [MRAID and Mobile Video Tutorial](mraid-and-mobile-video-tutorial.md) or the [IAB Guidelines for MRAID](https://www.iab.com/).

## VMAP

Video Multiple Ad Playlist (VMAP) is a form of “ad podding.” It allows sellers to create commercial breaks, similar to linear broadcast TV, and is mostly used in long-form content. VMAP is designed to produce rules around which types of ads can be played together and how they interact with one another. For example, VMAP can be configured to prevent ads from competitors (e.g. BMW and Audi) from playing directly next to one another.

For more information, see the [ IAB Guidelines for VMAP](https://www.iab.com/).
