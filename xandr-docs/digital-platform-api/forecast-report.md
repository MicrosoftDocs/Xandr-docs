---
title: Forecast Report
description: Use the Forecast report to view both buy and sell-side data for a network member.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Forecast report

The Forecast report can be used to view both buy and sell-side data for a network member:

- Direct advertiser impressions (bought across direct publishers and real-time inventory)
- Direct publishers (sold across direct advertisers and other platform buyers)

For instructions on retrieving a report, see [Report Service](./report-service.md) or the example below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- lifetime

### Data retention period

Data in this report is retained for 33 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `cpm_bid` | money | No | `100.00` | The bid price of a bid bucket. |
| `buyer_member_name` | string | No | `"My Network"` | The buyer member affected by the error. |
| `forecast` | string | No | `"MyForecast(11)"` | The forecast name with id. |
| `forecast_id` | int | Yes | `889` | The ID of a forecast object. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buyer member. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `buyer_member` | string | No | `"My Network (123)"` | The name of the buying member followed by the ID (Xandr format). |
| `campaign` | string | Yes | `"Default Campaign (222)"` | The name of the campaign followed by the ID (Xandr format). |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign. |
| `forecast_name` | string | No | `"MyForecast"` | The name of the forecast. |
| `hours_recorded` | int | No | `77` | The number of hours how long forecast has been run. |
| `bid_bucket_percent` | int | No | `66%` | The percentage of `cumulative_imps_available` that will win at `bid_bucket_price`. |
| `win_rate` | int | No | `71%` | The percentage of `cumulative_imps_available` will win at `bid_bucket_price`. |
| `bid_bucket_price` | money | No | `678.00` | The price to bid to win `cumulative_imps_available`. |
| `hours_recorded_start_time` | date | No | `"2010-02-01"` | The timestamp that forecast started to run. |
| `daily_winnable_imps` | int | No | `655` | The total imps to run within this bucket, projected to a full day. |
| `cumulative_cost` | money | No | `650.00` | The total price to pay if win all `cumulative_imps_available` at that bucket. |
| `media_cost` | money | No | `880.00` | The total price to pay if win all `daily_winnable_imps` at that bucket. |

## Metric

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `cumulative_imps_available` | int | `777` | The total imps to run within this bucket. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"periscope_forecast"`, as well as the `columns` (dimensions) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat periscope_forecast

{
    "report":
    {
        "report_type":"periscope_forecast",
        "columns":[
            "buyer_member",
            "media_cost",
            "win_rate",
            "forecast_name"
            
        ],
        "report_interval":"lifetime",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d periscope_forecast 'https://api.appnexus.com/report'
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
         "json_request":"{\"report\":{\"report_type\":\"periscope_forecast\",\"columns\":[\"lifetime\",\"media_cost\",
            \"buyer_member\",\"media_cost\",
            \"report_interval\":\"lifetime\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/periscope_forecast.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
