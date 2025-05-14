---
title: Microsoft Monetize - Seller Segment Performance Report
description: Learn how Seller Segment Performance Report helps sellers by providing data on the usage per segment, performance per segment and facilitating data clearing.  
ms.date: 10/28/2023
---


# Microsoft Monetize - Seller segment performance report

The **Seller Segment Performance Report** provides sellers insights into how their targeted segments are contributing to the overall performance of their line items. The report provides data on all targeted segments (includes and excludes) that contributed towards transacted impressions.

This reporting helps sellers in the following ways:

- by providing data on the usage per segment, so they can understand how often they used each segment and thus enable them to bill their data providers and/or advertisers appropriately
- by providing data of performance per segment, so they can analyze which segments are performing well or not well and optimize appropriately
- facilitating data clearing, so that instead of them being responsible for billing their data providers each month, Microsoft Advertising can do it for them

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

This report's data is retained for 100 days. The time granularity of the data is hourly.

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Bidder | Yes | The name and ID of the bidder associated with the impression, in the format "123.com (99000)". |
| Buyer Member | Yes | The name and ID of the buyer who buys the impression, in the format "Accenture LLP (11100)" |
| Country Code | No | The country code in which the impression took place. |
| Country Name | Yes | The country name in which the impression took place. |
| Curator Member | No | The deal curator name and ID, in the format "OMD - Renault Group (CURATOR) (12148)". |
| Deal | Yes | The name and ID of the deal associated with the transaction for the impression., in the format "5StarsCine (165888)" |
| Device Type | Yes | The type of device on which the impression is served. For example, desktop & laptop, mobile phone, tablets etc. |
| Line Item | Yes | The line item associated with the impression, in the format "Kansas City Winter Commuters (314)". |
| Media Type | Yes | The media type associated with the creative that served on an impression. For example, audio, banner, native, interstitial, video, etc. |
| Publisher | Yes | The name and ID of the publisher on whose inventory this impression occurred, in the format "12up.com (1825156)". |
| Sales Channel | Yes | The sales channels for the impression. For example, Managed, Open Exchange, Curated, Deals, Programmatic Guaranteed, etc. |
| Segment | Yes | The user segment associated with the impression in the format "Submitted application (220)". |
| Segment Owner | Yes | The name and ID of owner of a segment used in targeting, in the format "152 Media LLC (1939)". |
| Seller | Yes | The name and ID of seller of an impression, in the format "ABC Owned TV Stations (8164)". |
| Supply Type | Yes | The media type associated with the creative that served on an impression.. For example, Web, Mobile Web and App, Mobile App etc. |
| Targeting Type | Yes | The targeting type, whether its "Inclusion" or "Exclusion" |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Description |
|--|--|--|--|
| Targeted Clicks | int | 5 | Aggregated clicks for a segment |
| Targeted Conversions | int | 2 | Targeted conversions of a segment |
| Targeted Impressions | int | 12 | Aggregated impressions for a segment |
| Targeted Revenue | money | 123.45 | Targeted revenue of the segment which is sum of booked revenue and seller revenue. |
| Targeted Revenue eCPA | money | 1.1 | The targeted revenue, expressed as eCPA. For definitions of eCPA and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Targeted Revenue eCPC | money | 2.2 | The targeted revenue, expressed as eCPC. For definitions of eCPC and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Targeted Revenue eCPM | money | 1.5 | The targeted revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Targeted View Measured Impressions | int | 12 | Aggregated view measurable impressions for a segment |
| Targeted Viewable Impressions | int | 10 | Aggregate viewable impressions for a segment |

## To run your report

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

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Working with Segments](working-with-segments.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
