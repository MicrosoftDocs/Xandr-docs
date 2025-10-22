---
title: Bidder Bid Error Report API
description: Explore this article to understand the Bidder Bid Error report API, including its metrics, dimensions, and a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder Bid Error report API

The Bidder Bid Error Report helps you gain insight into your rejected demand through a randomly selected set of 1% of the errors logged on the Xandr platform. Error Count has been multiplied by 100 to account for the 1% sampling.

Use this report to troubleshoot buy-side and sell-side settings that result in auction errors, thereby blocking spend. The goal is to help you eliminate the error in the future. You can find information on the owner, cause and recommended resolution for each error in [Bid Error Codes](bid-error-codes.md).

For instructions on retrieving a report, see [Report Service](../digital-platform-api/report-service.md) or the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:  

- `last_hour`
- `last_24_hours`
- `yesterday`
- `last_2_days`
- `last_7_days`
- `last_30_days`

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](../digital-platform-api/report-service.md).

## Dimensions

| Column | Type | Group? | Filter? | Example | Description |
|:---|:---|:---|:---|:---|:---|
| `hour` | time | Yes | No | `"2010-02-01 06:00:00"` | The hour of the auction.   |
| `day` | time | Yes | No | `"2010-02-01"` | The day of the auction. |
| `error_id` | int | Yes | Yes | `101` | The specific error that occurred and was logged in ImpBus (ties to Error Message). |
| `error_message` | varchar | Yes | No | `“Creative brand banned by member's ad profile”` | A generic Error Message that describes the error that occurred (ties to Error ID). |
| `ad_profile_id` | int | Yes | Yes | `1432` | The Ad Profile ID of the Seller Member impacted by the error. |
| `brand_name` | string | Yes | No | `"Ace Hardware"` | The brand registered in the Xandr system and associated with the creative that is impacted by the error. |
| `brand_id` | int | Yes | Yes | `3` | The ID of the brand associated with the creative. |
| `buyer_member_name` | string | Yes | No | `"My Network"` | The Buyer Member who is impacted by the error. |
| `buyer_member_id` | int | Yes | Yes | `123` | The ID of the Buyer Member. |
| `creative_category_name` | string | Yes | No | `“Beauty”` | A classification assigned to both brands and creatives impacted by the error. |
| `creative_category_id` | int | Yes | Yes | `784` | The ID of the creative category. |
| `creative_code` | int | Yes | Yes | `485` | The Creative Code (internal creative ID) associated with the Creative that is impacted by the error. |
| `creative_id` | int | Yes | Yes | `554` | The Creative ID associated with the Buyer Member that is impacted by the error. |
| `creative_size` | string | Yes | No | `"728x90"` | The size of the creative impacted by the error. |
| `deal_id` | int | Yes | Yes | `2345` | The ID of the deal impacted by the error (if Deal ID = 0 no deal was involved). |
| `language_name` | string | Yes | No | `"English"` | The name of the language. |
| `language_id` | int | Yes | Yes | `1` | The ID of the language. |
| `publisher_id` | int | Yes | Yes | `321` | The ID of the publisher. |
| `seller_member_name` | string | Yes | No | `"NYTimes"` | The Seller Member who is impacted by the error. |
| `seller_member_id` | int | Yes | Yes | `123` | The ID of the Seller Member. |
| `technical_attribute_name` | string | Yes | No | `“Flash”` | Feature of the creative such as whether it is an image, flash, video, is expandable, etc. impacted by the error. |
| `technical_attribute_id` | int | Yes | Yes | `350` | The ID of the Technical Attribute. |
| `buyer_seat_code` | string | Yes | No | `"123abc"` | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| `buyer_seat_name` | string | Yes | No | `"123abc (dsp name)"` | The display name for the buyer seat code. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `error_count` | int | `2340` | sum(error_count)*100 | The amount of errors logged on the Xandr platform over the timeframe selected (a randomly selected set of 1% of the errors multiplied by 100 to account for the sampling). |

## Examples

### Create the JSON-formatted report request

The JSON file should include the `report_type` `bidder_bid_error_report`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](../digital-platform-api/report-service.md).

```
$ cat bidder_bid_error
{
        "report":
        {
                "report_type":"bidder_bid_error_report",
                "columns":[
                        "hour",
                        "seller_member_name",
                        "error_count"
                ],
                "report_interval":"last_24_hours",
                "format":"csv"
        }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @bidder_bid_error 'https://api.adnxs.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"bidder_bid_error_report\",\"columns\":[\"hour\",
            \"seller_member\",\"error_count\",
            \"report_interval\":\"last_48_hours\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use \\i or \\v in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.adnxs.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/bidder_bid_error.csv
```
