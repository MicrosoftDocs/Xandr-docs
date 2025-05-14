---
title: Network Video Mediation Demand Report    
description: Explore Network Video Mediation Demand Report that can be used to view video mediation demand metrics across multiple buyers and publishers.
ms.date: 10/28/2023
---

# Network video mediation demand report

A mediation bid allows you to specify how much you expect the mediated network will pay for a video impression on a particular placement, thereby allowing the mediated network to compete for the impression against RTB demand in the Microsoft Advertising auction. Video Mediation Demand report can be used to view video mediation demand metrics across multiple buyers and publishers.

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

Data in this report is retained for 45 days.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Buyer | Yes | The buyer of this impression. |
| Publisher | Yes | The publisher on whose inventory this impression occurred. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred. |
| Mediated Bid | Yes | The name and ID of the mediated bid under a mediated network. |
| Placement | Yes | The placement through which this impression occurred.<br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Call Type | No | The type of handler that was used to send the impression to Microsoft Advertising (e.g., `ttj`, `ut`, `mob`, `ptv`, `openrtb`). |
| Mediated Network | Yes | The name and ID of the mediated network under which mediated bids are present. |
| Device Type | Yes | Different device types on which the video impression will be rendered. For example, Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles , Media Players , Set Top Box, etc. |
| Operating System Family | Yes | The name and ID of the supported operating system family on which the devices run. For example, Android, Apple Mac, Apple iOS, Microsoft Windows, etc. |
| Operating System | Yes | The name and ID of an operating system under an operating system family on which devices run. For example, Android 8.1 ,Oreo 9.0 Popsickle under Android Operating System Family, iOS 8.1 , 9.0 under Apple iOS family, etc. |
| Country | Yes | The country in which the impression took place. |
| Waterfall Depth | No | The maximum number of waterfall attempts that are allowed to try and display the ad. |
| Waterfall Position | No | The position of the creative in the waterfall. |

> [!NOTE]
> In addition, you can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions. For video ads, an impression takes place when the first frame of the video is loaded. |
| Waterfall Depth | The maximum number of waterfall attempts that are allowed to try and display the ad. |
| Waterfall Latency | The average latency of the waterfall. |
| Waterfall Position | The position of the creative in the waterfall. |
| Waterfall Ad Attempts | The number of video waterfall ad load attempts to show an ad. |
| Waterfall Ad Loads | The number of succesful video waterfall ad loads after attempts to show an ad. |
| Waterfall Ad Timeouts | Maximum amount of time in milliseconds that waterfall processing of mediated ad sources is allowed to run before it stops attempting to deliver a viable ad. |
| Waterfall Ad Errors | The number of failed video waterfall ad loads (VAST errors) after attempts to show an ad. |
| Waterfall Inclusions | The total number of video waterfall inclusions. |
| Mediation Latency | The average video latency of the mediation. |
| Mediation Requests | The total number of mediation requests for a video creative to display. |
| Mediation Errors | The number of video mediation error responses received. |
| Mediation No Bid | The number of video mediation no bid responses received. |
| Mediation Timeouts | The maximum time in milliseconds that the mediation script will load mediated bids on the page. |
| Mediation Responses | The number of successful video mediation responses where a valid video creative was returned and unwrapped. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured).
    1. Or, from the Publishers top menu, click on **Prebid Server Premium \> Analytics \> Prebid Server Analytics**.
1. Select the relevant report from the list. The **Report** screen shows the available filters, dimensions, and delivery options for the report. The seletions you make here will determine what report data is delivered to you, and how.

    > [!IMPORTANT]
   > For an explanation of how grouping and filtering work, see [Dimensions, Metrics, Filtering, and Grouping](dimensions-metrics-filtering-and-grouping.md).

1. Select the relevant filters to limit the data displayed to just the information you want. For example, rather than running a report that shows impressions for all inventory sources, you may want to list results for just a select few. When you select a filter (by clicking **Edit**), a selection panel appears.  Select items in the **Available** list (left), then click **Add** to include them in the **Chosen** list (right).
1. Group by Dimension. Grouping allows you to display rows of data in the order you prefer.

   > [!WARNING]
   >  The more dimensions you group by, the larger the data set that is returned. Larger data sets can take substantially longer to process. Be sure to group using only the dimensions you need.

1. Choose a delivery option. Once you've selected your filters and grouped by your chosen dimensions, you need to choose a delivery method. Available delivery methods include:
    - **Run now, show results in screen**: For smaller amounts of data,  you may want to view the report as soon as possible in your browser. You can download the report in XLSX, CSV, Excel/TSV and JSON format. However, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file.
    - **Run in background, notify me when results are ready to view**: A popup notification will let you know when the report is ready to view or download.

      > [!TIP]
      > The maximum size of the report that can be downloaded from the UI is 100 MB. Also, there is a limit of 100,000 rows per report when downloading as XLSX and Excel file. If the size of the report is more than that, you can try to download it using the [API](../digital-platform-api/report-service.md) for that reporting service (The limit here is 10 million rows).

    - **Export, send results via email**: Run the report in the background and email the results to one or more email addresses.
    - **Save as report template**: Save your selected report settings so that you can run this report again in the future. You can name this template using the text entry field under **Name this report** (its checkbox is auto-selected when you choose this option). A saved report can be rerun from the **Your Reports** screen.
    - **Add to scheduled reports**: Run this report automatically at specified times and have it sent to one or more email addresses.
    - **Name this report**: Give this report with its current settings a name for future reference.
1. Click **Run report** to send your report request.
