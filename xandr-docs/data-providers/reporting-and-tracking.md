---
title: Reporting and Tracking Overview
description: In this article, learn about reporting and tracking methods used for tracking the user of shared segments.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Reporting and tracking overview

## Reporting

Xandr does not offer segment usage reporting for direct clearing between data providers and data buyers. In other words, there is no reporting for data providers outside of the Data Marketplace. The available reports show various metrics for the delivery of advertisers, insertion order, line items, and creatives. However, grouping by targeted segments is currently not available in these reports. If a data provider wishes to receive a report on the delivery per campaign targeting their segments, they should work with the data buyer to [schedule delivery of a report](reporting-instructions.md) to be emailed from.

## Tracking

The most common methods used for tracking the user of shared segments are impression pixels and client reporting.

- **Impression Pixels:** Impression pixels can be associated with each creative that is served by a campaign using the shared segments to target users/inventory. The impression pixel calls your servers each time the creative is served, informing you of the number of impressions served against the segments.
- **Click Trackers:** It is possible to insert another link in the click tracking chain which redirects the user to an external click tracker, giving you visibility into the performance of a campaign.
- **Conversion Trackers:** It is possible to redirect from a conversion pixel to an external conversion tracker, giving you visibility into the performance of a campaign.
    > [!NOTE]
    > You are responsible for performing attribution related to this conversion tracker.
- **Client Reporting:** Data recipients may schedule or otherwise send reports to the data provider for campaigns and line items utilizing the shared segments for targeting. For steps on how clients can schedule usage reports to be delivered to the data provider, see [Reporting Instructions](reporting-instructions.md).

## Related topics

- [Reporting Services](../digital-platform-api/reporting-services.md)
- [Segment Loads Report](../digital-platform-api/segment-loads-report.md)
