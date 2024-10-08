---
title: Prebid Server Premium Identity & User Syncing
description: In this article, find information on the types of user identifiers available for monetization with Prebid Server Premium (PSP).
ms.date: 10/28/2023
---

# Prebid Server Premium identity & user syncing

This page provides high-level guidance on the types of user identifiers available for monetization with Prebid Server Premium (PSP).

> [!NOTE]
> Local regulations, such as GDPR, CCPA, and others, are considered when processing bid requests through PSP.

## Cookies

Publishers do not need to take any specific action regarding PSP to sync user cookies. The integration with Microsoft Monetize will synchronize Microsoft Advertising cookies, along with a rotation of pixels from the Monetize marketplace and Prebid Demand Partners (typically SSPs). Prebid Server Demand Partners are automatically synced through the userSync endpoints they [provide in GitHub](https://github.com/prebid/prebid-server/tree/master/static/bidder-info). If no endpoint is provided in a partner's .yaml file, they must actively contact Microsoft Advertising to supply a URL for implementation.

> [!NOTE]
> User-matched request count and rate metrics currently include only cookies, not more persistent identifiers such as industry IDs (e.g., RampID, UID 2.0) or publisher-provided IDs (PPIDs). The presence of device IDs is also not reflected in these metrics.

### Prebid.js

Publishers using Prebid.js that prefer to maximize cookie sync opportunities by syncing on page load, instead of only syncing when delivers an ad, must override the default setting and enable iframe syncing. For more information, see [Prebid Server endpoints and cookie_sync](https://docs.prebid.org/prebid-server/endpoints/pbs-endpoint-cookieSync.html).

Generally, iframe or all syncs must be enabled with all bidders or at least Xandr included:

1. In the response object, under `filterSettings`
    1. If `filterSettings.iframe` is set to include * (all), Xandr, or `AppNexus`, and `syncEnabled` is `true`, iframe cookie syncing is enabled.
    1. If `filterSettings.all` is set to include * (all), Xandr, or `AppNexus`, and `syncEnabled` is true, iframe cookie syncing is enabled.
    1. If only `filterSettings.image` is enabled, them iframe syncing is not enabled, limiting cookie syncing opportunities.
1. If the settings are not as desired, publishers must change them in their Prebid.js deployment.

### AST

Monetize Ad Server publishers using AST that prefer to maximize cookie sync opportunities by syncing on page load, instead of only syncing when Microsoft Advertising delivers an ad, must set the userSync object following the example below. The sellerId and publisherId must be replaced with the relevant values and the syncDelay may be changed from the value in the example. For more information, see [Set Page Options](../seller-tag/set-page-options.md).

```
apntag.setPageOpts({
   "trackingManagement":{
      "userSync":{
         "syncEnabled":true,
         "syncDelay":3000,
         "publisherId":11111,
         "sellerId":12345
      }
   }
});        
        
```

### AMP

Publishers with AMP inventory that prefer to maximize cookie sync opportunities must override the default load-cookie.md behavior to enable iframe syncing. For more information, see [Prebid Server endpoints and cookie_sync](https://docs.prebid.org/prebid-server/endpoints/pbs-endpoint-cookieSync.html).

Similar to Prebid.js, AMP implementations must allow iframe syncs with all bidders or at least Xandr included.

## Persistent identifiers

### Devices identifiers

PSP supports pass-through of device IDs such as IDFAs and AAIDs. No action is needed from the publisher to allow demand partners to receive this data.

### Common industry identifiers

PSP supports pass-through of select industry identifiers supported by Microsoft Monetize such as UID 2.0. When a given industry ID is supported, it generally does not require action on the part of the publisher to be passed to demand partners. Contact Microsoft Advertising for more details. For more information, see the [supported industry identifiers for Microsoft Monetize](universal-id-support-matrix-for-sellers.md).

### Publisher provided identifiers

PSP supports pass-through of proprietary publisher-provided user identifiers (PPIDs) to demand partners. Controls to limit which demand partners receive this data are available via the [Demand Partner Service API](../digital-platform-api/demand-partner-service.md) and in the future, will be available via the Identity Management UI. For more information on the registration process and managing identifiers, review the [Identity Service documentation](../digital-platform-api/identity-service.md).

> [!IMPORTANT]
> The Identity Service is currently in **Alpha**. It is still under development and may be subject to change without notice. Contact Microsoft Advertising for more details.

## Related topics

- [Set Up Prebid Server Premium](set-up-prebid-server-premium.md)
- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md)
- [PSP Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Cookies](../industry-reference/cookies.md)
- [PSP Health Analytics Report](prebid-server-premium-health-analytics-report.md)
- [Demand Partner Service](../digital-platform-api/demand-partner-service.md)
