---
title: Microsoft Monetize - Site Domain Performance
description: Explore performance and optimization data by domain or mobile app with the Site Domain Performance Report for advertisers.
ms.date: 10/28/2023
---

# Microsoft Monetize - Site domain performance

The Site Domain Performance Report lets you view performance and optimization data by domain or mobile app for a specific advertiser.

To view performance and optimization data by domain or mobile app for multiple advertisers, use the [Network Site Domain Performance Report](network-site-domain-performance-report.md).

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

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the
  entire selected time range.

For more information about how quickly report data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Insertion Order | Yes | The name and ID of the insertion order under which the impression was purchased. For more information about insertion orders, see [Working with Insertion Orders](working-with-insertion-orders.md). |
| Line Item | Yes | The name and ID of the line item under which the impression was purchased. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Campaign | Yes | The name and ID of the campaign that purchased this impression. (Does not apply to all advertisers.) |
| Seller | Yes | The seller/publisher who sold the impressions in this data set. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the **Split** column (if included) will be null. |
| Site Domain | No | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: "`deals.unknown`" or "`managed.unknown`". These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| Mobile Application | No | For mobile app impressions, the Apple App Store or Google Play name and ID of the mobile application where the impression occurred, for example, "`Angry Birds (343200656)` or "`Angry Birds (com.rovio.angrybirds)`". |
| Top-level category | No | The name and ID of the top-level content category associated with the domain; for example, "`Shopping (19821)`". |
| Second-level category | No | The name and ID second-level content category associated with the domain; for example, "`Shoes (20129)`". |
| Remarketing Segment | No | Indicator of whether this is a remarketing campaign. |
| Age | Yes | The age of the user associated with the impression. For impressions older than 100 days, the age will be "unknown". |
| Gender | Yes | The gender of the user. For impressions older than 100 days, the gender will be "unknown". |
| Fold Position | Yes | The fold position of the impression (i.e., where on the page the placement is located).<br>Possible values for impressions:<br> - unknown<br> - above<br> - below |
| Operating System Family | Yes | The operating system family (e.g., Apple Mac, Chrome OS) associated with the impressions. |
| Operating System | Yes | The name and ID of the operating system of the device where the impression occurred. |
| Supply Type | Yes | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are "`web`", "`mobile_app`", and "`mobile_web`". |
| Conversion Pixel | Yes | The unique identification number of the conversion pixel.<br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. Although Pixel ID groupable, we do not recommend that you group by this dimension since doing so will cause conversion events to then be shown in separate rows from impression and click events. We generally assume you want to view all of these events in a single row so as to be able to retrieve accurate and aggregated values for conversion rate and cost-per-conversion calculations. As a result, we instead recommend that you filter by Pixel ID so you can retrieve conversion counts and related metrics for your most relevant pixel IDs. |
| Deal | Yes | The deal through which this impression was purchased. |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the monetary metrics to be displayed in the buying currency. This dimension is available only when Currency 2.0 is disabled. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions served. |
| Clicks | The total number of clicks recorded. |
| CTR | The click-through-rate; that is, the ratio of clicks to impressions. |
| Conversion Rate | The ratio of conversions to impressions. |
| Conversions Per Million | The number of conversions per million impressions. |
| Booked Revenue | The revenue received from the advertiser. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Revenue eCPM | The revenue, expressed as CPM. For definitions of CPM and other terms, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPC | The revenue, expressed as CPC. For definitions of CPC and other terms, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Revenue eCPA | The revenue, expressed as CPA. For definitions of CPA and other terms, see the [Industry Reference Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| Post View Conversions | The total number of post-view conversions recorded. For more information about how we record post-view conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post Click Conversions | The total number of post-click conversions recorded. For more information about how we record post-click conversions, see [Conversion Attribution](conversion-attribution.md). |
| Media Cost | The cost to the buying member for this inventory. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPC | The cost per click. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Cost eCPA | The cost per acquisition/conversion. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit | Booked revenue minus total cost.<br>This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Profit eCPM | The profit (defined as booked revenue minus total cost) per 1,000 imps.<br>This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| CPM | The cost per thousand impressions. This value will be displayed in USD as well as potentially the Buying Currency (if you've selected that dimension). |
| Post View Conversion Rate | The ratio of post-view conversions to impressions. |
| Post Click Conversion Rate | The ratio of post-click conversions to impressions. |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Profit eCPC | Profit per click. |
| Profit eCPA | Profit per conversion. |
| Profit Margin | Buyer profit margin. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   1. Or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \>  **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

   > [!WARNING]
   >  The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

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
