---
title: Ad Quality Profile - FAQ
description: In this article, find answers to some frequently asked questions regarding Ad Quality Profile.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Ad quality profile - FAQ

## What is an ad quality profile?

Ad quality profiles are used by publishers to determine which creatives are allowed to serve on their inventory. Ad quality profiles can block or allow creatives based on language, technical attribute, parent brand, brand, brand category, and/or buying member. Ad quality profiles can additionally block or allowlist individual creatives. Each ad quality profile has a unique ID on the platform. The ad quality profile incorporates all of the business rules. A creative can get blocked based on any of the aspects that are controlled in the ad quality profile. A seller can change on a given day the specifics of that ad quality profile - so on day 1, ad quality profile 12345 may block brands A, B, and C, and on day 2, it may only block brand B.

## How are ad quality profiles used?

Each seller on Xandr has a member-level ad quality profile. This ID will not change and will be present on every single bid request for that member as the `member_ad_profile_id`. Sellers will also have an impression-level ad quality profile. This may or may not be present, and can apply on a tag, site, publisher, or conditional basis (e.g. users per geo, number of impressions seen per day per user, etc.) The ID of the impression-level ad quality profile will come through in the bid request as `ad_profile_id`. If a creative is blocked by either the member-level ad profile or the impression-level ad profile, the creative cannot serve.
