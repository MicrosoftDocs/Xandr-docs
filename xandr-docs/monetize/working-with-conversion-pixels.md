---
title: Microsoft Monetize - Working with Conversion Pixels
description: Explore conversion pixel tracking, analyze user responses to creatives, and determine if conversions stem from user interactions.
ms.date: 10/28/2023
---

# Microsoft Monetize - Working with conversion pixels

A conversion pixel is used to track user actions in response to an advertiser's creatives, such as registering at a site or making a purchase. When a conversion pixel fires, we determine if the conversion (the registration, the purchase, etc.) can be "attributed", or tied to the user clicking on or viewing one of the advertiser's creatives previously.

Here's how it works:

1. You create and export a conversion pixel.
1. You ask the advertiser to place the pixel on the page where the user action should be noted, for example, the confirmation page for a registration or the checkout page for a purchase.
1. You associate the conversion pixel to the advertiser's line item(s), where you define the static revenue value that the advertiser will pay you for attributed conversions. Note that you can also configure to pass an [advanced    conversion pixel](conversion-pixels-advanced.md).
1. When the conversion pixel fires, we determine if the user clicked on or viewed one of the advertiser's creatives previously. If so, the conversion is considered attributed, and you earn the revenue for the conversion defined in the line item.

## Related topic

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Export Conversion Pixels](export-conversion-pixels.md)
- [Conversion Attribution](conversion-attribution.md)
- [Conversion Pixels Advanced](conversion-pixels-advanced.md)
- [Reporting on Conversions](reporting-on-conversions.md)
- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)
- [Set Up a Combined Segment and Conversion Pixel](set-up-a-combined-segment-and-conversion-pixel.md)
