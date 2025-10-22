---
title: Network Creative Search
description: Use the Network Creative Search report to view the list of creatives that have served on inventory within a network. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network creative search

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Network Creative Search report can be used to view the list of creatives that have served on the inventory within your network.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the example below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:
- "today"
- "yesterday"
- "last_7_days"
- "last_30_days"
- "last_100_days"

## Dimensions

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `day` | time | `"2010-02-01"` | The day of the auction.<br><br> **Filter**: No |
| `month` | time | `"2010-02"` | The month of the auction.<br><br> **Filter**: No |
| `buyer_member_id` | int | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br> `229` = PSA <br> `0` = Blank <br> `319` = Default<br><br>**Filter**: Yes |
| `seller_member_id` | int | `456` | The ID of the selling member.<br><br>**Filter**: Yes |
| `publisher_id` | int | `321` | The ID of the publisher.<br><br>**Filter**: Yes |
| `creative_id` | int | `654` | The ID of the creative.<br><br>**Filter**: Yes |
| `site_id` | int | `194` | The ID of the site.<br><br>**Note**: For RTB impressions older than 30 days, the `site_id` will be `0`.<br><br>**Filter**: Yes |
| `brand_id` | int | `3` | The ID of the brand associated with the creative.<br><br>**Filter**: Yes |
| `width` | int | `250` | The width of the creative.<br><br>**Filter**: Yes |
| `height` | int | `300` | The height of the creative.<br><br>**Filter**: Yes |
| `tag_id` | int | `491` | The ID of the tag.<br><br>**Filter**: Yes |
| `media_subtype_id` | int | `491` | The ID of the media subtype associated with the creative.<br><br>**Filter**: Yes |
| `audit_status` | string | `"audited"` | The creative's audit status. Possible values: <br> - `"pending"` <br> - `"audited"` <br> - `"unauditable"`<br><br> **Filter**: Yes |
| `format` | string | `"raw-html"` | The creative's format. Possible values: <br>  - `"image"` <br> - `"raw-js"` <br> - `"raw-html"` <br> - `"iframe-html"`<br><br>**Filter**: Yes |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |

## Example

1. **Create a JSON-formatted report request**

    The JSON file should include the `report_type` `"network_creative_search"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

    ```
    $ cat network_creative_search
    {
            "report":
            {
                    "report_type":"network_creative_search",
                    "columns":[
                            "day",
                            "seller_member_id",
                            "buyer_member_id",
                            "publisher_id",
                            "creative_id",
                            "brand_id",
                            "media_subtype_id",
                            "imps"
                    ],
                    "report_interval":"today",
                    "format":"csv"
            }
    }
    ```

1. **`POST` the request to the reporting service**

    ```
    $ curl -b cookies -c cookies -X POST -d @network_creative_search 'https://api.appnexus.com/report'
    {
       "response":{
          "status":"OK",
          "report_id":"9b52ff138e5f9c822bdd8eee4119acf2"
       }
    }
    ```

1. **`GET` the report status from the report service**

    Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is "ready". Then use the **report-download** service to save the report data to a file, as described in the next step.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=9b52ff138e5f9c822bdd8eee4119acf2'
    {
       "response":{
          "status":"OK",
          "report":{
             "name":null,
             "created_on": "2013-03-19 18:42:33",
             "json_request": "{\"report\":{\"report_type\":\"network_creative_search\",\"columns\" [\"day\",\"seller_member_id\",\"buyer_member_id\",\"publisher_id\",\"creative_id\",
             \"brand_id\",\"media_subtype_id\",\"imps\"],\"report_interval\":\"today\",\"format\":\"csv\",\"filters\":[{\"seller_member_id\":\"1066\"}]}}",
             "url": "report-download?id=9b52ff138e5f9c822bdd8eee4119acf2"
          },
          "execution_status":"ready"
       }
    }
    ```

1. **`GET` the report data from the Report Download Service**

    To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

    > [!NOTE]
    > If an error occurs during download, the response header will include an HTTP error code and message. Use -i or -v in your call to expose the response header.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=9b52ff138e5f9c822bdd8eee4119acf2' > /tmp/network_creative.csv
    ```
