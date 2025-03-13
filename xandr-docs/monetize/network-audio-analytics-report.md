---
title: Network Audio Analytics Report
description: Explore Network Audio Analytics, a tool that monitors and evaluates audio metrics between network buyers and sellers, enhancing evaluation.
ms.date: 10/28/2023
---

# Network audio analytics report

The Network Audio Analytics report can be used to view audio event metrics across multiple buyers and sellers.

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
- Cumulative: Data is grouped together in one figure, covering the
  entire selected time range.

> [!TIP]
> For more information about how quickly report data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).
>
## Currency 2.0

> [!NOTE]
> By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use **USD** as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Buyer | Yes | The buyer of this impression. |
| Seller | Yes | The seller of this impression. |
| Advertiser | Yes | The advertiser whose creative served on this impression. |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred.<br><br>**Note**: For impressions older than 100 days, the ID will be 0. |
| Placement | Yes | The placement through which this impression occurred. <br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Insertion Order | Yes | The insertion order under which this impression was purchased. |
| Line Item | Yes | The line item under which this impression was purchased. |
| Campaign | Yes | The campaign which purchased this impression. (Does not apply to all advertisers.) |
| Creative | Yes | The creative associated with the impression. |
| Brand | Yes | The brand associated with the creative. Microsoft Advertising keeps a list of advertiser brands in our systems that can be applied to a creative when its uploaded. For impression type "Resold", no information is available in the **Brand** field for this report. |
| Country | Yes | The country in which the impression took place. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Creative Recency | Yes | How recently the creative was viewed by the user. For more information, see [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md). |
| Creative Frequency | Yes | How many times the creative has been viewed by the user. For more information, see Creative Frequency Definitions in the [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md). |
| Creative Duration | No | The duration of the audio creative associated with this impression. |
| IO: Trafficker (reporting label) | Yes | The trafficker associated with this insertion order. This is an insertion order reporting label. |
| IO: Sales Rep (reporting label) | Yes | The sales rep associated with this insertion order. This is an insertion order reporting label. |
| Media Subtype | Yes | The media subtype for the creative. |
| Supply Type Filterable | Yes | Whether to filter by supply type. |
| Site Domain | Yes | The site domain associated with the impression. |
| Application ID | Yes | The application ID associated with the impression. |
| Buying Currency | Yes | The transaction currency that the buyer used to purchase this impression. |
| Audio Context | Yes | The type of the audio creative. Possible values are:<br> - Unknown<br> - Pre-roll<br> - Mid-roll<br> - Post-roll<br> - Outstream |

You can also choose to select the **Only include results where a Deal is present** option.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions. |
| Clicks | The total number of clicks. |
| CTR | The click-through rate; the ratio of clicks to impressions, expressed as a percentage. |  
| Total Conversions | The total number of post-view and post-click conversions. |  
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |  
| Revenue | The total revenue; the sum of booked and resold revenue. |  
| Revenue Per Audio Complete | The revenue per audio completion |  
| Total RPM | The revenue per 1000 impressions, including defaults, PSAs, and errors. |  
| Cost | The total media cost across direct publishers and RTB inventory. |  
| Cost Per Audio Complete | The cost per audio completion |  
| CPM | The total media cost per 1000 impressions. |  
| Profit | The total Network revenue minus the total Network media cost. |  
| PPM | The total profit per 1000 impressions. |  
| Completion Rate | The ratio of audio completions to impressions, expressed as a percentage. |  
| Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |  
| Skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |  
| Starts | The total number of times the first segment of the video creative was downloaded and started. |  
| Skip Rate | The percentage of times the user opted to skip the video. |  
| 25% Complete | The total number of times the video creatives completed 25% of the entire duration. |  
| 50% Complete | The total number of times the video completed 50% of the entire duration of time. |  
| 75% Complete | The total number of times the video completed 75% of the entire duration of time. |  
| 100% Complete | The total number of times the video played for the entire duration of time. |  
| Ad Responses | The total number of responses served to the audio player.<br><br>**Note**: An **Impression** is recorded when the audio player loads the creative, displays the first frame, and the impression tracker is fired from the audio player. **Ad Responses** refers to the VAST document (XML) being served in response to a request from the audio player, but does not mean that a successful impression event occurred. |  
| Errors | The total number of times an error occurred. |  
| Audio Fill | The percentage of audio impressions delivered out of the total number of audio ad responses received. (Imps / Ad Responses) |
| Device Type | The type of device on which the impression was served. Possible values are:<br> - desktops & laptops<br> - tablets<br> - mobile phones<br> - tv<br> - game consoles<br> - set top box<br> - media players<br> - other devices |  

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   1. Or, from the Publishers top menu, click on Prebid  Server **Premium** \> **Analytics** \> **Prebid Server Analytics**.
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
