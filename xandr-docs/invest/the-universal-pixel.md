---
title: Microsoft Invest - Universal Pixel
description: Learn about the universal pixel, which offers centralized data collection across multiple web pages for thorough ad campaign analysis and optimization.
ms.date: 10/28/2023
---

# Microsoft Invest - Universal pixel

Universal pixel provides insights into the interactions that users have with your website, so you can easily segment these users and measure the value of the actions they take. By providing a central configuration interface and unified pixel code, the universal pixel removes the need to separately define conversion pixels and segment pixels.

The universal pixel is implemented by placing the code within the head tag (\<head\> ... \</head\>) of your advertiser's website. You can analyze user traffic in three different ways in order to segment users and track conversions:

- Track the referrer URL of the page the pixel was loaded from.
- Track Standard events which can be fired based on user actions on a page.
- Track additional metadata that's passed using a parameter along with a standard event.

To set up the pixel, you'll create the pixel code, deploy it on your website, see the activity reflected in the Microsoft Advertising UI, and then do any further segment and conversion configuration to refine your data collection process. After you set up segments, you can also target them from your line items. For the complete setup workflow, see [Universal Pixel Basic Implementation](universal-pixel-basic-implementation.md).

> [!NOTE]
> You can only define one universal pixel per advertiser. Also, while you can reconfigure or rename the pixel after you create it, you cannot delete it.

## Related topics

- [Universal Pixel Audiences and Conversions](universal-pixel-audiences-and-conversions.md)
- [Universal Pixel Reporting](universal-pixel-reporting.md)
- [Universal Pixel Log-Level Data](../log-level-data/universal-pixel-feed.md)
