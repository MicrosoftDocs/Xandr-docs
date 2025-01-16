---
title: Video Mediation Demand Report
description: Explore the Video Mediation Demand report to evaluate performance of mediated networks and optimize waterfall priorities.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Video Mediation Demand report

The **Video Mediation Demand Report** can be used by video mediation clients to evaluate performance of mediated networks and optimize waterfall priorities. The report incorporates mediation and financial data as well as data on individual partner waterfall performance that will be made available through updates to the video mediation framework.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- today
- last_24_hours
- yesterday
- last_48_hours
- last_7_days
- last_14_days
- month_to_date
- month_to_yesterday
- last_30_days

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

### Data retention period

Data retention period for this report is 45 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `month` | time | Yes | `"2010-02"` | The month of the auction. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buyer member. |
| `seller_member_id` | int | Yes | `675` | The ID of the buyer member. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher. |
| `publisher_name` | string | No | `"Test"` | The name of the publisher. |
| `publisher` | string | No | `"Test (123)"` | The name and ID of the publisher. |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country/region. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country/region. |
| `site_id` | int | Yes | `194` | The ID of the site.<br><br>**Note:** For impressions older than 100 days, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site Name"` | The name of the site. |
| `site` | string | No | `"Site Name(194)"` | The name and ID of the site. |
| `tag_id` | int | Yes | `675` | The placement id with visibility profile. |
| `placement_code` | string | No | `"Ivillage Code"` | The custom code for the placement. |
| `placement_name` | string | No | `"Ivillage 160x600"` | The name of the placement.<br><br>**Note:** For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | No | `"Ivillage 160x600 (675)"` | The name and ID of the placement. |
| `media_type` | string | No | `"video"` | The general display style of the creative (`banner`, `expandable`, `video`, etc.) |
| `media_type_id` | int | Yes | `3` | The ID associated with the media type. |
| `device_type` | string | No | `"Laptop"` | The name for the type of device where the creative is displayed. |
| `mediated_network_id` | int | Yes | `121` | The ID of the mediated network. |
| `mediated_network_name` | string | No | `"MediatedNW"` | The name of the mediated network. |
| `mediated_bid_id` | int | Yes | `177` | The ID of the mediated bid. |
| `mediated_bid_name` | string | No | `"MediatedBidOne"` | The name of the mediated bid. |
| `call_type` | string | Yes | `"Open RTB"` | The type of the ad request call. |
| `operating_system_family_id` | int | Yes | `3` | The ID for an operating system family (`Linux`, `Windows` etc.) |
| `operating_system_family_name` | string | No | `"Linux"` | The name of an operating system family. |
| `waterfall_position` | int | Yes | `90` | The 0-based position of the creative in the video waterfall. |
| `waterfall_depth` | int | Yes | `8` | The depth of the video waterfall. |
| `video_operating_system_id` | int | Yes | `9` | The ID of the operating system of the video waterfall. |
| `video_operating_system_name` | string | No | `"Mac OS"` | The name of the operating system of the video waterfall. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `mediation_requests` | int | `5660` | mediation_requests | The total number of mediation requests. |
| `mediation_responses` | int | `7789` | mediation_responses | The total number of successful video mediation responses where a valid video creative was returned and unwrapped. |
| `mediation_response_no_bid` | int | `2000` | mediation_response_no_bid | The number of video mediation no-bid responses. |
| `mediation_response_timeout` | int | `677` | mediation_response_timeout | The number of video mediation timeouts. |
| `mediation_response_error` | int | `899` | mediation_response_error | The number of video mediation error responses. |
| `mediation_latency` | int | `77` | mediation_latency | The average video mediation latency. |
| `waterfall_inclusions` | int | `54` | waterfall_inclusions | The number of video waterfall inclusions. |
| `average_waterfall_depth` | int | `7` | average_waterfall_depth | The average video waterfall depth. |
| `average_waterfall_latency` | int | `6` | average_waterfall_latency | The average video waterfall latency. |
| `waterfall_ad_load_attempts` | int | `110` | waterfall_ad_load_attempts | The number of video waterfall ad load attempts. |
| `waterfall_ad_load_success` | int | `77` | waterfall_ad_load_success | The number of successful ad loads for video waterfall. |
| `waterfall_ad_load_vast_error` | int | `22` | waterfall_ad_load_vast_error | The number of VAST errors for ad loads in video waterfall. |
| `waterfall_ad_load_timeout` | int | `55` | waterfall_ad_load_timeout | The number of time outs for ad loads in video waterfall. |
| `average_waterfall_position` | int | `6` | average_waterfall_position | The average of video waterfall positions. |

## Examples

### Create JSON formatted report request

The JSON file should include the `report_type` `"video_mediation_demand_analytics"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_bid_error

{
    "report":
    {
        "report_type":"video_mediation_demand_report",
        "columns":[
            "hour",
            "media_type",
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
$ curl -b cookies -c cookies -X POST -d @video_mediation_demand 'https://api.appnexus.com/report'
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
         "json_request":"{\"report\":{\"report_type\":\"video_mediation_demand\",\"columns\":[\"hour\",\"media_type\",
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
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_mediation_demand.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
