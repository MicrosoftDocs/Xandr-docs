---
title: Microsoft Monetize - Identifiers - ID Combinations Report
description: In this article, learn about the ID Combinations report along with the dimensions and metrics associated with it.
ms.date: 10/28/2023
---

# Microsoft Monetize - Identifiers: ID combinations report

The ID Combinations Report provides users with insights on combinations of cookies, device IDs, and common IDs available in the purchased impressions. It also provides information on impression distribution, performance metrics for combinations of ID types, and what types of IDs are present in the purchased impressions. Users can access the report either through the platform or the Microsoft Advertising API.

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

This report's data is retained for 90 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

> [!NOTE]
> The **Filter?** column below shows whether a dimension can be used as a filter as well as being used to group by.

| Column | Filter? | Description |
|---|---|---|
| Advertiser | Yes | The advertiser for which impression was purchased. |
| Bidder | Yes | The bidder that bought the impression. |
| Billing Period | No | The insertion order's billing period. |
| BP End Date | No | The end date of the billing period. |
| BP Start Date | No | The start date of the billing period. |
| Buyer | Yes | The buyer of the impression. |
| Country | Yes | The id of the targeted country of the advertisement. |
| Creative | Yes | The creative associated with the impression. |
| Deal | Yes | The id of the [Deal](deals-faq.md) the ad was delivered against. |
| Device Type | Yes | The device type on which creative is displayed to the end-users such as mobiles, laptops, tablets, and other devices. |
| Flight | No | The ID of the billing period's flight. |
| Flight End Date | No | The end date of the flight within the billing period. |
| Flight Start Date | No | The start date of the flight within the billing period. |
| ID Type Combinations | No | Concatenated list of identifier types displayed in each row include: <br> - `UID2` <br> - `RampID` <br> - `NetID` <br> - `TradeDeskID` <br> - `CriteoID` <br> - `Cookie / Device ID` <br> - `Unidentified` |
| Impression Type | Yes | The type of impression served. For details, see [Impression Types](prebid-server-premium-seller-analytics.md#impression-types). |
| Insertion Order | Yes | The id of the insertion order for which impression was purchased. |
| Line Item | Yes | The ID of the line item under which the impression was purchased. For more information about line items, see our documentation on [Working with Line Items](working-with-line-items.md). |
| Media Type | No | The media type is the general display style of the creative. |
| Placement | No | The name and ID of the placement through which this impression occurred. |
| Placement Group | Yes | The placement group name. |
| Publisher | No | The publisher on whose inventory this impression occurred. |
| Seller | Yes | The seller of the impression. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to [Augmented Line Items (ALI)](augmented-line-items-ali.md). For any rows with a campaign name, the Split column (if included) will be null. |
| Supply Type | Yes | The type of targeting served (**App & Web**, **App Only**, or **Web Only**). |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Formula | Description |
|---|---|---|
| Booked Revenue CPM | booked revenue / imps * 1000 | The booked revenue per 1000 impressions. |
| Clicks | Clicks | The total number of clicks. |
| Cost | Cost | The media cost. |
| Cost eCPC |  | The average CPC based on media cost. |
| Cost eCPM |  | The average CPM based on media cost. |
| CTR | Clicks / Imps | The average Click Through Rate (CTR). |
| Imps | Imps | The total number of transacted impressions. Impression counts are not de-duplicated across ID Types. |
| Media Cost CPM |  | The media cost per 1000 impressions. |
| Region/State |  |  The user's [Region](../digital-platform-api/region-service.md) (e.g., Baja California or California). |
| Reseller Revenue |  | The revenue from resold impressions. This is only populated when the impression type is resold. |
| Resold CPM | reseller_revenue / imps * 1000 | The resold revenue per 1000 impressions. |
| Revenue | booked revenue + reseller revenue | The sum of booked revenue and reseller revenue. |
| Revenue CPM | (reseller_revenue + booked_revenue) / imps * 1000 | The revenue per 1000 impressions. |

## How to run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).

    Or, from the **Publishers** top menu, click on **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**.

1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).

1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV, and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (the limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.

1. Click **Run report** to send your report request.
