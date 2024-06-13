---
title: Prebid Server Premium Health Analytics Report
description: In this article, learn about the Prebid Server Premium health analytics report along with the dimensions and metrics associated with it.
ms.date: 10/28/2023
---

# Prebid Server Premium health analytics report

The Prebid Server Premium Health Analytics Report allows users to analyze data related to bid requests and transactions with their configured demand partners. This report is most useful in troubleshooting known issues and proactively identifying optimization opportunities.

> [!IMPORTANT]
> The Health Analytics Report is based on **sample data multiplied to estimate the full volume of PSP activity**. It is not intended to be used for delivery and revenue reporting. The [Prebid Server Premium Seller Analytics Report](prebid-server-premium-seller-analytics.md) and other [Microsoft Monetize reports](reporting-guide.md) should be used for those purposes.

The data in this report can also be accessed via the [Report Service API](../digital-platform-api/report-service.md). For more information, see [Prebid Server Premium Health Analytics API documentation](../digital-platform-api/prebid-server-premium-health-analytics.md).

## Time frame

### Ranges

Time ranges define the time period of the data extracted for the report. Following is a complete list of applicable time ranges available for this report.

- Custom: User defined fixed range.
- Today
- Last 24 Hours
- Yesterday
- Last 48 Hours
- Last 2 Days
- Last 7 Days
- Last 14 Days
- Month To Date
- Month To Yesterday
- Last 30 Days
- Last Month
- Quarter to Date
- Lifetime

### Intervals

Intervals determine how your data is grouped together into rows in the report response. Following is a complete list of intervals  available for this report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

### Timezone

Select the appropriate timezone from the dropdown list.

## Data retention period

Data in this report is retained for the past 33 days of activity.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Ad Size | Yes | The dimensions of the ad slot. |
| Allowed Media Type | No | The category of creative enabled by the publisher on the Monetize placement. For example: `banner`, `video`, `native`. |
| Application | Yes | The specific application used on the device. |
| Bidder | No | The bidder (Prebid Server). |
| Browser Code Name | No | The specific version of the browser. |
| Country Name | Yes | The name of the country in which the impression served. For example, `United States`. |
| Datacenter | Yes | The data center used to route the request to demand partners. |
| Demand Partner | Yes | The partner to which the request was sent and from which the response (if any) was received. |
| Device Browser | Yes | The browser used on the device. For example, `Chrome`, `Safari`, etc. |
| Device OS Extended | Yes | The specific version of the operating system. For example, `iOS 16.0.0`. |
| Device OS Family | Yes | The operating system of the device. For example, `Microsoft Windows`, `Apple iOS`, etc. |
| Device Type | Yes | The category of device. For example, `desktops`, `mobile phones`, etc. |
| Error | Yes | The category of error related to the bid response. For details, see the [Error Types](#error-types) section below. |
| External Creative | Yes | The external ID associated with the creative served. |
| Inventory URL | Yes | The mapped URL from the detected domain on the ad call and the ID in parentheses. For example, `"myurl.com/(1234)"` |
| Media Type | Yes | The category of creative on transacted impressions. For example: `banner`, `video`, `native`. |
| Placement | Yes | The name and ID of the placement through which the request originated. |
| Placement Group | Yes | The placement group (a collection of placements) that includes the placement through which the request originated. |
| Publisher | Yes | The publisher on whose inventory the request originated. |
| SDK Version | Yes | The version of the software development kit present in the app. |
| Supply Type | Yes | The category of inventory (`web`, `mobile web`, or `app`). App includes CTV and mobile. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Average Clear Price | The sum of bid price for delivered impressions divided by the number of bid requests sent. |
| Average Response Time | The average time demand partners took to respond to bid requests. |
| Bid Requests Sent | The number of requests sent from Prebid Server Premium to demand partners. |
| Bid Responses Received | The number of bid responses received by Prebid Server Premium from demand partners. |
| Bids Submitted to Ad Server | The number of ad requests that had a valid Prebid bid that was not subject to any additional Microsoft Advertising rejections returned to the ad server. This number is counted after the Microsoft Advertising auction process that evaluates bids received from all sources. The reduced volume between Valid Bids on Imps and this metric could be due to creative requirements not being met, being outbid by other bidders, or due to the option to [send only the top bid back to the ad server](integrate-web-mobile-web-with-psp.md). |
| Errors | The number of errors in bid responses from demand partners. |
| Errors Rate | The number of bid errors divided by the number of bid requests sent to demand partners. |
| Imps (delivered) | The number of impressions successfully delivered and ads rendered. Note this report is based on sample log data multiplied to estimate the full volume of PSP activity and does not represent final delivery. |
| No Bid Rate | The number of times demand partners did not bid divided by the number of bid requests sent to demand partners. |
| No Bids | The number of times demand partners did not bid on a request. This does not include bid errors. |
| Total Bid Price | The sum of the bid values received from demand partners. |
| Total Buyer Spend | The media cost to buyers of impressions delivered. <br><br> **Note**: This report is based on sample log data multiplied to estimate full volume of PSP activity and does not represent final delivery. |
| User Matched Requests | The number of requests where a user identifier was present. Note this metric currently only includes cookies for web and mobile web. |
| User Matched Requests Rate | The number of user matched requests divided by the number of bid requests sent to demand partners. |
| Valid Bids On Impression Rate | The number of valid bids divided by the number of bid requests sent to demand partners. |
| Valid Bids On Imps | The number of bids received from demand partners that do not trigger errors, have a creative ID, and have a bid above $0. There may be multiple bids counted for each auction when multiple demand partners return bids. |
| Win Rate | This metric should only be used with the demand partner dimension applied. It represents the percentage of impressions delivered by a demand partner relative to the total bid responses received. The calculation involves dividing the number of impressions delivered by the demand partner by the total number of bid responses received.|

## Error types

| Code | Error | Description | Remedy |
|---|---|---|---|
| 0 | `NONE` | No error. | None needed. |
| 1 | `INTERNAL` | There is a server-side error from Demand Partner, such as a 400 status code. | Seller should work with Microsoft Advertising to collect a specific example code to share with Demand Partner for investigation. |
| 2 | `TIMEOUT` | Demand Partner did not respond within the timeout limit. | Either increase timeout settings to allow for a longer response time or contact Demand Partner to inform them of the restriction. For more information on timeouts, see [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md). |
| 3 | `CLIENT` | Demand Partner's Prebid Server adapter generated an error. | For significant quantities of this error type, Seller should contact Microsoft Advertising support to diagnose issues by looking at the internal Microsoft Advertising logs. An example of this error could be that video supply has been sent to an adapter that does not support it. |
| 4 | `PARSE` | Demand Partner has formatted the bid response incorrectly. | Seller should work with Microsoft Advertising and Demand Partner to determine and resolve the specific formatting issue. |
| 21 | `NO_BID_PRICE` | No price received from Demand Partner. | Seller should notify Demand Partner of the issue. |
| 22 | `NO_CREATIVE_ID` | No creative ID received from Demand Partner. | Seller should notify Demand Partner of the issue. |
| 23 | `NEC_ERROR` | The bid was rejected during the Microsoft Advertising auction process. | The bid was successfully received from Demand Partner, but the bid was rejected within the Microsoft Advertising auction. Seller can use the seller bid error report to diagnose specific rejections occurring on their supply. |
| 24 | `CREATIVE_WRONG_SIZE` | Demand Partner is bidding with a creative size that doesn't match the tag size. | Seller should review the creative size and notify Demand Partner regarding the mismatch. |
| 70 | `MEMBER_NOT_ELIGIBLE` | Seller's settings are blocking the Buyer's member from participating in the auction. | Seller should notify the buyer that they are currently blocked from bidding. |
| 84 | `CATEGORY_REQ_ALLOWLIST` | The category of the creative is sensitive and requires addition to the allowlist. | Seller should work with Buyer to determine if the creative warrants addition to the allowlist. |
| 132 | `DYN_CREATIVE_INCOMPATIBLE_TYPE` | Dynamic ad-markup bidding is not supported for certain PSP demand partners that require client-side rendering when a Seller doesn't support it. | Seller should correct their setup to align with client-side rendering requirements, on both supply and PSP sides. |
| 150 | `SELLER_MEMBER_NO_CONTRACT` | Seller's contract isn't set up properly. | Seller should work with Microsoft Advertising to remedy the contract issue. |

> [!NOTE]
> For additional possible error codes, see [Bid Error Codes](../bidders/bid-error-codes.md).

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).

    Or, from the **Publishers** top menu, click on **Prebid Server Premium** > **Analytics** > **Prebid Health Analytics**

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

## Related topics

- [Prebid Server Premium Seller Analytics Report](prebid-server-premium-seller-analytics.md)
- [Reporting Guide](reporting-guide.md)
- [Bid Error Codes](../bidders/bid-error-codes.md)
