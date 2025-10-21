---
title: Publisher Video Analytics Report
description: In this article, learn about the Publisher Video Analytics report along with the dimensions and metrics associated with it.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Publisher video analytics report

The Publisher Video Analytics report can be used to view video event metrics for a specific publisher. To view such metrics across multiple advertisers and publishers, use the [Network Video Analytics Report](network-video-analytics-report.md).

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


### Data retention period

Data in this report has the following retention period:

- Hourly retention: 100 days
- Daily retention: 500 days


## Currency 2.0

By enabling **Currency 2.0**, you can select a currency for each individual report if you prefer not to use USD as the default currency. The report will show all the monetary fields in your report using the selected currency. For example, if you select **Advertiser**, click the **Currency 2.0** toggle to enable it, and select **Japanese Yen (JPY)** from the **Currency** menu, the report will show all monetary data in JPY, including data associated with child objects such as line items.

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| Buyer | Yes | The buyer of this impression. |
| Advertiser | Yes | The advertiser whose creative served on this impression. |
| Placement Group | Yes | The placement group (simply a collection of placements) which includes the placement through which this impression occurred. <br><br> **Note**: For impressions older than 100 days, the ID will be `0`. |
| Placement | Yes | The placement through which this impression occurred. <br><br> **Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| Brand | Yes | The brand associated with the creative. |
| Country | Yes | The country in which the impression took place. |
| Deal | Yes | The deal associated with the transaction for the impression. |
| Deal Code | Yes | The custom code for the deal. For deals with external supply partners, this is typically the string used to identify the deal.|
| Site Domain | Yes | The site domain of an impression |
| Application ID | Yes | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| Selling Currency | No | The seller/publisher currency associated with the video impressions sold. This dimension is available only when Currency 2.0 is disabled. |
| Creative Duration | No | The duration of the video creative (e.g., 15 seconds). |
| Is Takeover |Yes| Indicates whether an impression was `Blanked` or `Defaulted` due to at least one ad in the multi-ad request being a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|
| Supply Type | Yes | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are 'web', 'mobile_app', and 'mobile_web'. |
| Video Context | Yes | When and where the video creative was served. Possible values are Pre-roll, Mid-roll, Post-roll, Outstream, and Unknown. |
| Video Playback Method | Yes | The playback method for the creative, e.g, ' auto-start, sound on'. |
| Video Player Size | Yes | The size of the player based on pixel width, e.g., 'small', 'medium', 'large'. |
| Device Type | Yes | The type of device where the creative was set to play. Options include Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles, Media Players, Set Top Box, and Other Devices. |
| Video Content Duration | No | The length of the video content in seconds. |
| Video Content Genre | No | The main genre of the program in which the ad will be played. For example, Action, Adventure, Biography, Business, Comedy, etc. |
| Video Content Language | No | The language of the video program in which ad will be played. For example, Spanish. |
| Video Content Network | No | The network delivering the video content. For example, 9 Story, CBC, Disney, AMC, Fox, etc. |
| Video Content Rating | No | The publisher-identified audience group for which the content is rated. For example, All, Children (7+) , Teens (13+), Young Adults (14+), or Adults (18+). |
| Video Delivery Type | No | The type of streaming content delivery. For example, Video On Demand (VOD) and Live. |
| Video Program Type | No | The higher level categorization of the video program's format on which the ad will be played. For example, Movie, Series, Special, Show, Event, Clip, etc. |

> [!NOTE]
>
> - The data for the **Video Content Duration**, **Video Content Genre**, **Video Content Language**, **Video Content Network**, **Video Content Rating**, **Video Delivery Type**, and **Video Program Type** dimensions is only available if the publisher has implemented video taxonomy.
> - You can also filter on a particular number of impressions using the **Minimum Impressions** filter.

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Description |
|---|---|
| Imps | The total number of impressions. For video ads, an impression takes place when the first frame of the video is loaded. |
| Clicks | The total number of clicks. |
| CTR | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| Total Conversions | The total number of post-view and post-click conversions. |
| Conversion Rate | The ratio of conversions to impressions, expressed as a percentage. |
| Network Revenue | Total Network revenue. |
| Publisher Revenue | Total publisher revenue. |
| Network Profit | The sum of booked revenue plus reseller revenue, minus total cost. |
| Total RPM | Network revenue per 1000 impressions, including defaults, PSAs, or errors. |
| Sold Network RPM | Network revenue per 1000 impressions that were not defaults, PSAs, or errors. |
| Network PPM | **Deprecated**. Total Network profit per thousand impressions (total Network RPM - total publisher RPM). |
| Network ROI | **Deprecated**. Return on investment for the Network. |
| Sold Publisher RPM | Publisher revenue per 1000 impressions that were not defaults, PSAs, or errors. |
| Total Publisher RPM | Publisher revenue per 1000 impressions, including defaults, PSAs, or errors. |
| Errors | The total number of times an error occurred. |
| Ad Responses | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| Skips | The total number of times a user skipped the video. Use this metric for reporting on skippable inventory. |
| Starts | The total number of times the first segment of the video creative was downloaded and started. |
| Skip Rate | The percentage of times the user opted to skip the video. |
| Start Rate | The percentage of times the first segment of the video creative was downloaded and started. |
| Video Fill | The percentage of video impressions delivered out of the total number of video ad requests received. (impressions/requests) |
| 100% Complete | The total number of times the video creatives completed 100% of the entire duration. |
| 25% Complete | The total number of times the video creatives completed 25% of the entire duration. |
| 50% Complete | The total number of times the video creatives completed 50% of the entire duration. |
| 75% Complete | The total number of times the video creatives completed 75% of the entire duration. |
| Completion Rate | The ratio of video completions to impressions, expressed as a percentage. |
| Render Rate | The percentage of videos delivered based on the response rate from buyers. (impressions /ad responses) For video ads, an impression takes place when the first frame of the video is loaded. |
| Response Rate | The percentage of videos served to the video player (ad responses/ad requests) |
| Total Cost | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| Total Cost eCPM | The total cost per 1,000 imps. |
| Total Cost eCPC | The total cost per click. |
| Total Cost eCPA | The total cost per conversion. |
| Network Profit eCPM | Network profit per thousand impressions. <br><br> **Note**: This new field defines "Network profit" as the sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPC | Network profit per click. <br><br> **Note**: This new field defines "Network profit" as the sum of booked revenue and reseller revenue minus total cost. |
| Network Profit eCPA | Network profit per conversion. <br><br> **Note**: This new field defines "Network profit" as the sum of booked revenue and reseller revenue minus total cost. |
| Network Profit Margin | Network profit margin. <br><br> **Note**: This new field defines "Network profit" as the sum of booked revenue and reseller revenue minus total cost. |
| Video Content Duration | The length of the video content in seconds. <br><br> **Note**: The data for this metric is only available if the publisher has implemented video taxonomy. |
| Average View Time | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| Average View Time Percent | The average view time expressed as a percentage of the total possible view time. |

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
