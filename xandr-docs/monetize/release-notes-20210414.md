---
title: New Ad Quality Technical Attribute
description: Find the release note for the new Ad Quality technical attribute.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# New ad quality technical attribute

**Release date**: April 14, 2021

We've added a new Ad Quality technical attribute. Total Load >4MB is now available to prevent ads greater than 4MB on Chrome browsers. Eligibility of this attribute depends on the default eligibility setting for technical attributes on each member's Ad Quality profile. Most profiles are set to **Eligible**, which means Total Load >4mb will not be enforced by default, but any default setting of **Banned** will enforce the attributes.

For more information, see:

- [Chrome's New Heavy Ad Intervention Policy](https://developer.chrome.com/blog/heavy-ad-interventions)
- [Bidder Error Codes](../bidders/bid-error-codes.md)
- [Network Ad Quality](network-ad-quality-screen.md)
- [Publisher Ad Quality](working-with-publisher-ad-quality.md)
