---
title: Microsoft Curate - Curator Vendor Usage Report
description: Learn about the Curator Vendor Usage Report, including its time ranges, dimensions, metrics, delivery options, and data cost details.
ms.date: 09/10/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: v-garittar
---

# Microsoft Curate - Curator Vendor Usage Report

> [!IMPORTANT]
> This report is available only to curators.

The **Curator Vendor Usage Report** helps you understand the costs incurred from using Data Marketplace segments and other third-party data sources.

## Time frame

All dates and times in this report use **UTC**.

### Time ranges

Time ranges define the reporting period.

Available time ranges include:

- Custom
- Current Hour
- Last Available Day
- Last Hour
- Today
- Last 24 Hours
- Last 48 Hours
- Yesterday
- Last 2 Days
- Last 7 Days
- Last 7 Available Days
- Last 14 Days
- Last 14 Available Days
- Last 30 Days
- Last 30 Available Days
- Last Month
- Last 100 Days
- Last 365 Days
- Quarter to Date
- Month to Date
- Month to Yesterday
- Lifetime

> [!NOTE]
> Not all time ranges are available for every report.

### Intervals

Intervals determine how report data is grouped.

| Interval | Description |
| :--- | :--- |
| Hourly | Groups data by hour. |
| Daily | Groups data by day. |
| Monthly | Groups data by month. |
| Cumulative | Aggregates all data into a single result for the selected time range. |

> [!NOTE]
> Not all intervals are available for every report.

### Data retention

Report data is retained for **3 years**.

## Dimensions

> [!IMPORTANT]
> Dimensions marked as filterable can be used both for filtering and grouping.

| Dimension | Filterable | Description |
| :--- | :--- | :--- |
| Advertiser | Yes | Advertiser name and ID of the curator member that owns the deal line item associated with the curated deal. |
| Cost Type | No | Type of vendor cost incurred. |
| Deal | Yes | Curated deal name and ID. |
| Deal Line Item Currency | Yes | Currency configured for the curated deal line item. |
| Geo Country | Yes | Country where the impression occurred. |
| Insertion Order | Yes | Insertion order name and ID of the curator member that owns the deal line item. |
| Line Item | Yes | Curated deal line item name and ID. |
| Targeted Segment IDs | No | Comma-separated list of segment IDs used to target inventory. |
| Vendor | Yes | Third-party vendor name and ID. |
| Vendor Type | No | Vendor category. |

### Cost Type values

| Value | Description |
| :--- | :--- |
| Feature Costs | Costs associated with platform features such as Cross Device. |
| Segment Data Costs | Costs associated with Data Marketplace segment usage. |

### Vendor Type values

- Segment Marketplace
- Cross Device Graph

## Metrics

> [!NOTE]
> Percentage values shown in the UI are exported as decimal values.

| Metric | Description |
| :--- | :--- |
| Imps | Number of impressions that incurred third-party data costs. If multiple vendors contributed to a single impression, the impression appears once for each vendor. |
| Sales Tax | Deprecated. Amount of sales tax collected at auction time. |
| Vendor Costs | Total third-party costs, including segment and feature costs. |
| Vendor Costs Deal Line Item Currency | Vendor costs expressed in the deal line item's configured currency. |

## Run a report

1. Go to **Report** > **Report Center**.
1. Select **New Report**.
1. Select **Curator Vendor Usage Report**.
1. Configure the report settings, including:
   - Time range
   - Filters
   - Dimensions
   - Delivery options

    > [!TIP]
    > Filters help narrow report results. For example, you can report on specific vendors, deals, or geographic regions.

1. Select the filters you want to apply. For more information about filtering and grouping, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).
1. Choose one or more dimensions to group data.

    > [!IMPORTANT]
    > Adding more dimensions increases report size and processing time. Group only by the dimensions required for your analysis.

1. Choose a delivery option.

### Delivery options

#### Run now and view results

View report results immediately in the browser.

Supported download formats:

- XLSX
- CSV
- TSV
- JSON

##### Limits

- Maximum file size: 100 MB
- Maximum rows for XLSX and Excel exports: 100,000

#### Run in background

Generate the report in the background and receive a notification when results are available.

#### Export and email results

Generate the report and email the results to one or more recipients.

#### Save as a report template

Save report settings for future use.

Saved templates can be rerun from the **Your Reports** page.

#### Schedule a report

Run the report automatically at scheduled intervals and deliver results by email.

#### Name the report

Assign a name to the report configuration for future reference.

### Large reports

> [!TIP]
> If your report exceeds UI download limits, use the [reporting API](../digital-platform-api/report-service.md). The API supports exports of up to **10 million rows**.

### Submit the report

After configuring the report, select **Run report** to generate the report.
