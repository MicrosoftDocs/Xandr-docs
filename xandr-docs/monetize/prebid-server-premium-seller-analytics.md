---
title: Prebid Server Premium Seller Analytics Report
description: In this article, learn about the Prebid Server Premium seller analytics report along with the dimensions and metrics associated with it.
ms.date: 10/28/2023
---

# Prebid Server Premium seller analytics report

The Prebid Server Premium Seller Analytics Report contains performance information on configured Prebid Server Premium (PSP) demand partners.

Using this report, you can:

- Track revenue by heading bidder demand partner, publisher, or geographical region.
- Track lift on inventory you've opened up to header bidding demand.
- Monitor the health and efficiency of your Prebid Server Premium partners and placements.

For information on other downloadable reports, see the [Reporting Guide](reporting-guide.md). For information on accessing reporting data via API, see [Report Service](../digital-platform-api/report-service.md) and [Prebid Server Premium Seller Analytics](../digital-platform-api/prebid-server-premium-seller-analytics.md).

## Navigation

1. Go to **Reporting** > **Report Center** and click **Create New**
2. In **Search for a Report** search box, type the report name
3. The relevant report widget will be shown under its category such as **Analytics**, **Troubleshooting** or **Reach**.
4. Click on **Create new report** button to create the new report.
   
## Time frame

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a list of time ranges available for this report.

- Custom
- Last Hour
- Today
- Last 48 Hours
- Yesterday
- Last 7 Days
- Last Month
- Month to Date
- Month to Yesterday

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

### Time zone

Select the time zone for the report.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Country | Yes | The country where the impression was served. |
| Header Bidding Demand Partner | No | The demand partner associated with the placement. |
| Impression Type | Yes | The type of impression served. For details, see [Impression Types](#impression-types). |
| Placement Group | Yes | The name of the placement group associated with the impression. |
| Publisher | Yes | The publisher on whose inventory the impression occurred. |
| Seller | No | The name of the seller associated with the impression. |
| Size | Yes | The size of the placement. |
| Tag | Yes | The tag associated with the impression. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The number of impressions on the placement. |
| Seller eCPM | The seller revenue represented in eCPM. |
| Seller Revenue | The seller revenue represented as a dollar amount. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions (View Measured Imps / Imps). |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability (Viewed Imps / View Measured Imps). |
| Viewable Imps | The number of viewable impressions for the placement. |

## Impression types

| Value | Name | Definition |
|---|---|---|
| 1 | Blank | No creative served. |
| 2 | PSA | A public service announcement served because no other creative was eligible. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 4 | Default | A default creative served because no line item or campaign bid or no other creative was eligible. |
| 5 | Kept | One of your managed advertisers served a creative. |
| 6 | Resold | The impression was sold to a third-party buyer. |
| 7 | RTB | Your creative served on third-party inventory. |
| 8 | PSA Error | A public service announcement served due to a timeout issue. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |

## How to run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).

    Or, from the **Publishers** top menu, click on **Prebid Server Premium** > **Analytics** > **Prebid Server Premium Seller Analytics**

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!NOTE]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!NOTE]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV, and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service. The limit here is 10 million rows.

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.

1. Click **Run report** to send your report request.
