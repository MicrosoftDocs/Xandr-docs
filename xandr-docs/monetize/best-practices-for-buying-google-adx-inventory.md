---
title: Microsoft Monetize - Best Practices for Buying Google Ad Manager Inventory
description: Learn about general guidelines to target inventory in this page. This page also talks about Creative guidelines that are required for Google Ad Manager. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Best practices for buying Google Ad Manager inventory

This page provides recommendations for maximum ad campaign success when targeting Google Ad Manager inventory.

## General

The following are general guidelines to target inventory:

- Create a separate line item or campaign targeting Google Ad Manager(181). This is recommended, but not required.
- Make sure to turn off all inventory quality settings by setting your **Inventory Quality** Targeting to **Serve on any inventory**.
- The VAST tag must include the following formats since Google Ad Manager can request any of them on a bid request:
  - H.264 (MP4)
  - FlashVideo (FLV)
  - WebM
- The skip offset must be 5 seconds, otherwise the bid will be filtered out in Google Ad Manager's auction.

## Creative guidelines

The following are guidelines specific to creative standards required for Google Ad Manager:

- Must be SSL compliant. Serving on secure inventory is selected by default. Do NOT make any changes to the setting when you are creating a new creative.

- Click the **Run Check** button to have our VAST check scan your XML document. For more details, see [VAST Check](vast-check.md).

  For more information about adding in-stream video creatives, see [Add a Creative](add-a-creative.md) and [Upload a Hosted Video Creative](upload-a-hosted-video-creative.md).

## Campaign targeting

- Category targeting is possible for video, but it is not reflected in reporting.

- You can target Google Ad Manager inventory by position, but it is NOT recommended. In the **Video** section under **Targeting**, leave the default **Any position** selected.

  For more information about video targeting, see [Video Targeting](video-targeting.md). (For Deals targeting, see [Video Player Targeting](video-player-targeting.md))

## Related topics

- [Buying Video Inventory](buying-video-inventory.md)
- [Video Player Targeting](video-player-targeting.md)
- [Upload a Hosted Video Creative](upload-a-hosted-video-creative.md)
- [VAST Check](vast-check.md)
