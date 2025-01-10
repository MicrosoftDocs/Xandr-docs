---
title: Seller Podded Video
description: Learn how you can use Seller Podded Video to determine the number of pods, average number of impressions sold per pod, estimate of revenue per pre-roll in comparison to mid-roll, seconds sold per pod, fill rate in seconds and number of opportunities to serve impressions if a pod was unfilled.     
ms.date: 10/28/2023
---

# Seller podded video

> [!NOTE]
> This feature is currently in **Alpha**. It is still under development and may be subjected to changes without notice. Contact your Microsoft Advertising Account Representative to get it enabled.

The **Seller Pod Analytics** report shows metrics for groups of ads (aka pods) delivered sequentially in between segments of non-commercial video programming.

You can use this report to determine the following:

- The number of pods that were sent for Monetization
- The average number of impressions sold per pod
- The average estimate of revenue per pre-roll in comparison to mid-roll pod
- The average seconds sold per pod
- The fill rate in seconds
- The number of opportunities to serve impressions if a pod was unfilled

## Timeframe

All dates and times are given in UTC.

The `report_interval` field in the JSON request can be set to one of the following:

- Custom
- Today
- Yesterday
- Last 7 Days(not including today)
- Month to Date
- Last Month
- Quarter to Date

To run a report for a custom time frame, set the `Start Date` and `End Date` fields in your report request. For more details about these fields, see [Report Service](../bidders/report-service.md).

> [!NOTE]
> The timestamp this report uses is the hour that Microsoft Advertising received the ad request for the pod. It means that if a pod was requested at hour 05 and impressions rendered at hour 07, then the pod count, impressions, and video events will report together at hour 05. It means pods that playback cross-hour boundaries are reported in the same hour, and it ensures metrics such as impressions per pod are calculated accurately on pre-cached integrations.

## Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- **Hourly**: Data is grouped into rows by the hour.
- **Daily**: Data is grouped into rows by the day.
- **Monthly**: Data is grouped into rows by the month.
- **Cumulative**: Data is grouped together in one figure, covering the entire selected time range.

## Data retention period

This report's data is retained for 420 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](availability-of-reporting-data.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|--|--|--|--|--|
| Advertiser Default Currency | String | No | `EUR` | The default currency of the advertiser in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Advertiser Default Exchange Rate | Numeric | No |  |  |
| Application | String | Yes |  | The application name |
| Billing Currency | String | No | `USD` | The transaction currency that the buyer used to purchase this impression. This dimension is available only when Currency 2.0 is disabled. |
| Billing Currency Exchange Rate | Numeric | No |  |  |
| Browser | String | Yes | `webOS Browser (33)` | The name of the browser. |
| Call Type | String | Yes |  | The type of handler that was used to send the impression to Microsoft Advertising (e.g., ttj, ut, mob, ptv, openrtb) |
| City | String | Yes | `Vienna` | The city in which the user is located. |
| Country | String | Yes | `"France"` | The country/region of the user's location, both name and code, in the format "France". The string "250" can appear in cases where we don't know the country/region or if the country/region doesn't map correctly to a location in our database. |
| Device Type | String | Yes | `"set top box"` | The type of device on which the impression was served. Possible values are:<br> - "desktops & laptops"<br> - "tablets"<br> - "mobile phones"<br> - "tv"<br> - "game consoles"<br> - "set top box"<br> - "media players"<br> - "other devices" |
| Inventory URL | String | No |  | The URL of the inventory or application package. |
| Language | String | No | `German (6)` | The language of the creative. |
| Max Ad Duration | Numeric | No | `15` | Max duration of an individual ad within the pod |
| Max Duration | Numeric | No | `30` | Max duration of the entire pod. |
| Max Number Ads | Numeric | No | `4` | The maximum number of ads for the pod the slot served in. |
| Max Vast Version | String | No | `4.0` | The max VAST version supported for the slot. |
| Member Currency | String | No | `USD` | The currency of the member. |
| Member Exchange Rate | Numeric | No | `1.24` |  |
| Min Ad Duration | Numeric | No |  | The minimum duration allowed for an individual ad in the pod |
| Operating System | String | Yes | `"Android 2.3.5 Gingerbread"` | The name of the operating system. |
| Operating System Family | String | Yes | `"Android"` | The name of the operating system family |
| Placement | String | Yes | `My Placement` | The placement name |
| Placement Group | String | Yes | `My Placement Group` | The placement group name |
| Placement Set | Int | Yes | `1234` | The ID of the placement set |
| Playback Method | String | Yes | `auto_play_sound_on` | The playback method for the creative, e.g, 'auto-start, sound on'. |
| Player Height | Numeric | Yes |  | The height of the player in pixels |
| Player Width | Numeric | Yes |  | The width of the player in pixels |
| Pod has bumpers | Boolean | Yes |  | True if the pod is configured to use bumper ads |
| Publisher | String | Yes | `My Publisher` | The publisher name. |
| Publisher Currency | String | Yes |  | The default currency of the publisher in this impression. This dimension is available only when Currency 2.0 is disabled. |
| Publisher Exchange Rate | Numeric | No |  |  |
| Region | String | Yes |  |  |
| Supply Type | String | No | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are 'web', 'mobile_app', and 'mobile_web'. |
| Supports Vpaid | Boolean | No |  | True if the player supported VPAID creatives |
| Video Content Delivery Type | No | String |  | The type of streaming content delivery: Video on Demand (VOD) or Live. |
| Video Content Duration | No | String |  | The length of the video content in seconds. |
| Video Content Genre | No | String |  | The main genre of the program on which the ad will be played, for example, Cooking, Horror, News, or Football. |
| Video Content Language | No | String |  | The language of the content |
| Video Content Program Type | No | String |  | The format of the video program, for example, Movie, Series, Special, Show, Event, or Clip. |
| Video Content Rating | No | String |  | The publisher-identified audience group for which the content is rated, for example, All, Children (7+) , Teens (13+), Young Adults (14+), or Adults (18+). |
| Video Context | String | Yes | `Pre-Roll` | The type of the video creative. See [Video Context](../digital-platform-api/network-advertiser-video-analytics.md#video-context) for possible values. |

## Metrics

\* Filter by comma separated IDs only.

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Formula | Description |
|--|--|--|--|--|
| Booked Revenue Dollars | money | 578.98 | `booked_revenue_dollars` | The revenue generated from managed line items. |
| Clicks | int | 3445 | `clicks` | The number of clicks recorded. For video we record clicks from Microsoft Advertising Invest and external DSPs. |
| Completion rate | double | 0.85 | `video_completions / impressions` | The number of impressions that resulted in a completion. |
| Completions | int | 8458 | `completions` | The number of times the video player reported a completion event |
| CPM | money | 30.56 | `total_revenue / total_imps * 1000` | The average revenue per 1000 impressions sold |
| CTR | double | 0.01 | `clicks / total_imps` | The average number of clicks generated on your inventory from all impression types. |
| Error rate | double | 0.01 | `errors / impressions` | The rate of errors per impression |
| Errors | int | 523 | `errors` | The number of times the video player reported an error before the impression was counted |
| First quartile rate | double | 0.94 | `first_quartiles / video_starts` | The number of first quartiles fired by the video player divided by the number of start events. |
| First Quartiles | int | 9101 | `first_quartiles` | The number of times the video player reported a 25% complete event |
| Impression Seconds | int | 6976 | `creative_duration * imps` | The total number of seconds served on impressions. If you are using a house line item to report unsold opportunities then you may wish to filter or add impression type as a dimension to separate sold and unsold impression seconds. |
| Impression Seconds Kept | int | 34587 | `impression_seconds_kept` | The total number of seconds resold via managed line items. |
| Impression seconds per pod | double | 25.9 | `impression_seconds / pod_count` | The average duration of impressions sold per ad break. |
| Impression Seconds Resold | int | 435435 | `impression_seconds_resold` | The total number of seconds resold via deals or open exchange. |
| Impression Seconds Unsold | int | 6442 | `impression_seconds_unsold` | The total number of seconds unsold tracked by house line items which have the default impression type. |
| Imps (Kept) | int | 2340 | `imps_kept` | The total number of impressions sold by managed line items. |
| Imps (Resold) | int | 324 | `imps_resold` | The total number of impressions sold to other buyers via open exchange or deals. |
| Imps (Unsold) | int | 4523 | `imps_unsold` | The total number of impressions that have blank, default or PSA impression types. If you are using house line items to count unsold impressions, these will be recorded here. |
| Percent Pods 1 Imp | double | 0.43 | `(sum(pod_count) - sum(pod_no_imps)) / sum(pod_count)` | The percentage of ad breaks (pods) sent to Microsoft Advertising for monetization that had at least 1 impression delivered within them. |
| Percent Pods 1 response | double | 0.34 | `(sum(pod_count) - sum(pod_no_responses)) / sum(pod_count)` | The percentage of ad breaks (pods) sent to Microsoft Advertising for monetization that had at least 1 response returned within them. |
| Pod Available Seconds | int | 4534532 | `pod_available_seconds` | The maximum duration that could deliver within the ad breaks (pods). |
| Pod Count | int | 5345 | `pod_count` | The number of ad breaks (pods) sent to Microsoft Advertising for monetization. If multiple ad breaks are sent in one request, e.g. using cue points, then this will record the total number of ad breaks, not ad requests sent to Microsoft Advertising. |
| Pod Fill Rate Duration | double | 0.55 | `sum(impression_seconds_resold + impression_seconds_kept) / sum(max_duration * pod_count)` | The total resold and kept seconds divided by the maximum duration that could deliver within the ad breaks (pods). |
| Pod Fill Rate Slots | double | 0.28 | `sum(imps_kept + imps_resold) / sum(imps_resold + imps_kept + imps_unsold)` | The total resold and kept impressions divided by the total impressions served. This metric can be used when a house line item is being used to track unsold impressions as default impression types. |
| Pod No Imps | int | 34 | `pod_no_imps` | The number of ad breaks where no kept, resold or default impressions were recorded in any slot in the pod. |
| Pod Slot Opportunities | int | 43423 | `sum(unmatched_min_slot_opportunities) + sum(imps_resold + imps_kept + imps_unsold)` | How many impressions were delivered plus the total remaining opportunities based on the unfilled duration of the pod and the minimum ad duration. |
| Pod Total Max Slots | int | 464544 | `max_number_ads * pod_count` | The maximum number of slots that it would be possible to serve across pods. |
| Poda with 1 response or more | int | 453254 | `sum(pod_count) - sum(pod_no_responses)` | The total number of ad breaks (pods) that have at least 1 creative response within them. |
| Pods with 1 impression or more | int | 4534 | `pod_count - pod_no_imps` | The number of ad breaks where there was at least 1 impression recorded |
| Reseller Revenue Dollars | money | 8370 | `reseller_revenue_dollars` | The total revenue generated from open exchange and deals. |
| Revenue per available second | money | 0.01 | `total_revenue / (max_duration * pod_count)` | The unit revenue in terms of seconds available to sell. |
| Revenue per click | money | 0.20 | `total_revenue / clicks` | The revenue generated per click event recorded. |
| Revenue per pod mili | money | 99.12 | `total_revenue / pod_count * 1000` | The average revenue per ad break. |
| Revenue per second sold | money | 0.5 | `total_revenue / impression_seconds` | The revenue per second resold and kept. |
| Second quartile rate | double | 0.90 | `second_quartiles / video_starts` | The number of second quartiles fired by the video player divided by the number of start events. |
| Second Quartiles | int | 8912 | `second_quartiles` | The number of times the video player reported a 50% complete event |
| Seconds per impression | int | 6.8 | `sum(impression_seconds_resold + impression_seconds_kept + impression_seconds_unsold) / sum(imps_resold + imps_kept + imps_unsold)` | The total seconds on all impressions divided by the total number of seconds. |
| Skip rate | double | 0.01 | `skips / impressions` | The number of skips divided by the number of impressions recorded |
| Skips | int | 85 | `skips` | The number of times the video player reported a skip event |
| Start rate | double | 0.98 | `starts / impressions` | The number of starts divided by the number of impressions recorded. |
| Started Video Completion Rate | double | 0.98 | `video_completions / video_starts` | The number of video starts that resulted in a completion |
| Starts | int | 9236 | `starts` | The number of times the video player reported a start event |
| Third quartile rate | double | 0.87 | `third_quartiles / video_starts` | The number of third quartiles fired by the video player divided by the number of start events. |
| Third Quartiles | int | 8646 | `third_quartiles` | The number of times the video player reported a 75% complete event |
| Total Imps | int | 453456 | `imps_kept + imps_resold + imps_unsold` | The total number of impressions recorded. |
| Total Revenue | money | 324.0 | `booked_revenue_dollars + reseller_revenue_dollars` | The total revenue resold and kept. |
| Unmatched min slot opportunities | int | 5454 | `unmatched_min_slot_opportunities` | How many unfilled slot opportunities there were based on the duration filled and the minimum possible ad duration. When minimum ad duration is not set, or equals zero, this value is calculated with a minimum ad duration of 15 seconds. |

## To run your report

Follow these steps to run your report.

1. Select **Reporting** from the appropriate top menu (depending on how your account has been configured), or, from the Publishers top menu, click on **Prebid Server Premium** > **Analytics** > **Prebid Server Analytics**.
1. Select the relevant **report** from the list. The Report screen shows the available filters, dimensions, and delivery options for the report. The selections you make here will determine what report data is delivered to you, and how.

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
