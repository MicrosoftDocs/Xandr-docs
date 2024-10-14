---
title: Microsoft Invest - Buyer Geo Analytics Report
description: Learn about the Buyer Geo Analytics report that allows you to break down delivery and performance based on specific geographic area.
ms.date: 10/28/2023
---

# Microsoft Invest - Buyer Geo Analytics report

The **Buyer Geo Analytics** report allows you to break down delivery and performance by geographic area. Sample use cases for this report include:

- Buyers who would like to optimize their ad campaigns.
- Buyers who need to report to their client advertisers or agencies on line item delivery by geo.

This report can break down performance along the following geographic boundaries:

- **Country**: The user's [Country](../digital-platform-api/country-service.md).
- **Region/State**: The user's [Region](../digital-platform-api/region-service.md), e.g., Baja California or California.
- **Metro Code**: The user's [Metro Code](../digital-platform-api/designated-market-area-service.md).
- **Political Districts**: The user's [Political District](../digital-platform-api/political-district-service.md) (US Only).

For more information on the available data fields and their definitions, see [Dimensions](#dimensions) and [Metrics](#metrics) below.

> [!IMPORTANT]
> There is a limitation to how accurate the geo data is, particularly on impressions bought from external supply partners. Since some external supply partners (such as Google Ad Manager) truncate the last octet of the user's IP, we have a less precise IP to use when performing an IP geo-lookup. As a result, our geo data may not always be completely accurate at granular levels (such as region and metro code) for impressions bought from these supply sources.

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

> [!IMPORTANT]
> The **Filter?** column below shows whether a dimension can be used as a filter as well as being used to group by.

| Column | Filter? | Description |
|:-------|:--------|:------------|
| Advertiser | Yes | The advertiser name and ID, in the format "Great Advertiser (456)". |
| Insertion Order | Yes | The insertion order name and ID, in the format "Midwest Winter Getaways (789)". |
| Line Item | Yes | The line item name and ID, in the format "Kansas City Winter Commuters (314)". |
| Campaign | Yes | The campaign name and ID associated with the auction, in the format "South Texas Ford Drivers (123)". (Does not apply to all advertisers.) |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the **Split** column (if included) will be null. |
| City | No | The city in which the user is located. |
| Postal Code | No | The postal (zip) code in which the user is located. |
| Country | Yes | The country of the user's location, both name and code, in the format "France (FR)". The string "250" can appear in cases where we don't know the country or if the country doesn't map correctly to a location in our database. |
| Region | Yes | The region or state name and country code of the user's location, in the format "Baden-Wurttemberg (DE)". The string "4192" can appear in cases where we don't know the region/state or if the region/state doesn't map correctly to a location in our database. |
| Metro Code | Yes | The name and ID of the metro code of the user's location, in the format "New York NY (501)". The string "unknown values (-1)" can appear in cases where we don't know the metro code or if the metro code doesn't map correctly to a location in our database. <br/> **Note:** Our reporting derives metro codes from the city logged for the auction. However, our geo provider is sometimes unable to determine a city from the IP address associated with the impression, even when the metro code **is** determined. Therefore, there are cases where a line item targeting a specific metro code has impressions in reporting showing a metro code of 1. |
| Campaign Code | No | The custom code for the campaign. |
| State House District | Yes | The State House District of the user's location. |
| State Senate District | Yes | The State Senate District of the user's location. |
| Congressional District | Yes | The Congressional District of the user's location. |
| Buying Currency | No | The transaction currency used by the buyer to purchase this impression. |
| UK Constituent Country | No | The Constituent Country of the user's location. This is applicable for United Kingdom. Possible values include: <br/> - England <br/> - Scotland <br/> - Wales <br/> - Northern Ireland |

> [!NOTE]
> In addition, you can also filter on:
>
> - one or more conversion pixels using the **Conversion Pixel** filter.
> - a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Formula | Description |
|:-------|:-----|:--------|:------------|
| Imps | int | Imps | The total number of impressions (served and resold). |
| Clicks | int | Clicks | The total number of clicks across all impressions. |
| CTR % | double | (Clicks / Imps) x 100 | The rate of clicks to impressions, expressed as a percentage. |
| Total Conversions | int | Total Convs | The total number of post-view and post-click conversions. |
| Conversion Rate | double | Total Convs / Imps | The ratio of conversions to impressions. |
| Booked Revenue | money | Booked Revenue | The total revenue booked through direct advertisers (line item). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post View Conversions | int | Post View Convs | The total number of recorded post-view conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post Click Conversions | int | Post Click Convs | The total number of recorded post-click conversions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPM | money |  | The total revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPC | money |  | The total revenue, expressed as eCPC. For definitions of eCPC and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPA | money |  | The total revenue, expressed as eCPA. For definitions of eCPA and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPC | money |  | The effective cost per click. For definitions of eCPC and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPA | money |  | The effective cost per acquisition (conversion). For definitions of eCPA and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost | money | Cost | The total cost of the inventory purchased. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit | money | Booked Revenue - Cost | The booked revenue minus total cost. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| CPM | money | CPM | The cost per one thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Total Cost | money | Media Cost + Data Costs + Partner Fees + Commissions + Serving Fees + Publisher Revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | money | (Total Cost/Imps) * 1,000 | The total cost per 1,000 imps. |
| Total Cost eCPC | money | Total Cost/Clicks | The total cost per click. |
| Total Cost eCPA | money | Total Cost/Conversions | The total cost per conversion. |
| Profit eCPM | money | ((Booked Revenue - Total Cost)/Imps) * 1,000 | Profit per thousand impressions. |
| Profit eCPC | money | (Booked Revenue - Total Cost)/Click | Profit per click. |
| Profit eCPA | money | (Booked Revenue - Total Cost)/Conversion | Profit per conversion. |
| Profit Margin | money | (Booked Revenue - Total Cost)/Booked Revenue | Buyer profit margin. |
| Video Skips | int |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Starts | int |  | The total number of times the first segment of the video creative was downloaded and started. |
| 25% Video Complete | int |  | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | int |  | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | int |  | The total number of times the video creatives completed 75% of the entire duration. |
| Video Completions | int |  | The total number of times the video creatives played for the entire duration. |
| Videos Served | int |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Video Errors | int |  | The total number of times a video error occurred. |
| Revenue Per Video Complete | money |  | The revenue per video completion. |
| Cost Per Video Complete | money |  | The cost per video completion. |
| Video Completion Rate | double | (Video Completions/Total Impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage . |
| Video Start Rate | double |  | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Skip Rate | double |  | The percentage of times the user opted to skip the video. |
| Audience Imps | double |  | The number of impressions served to your desired demographic group. |

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
- [Member Reporting](network-reporting.md)
- [Advertiser Reporting](advertiser-reporting.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
