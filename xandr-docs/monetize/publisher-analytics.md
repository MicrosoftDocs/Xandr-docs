---
title: Microsoft Monetize - Publisher Analytics
description: In this article, learn about the Publisher Analytics report along with the dimensions and metrics associated with it.
ms.date: 10/28/2023
---

# Microsoft Monetize - Publisher analytics

The Publisher Analytics Report allows you to view sell-side performance data for a specific publisher. The data available via this report is even more granular than what you can get from the [Network Analytics Report](network-analytics-report.md).

## Navigation

1. Go to **Reporting** > **Report Center** and click **Create New**
2. In **Search for a Report** search box, type the report name
3. The relevant report widget will be shown under its category such as **Analytics**, **Troubleshooting** or **Reach**.
4. Click on **Create new report** button to create the new report.
   
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

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data. However, daily, monthly and cumulative intervals are still available.
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match statistics shown elsewhere in Microsoft Monetize for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months is aggregated. The data from Billing reports are kept in non-aggregated form indefinitely.

## Real time data

Real Time Data is a new feature being offered within this report (not all users have access yet). Traditionally, reports have had a 2 hour built-in delay to allow for a fuller reconciliation with conversions, impressions and other metrics associated with transactions. However, in some cases, it is important to have up-to-the-minute information even if it has not been fully reconciled yet. Dimensions which support the real-time option are marked with the clock icon.

:::image type="content" source="media/real-time-data-reporting.png" alt-text="Diagram that shows when Real-time data and Finalized data are available in relation to the time of event.":::

- To use this new feature, set the **Real Time Data** field to **Included**. This will cause the data in your report to contain both real-time and the more fully reconciled batch file data. If you want the report to break out the real-time data from batch file data, select the **Real-Time status** checkbox.
- Do not use information in the real-time data portion of your report to bill your clients as that data may change slightly once fully reconciled within 2 to 4 hours. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Adjustments | No | Changes to reported revenue based on factors such as revenue, conversions, clicks, or impressions reported by an advertiser's or agency's ad servers. |
| Advertiser | Yes | The specific advertiser that purchased the impression. |
| Brand | Yes | The brand associated with the creative that served on the impression. For more information about how to set up your brand preferences, see [Working with Network Ad Quality](working-with-network-ad-quality.md) and [Working with Ad Quality](working-with-publisher-ad-quality.md). For impression type "Resold", no information is available in the **Brand** field for this report. See the [Seller Brand Review Report](seller-brand-review-report.md) instead. |
| Buyer | Yes | The member whose advertiser purchased the impression. |
| Country | Yes | The country where the impression occurred. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Deal Code | Yes | The custom code for the deal. For deals with external supply partners, this is typically the string used to identify the deal.|
| External Code | No | The name and ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). |
| Filtered Request Reason | No | The reason the ad request was filtered out by Microsoft Advertising prior to bidding. |
| Is Takeover |Yes| Indicates whether an impression was `Blanked` or `Defaulted` due to at least one ad in the multi-ad request being a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|
| Impression Type | Yes | The type of impression that occurred. For the definitions of each impression type, see the [Impression Type Definitions](#impression-type-definitions) section below. |
| Line Item | No | The line item under which the impression was purchased. For more information about line items, see [Working with Line Items](working-with-line-items.md). |
| Media Type | Yes | The media type associated with the creative that served on this impression. |
| Payment Rule | Yes | The publisher's payment rule in effect on this impression, if any. For more information about payment rules, see [Working with Payment Rules](working-with-payment-rules.md). |
| Payment Type | Yes | How the publisher is being paid for the impression. For example, the publisher could be getting paid via revenue sharing ("revshare"). For the definitions of each payment type, see [Payment Type Definitions](#payment-type-definitions) below. |
| Placement | Yes | The placement where the impression occurred. For more information about placements, see [Working with Placements](working-with-placements.md). <br><br> **Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Placement Group | Yes | The placement group to which the sold inventory belonged. The hierarchy of sell-side objects is **Publisher** > **Placement Group** > **Placement**. For more information, see [Working with Placement Groups](working-with-placement-groups.md). <br><br> **Note**: For impressions older than 100 days, the ID will be `0`. |
| Revenue Type | Yes | How the impression is being paid for by the buying member. For example, the buying member could be paying a flat CPM rate. For the definitions of each revenue type, see the [Revenue Type Definitions](#revenue-type-definitions) section below. |
| Selling Currency | Yes | The transaction currency used by the seller to sell this impression. Including this dimension will cause the monetary metrics to be displayed in the selling currency. |
| Size | Yes | The size of the creative that served, for example, `"300x50"`. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the **Split** column, if included, will be `null`. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

### Impression type definitions

| Value | Name | Definition |
|---|---|---|
| 1 | Blank | No creative was delivered. |
| 2 | PSA | A PSA creative was served. |
| 3 | Default Error | Your default creative served due to a timeout issue. |
| 4 | Default | Your default creative served because there were no valid bids. |
| 5 | Kept | Your advertiser's creative served on your publisher's site. |
| 6 | Resold | Your publisher's impression was sold to a third party. |
| 7 | RTB | Your advertiser's creative served on third-party inventory. |
| 8 | PSA Error | A PSA served due to a timeout issue or lack of a default creative. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |

### Revenue type definitions

| Column | Description |
|---|---|
| No Payment | Revenue was not tracked. |
| Flat CPM | A flat payment per 1000 impressions. |
| Cost Plus CPM | Media cost (what was spent on inventory), plus an extra CPM. |
| Cost Plus Margin | Media cost (what was spent on inventory), plus a percentage of spend. |
| CPC | A flat payment per click. |
| CPA | A flat payment per conversion. |
| Revshare | The selling member gets paid a percentage of the ad revenue. |

### Payment type definitions

| Column | Description |
|---|---|
| No Payment | Revenue was not tracked. |
| Flat CPM | A flat payment per 1000 impressions. |
| Cost Plus CPM | Media cost (what was spent on inventory), plus an extra CPM. |
| Cost Plus Margin | Media cost (what was spent on inventory), plus a percentage of spend. |
| CPC | A flat payment per click. |
| CPA | A flat payment per conversion. |
| Revshare | The publisher gets paid a percentage of the ad revenue. |
| Flat Fee | The publisher gets paid a flat fee, usually agreed upon in advance. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| 25% Video Complete | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Video Complete | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Video Complete | The total number of times the video creatives completed 75% of the entire duration. |
| Clicks | The total number of clicks. |
| Conversion Rate | The ratio of conversions to impressions. |
| Conversions Per Million | The number of conversions per million impressions. |
| Cost Per Video Complete | The cost per video completion. |
| CTR | The click-through rate – the ratio of clicks to impressions. |
| Filtered Requests | The total number of bid requests for which Microsoft Advertising did not hold an auction due to inventory quality concerns. |
| Impression Requests | The total number of ad calls (impression requests). <br><br> **Warning**: This metric is typically inaccurate for video inventory due to occasional delays in receiving video events, which can lead to inflated request totals based on the assumption that the video has expired. For a better video request metric, you should use Ad Requests in the S[eller Fill and Delivery Network Report](seller-fill-and-delivery-network-report.md) or [Network Video Analytics Report](network-video-analytics-report.md). |
| Imps | The total number of impressions. |
| Imps (blank) | The number of blank impressions. |
| Imps (default error) | Impressions where a default creative served due to a timeout issue. |
| Imps (default) | Impressions where a default creative served because there were no valid bids. |
| Imps (kept) | A kept impression is one in which your managed advertiser's creative serves on your managed publisher's site. |
| Imps (master creative) | The number of page-level roadblocks that served the master creative. <br><br> **Note**: **Alpha-Beta Notice** <br> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Imps (Master Creative) | The number of page-level roadblocks that served the master creative. <br><br> **Note**: **Alpha-Beta Notice** <br> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Imps (PSA error) | Like **Imps (PSA)** above, except that the PSA is serving due to a timeout issue, as opposed to a lack of valid bids. |
| Imps (PSA) | The number of impressions that showed PSAs (Public Service Announcements). PSAs are served only if there is no other creative to serve. |
| Imps (resold) | A resold impression is one that is resold to a third-party buyer. |
| Imps (RTB) | Impressions your advertiser bought from a third party. |
| Network PPM | **Deprecated**. Total Network profit per thousand impressions (Total Network RPM - Total Publisher RPM). This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Network Profit | The sum of booked revenue and reseller revenue minus total cost.<br>This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Network Profit eCPA | Network profit per conversion. |
| Network Profit eCPC | Network profit per click. |
| Network Profit eCPM | Network profit per thousand impressions. |
| Network Profit Margin | Network profit margin. |
| Network Revenue | Total Network revenue. This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Network ROI | **Deprecated**. Return on investment for the Network. This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. |
| Post Click Convs | The number of post-click conversions. For more information about how we attribute post-view and other conversions, see [Conversion Attribution](conversion-attribution.md). |
| Post View Conversions | The number of post-view conversions. For more information about how we attribute post-view and other conversions, see [Conversion Attribution](conversion-attribution.md). |
| Profit eCPA | Profit per conversion. |
| Profit eCPC | Profit per click. |
| Profit eCPM | Profit per thousand impressions. |
| Profit Margin | Buyer profit margin. |
| Publisher Revenue | Total publisher revenue. This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Revenue Per Video Complete | The revenue per video completion. |
| Sold Network RPM | Network revenue per 1000 impressions that were not defaults, PSAs, or errors. This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Sold Publisher RPM | Publisher revenue per 1000 impressions that were not defaults, PSAs, or errors.This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Total Conversions | The total number of conversions. |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPA | The total cost per conversion. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Publisher RPM | Publisher revenue per 1000 impressions, including defaults, PSAs, or errors. This value will be displayed in USD as well as potentially the Selling Currency if you've selected that dimension. |
| Total RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. |
| Video Completion Rate | The ratio of video completions to impressions, expressed as a percentage (video completions/total impressions). |
| Video Completions | The total number of times the video creatives played for the entire duration. |
| Video Errors | The total number of times a video error occurred. |
| Video Skip Rate | The percentage of times the user opted to skip the video. |
| Video Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| Video Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Videos Served | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| View-Measured Imps | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| Viewable Imps | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu depending on how your account has been configured.

    Or, from the **Publishers** top menu, click on **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter by clicking **Edit**, a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
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

- [Publisher Reporting](publisher-reporting.md)
- [Seller Site Domain Report](seller-site-domain-report.md)
