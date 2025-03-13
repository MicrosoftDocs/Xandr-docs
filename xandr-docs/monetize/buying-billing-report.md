---
title: Microsoft Monetize - Buying Billing Report
description: Learn how Billing Report can be used to manage internal invoicing for your advertisers across both managed and third-party buying. This page also explains how to run the report.
ms.date: 10/28/2023
---


# Microsoft Monetize - Buying billing report

The Buying Billing Report allows you to manage internal invoicing for your advertisers across both managed and third-party buying.

If you would like to use this report to analyze your Microsoft Advertising invoice, see [Understanding Your Invoice](understanding-your-invoice.md).

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

> [!NOTE]
> Hourly impression data is available and spans 13 full months. For impressions that are older than 13 months, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight. 
>
> All daily data that is older than 13 months will be timestamped based on the UTC time zone.

## Dimensions

| Column | Filter? | Description |  |
|--|--|--|
| Advertiser | Yes | The advertiser that purchased the impression. |
| Advertiser Code | No | The external ID of the advertiser. |
| BP External Code | No | The optional external code supplied for the insertion order's billing period. |
| Buying Currency | No | The transaction currency that the buyer used to purchase this impression. Including this dimension will cause the **Booked Revenue**, **Buyer Media Cost**, **Auction Service Deduction**, **Net Media Cost Auction Service Fees** and **Creative average Fees** metrics to be displayed in the buying currency. |  |
| Campaign | Yes | The campaign which purchased this impression. (Does not apply to all advertisers.) |
| Campaign Code | No | The external ID of the campaign. (Does not apply to all advertisers.) |
| Clearing Event | Yes | The underlying auction event that was transacted (e.g., impression, viewable impression, completed video). |
| Deal | Yes | The deal associated with the impression. |
| Direct Cleared | Yes | Whether or not the buyer pays the seller directly for the cost of media. <br> For more details, see [Direct Cleared Table](#direct-cleared-table). |
| Impression Type | Yes | See [Impression Types](#impression-types) below for definitions of the different types of impressions. |
| Insertion Order | Yes | The Insertion Order under which this impression was purchased. |
| IO Code | No | The external ID of the insertion order. |
| Is Cross Seat Activity | Yes | Only relevant if you have more than one member/seat on the Microsoft Advertising platform. If you do, this field allows you to know whether the activity was associated with transactions between members you manage and therefore simplify the reconciling of their invoices. |
| Is Deal | Yes | Is there any deal associated with the impression. Different from 'Deal' which is the actual deal id |
| LI Code | No | The external ID of the line item. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Media Type (Billing) | Yes | The video-specific media type classification for billing only. If you don't have video-specific pricing, this field is irrelevant. Possible values are `--`, `Non-Video`, `Video (Hosted)`, and `Video (Non-Hosted)`. |
| Publisher | Yes | The publisher on whose inventory the impression occurred. |
| Seller | Yes | The seller of this impression. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the **Split** column (if included) will be null. |

### Direct Cleared Table

| Value | Description |
|--|--|
| 0 | Microsoft Advertising acts as the clearing house, collecting the cost of media from the buyer and paying the seller |
| 1 | Microsoft Advertising does not clear cash; the buyer pays the seller directly for the cost of media |
| -1 | Dummy value for un-billed activity |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|--|--|
| Ad Serving Fees | Cost of serving an ad when the buyer and seller are within a network + cost of serving an ad charged to the buyer when buying RTB. |
| Auction Service Deduction | The total deductions charged for impressions bought from third parties. These deductions are included in the buyer's media cost and deducted when calculating the seller's payment. |
| Auction Service Fees | Total fees charged for impressions bought from third parties. These fees are charged in addition to the buyer's media cost. |
| Billable Imps | The total number of impressions billed to the client. |
| Booked Revenue | The revenue booked through managed advertisers. |
| Buyer Media Cost | The total amount to be paid for media purchases. When buying impressions, this payment is made to Microsoft Advertising or an external exchange. When selling impressions, this payment is made to the publisher. |
| Clearing Event Booked Revenue eCPM | The total revenue per 1000 events (for the associated clearing event). |
| Clearing Event Booked Revenue Per Event | The total booked revenue per clearing event. |
| Clearing Event Buyer Media Cost eCPM | The total media cost per 1000 events (for the associated clearing event). |
| Clearing Event Buyer Media Cost Per Event | The media cost per clearing event. |
| Clearing Event Units | The total number of events purchased, for the associated Clearing Event. When buying a Clearing Event other than impression (e.g., viewable impressions), the number of billed events will be less than the number of impressions. |
| Clicks | The total number of clicks. |
| Conversions | The total number of post-view and post-click conversions. |
| Creative Hosting Fees (Video) | Fees incurred as a result of hosting your video creatives on our platform. |
| Creative Overage Fees | The total fees charged for hosted creatives that exceed the creative size limit. |
| eCPM Conversion Deduction | The amount that Microsoft Advertising takes out of a guaranteed outcomes bid/payment to cover eCPM conversion and post-auction outcome prediction services. If you aren't using a line item with a guaranteed outcomes payment model, this field's value equals 0. |
| Exchange Cost | The amount taken out of the exchange to give to the seller. If you aren't using a line item with a guaranteed outcomes payment model, this metric's value equals **Net Media Cost**. |
| FX Margin Deductions | Fx Margin deduction for buying members transacting in non-USD currencies |
| FX Margin Fees | Fx Margin fee for buying members transacting in non-USD currencies |
| GO Market Making Fee | The percentage-based fee (risk premium) that Microsoft Advertising takes out of a guaranteed outcomes bid/payment to cover the risk incurred when providing guaranteed outcomes. If you aren't using a line item with a guaranteed outcomes payment model, this field's value equals 0. The target for this fee is 10%, but the actual percentage used varies based on continuously shifting prediction accuracy.<br> - GO Market Making Fee Percentage = Fixed Percentage (10%) ± Prediction Variability (a positive or negative percentage that changes based on shifting prediction accuracy) |
| Net Media Cost | The total amount to be paid for media purchases, less the Auction Service Deduction. |
| Service Deductions | DSP Service deduction for buying members |
| Service Fees | DSP Service fee for buying members |

## Impression types

| Value | Name | Definition |
|--|--|--|
| 5 | Kept | Your creative served on managed inventory.<br>**Note**: We currently only display cost for Creative Overage Fee. All other monetary metrics are set to zero out by design. |
| 7 | RTB | Your creative served on third-party inventory. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |

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

- [Working With Insertion Orders](working-with-insertion-orders.md)
- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Network Revenue And Billing Your Clients](network-revenue-and-billing-your-clients.md)
- [Billing](billing.md)
- [Working With Line Items](working-with-line-items.md)