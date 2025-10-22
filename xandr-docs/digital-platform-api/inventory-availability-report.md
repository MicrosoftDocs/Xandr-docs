---
title: Digital Platform API - Inventory Availability Report
description: Explore the Inventory Availability report to gain insights into the types of inventory available on the platform.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Inventory Availability report

Inventory availability reports offer insight into the types of inventory available on the platform. These reports are available by request only; use the [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com). Due to the structure of our impression availability databases, reporting dimensions are limited to those outlined below. Also note:

- Our databases contain 30 days worth of historical inventory availability data. Reports are therefore limited to this timeframe.
- Additional reporting restrictions may apply to mobile impressions. Contact your Xandr representative for further information.

## Time frame

You can run this report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

### Data retention period

Data in this report is retained for 30 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `day` | date | Yes | `"2023-04-18"` | The day of the impression. |
| `month` | date | Yes | `"2023-04"` | The month of the impression. |
| `seller_member_id` | int | Yes | `9876` | Internal ID of the selling member. |
| `seller_member_name` | string | No | `"CNN"` | Display name of the seller member. |
| `size` | string | Yes | `"120"x"600"` | The standard size of a creative. To know more about the sizes, see `standard_sizes` returned from [Member Service](member-service.md). |
| `geo_country` | string | Yes | `"US"` | The code of the geographical country/region associated with the impression. |
| `imp_type_id` | int | Yes | `5` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1` ("Blank"): No creative served.<br> - `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br> - `3` ("Default Error"): A default creative served due to a timeout issue.<br> - `4` ("Default"): A default creative served because there were no valid bids.<br> - `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br> - `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br> - `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br> - `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9` ("External Impression"): An impression from an impression tracker.<br> - `10` ("External Click"): A click from a click tracker. |
| `media_type_id` | int | Yes | `5` | The ID associated with a certain media type. For example, video. For more details, see [Media Type Service](media-type-service.md). |
| `audit_type_id` | int | Yes | `2`| The integer code for the priority of the audit. Allowed values:<br> - `1`: Standard<br> - `2`: Priority |
| `browser_id` | int | Yes | `3` | The ID associated with a certain browser. For example, Microsoft Edge. For more details, see [Browser Service](browser-service.md). |
| `mobile_application` | string | No | `"Angry Birds (com.rovio.angrybirds)"` | The name of the mobile application followed by the ID in Xandr's format. |
| `language_id` | int | Yes | `1` | The ID associated with a certain browser. For example, English. For more details, see [Language Service](language-service.md). |
| `operating_system_family_id` | int | Yes | `5` | The ID associated with a certain operating system family. For example, Microsoft Windows. For more details, see [Operating System Family Service](operating-system-family-service.md). |
| `datacenter_id` | int | Yes | `001` | The ID of the data center used to route the request to demand partners. |
| `seller_join_date` | int | Yes | `20220901` | The date when a seller member was added. If less than a year, the exact date will show; if over a year, the join date will show as **+1 year**. |
| `mobile_application_id` | string | Yes | `"343200656"` (iOS) or `"com.rovio.angrybirds"` (Android) | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `device_type` | int | Yes | `1` | Device type ID on which the impression was served. Possible values are:<br> - `0` (other devices)<br> - `1` (desktops & laptops)<br> - `2` (mobile phones)<br> - `3` (tablets)<br> - `4` (tv)<br> - `5` (game consoles)<br> - `6` (media players)<br> - `7` (set top box) |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `1000` | imps | The number of available impressions. |

## Examples

### Create the JSON-formatted report request

The JSON file should include the `report_type` of `"platform_inventory_avail"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat platform_inventory_avail

{
    "report": {
        "columns": [
            "day",
            "seller_member_name",
            "audit_type",
            "size",
            "device_type",
            "operating_system_family",
            "geo_country",
            "imps"
        ],
        "format": "csv",
        "report_interval": "today",
        "report_type": "platform_inventory_avail"
    }
}
```

### `POST` the request to the Report service

```
$ curl -b cookies -X POST -d @platform_inventory_avail 'https://api.appnexus.com/report'

{
   "response":{
      "status":"OK",
      "report_id":"6b177543a9411ffa67b09bdf5e76cac1"
   }
}
```

### `GET` the report status from the Report service

```
$ curl -b cookies 'https://api.appnexus.com/report?id=6b177543a9411ffa67b09bdf5e76cac1'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2020-08-25 13:03:37",
         "json_request":"{\"report\":{\"report_type\":\"platform_inventory_avail\",\"columns\":[\"day\",\"seller_member_name\",\"audit_type\",\"imps\",\"size\",\"device_type\,\"operating_system_family\,\"geo_country\"],\"report_interval\":\"today\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"device_type\":\"123456\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1598400000,\"start_date\":1598313600,\"user_id\":\"987654\"}",
         "url": "report-download?id=6b177543a9411ffa67b09bdf5e76cac1"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies 'https://api.appnexus.com/report-download?id=6b177543a9411ffa67b09bdf5e76cac1' > /tmp/platform_inventory_avail.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
