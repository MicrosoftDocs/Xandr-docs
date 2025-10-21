---
title: Non-Prebid Integrations With PSP
description: In this article, learn about the non-prebid integrations with PSP.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Non-prebid integrations with PSP

Prebid Server Premium (PSP) primarily supports integrations via [Prebid.js for web/mobile web](./integrate-web-mobile-web-with-psp.md) and [Prebid Mobile SDK for in-app inventory](./integrate-apps-with-psp.md).

If those integration methods are not feasible, and **Prebid key values are not needed** for PSP demand to compete in the ad server's auction, the Direct Supply customer's existing integration into Microsoft Monetize can be used instead:

- `/openrtb2` (For more details, see [Incoming Bid Request from SSPs](../supply-partners/incoming-bid-request-from-ssps.md))
- Video tags (For more details, see [Integrating In-Stream Video with Tags](../monetize/integrating-in-stream-video-with-tags.md))
  - `/ptv` (client-side video)
  - `/ssptv` (server-side video)
  - `/vmap` (long-form client-side video)
  - `/ssvmap` (long-form server-side video)
- `/ttj` (For more details, see [TinyTags](../bidders/tinytags.md))

In this scenario, maintain the above integration methods and proceed with the [PSP Setup steps](./integrate-with-psp.md).

## Related topics

- [Integrate with PSP](integrate-with-psp.md)
- [Integrate Apps with PSP](integrate-apps-with-psp.md)
- [Video Guidance](video-guidance.md)
- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)
- [PSP supported formats and integration paths](./prebid-server-premium-supported-formats-and-integration-paths.md)
