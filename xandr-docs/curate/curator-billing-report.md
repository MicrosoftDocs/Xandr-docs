---
title: Microsoft Curate - Curator Billing Report
description: Explore this article to understand the Curator billing report, including its metrics, dimensions, and a detailed guide on running a report.
ms.date: 10/28/2023
---

# Microsoft Curate - Curator Billing report

The **Curator Billing Report** allows you to manage internal invoicing for your curation activities. Curators who choose to direct-clear with sellers can report on the revenue amounts they need to clear with those sellers.

> [!NOTE]
> This report is only available to curators.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports.

However, all time ranges are not available for every report.

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

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

> [!NOTE]
> Hourly impression data is available and spans 13 full months. For impressions that are older than 13 months, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight.
>
> All daily data that is older than 13 months will be timestamped based on the UTC time zone.

## Dimensions

> [!IMPORTANT]
> The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.
>
> For all revenue fields, the currency is defined by the **Buying Currency** field.

| Column | Filter | Description |
|:---|:---|:---|
| Buyer | Yes | Member ID of the buyer who bought on the transaction. |
| Seller | Yes | Member ID of the seller where the curated transaction served on. |
| Publisher | Yes | Publisher ID of the seller where the curated transaction served on. |
| Curator | No | Member ID of the curator who facilitated the transaction. |
| Curated Deal ID | Yes | Curated deal ID. |
| Curator Cleared | Yes | - "0" if Microsoft Advertising clears net seller revenue with the seller.<br> - "1" if the curator direct clears net seller revenue with the seller. |
| Buying Currency | No | The transaction currency used by the buyer. |
| Selling Currency | No | The transaction currency used by the seller. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|:---|:---|
| Billable Imps | The total number of impressions billed to the client. |
| Net Seller Revenue | The amount of net revenue a seller earns, exclusive of seller auction service fees (SASC) they owe to Microsoft Advertising. <br><br>**Note:** This field is only filled for sellers for which the curator has a direct clear relationship. |
| Curator Margin Deduction | The profit a curator makes on a transaction. |
| Curator Auction Service Deductions | The amount Microsoft Advertising charged to the curator as a deduction at auction time. |
| Curator Auction Fees | The amount Microsoft Advertising charged to the curator as a fee at auction time. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium \> Analytics \> Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery
    method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your
      browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report
      when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to
      view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name
      this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.
