---
title: Conversion Pixel Last Fire
description: In this article, learn about the Conversion Pixel Last Fire report, their time frame, dimensions, and metrics with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Conversion Pixel Last Fire

The Conversion Pixel Fire report allows you to view the date and time when your advertisers' conversion pixels last fired. You can use this information both to verify the pixels that are firing properly and to identify the pixels in need of troubleshooting.

For each conversion pixel, the last fire should correspond to the last time a user visited the web page on which the pixel is placed. If a pixel has never fired, or last fired a long time ago, it is a sign that the pixel may not be placed correctly on the page.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [examples](#examples) below.

> [!NOTE]
> A conversion pixel fire does not necessarily mean that there was a conversion attributed to one of your campaigns. Therefore, you may see that a conversion pixel is firing even if the associated line items do not show any revenue from conversions. To get data on attributed conversions, rather than just conversion pixel fires, use the [Advertiser Attributed Conversions](advertiser-attributed-conversions.md) report.

## Time frame

This report retrieves data for the entire lifetime of a pixel but only in UTC timezone. The `report_interval` field in the JSON request can be set only to `lifetime`, but this is not necessary, as the interval defaults to `lifetime` if not specified. Likewise, the `timezone` field in the JSON request can be set only to `UTC`, but this is not necessary, as the timezone defaults to `UTC` if not specified.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `pixel_id` | int | yes | `10` | The ID of the conversion pixel. |
| `advertiser_id` | int | yes | `234` | The ID of the advertiser that owns the pixel. |
| `advertiser_name` | string | no | `Advertiser 1` | The name of the advertiser that owns the pixel. |
| `advertiser` | string | no | `Advertiser 1 (234)` | **Deprecated** (as of October 17, 2016). |
| `buyer_member_id` | int | yes | `567` | The ID of the buying member. |
| `buyer_member_name` | string | no | `Member Name` | The name of the buying member. |
| `buyer_member` | string | no | `Member Name (567)` | **Deprecated** (as of October 17, 2016). |

## Metrics

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `last_fired` | time | no | `2023-01-27 18:58:49` | The date on which the conversion pixel last fired. If the pixel has never fired, this will be 1900-01-01 00:00:00. |

## Examples

### Create the JSON-formatted report request

```
$ cat pixel_fired
  {
    "report": {
        "report_type": "pixel_fired",
        "columns": [
            "pixel_id",
            "last_fired",
            "advertiser_id",
            "buyer_member_id"
        ],
        "report_interval": "lifetime",
        "emails": ["js@email.com"],
        "format": "csv"
    }
}
```

### `POST` the request to the Reporting Service

```
$ curl -b cookies -c cookies -X POST -d @pixel_fired_report 'https://api.appnexus.com/report?advertiser_id=123'

{
    "response":{
        "status":"OK",
        "report_id":"07af1282c9485adcef49c95fa5d7496b"
    }
}
```

### `GET` the report status from the Report Service

You make a `GET` call with the Report ID to retrieve the status of the report. You continue making this `GET` call until the `execution_status` is `"ready"`. Then you use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=07af1282c9485adcef49c95fa5d7496b'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2012-01-27 19:47:51",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "did not find any cache table for 2,59",
            "json_request": "{\"report\":{\"report_type\":\"pixel_fired\",\"columns\":[\"pixel_id\",
             \"last_fired\",\"advertiser_id\",\"buyer_member_id\"],\"report_interval\":\"lifetime\",\"emails\":
             [\"js@email.com\"],\"filters\":[{\"buyer_member_id\":\"319\"}]}}",
            "header_info": "Report type:,pixel_fired\u000d\u000a,\u000d\u000aRun at:,2012-01-27 19:47:51\
             u000d\u000aStart date:,\u000d\u000aEnd date:,\u000d\u000aTimezone:,\u000d\u000aUser:,
             Sample User (2562)\u000d\u000a",
            "url": "report-download?id=677556dvds34013ff1108f159d7f39b"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the Report Download Service

To download the report data to a file, you make another `GET` call with the Report ID, but this time to the **report-download** service. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> For added convenience, the url field in the previous `GET` response provides you the service and ID to use in this call.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=677556dvds34013ff1108f159d7f39b' > /tmp/pixel_fire.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
