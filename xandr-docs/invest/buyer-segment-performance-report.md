---
title: Microsoft Invest - Buyer Segment Performance Report
description: Use the Buyer Segment Performance report for insights on segment engagement, performance, and conversions within your advertising campaign.
ms.date: 10/28/2023
---

# Microsoft Invest - Buyer Segment Performance report

This report provides buyers with segment performance across multiple ad campaigns and advertisers. This allows you to:

- Understand the performance of individual targeted segments across your account.
- Filter for specific conversion pixels to further identify how these segments contribute to your overall buying strategy.

> [!NOTE]
> **Impressions across user segments:**
>
> Since this report aggregates impressions served by user segment, impressions associated with users present in multiple segments will be counted more than once. The purpose of this report is to analyze user segments, not individual user counts. The report is set to automatically group by segment.

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

## Data retention period

This report's data is retained for 45 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Filter? | Description |
|:-------|:--------|:------------|
| Advertiser | Yes | The advertiser name and ID, in the format "Great Advertiser (456)". |
| Insertion Order | Yes | The insertion order associated with the impression, in the format "Midwest Winter Getaways (789)". |
| Line Item | Yes | The line item associated with the impression, in the format "Kansas City Winter Commuters (314)". |
| Campaign | Yes | The campaign associated with the impression, in the format "South Texas Ford Drivers (123)". (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Segment | Yes | The user segment associated with the impression in the format "Submitted application (220)". |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the monetary metrics to be displayed in the buying currency. |
| Age | Yes | The age range of the user associated with the impression. |
| Gender | Yes | The gender of the user assocaited with the impression. |

Reports automatically group by all selected dimensions.

> [!NOTE]
> In addition, you can also filter on:
>
> - one or more conversion pixels using the **Conversion Pixel** filter.
> - a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Formula | Description |
|:-------|:-----|:--------|:--------|:------------|
| Imps | int | 34534 | Imps | The total number of impressions (served and resold). |
| Clicks | int | 345 | Clicks | The total number of clicks across all impressions. |
| CTR | double | 0.00237 | (Clicks / Imps) x 100 | The rate of clicks to impressions, expressed as a percentage. |
| Conversion Rate | double | 0.000221877080097626 | Total Convs / Imps | The ratio of conversions to impressions. |
| Booked Revenue | money | 450.00 | Booked Revenue | The total revenue booked through direct advertisers. |
| Post View Conversions | int | 15 | Post View Conversions | The total number of recorded post-view conversions. |
| Post Click Convs | int | 19 | Post Click Convs | The total number of recorded post-click conversions. |
| Media Cost | money | 100.00 | Cost | The total cost of the inventory purchased. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit | money | 4.14 | Booked Revenue - Total Cost | Booked revenue minus total cost. <br> This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| CPM | money | 5.00 | CPM | The cost per one thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Conversion per Million | double | 384.4 | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Total conversions | int | 5 | total_convs | The total number of post-view and post-click conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPA | money | 1.1111 | media_cost / total_convs | The cost per acquisition/conversion. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPM | money | 1.234 |  | The total revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Profit eCPM | money | 0.4949 | (Booked Revenue - Total Cost) / Imps * 1000 | Profit per thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Commissions | money | 0 | $0. | Fees that come out of the booked revenue. $0. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Partner Fees | money | 123.45 | Third-party costs. | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. |
| Total Cost | money | 123.45 | Media Cost + Data Costs + Partner Fees + Commissions + Serving Fees + Publisher Revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | money | 123.45 | (Total Cost/Imps) * 1,000 | The total cost per 1,000 imps. |
| Total Cost eCPC | money | 123.45 | Total Cost/Clicks | The total cost per click. |
| Total Cost eCPA | money | 123.45 | Total Cost/Conversions | The total cost per conversion. |
| Profit eCPC | money | 123.45 | (Booked Revenue - Total Cost)/Clicks | Profit per click. |
| Profit eCPA | money | 123.45 | (Booked Revenue - Total Cost)/Conversions | Profit per conversion. |
| Profit Margin | money | 123.45 | (Booked Revenue - Total Cost)/Booked Revenue | Buyer profit margin. |
| Video Skips | int | 10 |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Starts | int | 11 |  | The total number of times the first segment of the video creative was downloaded and started. |
| 25% Video Complete | int | 10 |  | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | int | 10 |  | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | int | 10 |  | The total number of times the video creatives completed 75% of the entire duration. |
| Video Completions | int | 12 |  | The total number of times the video creatives played for the entire duration. |
| Videos Served | int | 10 |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Video Errors | int | 2 |  | The total number of times a video error occurred. |
| Revenue Per Video Complete | money | 25.767257 |  | The revenue per video completion. |
| Cost Per Video Complete | money | 22.767257 |  | The cost per video completion. |
| Video Completion Rate | double | 1.12359550561797% | (Video Completions/Total Impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage . |
| Video Start Rate | double | 1.12359550561797% |  | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Skip Rate | double | 1.12359550561797% |  | The percentage of times the user opted to skip the video. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, select **Prebid Server Premium &gt; Analytics &gt; Prebid Server Analytics**
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to
      view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name
      this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Select **Run report** to send your report request.

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Working with Segments](working-with-segments.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
