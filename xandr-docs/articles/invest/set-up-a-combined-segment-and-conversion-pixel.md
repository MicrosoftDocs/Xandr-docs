---
title: Microsoft Invest - Set Up a Combined Segment and Conversion Pixel
description: Use segment targeting to exclude converters and increase ROI by creating a combined Segment and Conversion pixel for advertisers.
---

# Microsoft Invest - Set up a combined segment and conversion pixel

Do you have an advertiser that only accepts one conversion event per user or only one conversion event per user every X minutes/hours/days? If so, you should be using segment targeting to exclude converters and increase ROI. You can create a combined Segment and Conversion pixel, so you only have to give your advertiser a single pixel to put on their conversion page.

## Scenario

Let's say you want to run a remarketing campaign where I only show impressions to users that are in my "Auto Intenders" segment. In this use case, your advertiser only allows one conversion per user.

## Solution

There are two possible approaches. Once a user has converted, you can either:

1. Add them to a "Converters" segment and exclude that segment in your targeting.
2. Remove them from the "Auto Intenders" segment that you're targeting.

Generally, it is recommended that you use the first approach for a couple of reasons:

1. If you're constantly adding new users to your "Auto Intenders" segment, you could end up re-adding a converted user.
1. If multiple advertisers are using your "Auto Intenders" segment, you end up removing users that didn't convert for every advertiser and delete valuable data.

## Setup

For this scenario, you need to create the following:

- Auto Intenders Segment Pixel
- Converters Segment Pixel with no expiration
  - If your advertiser allowed conversions every X minutes/hours/days, you would simply set that as my expiration window on your Converters segment pixel
  - Conversion Pixel

When you [export conversion pixels](./export-conversion-pixels.md), you can use the **Advanced Options** section to create a combined Segment and Conversion Pixel. The pixel tag that Microsoft Invest generates looks like the following:
    
:::image type="content" source="./media/combined-pixel.png" alt-text="Screenshot of a generated pixel tag by Microsoft Invest.":::

The above pixel tag will record conversion events as well as add the converting user to segment ID 45962.

The final step is to set [segment targeting](./segment-targeting.md) in your line item so that the "Auto Intenders" segment is included and the "Converters" segments is excluded.

## Related topics

- [Export Conversion Pixels](./export-conversion-pixels.md)
- [Conversion Pixels Advanced](./conversion-pixels-advanced.md)
