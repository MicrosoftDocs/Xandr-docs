---
title: Digital Platform API - Seller Bid Error Report
description: Use the Seller Bid Error report to get an insight into rejected demand through a randomly selected set of errors. Helps troubleshoot sell-side and buy-side settings.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Seller Bid Error report

The **Seller Bid** **Error Report** helps you gain insight into rejected demand through a randomly selected set of 5% of the errors logged on the AppNexus platform. Error Count has been multiplied by 100 to account for the 5% sampling.

Use this report to troubleshoot sell-side and buy-side settings that result in auction errors, thereby blocking spend. The goal is to help you eliminate the error in the future. You can find information on the owner, cause and recommended resolution for each error in [Bid Error Codes](../bidders/bid-error-codes.md).

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- yesterday
- last_24_hours
- last_2_days
- last_7_days
- last_30_days

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 403 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `day` | time | No | `"2010-02-01"` | The day of the auction. |
| `error_id` | int | Yes | `101` | The specific error that occurred and was logged in ImpBus (ties to Error Message) |
| `error_message` | varchar | No |`“Creative brand banned by member's ad profile”` | A generic Error Message that describes the error that occurred (ties to Error ID) |
| `ad_profile_id` | int | Yes | `1432` | The Ad Profile ID of the Seller Member affected by the error. |
| `bidder_name` | int | No | `"DBM"` | The technology provider who is representing a Buyer Member and is affected by the error. |
| `bidder_id` | string | Yes | `101` | The ID associated with the bidder |
| `brand_name` | string | No | `"Ace Hardware"` | The brand registered in the AppNexus system and associated with the creative that is affected by the error. |
| `brand_id` | int | Yes | `3` | The ID of the brand associated with the creative. |
| `buyer_member_name` | string | No | `"My Network"` | The Buyer Member affected by the error. |
| `buyer_member_id` | int | Yes | `123` | The ID of the Buyer Member. |
| `creative_category_name` | string | No | `“Beauty”` | A classification assigned to both brands and creatives affected by the error. |
| `creative_category_id` | Int | Yes | `784` | The ID of the creative category. |
| `creative_id` | int | Yes | `554` | The Creative ID associated with the Buyer Member that is affected by the error. |
| `creative_size` | string | No | `"728x90"` | The size of the creative affected by the error. |
| `deal_id` | int | Yes | `2345` | The ID of the deal affected by the error (if `Deal ID = 0` no deal was involved). |
| `language_name` | string | No | `"English"` | The name of the language. |
| `language_id` | int | Yes | `1` | The ID of the language. |
| `placement_name` | string | No | `"My placement"` | The Placement of the Seller Member that is associated with the error. |
| `placement_id` | int | Yes | `7890` | The ID of the placement. |
| `publisher_name` | string | No | `"Skype"` | The Publisher affected by the error. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher. |
| `technical_attribute_name` | string | No | `"Flash"` | The feature of the creative, such as whether it is an image, flash, video, is expandable, etc., that is affected by the error. |
| `technical_attribute_ID` | int | Yes | `350` | The ID of the Technical Attribute. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `error_count` | int | `2340` | sum(error_count)*100 | The amount of errors logged on the AppNexus platform over the timeframe selected (a randomly selected set of 5% of the errors multiplied by 100 to account for the sampling). |
| `blocked_bid_cpm` | double | `5.68` | sum(blocked_bid_value) / sum (error_count) | The bid price of the blocked bid. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` `"seller_bid_error_report"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_bid_error

{
    "report":
    {
        "report_type":"seller_bid_error_report",
        "columns":[
            "hour",
            "bidder",
            "buyer_member",
            "error_count"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @seller_bid_error 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `{{execution_status}}` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"seller_bid_error_report\",\"columns\":[\"hour\",\"bidder\",
            \"buyer_member\",\"error_count\",
            \"report_interval\":\"last_48_hours\"}}",
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/advertiser_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
