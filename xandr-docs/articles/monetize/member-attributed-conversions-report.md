---
title: Network Attributed Conversions Report
description: This page covers concepts on how conversion attribution work.
ms.date: 10/28/2023
---


# Network attributed conversions report

When a conversion pixel fires, Xandr determines
if the conversion can be attributed (tied to a creative that the user
previously viewed or clicked). For more information about how conversion
attribution works, see [Conversion Attribution](conversion-attribution.md).

The Network Attributed Conversions Report lets
you see conversion pixel IDs, order IDs, when clicks or impressions were
attributed, and other information related to attributed conversions for
your network.

## Time frame

All dates and times are given in UTC.

**Time ranges**

Time ranges define the time period of the data extracted for the report.
The following is a complete list of time ranges available for reports.

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

Intervals determine how your data is grouped together into rows in the
report response. The following is a complete list of intervals available
for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the
  entire selected time range.

This report can retrieve data for the last 33 days.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Campaign | Yes | The campaign that purchased this impression. (Does not apply to all advertisers.) |
| Conversion Pixel | Yes | The conversion pixel which was fired in this conversion event. For more information about conversion pixels, see [Working with conversion pixels](working-with-conversion-pixels.md). |
| Creative | Yes | The creative that served on this impression. For more information about creatives, see [Working with Creatives](working-with-creatives.md). |
| Custom Data | No | The data from custom parameters received by the Universal Pixel. This data is associated with the auction to which a conversion was attributed. |
| Event Name | No | The name of the Universal Pixel event. This field captures both standard and custom events. |
| Event Value | No | The monetary value, such as a cart or purchase total, associated with an event logged by a Universal Pixel. This value corresponds to the Event Value standard parameter in the Universal Pixel UI. |
| Event Value Currency | No | The currency associated with the event value logged by a Universal Pixel. This value corresponds to the Currency parameter in the Universal Pixel UI. |
| Impression Type | Yes | The type of impression. For more information, see [Impression Type](#impression-types). |
| Item IDs | No | The list of item IDs logged by Universal Pixel through the Item ID parameter. |
| Item Names |  | The list of item names logged by Universal Pixel through the Item Name parameter. |
| Item Types | No | The list of item types logged by a Universal Pixel through the Item Type parameter. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Order ID | No | The order ID or SKU optionally passed in the conversion pixel. If your advertiser is passing in an order ID when the conversion pixel fires, you could send a full list of order IDs back to them to help with conversion attribution. For more information, see [Conversion Pixels Advanced](conversion-pixels-advanced.md). |
| Post Click/Post View Conversion | Yes | Whether the conversion was a post-click (PC) or post-view (PV) conversion. |
| Post Click/Post View Revenue | No | Whether the revenue generated was from a post-click (PC) or post-view (PV) conversion. |
| Split | Yes | The name and ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| Traffic Type | Yes | The source of the traffic that caused the Universal Pixel to fire. Possible Values are `WEB` and `APP` |
| Universal Pixel | Yes | The UUID of the Universal Pixel associated with a conversion. |
| User ID | No | The Xandr user ID for the user who converted. If you have a mapping of your own user IDs to Xandr IDs, you might be able to do some analysis around which segments are converting, or you could count your unique and repeat converters.<br>**Warning**: Post GDPR implementation, this field is deprecated on May 21, 2018. Subject to requirements under the GDPR, this field will continue to be available if you receive log level data via [Cloud Export](../log-level-data/log-level-data-cloud-export.md). For details, see [Changes to Log-Level Data and Console Reporting](https://microsoftapc.sharepoint.com/teams/PrivacyRegulations/SitePages/Changes-to-Log-Level-Data-and-Reporting-Support-for-European-Privacy-Regulations.aspx?xsdata=MDV8MDJ8fDU1NmM5MjFhZmUzZjRkZDE4ZDc2MDhkYzBkMmRlYWU5fDcyZjk4OGJmODZmMTQxYWY5MWFiMmQ3Y2QwMTFkYjQ3fDB8MHw2MzgzOTk3MzgwNDU2MzE4NjJ8VW5rbm93bnxWR1ZoYlhOVFpXTjFjbWwwZVZObGNuWnBZMlY4ZXlKV0lqb2lNQzR3TGpBd01EQWlMQ0pRSWpvaVYybHVNeklpTENKQlRpSTZJazkwYUdWeUlpd2lWMVFpT2pFeGZRPT18MXxMM1JsWVcxekx6RTVPamhrWkVSV2JHd3dhVWxKYTNaVVduUkhXR3hOY2xReFJtWkpVa1J2ZGtOclZXa3RXblkyUVZOU2VqZ3hRSFJvY21WaFpDNTBZV04yTWk5amFHRnVibVZzY3k4eE9Ub3lNbVl5Tm1aaFkyTXdaVEkwWlRFMllqVTRPV05sTXpBeU9HVTJaR0V6TVVCMGFISmxZV1F1ZEdGamRqSXZiV1Z6YzJGblpYTXZNVGN3TkRNM056QXdNekl6Tmc9PXxlZjQ2N2QxMzk0MWI0YzZkOGQ3NjA4ZGMwZDJkZWFlOXwzMDY5MmUyNmMyZGI0MzZjYjNjMGNmYjI3MjY1YzIyNw%3D%3D&sdata=aUFsNGRpMkZEZ1daL091U3I0TzZtQ0lMamhGd1ZiSWpnaFpTMzk5MGVCVT0%3D&ovuser=72f988bf-86f1-41af-91ab-2d7cd011db47%2Cv-soambasta%40microsoft.com&OR=Teams-HL&CT=1704430333131&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiI0OS8yMzExMzAyODcxOCJ9). |

## Impression types

| Value | Name | Definition |
|---|---|---|
| 1 | Blank | No creative served. |
| 4 | Default | A default creative served because there were no valid bids. |
| 3 | Default Error | A default creative served due to a timeout issue. |
| 10 | External Click | A click from a click tracker. |
| 9 | External Impression | An impression from an impression tracker. |
| 5 | Kept | Your advertiser's creative served on your publisher's site. |
| 2 | PSA | A PSA served because there were no valid bids and no default creative was available. |
| 8 | PSA Error | A public service announcement served due to a timeout issue or lack of a default creative. |
| 6 | Resold | Your publisher's impression was sold to a third-party buyer. |
| 7 | RTB | Your advertiser's creative served on third-party inventory. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Auction ID | The auction ID for which the conversion was attributed. |
| External Data | Optional extra data passed in on conversion pixel using the "other" parameter. |
| Impression Time | The time at which the impression occurred. |
| Time of Conversion | The time at which the conversion occurred. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the
    appropriate top menu (depending on how your account has been
    configured).
    1. Or, from the Publishers top menu, click on
        **Prebid
        Server Premium** \>
        **Analytics** \>
        **Prebid Server Analytics**
1. Select the relevant report from the list. The
    **Report** screen shows the available
    filters, dimensions, and delivery options for the report. The
    selections you make here will determine what report data is
    delivered to you, and how.

    > [!IMPORTANT]
    > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the
    information you want. For example, rather than running a report that
    shows impressions for all inventory sources, you may want to list
    results for just a select few. When you select a filter (by clicking
    **Edit**), a selection panel appears.
    Select items in the **Available** list (left), then click
    **Add** to include them in the
    **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in
    the order you prefer.

    > [!WARNING]
    > The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and
    grouped by your chosen dimensions, you need to choose a delivery
    method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data,
      you may want to view the report as soon as possible in your
      browser. You can download the report in XLSX, CSV, Excel/TSV and
      JSON format. However, there is a limit of 100,000 rows per report
      when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A
      popup notification will let you know when the report is ready to
      view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to
      one or more email addresses.
    - **Save as report template**: Save your selected report settings so
      that you can run this report again in the future. You can name
      this template using the text entry field under
      **Name this report** (its checkbox
      is auto-selected when you choose this option). A saved report can
      be rerun from the **Your Reports**
      screen.
    - **Add to scheduled reports**: Run this report automatically at
      specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a
      name for future reference.
1. Click **Run report** to send your report request.

## Related topics

- [Network Reporting](network-reporting.md)
- [Conversion Attribution](conversion-attribution.md)