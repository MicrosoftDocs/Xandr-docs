---
title: Prebid Server Premium Analytics
description: In this article, find information about the reports that can retrieve Prebid Server Premium (PSP) activity.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Prebid Server Premium analytics

Prebid Server Premium (PSP) activity should be reviewed frequently to identify and resolve any issues with demand partners. Underperforming partners should be removed in favor of testing new partners with unique demand. Sellers can pull PSP data from key resources:

- [Prebid Server Premium Health Analytics Report](prebid-server-premium-health-analytics-report.md): The primary report for optimization and troubleshooting which includes delivered impressions, bid requests sent, bid errors, and other granular information. Due to the granular nature of the data, this report is based on a sample of log data multiplied to estimate the full volume of PSP activity. This report should not be used to report final delivery or spend. Data retention period of this report is 99 days.
- [Monetize Historical Report](monetize-historical-reporting.md): The primary report for delivered impressions and spend with permanent retention of aggregate data. Views of PSP can be created using filters or dimensions including bidder (Prebid Server Premium as a single entity), buyer (PSP demand partners), and SSP (comparing Monetize SSP as a whole to each demand partner). This replaces the legacy Monetize network analytics and Prebid Server Seller Analytics reports.
- [Monetize Insights dashboard](monetize-insights-for-publishers.md): Offering visualizations of trends and actionable alerts, Insights offers sellers multiple paths to optimization and higher revenue. Views of PSP are available by channel (PSP vs. managed demand, among other breakouts), SSP (comparing Monetize SSP as a whole to each demand partner), and DSP (PSP demand represented as a single entity). Insights recommendations include PSP demand partners with no spend across all configurations as well as PSP configurations with no spend across all demand partners.
- [Prebid Server Premium Request Response Sampler](prebid-server-premium-request-response-sampler.md): A tool to retrieve examples of bid requests and bid responses exchanged between Prebid Server Premium and its demand partners. This tool is used to identify specific issues and errors from Health Analytics and subsequently share them with demand partners.
- [Reporting Guide](reporting-guide.md): Information on the full catalog of Microsoft Monetize reports available to sellers.
- [Report Service](../digital-platform-api/report-service.md): Instructions to access reporting data via API.
- [Report Discrepancies](report-discrepancies.md): Guidance on what to check and how to get support when Microsoft Monetize reporting is substantially different from demand partner reporting.
