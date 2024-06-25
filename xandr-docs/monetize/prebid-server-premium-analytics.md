---
title: Prebid Server Premium Analytics
description: In this article, find information about the reports that can retrieve Prebid Server Premium (PSP) activity.
ms.date: 10/28/2023
---

# Prebid Server Premium analytics

Prebid Server Premium (PSP) activity can be retrieved from many Microsoft Monetize network-level reports. You can review following key resources:

- [Network Analytics Report](network-analytics-report.md): The primary report for delivered impressions and spend with permanent retention of aggregate data. This report leverages buyer, bidder filters and dimensions to view PSP activity along or alongside that of other marketplace bidders.
- [Prebid Server Premium Seller Analytics Report](prebid-server-premium-seller-analytics.md): The legacy report for PSP delivered impressions and spend. This report is limited by 30-day data retention period and only certain metrics and dimensions, this will be deprecated in favor of Network Analytics in the future.
- [Prebid Server Premium Health Analytics Report](prebid-server-premium-health-analytics-report.md): The primary report for optimization and troubleshooting which includes delivered impressions, bid requests sent, bid errors, and other granular information. Due to the granular nature of the data, this report is based on a sample of log data multiplied to estimate the full volume of PSP activity. This report should not be used to report final delivery or spend. Data retention period of this report is 99 days.
- [Prebid Server Premium Request Response Sampler](prebid-server-premium-request-response-sampler.md): A tool to retrieve examples of bid requests and bid responses exchanged between Prebid Server Premium and its demand partners. This tool is used to identify specific issues and errors from Health Analytics and subsequently share them with demand partners.
- [Reporting Guide](reporting-guide.md): Information on the full catalog of Microsoft Monetize reports available to sellers.
- [Report Service](../digital-platform-api/report-service.md): Instructions to access reporting data via API.
- [Report Discrepancies](report-discrepancies.md): Guidance on what to check and how to get support when Microsoft Monetize reporting is substantially different from demand partner reporting.

It is highly recommended that sellers frequently check the performance of their demand partners, resolve any errors, and optimize away from or remove underperforming partners.
