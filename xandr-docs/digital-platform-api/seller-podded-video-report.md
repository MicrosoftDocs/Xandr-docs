---
title: Seller Pod Analytics Report
description: Use the Seller Pod Analytics report to view metrics for groups of ads (aka pods) delivered sequentially in between segments of non-commercial video programming.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Seller Pod Analytics report

> [!NOTE]
> This feature is currently in **Alpha**. It is still under development and may be subjected to changes without notice. Contact your Xandr Account Representative to get it enabled.

The **Seller Pod Analytics** **report** shows metrics for groups of ads (aka pods) delivered sequentially in between segments of non-commercial video programming.

You can use this report to determine the following:

- The number of pods that were sent for Monetization
- The average number of impressions sold per pod
- The average estimate of revenue per pre-roll in comparison to mid-roll pod
- The average seconds sold per pod
- The fill rate in seconds
- The number of opportunities to serve impressions if a pod was unfilled

## Time frame

All dates and times are given in UTC.

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- today
- yesterday
- last_7_days(not including today)
- month_to_date
- last_month
- quarter_to_date

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data in this report has the following retention period:
- Hourly retention: 100 days
- Daily retention: 500 days

## Dimensions
| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `advertiser_default_currency` | string | No | `EUR` | The default currency of the advertiser in this impression. This dimension is available only when Currency 2.0 is disabled. |
| `advertiser_default_exchange_rate` | numeric | No |  |  |
| `application` | string | Yes |  | The application name. |
| `billing_currency` | string | No | `USD` | The transaction currency that the buyer used to purchase this impression. This dimension is available only when Currency 2.0 is disabled. |
| `billing_currency_exchange_rate` | numeric | No |  |  |
| `browser` |  |  | `webOS Browser (33)` | The name of the browser. |
| `call_type` | string | Yes |  | The type of handler that was used to send the impression to Xandr (e.g., `ttj`, `ut`, `mob`, `ptv`, `openrtb`). |
| `city` | string | Yes | `Vienna` | The city in which the user is located. |
| `country` | string | Yes | `"France"` | The country of the user's location, both name and code, in the format `"France"`. The string `"250"` can appear in cases where we don't know the country or if the country doesn't map correctly to a location in our database. |
| `device_type` | string | Yes | `"set top box"` | The type of device on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"` |
| `inventory_url` | string | No |  | The URL of the inventory or application package. |
| `language` | string | No | `German (6)` | The language of the creative. |
| `max_ad_duration` | numeric | No | `15` | Max duration of an individual ad within the pod. |
| `max_duration` | numeric | No | `30` | Max duration of the pod the slot served in. |
| `max_number_ads` | numeric | No | `4` | The maximum number of ads for the pod the slot served in. |
| `max_vast_version` | string | No | `4.0` | The max VAST version supported for the slot. |
| `member_currency` | string | No | `USD` | The currency of the member. |
| `member_exchange_rate` | numeric | No | `1.24` |  |
| `min_ad_duration` | numeric | No |  | The minimum duration allowed for an individual ad in the pod. |
| `operating_system` |  |  | `"Android 2.3.5 Gingerbread"` | The name of the operating system. |
| `operating_system_family` |  |  | `"Android"` | The name of the operating system family. |
| `placement` | string | Yes | `My Placement` | The placement name. |
| `placement_group` | string | Yes | `My Placement Group` | The placement group name. |
| `placement_set` | int | Yes | `1234` | The ID of the placement set. |
| `playback_method` | string | Yes | `auto_play_sound_on` | The playback method for the creative, e.g, `'auto-start, sound on'`. |
| `player_height` | numeric | Yes |  | The height of the player in pixels. |
| `player_width` | numeric | Yes |  | The width of the player in pixels. |
| `pod_has_bumpers` | boolean | Yes |  | `True` if the pod is configured to use bumper ads. |
| `publisher` | string | Yes | `My Publisher` | The publisher name. |
| `publisher_currency` | string | Yes |  | The default currency of the publisher in this impression. This dimension is available only when Currency 2.0 is disabled. |
| `publisher_exchange_rate` | numeric | No |  |  |
| `region` | string | Yes |  | The region in which the user is located. |
| `supply_type` | string | No | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `'web'` <br> - `'mobile_app'` <br> - `'mobile_web'`. |
| `supports_vpaid` | boolean | No |  | `True` if the player supported VPAID creatives. |
| `video_content_delivery_type` | no | String |  | The type of streaming content delivery: `Video on Demand (VOD)` or `Live`. |
| `video_content_duration` | no | String |  | The length of the video content in seconds. |
| `video_content_genre` | no | String |  | The main genre of the program on which the ad will be played, for example, `Cooking`, `Horror`, `News`, or `Football`. |
| `video_content_language` | no | String |  | The language of the content. |
| `video_content_program_type` | no | String |  | The format of the video program, for example, `Movie`, `Series`, `Special`, `Show`, `Event`, or `Clip`. |
| `video_content_rating` | no | String |  | The publisher-identified audience group for which the content is rated, for example, `All`, `Children (7+)`, `Teens (13+)`, `Young Adults (14+)`, or `Adults (18+)`. |
| `video_context` |  |  | `Pre-Roll` | The type of the video creative. See `video_context` field in [Network Advertiser Video Analytics](./network-advertiser-video-analytics.md) for possible values. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `booked_revenue_dollars` | money | `578.98` | booked_revenue_dollars | The revenue generated from managed line items. |
| `clicks` | int | `3445` | clicks | The number of clicks recorded. For video we record clicks from Microsoft Invest and external DSPs. |
| `completion_rate` | double | `0.85` | video_completions / impressions | The number of impressions that resulted in a completion. |
| `completions` | int | `8458` | completions | The number of times the video player reported a completion event. |
| `cpm` | money | `30.56` | total_revenue / total_imps * 1000 | The average revenue per 1000 impressions sold. |
| `ctr` | double | `0.01` | clicks / total_imps | The average number of clicks generated on your inventory from all impression types. |
| `error_rate` | double | `0.01` | errors / impressions | The rate of errors per impression. |
| `errors` | int | `523` | errors | The number of times the video player reported an error before the impression was counted. |
| `first_quartile_rate` | double | `0.94` | first_quartiles / video_starts | The number of first quartiles fired by the video player divided by the number of start events. |
| `first_quartiles` | int | `9101` | first_quartiles | The number of times the video player reported a 25% complete event. |
| `impression_seconds` | int | `6976` | creative_duration * imps | The total number of seconds served on impressions. If you are using a house line item to report unsold opportunities then you may wish to filter or add impression type as a dimension to separate sold and unsold impression seconds. |
| `impression_seconds_kept` | int | `34587` | impression_seconds_kept | The total number of seconds resold via managed line items. |
| `impression_seconds_per_pod` | double | `25.9` | impression_seconds / pod_count | The average duration of impressions sold per ad break. |
| `impression_seconds_resold` | int | `435435` | impression_seconds_resold | The total number of seconds resold via deals or open exchange. |
| `impression_seconds_unsold` | int | `6442` | impression_seconds_unsold | The total number of seconds unsold tracked by house line items which have the default impression type. |
| `imps (Kept)` | int | `2340` | imps_kept | The total number of impressions sold by managed line items. |
| `imps (Resold)` | int | `324` | imps_resold | The total number of impressions sold to other buyers via open exchange or deals. |
| `imps (Unsold)` | int | `4523` | imps_unsold | The total number of impressions that have blank, default or PSA impression types. If you are using house line items to count unsold impressions, these will be recorded here. |
| `percent_pods_1_imp` | double | `0.43` | (sum(pod_count) - sum(pod_no_imps)) / sum(pod_count) | The percentage of ad breaks (pods) sent to Xandr for monetization that had at least 1 impression delivered within them. |
| `pod_available_seconds` | int | `4534532` | pod_available_seconds | The maximum duration that could deliver within the ad breaks (pods). |
| `pod_count` | int | `5345` | pod_count | The number of ad breaks (pods) sent to Xandr for monetization. If multiple ad breaks are sent in one request, e.g. using cue points, then this will record the total number of ad breaks, not ad requests sent to Xandr. |
| `pod_fill_rate_duration` | double | `0.55` | sum(impression_seconds_resold + impression_seconds_kept) / sum(max_duration * pod_count) | The total resold and kept seconds divided by the maximum duration that could deliver within the ad breaks (pods). |
| `pod_fill_rate_slots` | double | `0.28` | sum(imps_kept + imps_resold) / sum(imps_resold + imps_kept + imps_unsold) | The total resold and kept impressions divided by the total impressions served. This metric can be used when a house line item is being used to track unsold impressions as default impression types. |
| `pod_no_imps` | int | `34` | pod_no_imps | The number of ad breaks where no impression was recorded in any slot. |
| `pod_slot_opportunities` | int | `43423` | sum(unmatched_min_slot_opportunities) + sum(imps_resold + imps_kept + imps_unsold) | How many impressions were delivered plus the total remaining opportunities based on the unfilled duration of the pod and the minimum ad duration. |
| `pod_total_max_slots` | int | `464544` | max_number_ads * pod_count | The maximum number of slots that it would be possible to serve across pods. |
| `pods_with_1_impression` or more | int | `4534` | pod_count - pod_no_imps | The number of ad breaks where there was at least 1 impression recorded. |
| `reseller_revenue_dollars` | money | `8370` | reseller_revenue_dollars | The total revenue generated from open exchange and deals. |
| `revenue_per_available_second` | money | `0.01` | total_revenue / (max_duration * pod_count) | The unit revenue in terms of seconds available to sell. |
| `revenue_per_click` | money | `0.20` | total_revenue / clicks | The revenue generated per click event recorded. |
| `revenue_per_pod_mili` | money | `99.12` | total_revenue / pod_count * 1000 | The average revenue per ad break. |
| `revenue_per_second_sold` | money | `0.5` | total_revenue / impression_seconds | The revenue per second resold and kept. |
| `second_quartile_rate` | double | `0.90` | second_quartiles / video_starts | The number of second quartiles fired by the video player divided by the number of start events. |
| `second_quartiles` | int | `8912` | second_quartiles | The number of times the video player reported a 50% complete event. |
| `seconds_per_impression` | int | `6.8` | sum(impression_seconds_resold + impression_seconds_kept + impression_seconds_unsold) / sum(imps_resold + imps_kept + imps_unsold) | The total seconds on all impressions divided by the total number of seconds. |
| `skip_rate` | double | `0.01` | skips / impressions | The number of skips divided by the number of impressions recorded. |
| `skips` | int | `85` | skips | The number of times the video player reported a skip event. |
| `start_rate` | double | `0.98` | starts / impressions | The number of starts divided by the number of impressions recorded. |
| `started_video_completion_rate` | double | `0.98` | video_completions / video_starts | The number of video starts that resulted in a completion. |
| `starts` | int | `9236` | starts | The number of times the video player reported a start event. |
| `third_quartile_rate` | double | `0.87` | third_quartiles / video_starts | The number of third quartiles fired by the video player divided by the number of start events. |
| `third_quartiles` | int | `8646` | third_quartiles | The number of times the video player reported a 75% complete event. |
| `total_imps` | int | `453456` | imps_kept + imps_resold + imps_unsold | The total number of impressions recorded. |
| `total_revenue` | money | `324.0` | booked_revenue_dollars + reseller_revenue_dollars | The total revenue resold and kept. |
| `unmatched_min_slot_opportunities` | int | `5454` | unmatched_min_slot_opportunities | How many unfilled slot opportunities there were based on the duration filled and the minimum possible ad duration. When minimum ad duration is not set, or equals zero, this value is calculated with a minimum ad duration of 15 seconds. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"seller_pod_analytics_report"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_pod_analytics_report
 
{
    "report":
    {
        "report_type":"seller_pod_analytics_report",
        "columns":[
            "hour",
            "bidder",
            "clicks"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @seller_pod_analytics_report 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `{{execution_status}}` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"seller_pod_analytics_report\",\"columns\":[\"hour\",\"bidder\",
            \"clicks\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/seller_pod_analytics_report.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
