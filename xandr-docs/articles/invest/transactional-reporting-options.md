---
title: Microsoft Invest - Transactional Reporting Options
description: In this article, explore Microsoft Invest's transactional reporting options, including features, resource requirements, and links to comprehensive documentation.
---

# Microsoft Invest - Transactional reporting options

This page describes a number of reporting options for clients who need to go beyond the capabilities exposed by Microsoft Invest. The reporting options described below can be used for:

- Monitoring by your ad operations teams.
- Optimization by your analytics teams.
- Advertiser or publisher client dashboards and reports.

The reporting options described here have different levels of resource requirements and transactional granularity. For more information, see the relevant sections below.

## Overview

The table below provides an overview of the transactional reporting options we offer. It also lists features, resource requirements, and has links to detailed documentation.

For more information about each option, click its name in the **Option** column.

| Option | Documentation | Resource Level | Requirements | Features |
|:---|:---|:---|:---|:---|
| [Reporting](#reporting) | [Reporting Guide](reporting-guide.md) | Low | Ability to manipulate reporting data offline (optional) | - Manual processing<br> - Can whitelabel UI for client reporting<br> - Can manually export and manipulate reports |
| [Reporting API](#reporting-apis) | - [Report Service](../digital-platform-api/report-service.md)<br> - [Report Pagination](../digital-platform-api/report-pagination.md)<br> - [Bulk Reporting Feeds](../digital-platform-api/bulk-reporting-feeds.md) | Medium | - Scripts to pull data<br> - Offline data storage for local housing | - Can be automated<br> - Access to Bulk Reporting Feeds<br> - Additional granularity beyond Microsoft Invest reports<br> - Use of custom `code` field |
| [Creative Macros](#creative-macros) | [Creative Macros](creative-macros.md) | Medium-High | - HTTP or tag request listening<br> - Query string parsing<br> - Aggregation of parsed fields | Auction level granularity real time. Option to choose which parameters to ingest. Raw data not processed by Xandr. |
| [Log Level Data](#log-level-data) | [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md) | High | Data storage and aggregation system | - Auction level granularity<br> - Additional parameters not available in Microsoft Invest reporting<br> - Large data sets<br> - Aggregation is **not** handled by Xandr |

## Reporting

Reporting modules are accessible to all Microsoft Invest clients. Key features and caveats include:

- 2-3 hour reporting delay depending on the report (except daily reports which close the following day).
- Data aggregation to hourly or daily granularity depending on the report.
- Lookback windows are limited and vary depending on the fields being analyzed.
- No auction level impression data.
- Certain data elements (e.g., IP address) are not available.
- Need to be logged in to run these reports (though API equivalents often exist).

Reports can be delivered through various automated options as well as on an ad hoc basis via the user interface. There is also the option to whitelabel the reporting UI and provide advertisers or publishers a dashboard they can run reports in.

## Reporting APIs

The aggregation, filtering and processing of the data available via UI reporting can be conducted automatically using API scripts. This method allows you to store data for longer than is possible in Microsoft Invest reporting. Certain reporting services offer more granular data via the API; there is also the ability to use [Bulk Reporting Feeds](../digital-platform-api/bulk-reporting-feeds.md) to synchronize
offline data sets with Xandr-aggregated data over the last 30 days. In addition, there is a custom `code` field that
can be used for filtering and reporting through the API to map Microsoft Invest objects back to objects in an external system or data store. Buyers will often store data pulled via the API offline to present to clients in delivery or metrics dashboards.

## Log-level data

Each feed has different parameters that can be valuable to clients looking for auction-level granularity or metrics not available in
Microsoft Invest reporting. To handle this data, you must be able to support offline aggregation and large scale storage capabilities. For more details, see [Log-level Data (LLD) Feeds](../log-level-data/log-level-data-feeds.md).

## Creative macros

Creative macros are automatically populated by Xandr on each auction. There are different methods to receive these filled-in creative macros:

- Build the macros into impression tracker query strings. The impression trackers could then be attached to creatives on the buy or sell side.
  They can also be piggybacked onto placements on the sell side.
- Build the macros directly into JavaScript creative tag or URL query strings. This could be used for creative content decisioning (i.e.,
  certain populated macros flag which creative to deliver) as well as for the ingestion and storage of auction level parameters.

This impression data stream is available realtime, unlike the other reporting options mentioned in this article. Reporting and taking action based on this data is dictated by client data ingestion methods and processing time.

Note that these macros can include raw data grabbed from the impressions (unlike Log Level Data which includes parameters processed by
Xandr). For example, creative macros like `${USER_AGENT}` and `${REFERRER_URL}` will include raw strings of the impressions' full referrer (not just the domain) and user agent from the HTTP header (not just device make, operating system, browser, and model information) which can be valuable.

The same creative macros would also function for landing page URL parameters to store click information.

## Related topics

- [General Reporting Concepts](general-reporting-concepts.md)
- [Creative Macros](creative-macros.md)
- [Report Service](../digital-platform-api/report-service.md)
- [Log Level Data Feeds](../log-level-data/log-level-data-feeds.md)
