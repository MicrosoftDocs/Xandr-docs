---
title: Microsoft Monetize - Data Usage Report
description: The Data Usage report gives details related to your usage of data provided by third parties, the costs of that data usage and campaigns in which that data was used to target users. This page also explains steps to run this report.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Data usage report

The Data Usage report gives details related to your usage of data provided by third parties (e.g., user segment providers), the costs of that data usage and campaigns in which that data was used to target users.

> [!NOTE]
> This report will only return data for buyers in the data marketplace.

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

For more information about how quickly report data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Advertiser | Yes | The advertiser that used the third-party data and incurred these costs. |
| Buying Currency | Yes | The buying currency used for the transaction that incurred the third-party data usage costs. |
| Campaign | Yes | The campaign that used the third-party data and incurred these costs. (Does not apply to all advertisers.) |
| Country | Yes | The country that the impression is from. |
| Data Provider | Yes | The name and ID of the provider associated with the third-party costs. |
| Insertion Order | Yes | The insertion order that used the third-party data and incurred these costs. |
| Line Items | Yes | The line item that used the third-party data and incurred these costs. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Targeted Segment IDs | No | The IDs of the data segments that were targeting via the line item/campaign. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Data Costs | The total costs attributed to the use of third-party data. |
| Data Type | The two choices are Segment or Cross Device. See [Cross-Device Targeting and Measurement](cross-device-targeting-and-measurement.md) for more information. |
| Imps | The number of impressions where a cost was incurred due to use of a third-party's data. If multiple third-party providers were used for a single impression, that impression will be listed for each third-party provider. |
| Sales Tax | The amount of sales tax collected. This field is only populated when the Buyer's billing address is located in one of the following U.S. states: NY, TX or NJ. Microsoft Advertising is required (by the relevant local state regulator) to collect this tax. |

> [!WARNING]
> Cross-device functionality is available to sellers when running line items that purchase inventory from the ad exchange using RTB. It's not available when sellers are running managed campaigns on their own inventory.

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

## Related topic

   [Network Reporting](network-reporting.md)
