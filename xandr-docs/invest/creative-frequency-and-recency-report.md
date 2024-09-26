---
title: Microsoft Invest - Creative Frequency and Recency Report
description: Learn how the Creative Frequency and Recency report lets you view how often and how frequently users are viewing a specific advertiser's creatives. The page lists and explains the different parameters of this report.  
ms.date: 10/28/2023
---

# Microsoft Invest - Creative frequency and recency report

The Creative Frequency and Recency report lets you view how often and how frequently users are viewing a specific advertiser's creatives.

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

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, select the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|--|--|--|
| Insertion Order | Yes | The insertion order under which the impression was purchased. |
| Line Item | Yes | The line item under which the impression was purchased. For more information about line items, see [Working with Line Items](working-with-line-items.md) . |
| Campaign | Yes | The campaign that purchased this impression. (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Creative | Yes | The creative that we're reporting on the frequency and/or recency of. |
| Media Type | Yes | The media type is the general display style of the creative. |
| Size | Yes | The size of the creative; for example, `"300x250"`. |
| Creative Recency | Yes | How recently the creative was viewed by the user. For more information, see [Creative Recency Definitions](#creative-frequency-definitions). |
| Creative Frequency | Yes | How many times the creative has been viewed by the user. For more information, see [Creative Recency Definitions](#creative-frequency-definitions). |
| IO: Trafficker (reporting label) | Yes | The trafficker associated with this insertion order. This is an insertion order reporting label; for more information, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| IO: Sales Rep (reporting label) | Yes | The sales rep associated with this insertion order. This is an insertion order reporting label; for more information, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| IO: Type (reporting label) | Yes | The type of insertion order. This is an insertion order reporting label; for more information, see Working with [Working with Insertion Orders](working-with-insertion-orders.md). |
| LI: Type (reporting label) | Yes | The type of line item. This is a line item reporting label; for more information, see [Working with Line Items](working-with-line-items.md). |
| LI: Trafficker (reporting label) | Yes | The trafficker associated with this line item. This is a line item reporting label; for more information, see [Working with Line Items](working-with-line-items.md). |
| LI: Sales Rep (reporting label) | Yes | The sales rep associated with this line item. This is a line item reporting label; for more information, see [Working with Line Items](working-with-line-items.md). |
| Campaign: Test/Control (reporting label) | Yes | The test/control segment associated with the campaign. (Does not apply to all advertisers.) |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Videos Served | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Video Completions | The total number of times the video creatives played for the entire duration. |
| 75% Video Complete | The total number of times the video creatives completed 75% of the entire duration. |
| 50% Video Complete | The total number of times the video creatives completed 50% of the entire duration. |
| 25% Video Complete | The total number of times the video creatives completed 25% of the entire duration. |
| Video Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Video Errors | The total number of times a video error occurred. |
| Video Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Total Conversions | The total number of post-view and post-click conversions. |
| Imps | The total number of impressions. |
| Clicks | The total number of clicks. |
| Total Cost eCPA | The total cost per conversion. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Media Cost | The total amount of media cost across both managed publishers and RTB inventory. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Booked Revenue | The revenue received from the advertiser. |
| Revenue Per Video Complete | The revenue per video completion. |
| Video Completion Rate | The ratio of video completions to impressions, expressed as a percentage (video completions/total impressions). |
| Post Click Conversion Rate | The ratio of post-click conversions to impressions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Video Skip Rate | The percentage of times the user opted to skip the video. |
| Video Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Post View Conversions | The number of post-view conversions. For more information about how we attribute post-view conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Conversions | The number of post-click conversions. For more information about how we attribute post-view conversions, see [Conversion Attribution](conversion-attribution.md). |
| Cost Per Video Complete | The cost per video completion. |
| Cost eCPM | The cost per mille (1000 impressions). |
| Cost eCPC | The cost per click. |
| Cost eCPA | The cost per acquisition/conversion. |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Post View Revenue | The amount of revenue derived from post-view conversions. |
| Post Click Revenue | The amount of revenue derived from post-click conversions. |
| Profit eCPA | Profit per conversion. |
| Profit eCPC | Profit per click. |
| Profit eCPM | Profit (defined as booked revenue minus total cost) per 1,000 imps. |
| Profit Margin | Buyer profit margin. |
| Profit | Booked revenue minus total cost. |

## Creative recency definitions

| Value | Name | Definition |
|--|--|--|
| -2 | no-cookie-data | The cookie lookup failed. |
| -1 | no-cookie | The user does not have cookies enabled. |
| 0 | < 1 minute | The user has never viewed the creative or last viewed the creative less than 1 minute ago. |
| 8 | 1-2 days | The user last viewed the creative between 1 and 2 days ago. |
| 5 | 1-4 hours | The user last viewed the creative between 1 and 4 hours ago. |
| 1 | 1-5 minutes | The user last viewed the creative between 1 and 5 minutes ago. |
| 7 | 12-24 hours | The user last viewed the creative between 12 and 24 hours ago. |
| 11 | 14-30 days | The user last viewed the creative between 14 and 30 days ago. |
| 3 | 15-30 minutes | The user last viewed the creative between 15 and 30 minutes ago. |
| 9 | 2-7 days | The user last viewed the creative between 2 and 7 days ago. |
| 4 | 30-60 minutes | The user last viewed the creative between 30 and 60 minutes ago. |
| 6 | 4-12 hours | The user last viewed the creative between 4 and 12 hours ago. |
| 2 | 5-15 minutes | The user last viewed the creative between 5 and 15 minutes ago. |
| 10 | 8-14 days | The user last viewed the creative between 8 and 14 days ago. |

## Creative frequency definitions

Please note that the below buckets refer to the lifetime of the user and the lifetime of the creative. For example, if a user falls into the 21-40 bucket, that means they have seen this creative between 21 and 40 times since the user's cookie was first created and the creative first served.

| Value | Name | Definition |
|--|--|--|
| -2 | no-cookie-data | The cookie lookup failed. |
| -1 | no-cookie | The user does not have cookies enabled. |
| 0 | 0 | The user had not viewed the creative prior to the current impression. |
| 1 | 1 | The user viewed the creative one time prior to the current impression. |
| 2 | 2-5 | The user viewed the creative between 2 and 5 times prior to the current impression. |
| 3 | 6-10 | The user viewed the creative between 6 and 10 times prior to the current impression. |
| 4 | 11-20 | The user viewed the creative between 11 and 20 times prior to the current impression. |
| 5 | 21-40 | The user viewed the creative between 21 and 40 times prior to the current impression. |
| 6 | 41-60 | The user viewed the creative between 41 and 60 times prior to the current impression. |
| 7 | 61-100 | The user viewed the creative between 61 and 100 times prior to the current impression. |
| 8 | 101-150 | The user viewed the creative between 101 and 150 times prior to the current impression. |
| 9 | 151-250 | The user viewed the creative between 151 and 250 times prior to the current impression. |
| 10 | 251-500 | The user viewed the creative between 251 and 500 times prior to the current impression. |
| 11 | 500+ | The user viewed the creative 500 times or more prior to the current impression. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured)

    Or, from the Publishers top menu, select on **Prebid Server Premium \> Analytics \> Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.
  
   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
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
1. Select **Run report** to send your report request.
