---
title: Microsoft Monetize - Seller Bid Error Report
description: Learn what is the Seller Bid Error Report and how it can be used to troubleshoot sell-side and buy-side settings that result in auction errors, thereby blocking spend.  
ms.date: 10/28/2023
---


# Microsoft Monetize - Seller bid error report

The **Seller Bid Error Report** helps you gain insight into rejected demand through a randomly selected set of 5% of the errors logged on the Microsoft Advertising platform. Error Count has been multiplied by 100 to account for the 5% sampling.

You can use this report to troubleshoot sell-side and buy-side settings that result in auction errors, thereby blocking spend. The goal is to help you eliminate the error in the future. You can find information on the owner, cause and recommended resolution for each error in [Bid Error Codes](../bidders/bid-error-codes.md).

## Navigation

1. Go to **Reporting** > **Report Center** and click **Create New**
2. In **Search for a Report** search box, type the report name
3. The relevant report widget will be shown under its category such as **Analytics**, **Troubleshooting** or **Reach**.
4. Click on **Create new report** button to create the new report.
   
## Time frame

All dates and times are given in UTC.

**Time ranges**

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

**Intervals**

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

## Data retention period

This report's data is retained for 403 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Ad Profile ID | Yes* | The Ad Profile ID of the Seller Member impacted by the error. |
| Ad Quality Rule ID | No | The ID of the ad quality rule that applied to the block. |
| Ad Server | Yes | The adserver associated with the creative that is impacted by the error. There may be more than one adserver associated to a single creative. |
| Bidder | Yes* | The technology provider whose representing a Buyer and is impacted by the error. |
| Brand | Yes | The brand registered in the Microsoft Advertising system and associated with the creative that is impacted by the error. |
| Buyer | Yes | The Buyer Member who is impacted by the error. |
| Buyer Seat Code | No | The Custom Buyer Seat ID (submitted by DSP) which was used to bid on the impression |
| Buyer Seat Name | No | The display name for the buyer seat code |
| Creative Category | Yes | A classification assigned to both brands and creatives impacted by the error. |
| Creative ID | Yes* | The Creative ID associated with the Buyer Member that is impacted by the error. |
| Creative Size | No | The size of the creative impacted by the error. |
| Deal | Yes | The ID of the deal impacted by the error (if Deal ID = 0 no deal was involved). |
| Error ID | Yes | The specific error that occurred and was logged in ImpBus (ties to Error Message). |
| Error Message | Yes | A generic Error Message that describes the error that occurred (ties to Error ID) |
| Language | Yes | The language the creative was tagged with that is impacted by the error. |
| Placement | Yes* | The Placement of the Seller Member that is associated with the error. |
| Publisher | Yes | The Publisher who is affected by the error. |
| Technical Attribute | Yes | Feature of the creative such as whether it is an image, flash, video, is expandable, etc. affected by the error. |
| YM Floor ID | Yes | The ID of the YM Floor that blocked the bid. |

- Filter by comma separated IDs only.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Error Count | The amount of errors logged on the Microsoft Advertising platform over the time range selected (a randomly selected set of 5% of the errors multiplied by 100 to account for the sampling). |
| Blocked bid CPM | The bid price of the blocked bid. |

## How to run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured), or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.
