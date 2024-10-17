---
title: Data Usage Report for Data Providers
description: This page talks about your data usage information provided by third parties, costs of that data usage, and the campaigns in which that data was used.    
ms.custom: data-providers
ms.date: 11/30/2023
---

# Data usage report for data providers

This report provides details related to your usage of data provided by third parties (e.g., user segment providers), the costs of that data usage and the campaigns in which that data was used to target users.

The `time_granularity` of the data is `hourly`.

> [!WARNING]
> For impressions older than 100 days, the day is returned rather than the hour. For instructions on retrieving a report, see the [Example](#example) below.

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- `today`
- `yesterday`
- `last_7_days`
- `last_30_days`
- `month_to_date`
- `quarter_to_date`
- `last_month`
- `lifetime`

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](../digital-platform-api/report-service.md).

## Dimensions

| Column | Type | Group? | Filter? | Example | Description |
|--|--|--|--|--|--|
| month | date | no | yes | `"2010-02"` | The month at which the auction associated with the impression occurred |
| day | date | yes | yes | `"2010-02-01"` | The day at which the auction associated with the impression occurred |
| hour | date | yes | yes | `"2010-02-01 05:00:00"` | The hour at which the auction associated with the impression occurred. |
| buyer_member_id | int | yes | yes | `643` | The ID of the member that used the third-party data. |
| buyer_member_name | string | yes | yes | `"Buyer A"` | The name of the member that used the third-party data. |
| advertiser_name | string | yes | yes | `"Advertiser"` | The name of the advertiser that used the third-party-data. |
| geo_country | string | yes | yes | `"US"` | The code of the geographical country associated with the impression. |
| geo_country_name | string | no | no | `"United States"` | The name of the geographical country associated with the impression. |
| geo_country_code | string | yes | yes | `"CA"` | A two-character string denoting the country associated with the impression. For a complete listing of allowed values, see ISO 3166-1 country codes. |
| line_item_id | int | yes | yes | `12345` | The ID of the line item associated with impressions that use third-party data targeting. |
| line_item_name | string | no | no | `line item name` | The name of the line item associated with impressions that use third-party data targeting. |
| data_provider_id | int | yes | yes | `517` | The ID of the third-party that provided the targeting data. |
| targeted_segment_ids | string | no | no | `"935035, 935146"` | The comma-separated list of IDs for each of the segments used when targeting. |
| data_provider_name | string | no | no | `"Peer 39 (Data Provider)"` | The name and ID of the third-party that provided the targeting data. |
| cpm_usd | int | yes | no | `"0.75"` | The CPM value of the data segment used |

## Metrics

| Column | Type | Example | Formula | Description |
|--|--|--|--|--|
| imps | int | `34534` | imps | The total number of impressions that used third-party data to serve the ad. |
| data_costs | money | `3.50` | imps * CPM/1000 | The monetary value of the data segments that were purchased from third-party data providers. |
| data_clearing_fee_usd | money | `0.50` | data_costs * Xandr revshare | The monetary value of the revshare earned by Xandr. |
| data_provider_payout_usd | money | `3.00` | data_costs - data_clearing_fee_usd | The monetary value of the revenue that was paid or will be paid to the data provider. |

## Example

**Step 1:** Create the JSON report request.

The JSON file should include the `report_type` of `"data_usage_analytics_for_data_providers"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (month, day, hour), and specify the format in which the data should be returned (csv, excel, or html).

``` 
$ cat data_usage_analytics
        {"report":
                {
                        "format": "csv",
                        "report_interval": "yesterday",
                        "row_per": ["geo_country"],
                        "columns": ["imps","campaign_id","geo_country"],
                        "report_type": "data_usage_analytics_for_data_providers"
                }
         }
```

For a full explanation of fields that can be included in the JSON file, see the [Report Service](../digital-platform-api/report-service.md).

**Step 2:** `POST` the request to the [Report Service](../digital-platform-api/report-service.md).

`POST` the JSON request to get back a report ID.

``` 
$ curl -b cookies -c cookies -X POST -d @data_usage_analytics "https://api.adnxs.com/report?member_id=MEMBER_ID"
         {
            "response":{
               "status":"OK",
               "report_id":"c445bca183a3d338dc1c5b85a3d484f5"
            }
         }                 
```

**Step 3:** `GET` the report status from the Report Service.

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/report?id=c445bca183a3d338dc1c5b85a3d484f5'
         {
            "response": {
                "status": "OK",
                "report": {
                    "name": null,
                    "created_on": "2014-11-19 22:33:31",
                    "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"geo_country\"],\"columns\":[\"imps\",\"campaign_id\",\"geo_country\"],\"report_type\":\"buyer_data_usage_analytics\",\"filters\":[{\"buyer_member_id\":\"958\"}]}}",
                    "url": "report-download?id=c445bca183a3d338dc1c5b85a3d484f5"
                },
                "execution_status": "ready"
            }
         }           
```

**Step 4:** `GET` the report data from the Report Download Service.

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during the download, the response header includes an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.
>
> `$ curl -b cookies -c cookies 'https://api.adnxs.com/report-download?id=c445bca183a3d338dc1c5b85a3d484f5' > /tmp/data_usage_analytics.csv`
