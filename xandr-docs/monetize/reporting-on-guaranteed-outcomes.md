---
title: Microsoft Monetize - Reporting on Guaranteed Outcomes
description: Transaction data from Guaranteed Outcomes is identifiable by the Clearing Event associated with the type of outcome purchased. Learn how column Clearing Event is available as both a filter and a dimension in Network and Video Analytics reports and Billing report.  
ms.date: 10/28/2023
---


# Microsoft Monetize - Reporting on guaranteed outcomes

Throughout Monetize reporting, transaction data from Guaranteed Outcomes is identifiable by the underlying Clearing Event associated with the type of outcome purchased. See [Supported Viewability Standards for Guaranteed Outcomes](supported-viewability-standards-for-guaranteed-outcomes.md) and [Supported Video Completion Standards](supported-video-completion-standards.md) for the list of supported Clearing Events.

## Network and video analytics reports

Currently available in the Network and Video Analytics Reports, the column Clearing Event is available as both a Filter and a Dimension. The following metrics are available.

| Clearing Event Name | ID | Viewability Definition | Media Type | Measurement Technology Vendor |
|--|--|--|--|--|
| Views - Standard Display | 2 | IAB (50% of pixels in-view for 1 continuous second) | Display/Banner | Microsoft Advertising |
| Views - Custom Display - 100pv1s | 6 | 100% of pixels in-view for 1 continuous second | Display/Banner | Microsoft Advertising |
| Views - Standard Video | 8 | IAB (50% of pixels in-view for 2 continuous seconds) | Video | Microsoft Advertising |
| Views - Custom Video - 100pv50pd | 9 | 100% of pixel in-view for 50% of the duration of the video with audio on | Video | Microsoft Advertising |

| Metric | Description |
|--|--|
| Clearing Event Units | The total number of events that were purchased, for the associated Clearing Event. |
| Clearing Event Booked Revenue eCPM | The total revenue per 1000 events, for the associated Clearing Event |
| Clearing Event Buyer Media Cost eCPM | The total media cost per 1000 events, for the associated Clearing Event |

The Clearing Event data in Monetize analytics reporting is available as of September 20th, 2017. For report data before this date, the Clearing Event column will display "-", and the metrics will all report zero. Note that in reporting on Standard Line Items (non-ALI), the Clearing Event dimension is also displayed as "-".

> [!TIP]
> To eliminate the noise of other impression types in reporting, use the report filters to select Impression Type=RTB. This configuration ensures the report will only be generated for RTB impressions (the only impression type eligible for Guaranteed Outcomes).

## Billing report

Data for Guaranteed Views activity are similarly available in the Buyer Billing Report. See the report [Buying Billing Report](buying-billing-report.md) for more information, as well as the related [Understanding Your Invoice](understanding-your-invoice.md) documentation.

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [Reporting Guide](reporting-guide.md)