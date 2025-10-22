---
title: Creative Approval - Implementation
description: Learn what is an ad profile and how many elements it consists of. Also, this page covers what is a trusted brand and banned brand.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Creative Approval - Implementation

> [!NOTE]
> This document is for informational purposes only. It explains how the sell-side does creative approval. Bidders have no active role in this process.

Xandr's UI allows publishers to review creatives and approve on a case by case basis. In order to approve creatives, a publisher must create an ad profile. If no default ad profile is created, all creatives will be able to run on publishers' domains.

An ad profile consists of three elements: members, brands, and creatives. To reduce the number of creatives that need to be explicitly approved, you can use member and brand level approval standards. When setting up the profile, choose "trusted" for members and brands only if you believe their ads will always be acceptable. If a brand is selected as "trusted," then all creatives of that brand will automatically run by default. However, the publisher can review the creatives and ban individual creatives of the trusted brand.

If a brand is banned, then no creatives of the banned brand will be shown. Once a brand is banned, you will still have the ability to approve a specific creative from that brand. However, if a buyer is banned in this same ad quality section, approving a specific creative from this buyer will still not allow it to serve. In the case of buyers, once they are banned, none of their creatives can be served even if a specific creative is approved.

Approving and banning at the creative level is the most granular way to set quality standards. To review the specific creatives, run a search for creatives within a specific criteria. A preview of the creative will appear and you can choose to click approve or ban.
