---
title: Microsoft Monetize - Creative Macros
description: In this article, find information on what creative macros are and a few common use cases for creative macros.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Creative macros

You can insert creative macros into your creative third-party tags, impression trackers, landing page URLs, and third-party pixels for reporting and optimization purposes.

A creative macro is a text placeholder that is replaced with impression-level information when a creative is served. This impression-level information is transmitted to systems outside of Microsoft Advertising, which you can then use for reporting, optimization, and many other purposes. When multiple values are requested, data is sent in a comma separated list. For more information about the creative macros that we support, see [Supported Creative Macros](supported-creative-macros.md).

Every macro needs a key to precede it to communicate to the ad server what information should be populated. In the example below, the keys are `cb` and `age` and the macros are `${CACHEBUSTER}` and `${AGE}`:

```
https://lensmaster.com/newsunglasses?cb=${CACHEBUSTER}&age=${AGE}
```

Keys are specific to the ad server. It's important to note that Microsoft Advertising auto-inserts click tracking and cache buster macros for specific ad servers. For more information, see [Auto Macro Insertion](auto-macro-insertion.md). Additionally, most creative macros are populated by our bidder engine with the exception of click tracking macros. Therefore, they won't populate in creative previews, but only during true auctions.

> [!NOTE]
> Creative macros are case-sensitive and aren't available for piggyback conversion pixels.

## Common use cases for creative macros

Inserting creative macros inside of third-party ad tags such as `${CACHEBUSTER}` and `${CLICK_URL}` is a common use case, but you can also use them in:

- Impression trackers
- Creative landing page URLs specified at the creative or line item or campaign level

| Common Use Case | Example |
|---|---|
| Impression Tracker | You would like to store a number of factors related to each impression for reporting and analysis. You can use the `${CREATIVE_ID}`, `${CP_ID}` (campaign ID), `${PUBLISHER_ID}`, `${SITE_ID}`, and `${TAG_ID}` macros to transmit information about the inventory you're buying back to your ad server. If you have third-party creative tags from an ad server outside of your control such as DART tags, you can use these macros to pass this same information to an impression tracker. After you've stored this data, it can be used for various purposes such as self-service reporting for your clients and feeding a proprietary optimization algorithm. |
| Landing Page URL | You would like to pass impression-level data into landing page URLs to enable landing page optimization systems and provide valuable data about impressions and creatives to your advertisers. A common creative macro use case involves passing the `${SSP_DATA}` macro to the landing page URL to transmit server-side conversion pixel data. For more information about how to use the `${SSP_DATA}` macro, see [Server-Side Conversion Pixels](server-side-conversion-pixels.md). |
| Third-Party Ad Tag | You have a dynamic ad server that accepts information about the user in order to render a customized creative. You can pass in `${USER_IP}`, `${USER_CITY}`, and `${POSTAL_CODE}` to generate a highly relevant, location-based creative for that user. You can also use creative macros to pass information, such as Creative ID, Creative Size, Line Item ID, and Advertiser ID, into the AdChoices tags. |

## Related topics

- [Create a Third-Party Network Pixel for Your Creatives](create-a-third-party-network-pixel-for-your-creatives.md)
- [Create a Third-Party Advertiser Pixel for Your Creatives](create-a-third-party-advertiser-pixel-for-your-creatives.md)
- [Click Tracking](click-tracking.md)
- [Third-Party Pixel Service](../digital-platform-api/third-party-pixel-service.md)
