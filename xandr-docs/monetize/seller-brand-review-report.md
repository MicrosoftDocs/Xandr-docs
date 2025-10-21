---
title: Microsoft Monetize - Seller Brand Review Report
description: Learn how you can review what creative has served, the performance of creative and client brand category using the Seller Brand Review Report.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Seller brand review report

This report provides sellers with a view of brand performance across all of your inventory. You can:

- Review what creative has served on your inventory and how it performed
- Review creative performance by audit status
- Review client brand category performance across all of your inventory

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

## Data retention period

Data in this report is retained for 14 months.

## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Group? | Description |
|--|--|--|--|
| Audit Status | Yes | Yes | The audit status of the creatives you want included in the report (e.g., Unaudited, Self Audit Only, Microsoft Advertising Audited). |
| Brand | Yes | Yes | The name and ID of the brand associated with the impression. |
| Brand Offer Category | Yes | Yes | The name of the brand offer category associated with the impression. |
| Buyer | Yes | Yes | The member name and ID with whom you are sharing segments. |
| Country | Yes | Yes | The country associated with the impressions. |
| Creative Id | Yes | Yes | The ID of the creatives to be included in the report. |
| Deal | Yes | Yes | The name and ID of the deal associated with the impression. |
| Impression Type | Yes | Yes | The impression type associated with the creatives. See **Impression Types** within the [Network Analytics Report](network-analytics-report.md) for definitions of the different types of impressions. |
| Media Type | Yes | Yes | The general display style of a creative served on the publisher's inventory (e.g., Banner, Pop). |
| Payment type | Yes | Yes | The type of payment made to the broker. |
| Placement | Yes | Yes | The name and ID of the placement associated with this impression. |
| Placement Group | Yes | Yes | The name and ID of the placement group associated with the impression. |
| Publisher | Yes | Yes | A full description of the publisher on whose site the impression occurred, including their name and ID. |
| Revenue type | Yes | Yes | The way the advertiser has agreed to pay you. |
| Selling Currency | Yes | Yes | The transaction currency used by the seller to sell this impression. Including this dimension will cause the Resold Revenue metric to be displayed in the selling currency. This dimension is available only when Currency 2.0 is disabled. |
| Size | Yes | Yes | The width and height of the creatives associated with the impressions. |

> [!NOTE]
> You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Formula | Description |
|--|--|--|--|--|
| Booked Revenue | money | 450.00 | Booked Revenue | The total revenue booked through direct advertisers (line item). |
| Clicks | int | 345 | Clicks | The total number of clicks across all impressions. |
| Conversion per million | double | 384.4 | total conversions / imps x 1,000,000 | The number of conversions per million impressions. |
| Conversion Rate | double | 0.000221877080097626 | Total Convs / Imps | The ratio of conversions to impressions. |
| Cost | money | 100.00 | Cost | The total cost of the inventory purchased. |
| CPM | money | 5.00 | CPM | The cost per one thousand impressions. |
| CTR | double | 0.00237 | (Clicks / Imps) x 100 | The rate of clicks to impressions, expressed as a percentage. |
| Imps | int | 34534 | Imps | The total number of impressions (served and resold). |
| Network Profit | money | 123.45 | Booked Revenue + Reseller Revenue - Total Cost | The sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPA | money | 123.45 | Network Profit/Conversions | Network profit per conversion. |
| Network Profit eCPC | money | 123.45 | Network Profit / Clicks | Network profit per click. |
| Network Profit eCPM | money | 123.45 | (Network Profit / Imps) * 1,000 | Network profit per thousand impressions. |
| Network Profit Margin | money | 123.45 | Network Profit/(Booked Revenue + Reseller Revenue) | Network profit margin. |
| PPM | money | 0.944966292134831 | (profit / imps) x 1000 | **Deprecated**. The profit per 1000 impressions. |
| Profit | money | 4.14 | Booked revenue - total cost. | Booked revenue minus total cost. |
| Profit eCPA | money | 123.45 | (Booked Revenue - Total Cost)/Conversions | Profit per conversion. |
| Profit eCPC | money | 123.45 | (Booked Revenue - Total Cost)/Clicks | Profit per click. |
| Profit eCPM | money | 123.45 | (Booked Revenue - Total Cost)/Clicks * 1,000 | Profit per thousand impressions. |
| Profit Margin | money | 123.45 | (Booked Revenue - Total Cost)/Booked revenue | Buyer profit margin. |
| Resold Revenue | money | 0 | Resold Revenue | The total revenue on resold impressions through direct publishers. |
| Revenue | money | 25.767257 | Booked Revenue + Resold Revenue | The sum of booked revenue and reseller/resold revenue. |
| Total conversions | int | 5 | Total Conversions | The total number of post-view and post-click conversions. |
| Total Cost | money | 123.45 | Media Cost + Data Costs + Partner Fees + Commissions + Serving Fees + Publisher Revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPA | money | 123.45 | Total Cost/Conversions | The total cost per conversion. |
| Total Cost eCPC | money | 123.45 | Total Cost/Clicks | The total cost per click. |
| Total Cost eCPM | money | 123.45 | (Total Cost/Imps) * 1,000 | The total cost per 1,000 imps. |
| Total RPM | money | 2.60548314606741 | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| View-Measured Imps | int | 10,120 | Impressions measured for Viewability | The total number of impressions that were measured for viewability. |
| Viewability Measurement Rate | double | 45% | View Measured Imps / Imps | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| Viewability Rate | double | 58% | Viewed Imps / View Measured Imps | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| Viewable Imps | int | 30,450 | Viewable Impressions | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |

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
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under
      **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Reporting Guide](reporting-guide.md)
- [Network Reporting](network-reporting.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
- [Seller Site Domain Report](seller-site-domain-report.md)
