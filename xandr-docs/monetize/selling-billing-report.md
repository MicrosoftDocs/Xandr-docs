---
title: Microsoft Monetize - Selling Billing Report
description: Use this report to analyze your invoice. This page also provides steps to run this report.
ms.date: 10/28/2023
---


# Microsoft Monetize - Selling billing report

This report allows you to manage internal invoicing for your publishers across both managed and third-party selling.

For a detailed discussion of booked revenue, media cost, profit, and using your billing report, see [Network Revenue and Billing Your Clients](network-revenue-and-billing-your-clients.md).

**Use this report to understand your Invoice:** If you would like to use this report to analyze your invoice, see [Understanding Your Invoice](understanding-your-invoice.md).

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

| Column | Filter? | Description |
|--|--|--|
| Advertiser | Yes | The advertiser that purchased the impression. |
| Auction Charges Available | Yes | Indicates if there are charges from the auction associated with the impression (2-step pricing). |
| Buyer Cleared | Yes | Whether or not the buyer pays the seller or curator directly for the cost of media. <br> See [Buyer Cleared Table](#buyer-cleared-table) |
| Buyers | Yes | The buyer of this impression. |
| Country | Yes | Country of this impression. |
| Curator | Yes | The curator of this impression. |
| Curator Cleared | Yes | Whether or not the seller receives the reseller revenue from Microsoft Advertising or the curator.<br> See [Curator cleared Table](#curator-cleared-table) |
| Deal ID | Yes | The deal associated with the impression. |
| Deal Type | Yes | The deal type associated with the impression. Possible values are:<br> - Private Marketplace<br> - First Look<br> - Programmatic Guaranteed<br> - Curated |
| Impression Type | Yes | See [Impression Types](#impression-types) below for definitions of the different types of impressions. |
| Insertion Order | Yes | The insertion order of this impression. |
| Is Claims Activity | Yes | Is adjustment made from Invalid Trafffic (IVT) claims. |
| Is Cross Seat Activity | Yes | Only relevant if you have more than one member/seat on the Microsoft Advertising platform. If you do, this field allows you to know whether the activity was associated with transactions between members you manage and therefore simplify the reconciling of their invoices. |
| Is Deal | Yes | Is there any deal associated with the impression. Different from 'Deal' which is the actual deal id |
| Media Type (Billing) | Yes | The video-specific media type classification for billing only. If you don't have video-specific pricing, this field is irrelevant. Possible values are<br> - -- <br> - Non-Video<br> - Video (Hosted)<br> - Video (Non-Hosted) |
| Publisher | Yes | The publisher on whose inventory the impression occurred. |
| Publisher ID | Yes | The external code associated with a publisher. |
| Selling Currency | Yes | The transaction currency used by the seller to sell this impression. Including this dimension will cause the **Resold Revenue** and **Seller Media Cost** metrics to be displayed in the selling currency. |

### Buyer cleared table

|Code  |Description  |
|--|--|
| 0 | Microsoft Advertising acts as the clearing house, collecting the cost of media from the buyer and paying the seller. |
| 1 | Microsoft Advertising does not clear cash; the buyer pays the seller directly for the cost of media. |
| -1 | Dummy value for unbilled activity. |

### Curator cleared table

|Code  |Description  |
|--|--|
| 0 | The seller receives the reseller revenue from Microsoft Advertising. |
| 1 | The seller receives the reseller revenue from the curator. |
| -1 | Dummy value for unbilled activity. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

> [!NOTE]
> If you have signed a new contract with Microsoft Advertising and completed the cutover, FX margin and Foreign exchange fees will no longer be applicable.

| Column | Description |
|--|--|
| Ad Serving Fees | Cost of serving an ad when the buyer and seller are within a network + cost of serving an ad charged to the buyer when buying RTB. |
| Ad Serving Fees (Non-Hosted Video) | Fees typically charged for Kept, Default, PSA, and blank impressions that served a non-hosted video creative. |
| Bad Debt Deductions | The charges for waiving sequential liability taken at time of auction. |
| Bad Debt Fees | The charges assessed for waiving sequential liability. |
| Billable Imps | The total number of impressions billed to the client. |
| Clicks | The total number of clicks. |
| Conversions | The total number of post-view and post-click conversions. |
| Conversions | The total number of post-view and post-click conversions. |
| Filtered Requests | The total number of Blocklisted or Fraud impressions. |
| Gross CPM | The gross revenue per 1000 impressions. |
| Gross Seller Revenue | The gross revenue generated through sales to buyers (before deductions). |
| Net CPM | The total revenue per 1000 impressions. |
| Other Deductions | FX Margins taken at time of auction. |
| Other Fees | FX Margins assessed for services. |
| Reseller Revenue | The net revenue generated through sales to buyers. |
| SASC Deduction | The platform charges for services taken at time of auction. |
| SASC Fees | The platform charges assessed for services. |
| Seller Media Cost | The amount owed to the publisher. |

## Impression types

| Value | Name | Definition |
|--|--|--|
| 1 | Blank | No creative served. |
| 2 | PSA | A public service announcement served because no other creative was eligible. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 4 | Default | A default creative served because no campaigns bid or no other creative was eligible. |
| 5 | Kept | One of your managed advertisers served a creative. |
| 7 | RTB | The impression was sold to a third-party buyer. |
| 8 | PSA Error | A public service announcement served due to a timeout issue. |
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
  
     1. **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
     1. **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

          > [!TIP]
          > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).
     1. **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
     1. **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
     1. **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
     1. **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Network Revenue and Billing Your Clients](network-revenue-and-billing-your-clients.md)
- [Billing](billing.md)
- [Working with Line Items](working-with-line-items.md)
<!--- [Working with Campaigns](working-with-campaigns.md)-->
