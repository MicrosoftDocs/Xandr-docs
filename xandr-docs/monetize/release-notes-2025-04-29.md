---
title: April 30, 2025 - Deprecation of public Prebid Cache
description: Explore the April 30, 2025 release, Deprecation of public Prebid Cache
ms.topic: release-notes
ms.date: 12/12/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# December 12, 2025 - Upcoming deprecation of public Prebid Cache

On April 30, 2026, the Microsoft-hosted (formerly AppNexus) public Prebid Cache will be deprecated. Prebid.js and Prebid Server implementations using this cache to store and retrieve video creatives need to migrate to another solution.

The specific cache URL is `http://prebid.adnxs.com/pbc`.
 
Alterative local caching options are detailed in the [Prebid.org documentation](https://docs.prebid.org/dev-docs/publisher-api-reference/setConfig.html#client-side-caching-of-vast-xml).  

Examples include:
- Local client-side caching (Prebid.js)
- Client-side caching
- Server-side caching using a host other than Microsoft/AppNexus

Local caching is the preferred method offering a smoother customer experience and reduced bandwidth for all participants. We'll continue to work through any niche use cases with the community, as core contributors to Prebid.js.
 
Please reach out to our [Support team](https://support.ads.microsoft.com/sign-in) or your account manager with any questions.
