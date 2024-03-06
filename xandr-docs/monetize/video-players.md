---
title: Video Players
description: Explore video player options, discover optimal uses, and understand Instream and Outstream Video distinctions for effective ad placement.
ms.date: 10/28/2023
---

# Video players

This page describes the Microsoft Advertising video player offerings, as well as ideal use cases and limitations of each player.

## Instream versus outstream video

Instream video refers to video advertising for which publishers provide their own players (usually to house their own content).

Outstream video refers to video advertising that is dependent on a player provided as part of the video placement architecture which has zero footprint and expands as needed to host an ad on the page.

This page concerns the various player options we provide for outstream video (including outstream mediation) when players are not hosted by the publisher.

## Player types and uses

| Player Type | Details | Use Cases |
|---|---|---|
| Flash | This option is set via the playerTechnology options when selecting [Outstream Video Player Options](outstream-video-player-options.md). | desktop, depending on client settings |
| Inline IOS/Javascript VPAID* | The inline player is automatic, unless disabled via [Outstream Video Player Options](outstream-video-player-options.md) or via Microsoft Monetize or the API. (coming soon) | iPhone, iPad |
| HTML5/JavaScript | This option is set via the playerTechnology options when selecting [Outstream Video Player Options](outstream-video-player-options.md). | iOS/iPad and Android (HTML5), desktop |

   > [!NOTE]
   > The JavaScript VPAID player will be included in a subsequent release of Microsoft Advertising video players.
