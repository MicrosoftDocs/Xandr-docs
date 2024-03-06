---
title: Microsoft Monetize - Set Up Cross-Device Attribution
description: Explore setting up line items, conversion pixels, and segment targeting for precise attribute conversions in multi-device consumer journeys.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up cross-device attribution

To attribute conversions across a multi-device consumer journey, you need to ensure your line item is correctly set up, including conversion pixels and segment targeting.

Set up a conversion pixel to track [Conversion Attribution](conversion-attribution.md).

In order to track conversions across devices and view associated metrics, please set the Augmented Line Item in the following way:

1. Have **Cross Device** enabled in **Basic Settings**.
1. Implement first/third party audience segment  targeting in **Audience Segments**.

   (Recommended for a CTV campaign. Optional for other campaigns).

1. In the **Optimization** section, select the pixels you want to track conversions against using the **Conversion Tracking** option.
1. You can then run the **Analytics Report** and/or the **Device Analytics** report to get the number of conversions/details on the conversion device. (See [Cross-Device Reporting](cross-device-reporting.md)). The cross-device related metrics in these reports are as follows:

    - **Advertiser Analytics** - The report has two metrics:
      - Post View Conversions Cross Device
      - Post Click Conversions Cross Device
    - **Device Analytics** - The report also has two metrics:
      - Conversion Device Make
      - Conversion Device Type

1. **Recommended**: Set the limits in the **Frequency Capping** section to ensure that, now that consumers can see your ads on multiple devices, they do not see more impressions than you intend.

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Working with Conversion Pixels](working-with-conversion-pixels.md)
- [Segment Targeting](segment-targeting.md)
- [Frequency and Recency Caps](frequency-and-recency-caps.md)
