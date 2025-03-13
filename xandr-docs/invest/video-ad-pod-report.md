---
title: Microsoft Invest - Video Ad Pod Report
description: This report shows metrics for groups of ads delivered sequentially in between segments of non-commercial video programming.
ms.date: 10/28/2023
---

# Microsoft Invest - Video Ad Pod report

> [!NOTE]
> This report is deprecated in August, 2023.

The Video Ad Pod report shows metrics for groups of ads delivered sequentially in between segments of non-commercial video programming.

> [!NOTE]
> Video metrics are recorded for VAST creatives only.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports. However, all time ranges are not available for every report.

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

### Data retention period

Data in this report has the following retention period:
- Hourly retention: 100 days
- Daily retention: 500 days

## Dimensions

| Column | Filter? | Description |
|:---|:---|:---|
| Buyer | Yes | The buyer of the video ad pod. |
| Seller | Yes | The seller of the ad pod. |
| Seller Type | Yes | The type of seller for the ad pod. Options are platform or partner. |
| Placement Set | No | The name of the ad pod. |
| Creative | Yes | The name of a creative served in the pod. |
| Content Category | Yes | The content category associated with the ad pod in the placement or placement group. |
| Device Type | Yes | The type of device where the ad pod played. |
| Video Context | Yes | When the video creative was served, e.g., 'pre-roll'. |
| Video Playback Method | Yes | The playback method for the creative, e.g, 'auto-play, sound on'. |
| Video Player Size | Yes | The size of the player based on pixel width, e.g., 'small', 'medium', 'large'. |
| Slot Position | Yes | The chronological order of an ad within its ad pod (placement set). |
| Slot Type | Yes | The type of position (ad or bumper) within an ad pod. |
| Creative Duration | Yes | The duration of the video creative in seconds. |
| Country | Yes | The country in which the impression took place. |
| Max Ad Duration | No | The maximum play duration of the video ad. |

## Metrics

| Column | Description |
|:---|:---|
| Imps | The total number of impressions. For video ads, an impression takes place when the first frame of the video is loaded. |
| CTR | The click-through rate--the ratio of clicks to impressions, expressed as a percentage. |
| Viewability Rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps). |
| Completions | The number of video ads that play to completion. |
| Completion Rate | The ratio of video ad completions to impressions, expressed as a percentage. (completions/impressions) |
| Average Ad Duration | The average duration of individual ads delivered in ad pods, in seconds. (total seconds played/completions) |
| Unfilled Seconds | The number of seconds in the ad pod that could not be supplied with ad content. |

## Run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
   <br>Or<br>
   From the Publishers top menu, select on **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.
   > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](./dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by selecting **Edit**), a selection panel appears. Select items in the **Available** list (left), then select **Add** to include them in the **Chosen** list (right).
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
1. Select **Run report** to send your report request.
