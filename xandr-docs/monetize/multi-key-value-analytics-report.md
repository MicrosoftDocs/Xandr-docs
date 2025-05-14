---
title: Multi-Key Value Analytics Report
description: Explore analytics report for Multi-Key values in your network, revealing info linked to various targeting keys and values.
ms.date: 10/28/2023
---

# Multi-key value analytics report

The Multi-Key Value Analytics report shows you the information associated with your network's defined multiple targeting keys and values.

Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the **kw\_** prefix on the key name. For example, a placement tag containing `keyname=value1` will not serve and therefore not be logged, whereas a placement tag containing **kw\_**`keyname=value1` will serve
and be logged. This applies to ad calls with the following tag types: `/tt`, `/ttj`, `/fpt`, `/jpt`, `/pt`, `/ptv`, `/ssptv`, `/mtj`, `/map`, and `/mob`.

> [!NOTE]
> **Microsoft Advertising Seller Tags:** When using [Microsoft Advertising's seller tag](../seller-tag/seller-tag.md) (AST), omit the **kw\_** prefix. AST has the keyword object in the body of the request, so the prefix is not needed.

Not all impressions from key/value targets will be included in reports. To be included, the targets must meet the following criteria:

- Key must be pre-defined.
- Value must be pre-defined OR Value must be targeted by at least one
  line item or campaign.
- Value is not a numeric range (greater than or less than).
- Value does not include a wildcard.

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

For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Time ranges including dates occurring greater than 45 days ago

If you create a Multi-Key Value Analytics report with the Range field set to Custom (where the end date is greater than 45 days from today), your report (regardless of metrics included) will be added to a special queue for "resource-intensive" reports. As a result, the report may take longer than usual to complete. In addition, this resource-intensive report may, due to the amount of data being requested, fail before being completed. If your report fails to complete, you will receive a notification. If your report request fails, you can:

- rerun the report at a later time.
- use a report type other than Key Value Analytics.
- alter the way you structure your reports (if possible) so they do not
  include dates greater than 45 days ago.

If you are frequently requesting Multi-Key Value Analytics reports which include dates longer than 45 days ago, you may need to consider running these reports via the API, caching the data and using [Bulk Reporting Feeds](../digital-platform-api/bulk-reporting-feeds.md) or [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md)(LLD). See [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md) for more details on how to alter your reports to avoid these issues.

## Data retention period

Data in this report is retained for 428 days.

## Dimensions

> [!IMPORTANT]
> The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.

| Column | Filter? | Description |
|--|--|--|
| Buyer ID | Yes | The member name and Microsoft Advertising ID of the buyer. |
| Advertiser | Yes | The advertiser whose creative served on this impression. |
| Insertion Order | Yes | The name of the insertion order associated with the line item or campaign that purchased the impression. |
| Line Item | Yes | The line item associated with this impression. |
| Deal | Yes | The name and ID of a deal if associated with the line item. |
| Creative | Yes | The creative served for the impression.<br>**Note**:<br> - For impressions older than 100 days, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be "`External Clicks`" or "`External Imps`". |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement | Yes | The placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, the ID will be `0`. |
| Publisher Currency | Yes | The transaction currency used by the seller to sell this impression. Including this dimension will cause most monetary metrics to be displayed in the selling currency. |
| Size | Yes | The size of the creative (e.g., 320x50). |
| Advertiser Currency | Yes | The transaction currency that the buyer used to purchase the impression. Including this dimension will cause most monetary metrics to be displayed in the buying currency. |
| Impression Type | Yes | See the **Impression Types** table below for definitions of the different types of impressions. |
| Revenue Type | Yes | The revenue type associated with the line item . For example, CPC, CPA, vCPM etc. |
| Device Type | Yes | Different device types on which the video impression will be rendered . For example, Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles , Media Players , Set Top Box etc. |
| Reporting Key 1 Name Label | Yes | The label (alias) of the first reporting key name. |
| Reporting Key 1 Value Label | Yes | The label (alias) of the first reporting key value. |
| Reporting Key 1 Name | Yes | The name of the first reporting key. |
| Reporting Key1 Value | Yes | The value associated with the first reporting key. |
| Reporting Key 2 Name Label | Yes | The label (alias) of the second reporting key name. |
| Reporting Key 2 Value Label | Yes | The label (alias) of the second reporting key value. |
| Reporting Key 2 Name | Yes | The name of the second reporting key. |
| Reporting Key 2 Value | Yes | The value associated with the second reporting key. |
| Reporting Key 3 Name Label | Yes | The label (alias) of the third reporting key name. |
| Reporting Key 3 Value Label | Yes | The label (alias) of the third reporting key value. |
| Reporting Key 3 Name | Yes | The name of the third reporting key. |
| Reporting Key 3 Value | Yes | The value associated with the third reporting key. |

> [!NOTE]
> In addition, you can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions. |
| Imps (master creative) | The number of page-level roadblocks that served the master creative.<br>**Note**: Alpha-Beta Notice:<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| Clicks | The total number of clicks. |
| Total Conversions | The total number of post-view and post-click conversions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Booked Revenue | The total revenue booked through direct advertisers. |
| Revenue | The total revenue; the sum of booked and resold revenue. |
| Total RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. For more information about these impression types, see Impression Types below. |
| Imps (Viewed) | The total number of impressions viewed by the consumers |
| Measured Imps | The number of impressions counted when the measurement script fires a pixel to the Microsoft Advertising platform. |
| Measurement Rate | Measured Impressions / Total number of impressions |
| View Rate | Viewed Impressions / View Measured Impressions |
| Resold Revenue | The total revenue on resold impressions through direct publishers. |

You may also choose to display currency values in the Advertiser/Buying and/or Publisher/Selling currency as well as USD.

## Impression types

| Value | Name | Definition |
|--|--|--|
| 1 | Blank | No creative served. |
| 2 | PSA | A public service announcement served because no other creative was eligible. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 4 | Default | A default creative served because no line item or campaign bid or no other creative was eligible. |
| 5 | Kept | One of your managed advertisers served a creative. |
| 6 | Resold | The impression was sold to a third-party buyer. |
| 7 | RTB | Your creative served on third-party inventory. No RTB impressions are included in this report. |
| 8 | PSA Error | A public service announcement served due to a timeout issue. |
| 9 | External Impression | An impression from an impression tracker. |
| 10 | External Click | A click from a click tracker. |
| 11 | Insertion | Your creative served on third-party inventory where it persists across page-loads and sessions.<br>**Note**: This impression type is currently only for Facebook News Feed creatives. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   1. Or, from the Publishers top menu, click on **Prebid Server Premium** \> **Analytics** \> **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears.
    a. Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data, you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      >  The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.
