---
title: Microsoft Monetize - Reporting (Cross-Device)
description: Learn how reporting on cross-device targeting and measurement is available across the Network Analytics report, the Device Analytics report, and the Data Usage report.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Reporting (Cross-Device)

Reporting on cross-device targeting and measurement is available in the Network Analytics report, the Device Analytics report, and the Data Usage report, as well as on the **Analytics** tab for the augmented line item.

> [!NOTE]
> Cross Device Metrics on the Line Item Analytics tab includes data for the last 60 days only.

## Reports with Cross-Device metrics

> [!WARNING]
> Cross-device functionality is available to sellers when running line items that purchase inventory from the ad exchange using RTB. It's not available when sellers are running managed campaigns on their own inventory.

| Report | Cross-Device Metric(s) | Notes |
|--|--|--|
| Buyer Reach and Frequency | - Cross Device Incremental Device Reach<br> - Cross Device Incremental Imps | The number of unique devices reached and the number of impressions which are transacted due to cross-device audience extension. |
| Data Usage | Data Type | Supported values are Segment and Cross Device. |
| Device Analytics | - Conversion Device Make<br> - Conversion Device Type | Compare these metrics to the standard Device Make and Device Type metrics, which include all devices, not just ones where a conversion occurred. |
| Network Analytics | - Post View Cross Device Conversions<br> - Post Click Cross Device Conversions | Compare these metrics to the standard Post View Conversions and Post Click Conversions metrics, which include all conversions including cross-device conversions. |

## Related topics

- [Cross-Device Targeting and Measurement](cross-device-targeting-and-measurement.md)
- [Set Up Cross-Device Attribution](set-up-cross-device-attribution.md)
- [Network Analytics Report](network-analytics-report.md)
- [Device Analytics Report](device-analytics-report.md)
- [Buyer Reach and Frequency Report](buyer-reach-and-frequency-report.md)