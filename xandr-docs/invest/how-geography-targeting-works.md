---
title: Microsoft Invest - Geography Targeting Process
description: This article explains how geography targeting works. Geography targeting is supported by Digital Envoy's IP lookup service.
ms.date: 10/28/2023
---

# Microsoft Invest - Geography targeting process

Geography targeting is supported by an IP lookup service provided by [Digital Envoy](https://www.digitalelement.com/). This service maps IP addresses to known countries, regions, cities, metro codes, and postal codes. We currently use [Digital Envoy's NetAcuity Pulse](https://www.digitalelement.com/solutions/netacuity-pulse/) database. Note that GPS coordinates, when available, are not derived from IP addresses but are provided directly from certain environments when users consent to share their location (for example, in mobile apps).

Geolocation is performed using the IP address received from the ad call. This IP address is read in directly from client-side ad calls (for example, `ttj`) or contained in the request body of server-side bid requests (for example, in OpenRTB).

We automatically update geolocation data provided by Digital Envoy every two weeks when Digital Envoy publishes an updated database. After some validation, we propagate this new data to our servers. For details on recent and upcoming changes, see [Changes to Geography Objects](./changes-to-geography-objects.md).

Occasionally, new regions, cities, metro codes, and postal codes may become available for targeting, while some others might be deactivated. These changes can reflect actual geographic changes (for example, when a country redefines its regions), changes in IP address allocations by Internet Registries and ISPs, and improvements to Digital Envoy's geolocation techniques. Countries may be added or deactivated as well, however, this happens very infrequently.

If a country, region, city, or metro code has been deactivated, it will no longer be available for targeting. If your line item is already targeting a deactivated geography object, it will appear grayed out.

Deactivated geography objects can also be identified via the API. See the following API services:

- [Country Service](../digital-platform-api/country-service.md)
- [Region Service](../digital-platform-api/region-service.md)
- [City Service](../digital-platform-api/city-service.md)
- [Designated Market Area Service](../digital-platform-api/designated-market-area-service.md)
