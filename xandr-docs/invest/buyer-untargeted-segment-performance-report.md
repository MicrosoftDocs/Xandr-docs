---
title: Microsoft Invest - Buyer Untargeted Segment Performance Report
description: Learn about the Buyer Untargeted Segment Performance report that offers insights on the non-targeted segment performance in your advertising campaigns.
ms.date: 10/28/2023
---

# Microsoft Invest - Buyer Untargeted Segment Performance report

This report provides buyers with segment performance across multiple ad campaigns and advertisers over untargeted segments. This allows you to:

- Understand the performance of individual untargeted segments across your account.
- Filter for specific conversion pixels to further identify how these segments contribute to your overall buying strategy.

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

## Dimensions

| Column | Filter? | Description |
|:-------|:--------|:------------|
| Advertiser | Yes | The advertiser name and ID, in the format "Great Advertiser (456)". |
| Insertion Order | Yes | The insertion order associated with the impression, in the format "Midwest Winter Getaways (789)". |
| Line Item | Yes | The line item associated with the impression, in the format "Kansas City Winter Commuters (314)". |
| Campaign | Yes | The campaign associated with the impression, in the format "South Texas Ford Drivers (123)". (Does not apply to all advertisers.) |
| Campaign Code | No | The ID associated with a campaign by Microsoft Advertising platform or by user as an external code. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Segment | Yes | The user segment associated with the impression in the format "Submitted application (220)". |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the monetary metrics to be displayed in the buying currency. |
| Is Targeted | Yes | Whether a user segment is targeted or not by advertiser. |
| Is Advertiser Segment | Yes | Whether a target segment is an advertiser segment. |
| Campaign Group Type Id | No | The ID for a campaign group type. For example, Buy direct/third-party inventory. |
| Segment Owner Member Id | No | The member ID of the user segment owner. |

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
| Total conversions | int | 5 | total_convs | The total number of post-view and post-click conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Conversion Rate | double | 0.000221877080097626 | Total Convs / Imps | The ratio of conversions to impressions. |
| Conversion per Million | double | 384.4 | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post View Conversions | int | 15 | Post View Conversions | The total number of recorded post-view conversions. |
| Post View Conversion Rate | int | 15 | Post View Convs | The total number of recorded post-view conversions. |
| Post View Revenue | money | 450.00 | Post View Revenue | The total revenue booked through post-view conversions. |
| Post Click Conversions | int | 19 | Post Click Convs | The total number of recorded post-click conversions. |
| Post Click Conversion Rate | int | 19 | Post Click Convs | The total number of recorded post-click conversions. |
| Post Click Revenue | money | 450.00 | Post Click Revenue | The total revenue booked through post-click conversions. |
| Booked Revenue | money | 450.00 | Booked Revenue | The total revenue booked through direct advertisers. |
| Revenue eCPM | money | 1.234 |  | The total revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPC | money | 1.234 |  | The total revenue, expressed as eCPC. For definitions of eCPC and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPA | money | 1.234 |  | The total revenue, expressed as eCPA. For definitions of eCPA and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Media Cost | money | 100.00 | Cost | The total cost of the inventory purchased. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit | money | 4.14 | **During the transition period:** Booked Revenue - Media Cost <br/> **After the transition period:** Booked Revenue - Total Cost | **During the transition period:** Booked revenue minus media cost. <br/> **After the transition period:** Booked revenue minus total cost. <br/> This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| CPM | money | 5.00 | CPM | The cost per one thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPA | money | 1.1111 | media_cost / total_convs | The cost per acquisition/conversion. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPC | money | 123.45 | Cost/Clicks | The cost per click. |
| Profit eCPM | money | 0.4949 | **During the transition period:** (Booked Revenue - Media Cost) / Imps * 1000 <br/> **After the transition period:** (Booked Revenue - Total Cost) / Imps * 1000 | Profit per thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Commissions | money | 0 | **During the transition period:** Commissions + equivalent partner_fees. <br/> **After the transition period:** $0. Commissions created on ALIs prior to this date will be automatically migrated to **partner_fees**. Previous data will not be impacted. | Fees that come out of the booked revenue. <br/> **During the transition period:** Commissions + equivalent partner fees. <br/> **After the transition period:** $0. Commissions created on ALIs prior to this date will be automatically migrated to partner fees. Previous data will not be impacted. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium &gt; Analytics &gt; Prebid Server Analytics**
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
