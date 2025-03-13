---
title: Digital Platform API - Video Ad Pod Report
description: Explore insights into ad metrics delivered sequentially between segments of non-commercial video content with the Video Ad Pod report.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Video Ad Pod report

> [!NOTE]
> This report is **deprecated** in August, 2023.

The **Video Ad Pod report** shows metrics for groups of ads delivered sequentially in between segments of non-commercial video programming.

> [!NOTE]
> Video metrics are recorded for VAST creatives only.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_hour
- today
- yesterday
- last_48_hours
- last_7_days(not including today)
- last_30_days
- month_to_date
- last_365_days

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

### Data retention period

Data in this report is retained for 420 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `month` | time | Yes | `"2010-02"` | The month of the auction. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buyer member of the video ad pod. |
| `buyer_member_name` | string | No | `"Test"` | The name of the buyer member of the video ad pod. |
| `buyer_member` | string | No | `"Test (123)"` | The name and ID of the buyer member. |
| `seller_member_id` | int | Yes | `675` | The ID of the seller member of the ad pod. |
| `seller_member_name` | string | No | `"Test"` | The name of the seller member of the ad pod. |
| `seller_member` | string | No | `"Test (123)"` | The name and ID of the seller member. |
| `creative_id` | int | Yes | `9` | The ID of a creative served in the pod. |
| `creative_name` | string | No | `"MyCreative"` | The name of a creative served in the pod. |
| `creative` | string | No | `"MyCreative(9)"` | The name and ID of a creative served in the pod. |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country/region. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country/region. |
| `content_category_id` | int | Yes | `3` | The ID of the content category associated with the ad pod in the placement or placement group. |
| `content_category` | string | No | `"Travel"` | The name of the content category associated with the ad pod in the placement or placement group. |
| `video_context` | string | Yes | `"bannerstream"` | When the video creative was served in the pod. |
| `video_playback_method` | string | Yes | `"auto-play, sound on"` | The playback method for the creative. |
| `ad_pod_call_type` | string | Yes | `"Open RTB"` | The type of the ad request call. |
| `creative_duration` | int | Yes | `"10"` | The length of the ad in seconds. |
| `max_ad_duration` | int | Yes | `"45"` | The maximum video ad duration in seconds allowed by a placement. |
| `max_placement_duration` | int | Yes | `"60"` | The maximum placement duration in seconds. |
| `video_player_size` | string | Yes | `"small"` | The size of the video player based on pixel width and calculated from player dimensions. |
| `seller_type` | string | Yes | `"console"` | The type of seller for the ad pod. Options are console or external. |
| `ad_slot_type` | int | Yes | `1` | The ID of the type of position (ad or bumper) within an ad pod.<br>- `0`: Normal slot<br>- `1`: Intro bumper<br>- `2`: Outro bumper |
| `ad_slot_position` | string | Yes | `"Outro Bumper"` | The chronological order of an ad within its ad pod (placement set). |
| `average_ad_slot_creative_duration` | int | No | `10` | The average length of creatives that were served in an ad slot. |
| `placement_set_id` | int | No | `7` | The ID of the placement set. |
| `device_type` | string | No | `"Laptop"` | The name for the type of device where the creative is displayed. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions. For video ads, an impression takes place when the first frame of the video is loaded. |
| `clicks` | int | `4000` | clicks | The total number of clicks. |
| `ctr` | double | `0.4` | clicks/imps | The click-through rate--the ratio of clicks to impressions, expressed as a percentage. |
| `completion_rate` | double | `0.5` | completions/imps | The ratio of video ad completions to impressions, expressed as a percentage. |
| `unfilled_seconds` | int | `15` | unfilled_seconds | The number of seconds in the ad pod that could not be supplied with ad content. |
| `completions` | int | `10` | completions | The number of video ads that play to completion. |
| `ad_pod_revenue` | int | `100` | ad_pod_revenue | The booked/reseller revenue of the ad pod based on the type of impressions. |

## Examples

### Create JSON formatted report request

The JSON file should include the `report_type` `"video_pod_analytics_network"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat video_pod_analytics_network
  {
    "report":
    {
        "report_type":"video_pod_analytics_network",
        "columns":[
            "hour",
            "ad_slot_type",
            "buyer_member",
            "imps"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the Reporting service

```
$ curl -b cookies -c cookies -X POST -d @video_ad_pod 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the Report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `{{execution_status}}` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.


```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"video_pod_analytics_network\",\"columns\":[\"hour\",\"ad_slot_type\",
            \"buyer_member\",\"imps\",
            \"report_interval\":\"last_48_hours\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_pod_analytics_network.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
