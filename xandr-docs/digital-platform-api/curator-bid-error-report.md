---
title: Digital Platform API - Curator Bid Error Report
description: Use the Curator Bid Error report to gain insight into rejected demand through a randomly selected set of 5% of the errors logged on the platform.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Curator Bid Error report

The **Curator Bid Error Report** helps you gain insight into rejected demand through a randomly selected set of 5% of the errors logged on the Xandr platform. Error Count is multiplied by 100 to account for the 5% sampling. You can use this report to troubleshoot sell-side and buy-side settings that result in auction errors, thereby blocking spend. The goal is to help you eliminate the error in the future. You can find information on the owner, cause and recommended resolution for each error in [Bid Error Codes](../bidders/bid-error-codes.md).

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_hour

### Data retention period

Data in this report is retained for 33 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the error occurred. |
| `day` | time | No | `"2010-02-01"` | The day of the error occurred. |
| `month` | time | No | `"2010-02"` | The month of the error occurred. |
| `error_id` | int | Yes | `101` | The specific error that occurred and was logged in ImpBus (ties to Error Message). |
| `error_message` | varchar | No | `“Creative brand banned by member's ad profile”` | A generic error message that describes the error that occurred (ties to Error ID). |
| `ad_profile_id` | int | Yes | `1432` | The Ad Profile ID of the seller member affected by the error. |
| `bidder_name` | int | No | `“DBM”` | The technology provider who is representing a Buyer Member and is affected by the error. |
| `bidder_id` | string | Yes | `101` | The ID associated with the bidder. |
| `bidder` | string | No | `"DBM(101)"` | The name and ID associated with the bidder. |
| `brand_name` | string | No | `"Ace Hardware"` | The brand registered in the Xandr system and associated with the creative that is affected by the error. |
| `brand_id` | int | Yes | `3` | The ID of the brand associated with the creative. |
| `brand` | string | No | `"Ace Hardware(3)"` | The name and ID of the brand. |
| `buyer_member_name` | string | No | `"My Network"` | The buyer member affected by the error. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buyer member. |
| `buyer_member` | string | No | `"My Network(123)"` | The name and ID of the buyer member. |
| `seller_member_id` | int | Yes | `122` | The ID of the seller member. |
| `seller_member_name` | string | No | `"My Network"` | The seller member affected by the error. |
| `seller_member` | string | No | `"My Network(122)"` | The name and ID of the seller member. |
| `creative_category_name` | string | No | `“Beauty”` | A classification assigned to both brands and creatives affected by the error. |
| `creative_category_id` | Int | Yes | `784` | The ID of the creative category. |
| `creative_category` | string | No | `“Beauty(784)”` | The name and ID of the creative category. |
| `creative_id` | int | Yes | `554` | The creative identifier associated with the buyer member that is affected by the error. |
| `creative_size` | string | No | `"728x90"` | The size of the creative affected by the error. |
| `deal_id` | int | Yes | `2345` | The ID of the deal affected by the error (if Deal ID = 0 no deal was involved). |
| `deal_name` | string | No | `"My Deal"` | The name of the affected deal. |
| `deal` | string | No | `"My Deal(2345)"` | The name and ID of the affected deal. |
| `language_name` | string | No | `"English"` | The name of the language. |
| `language_id` | int | Yes | `1` | The ID of the language. |
| `language` | string | No | `"English(1)"` | The name of the language. |
| `placement_name` | string | No | `"My placement"` | The placement of the seller member that is associated with the error. |
| `placement_id` | int | Yes | `7890` | The ID of the placement. |
| `placement` | string | No | `"My placement(780)"` | The name and ID of the placement. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher affected by the error. |
| `publisher_name` | string | No | `"My publisher"` | The name of the publisher affected by the error. |
| `publisher` | string | No | `"My publisher(321)"` | The name and ID of the publisher affected by the error. |
| `media_type` | int | Yes | `3` | The ID of the general display style of the creative (banner, expandable, video, etc.) |
| `brand_category_id` | int | Yes | `1` | The ID of a category under which brands fall (Airline, Apparel, Computers and Electronics etc.) |
| `brand_category_name` | string | No | `"Airline"` | The name of a brand category. |
| `brand_category` | string | No | `"Airline(1)"` | The name and ID of a brand category. |
| `video_context` | string | Yes | `"Outstream"` | When and where the video creative plays (Outstream, Pre-roll, Mid-roll, Post-roll etc.) |
| `logged_error_message` | string | No | `"Banned brand id(111) detected for the profile"` | The specific error message that describes the error that occurred (ties to Error ID) and present in error logs. |
| `device_type` | int | Yes | `6` | The ID for the type of device where the error occured. |
| `adserver_name` | string | No | `"AdServer One"` | The name of the adserver. |
| `adserver_id` | int | Yes | `132` | The ID of the adserver. |
| `adserver` | string | No | `"AdServer One(132)"` | The name and ID of the adserver. |
| `technical_attribute_name` | string | No | `“Flash”` | The feature of the creative, such as whether it is an image, flash, video, is expandable, etc., that is affected by the error. |
| `technical_attribute_id` | int | Yes | `350` | The ID of the Technical Attribute. |
| `technical_attribute` | string | No | `“Flash(350)”` | The name and ID of the Technical Attribute. |
| `buyer_seat_id` | int | Yes | `350` | The identifier for the seat of the buyer member that is affected by the error. |
| `buyer_seat_code` | string | No | `"SCID001"` | The custom buyer seat ID (submitted by DSP) which was used to bid on the impression |
| `buyer_seat_name` | string | No | `"FirstSeatCodeID"` | The display name for the buyer seat code. |
| `curator_member_id` | int | Yes | `12148` | The curator ID associated with the errors. |
| `curated_deal_id` | int | Yes | `991` | The ID of the curated deal affected by the error |
| `curated_deal_name` | string | No | `"Renault Curator Deal"` | The name of the affected curated deal. |
| `curated_deal` | string | No | `"Renault Curator Deal (111)"` | The name and ID of the affected curated deal. |
| `curator_deal_line_item_id` | int | Yes | `675` | The ID of the line item associated with the deal of the curator member. |
| `curator_deal_line_item_name` | string | No | `"LIOne"` | The name of the line item associated with the deal of the curator member. |
| `curator_deal_line_item` | string | No | `"LIOne(675)"` | The name and ID of the line item associated with the deal of the curator member. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `error_count` | int | `2340` | sum(error_count)*100 | The amount of errors logged on the Xandr platform over the timeframe selected (a randomly selected set of 5% of the errors multiplied by 100 to account for the sampling). |

## Examples

### Create a JSON-formatted report request

The JSON file should include the `report_type` `"curator_bid_error_report"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat curator_bid_error_report  
{
    "report":
    {
        "report_type":"curator_bid_error_report",
        "columns":[
            "hour",
            "bidder",
            "buyer_member",
            "error_count"
        ],
        "report_interval":"custom",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @curator_bid_error_report 'https://api.appnexus.com/report'
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"curator_bid_error_report\",\"columns\":[\"hour\",\"bidder\",
            \"buyer_member\",\"error_count\",
            \"report_interval\":\"custom\"}}",
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/curator_bid_error_report.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
