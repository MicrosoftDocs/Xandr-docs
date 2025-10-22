---
title: Digital Platform API - Segment Loads Report
description: Explore the Segment Loads report to view metrics about your segments, such as the total segment pixel loads and the count of unique user IDs at specific time points.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Segment Loads report

The Segment Loads report allows you to view metrics about your segments, including the total number of segment pixel loads and the number of unique user IDs included at specific points in time.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [Examples](#examples) below.

> [!NOTE]
> You must select the shared segments explicitly to report on them.

## Time frame

The `report_interval` field in the JSON request can be set to:

- today
- yesterday
- last_48_hours
- last_7_days
- month_to_date

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `segment_id` | int | yes | `220` | The ID of the segment. |
| `segment_name` | string | no | `"Submitted application"` | The name of the segment. |
| `segment` | string | no | `"Submitted application (220)"` | **Deprecated** (as of October 17, 2016). |
| `day` | time | yes | `2011-01-06` | The day for which you want segment metrics. |
| `month` | time | yes | `2011-01` | The month for which you want segment metrics. |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `total_loads` | int | `28375` | The total number of times the segment pixel loaded. |
| `daily_uniques` | int | `556` | The number of unique user IDs added to the segment on a specific day. To view this metric, you must include the day dimension. |
| `monthly_uniques` | int | `10998` | The number of unique user IDs added to the segment in a specific month. To view this metric, you must include the month dimension. |
| `avg_daily_uniques` | int | `675` | The average number of users added to a segment per day for a specific month. To view this metric, you must include the month dimension. |

## Examples

### View monthly and average daily metrics for all segments

1. Create the JSON request for the report.

    ```
    $ cat segment_load
    {
        "report":
        {
            "report_type": "segment_load",
            "columns": [
                "segment_id",
                "segment_name",
                "month",
                "total_loads",
                "monthly_uniques",
                "avg_daily_uniques"
            ],
            "groups": [
                "segment_id",
                "month"
            ],
            "orders": [
                "month"
            ],
            "emails": ["js@email.com"],
            "format": "csv"
        }
    }
    ```

1. `POST` the request to the Report Service.

    ```
    $ curl -b cookies -c cookies -X POST -d @segments_monthly 'https://api.appnexus.com/report'
    
    {
        "response":{
            "status":"OK",
            "report_id":"07af1282c9485adcef49c95fa5d7496b"
        }
    }
    ```

1. `GET` the report status from the Report service.

    Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=07af1282c9485adcef49c95fa5d7496b'
    
    {
        "response": {
            "status": "OK",
            "report": {
                "name": null,
                "created_on": "2012-02-10 16:41:39",
                "cache_hit": false,
                "fact_cache_hit": false,
                "fact_cache_error": null,
                "json_request": "{\"report\":{\"report_type\":\"segment_load\",\"columns\":
                 [\"segment_id\",\"segment_name\",\"month\",\"total_loads\",\"monthly_uniques\",
                 \"avg_daily_uniques\"],\"groups\":[\"segment_id\",\"month\"],\"orders\":
                 [\"month\"],\"emails\":[\"js@email.com\"],\"row_per\":[\"segment_id\",
                 \"month\"]}}",
                "header_info": "Report type:,segment_load\u000d\u000a,\u000d\u000aRun at:,
                 2012-02-10 16:41:39\u000d\u000aStart date:,\u000d\u000aEnd date:,\u000d\u000aTimezone:,
                 \u000d\u000aUser:,John Smith (10055)\u000d\u000a",
                "url": "report-download?id=07af1282c9485adcef49c95fa5d7496b"
            },
            "execution_status": "ready"
        }
    }
    ```

1. `GET` the report data from the Report Download service.

    To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

    ```
    curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=07af1282c9485adcef49c95fa5d7496b' > /temp/segement_load.csv
    ```

### View daily metrics for segment `184531`

1. Create the JSON request for the report.

    > [!NOTE]
    > To get metrics for a specific segment, you must filter the report by `segment_id`.

    ```
    $ cat segment_daily
    
    {
        "report":
        {
            "report_type": "segment_load",
            "columns": [
                "segment_id",
                "segment_name",
                "day",
                "total_loads",
                "daily_uniques"
            ],
            "filters": [
                {
                    "segment_id": 184531
                }
            ],
            "groups": [
                "segment_id",
                "day"
            ],
            "orders": [
                "day"
            ],
            "emails": ["js@email.com"],
            "format": "csv"
        }
    } 
    ```

1. `POST` the request to the Report service.

    ```
    $ curl -b cookies -c cookies -X POST -d segment_load 'https://api.appnexus.com/report'
    
    {
        "response":{
            "status":"OK",
            "report_id":"c5975474b00c68f3cd1db49b8fe758da"
        }
    }
    ```

1. `GET` the report status from the Report service.

    Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=c5975474b00c68f3cd1db49b8fe758da'
    
    {
        "response": {
            "status": "OK",
            "report": {
                "name": null,
                "created_on": "2012-02-10 15:52:16",
                "cache_hit": false,
                "fact_cache_hit": false,
                "fact_cache_error": null,
                "json_request": "{\"report\":{\"report_type\":\"segment_load\",\"columns\":
                 [\"segment_id\",\"segment_name\",\"day\",\"total_loads\",\"daily_uniques\"],
                 \"filters\":[{\"segment_id\":184531}],\"groups\":[\"segment_id\",\"day\"],
                 \"orders\":[\"day\"],\"emails\":[\"js@email.com\"],\"row_per\":
                 [\"segment_id\",\"day\"]}}",
                "header_info": "Report type:,segment_load\u000d\u000a,\u000d\u000aRun at:,
                 2012-02-10 15:52:16\u000d\u000aStart date:,\u000d\u000aEnd date:,
                 \u000d\u000aTimezone:,\u000d\u000aUser:,John Smith (10356)\u000d\u000a",
                "url": "report-download?id=c5975474b00c68f3cd1db49b8fe758da"
            },
            "execution_status": "ready"
        }
    }
    ```

1. `GET` the report data from the Report Download service.

    To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

    ```
    curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c5975474b00c68f3cd1db49b8fe758da' > /temp/segment_load.csv
    ```

    > [!NOTE]
    > There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
