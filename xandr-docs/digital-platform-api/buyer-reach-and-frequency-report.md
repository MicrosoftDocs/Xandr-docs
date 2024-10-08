---
title: Digital Platform API - Buyer Reach and Frequency Report
description: In this article, learn about the Buyer Reach and Frequency report, their time frame, data retention period, dimensions, and metrics with thorough examples.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Buyer Reach and Frequency report

The Buyer Reach and Frequency report shows you the information associated with two parameters: **"reach"** and **"frequency"**. **"reach"** is the number of unique devices or persons exposed to ads. **"frequency"** is the average number of times each unique device or person was exposed to advertisements. It helps to draw meaningful conclusions about the impact of cross device on conversion use cases. In short, buyers can have an insight on how cross device impacted the number of times a single person saw their ads across all their devices using this report as this report shows historical reach and average frequency on your buying.

The Buyer Reach and Frequency Report offers flexible filtering to analyze unique devices by facilitating below procedure:

- Pull a **basic running total** of unique devices for their active Line Items or Insertion Orders.
- Pull unique devices for these objects over a **defined period of time** (for example, past week).
- You can **filter and group on specific criteria**, which will provide an accurate unique device count across the specified criteria. For example, the count of unique devices across Line Items A, B, and D, in the US and Canada, for the past month.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- today
- last_hour
- last_24_hours
- yesterday
- last_48_hours
- last_2_days
- last_7_days
- last_14_days
- last_30_days
- last_month
- month_to_date
- quarter_to_date
- lifetime

### Data retention period

Data in this report is retained for 90 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | Yes | `"2010-02"` | The month of the auction. |
| `day` | date | Yes | `"2010-02-01"` | The day of the auction. |
| `hour` | date | Yes | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. |
| `geo_country` | string | Yes | `"US"` | The targeted country of the advertisement. |
| `media_type` | string | No | `"Banner"` | The general display style of the creative. |
| `media_type_id` | int | Yes | `1` | The ID of the media type. |
| `supply_type` | string | Yes | `"Mobile App"` | The method of rendering the creative on a device. |
| `billing_period_id` | int | Yes | `453` | The ID of the insertion order's billing period. |
| `billing_period.start_date` | string | No | `"2010-02-01"` | The start date of the insertion order's billing period. |
| `billing_period.end_date` | string | No | `"2010-02-08"` | The end date of the insertion order's billing period. |
| `split_id` | int | Yes | `111` | The ID of the split that purchased the impressions in this data set. |
| `split_name` | string | No | `"FirstSplit"` | The name of the split that purchased the impressions in this data set. |
| `flight` | int | No | `32` | The ID of the flight in a billing period under an insertion order. |
| `flight.start_dt` | string | No | `"2010-02-01"` | The start date of the flight in a billing period under an insertion order. |
| `flight.end_dt` | string | No | `"2010-02-03"` | The end date of the flight in a billing period under an insertion order. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser for which impression was purchased. |
| `advertiser_name` | string | No | `"AdvertiserA"` | The name of the advertiser for which impression was purchased. |
| `line_item_id` | int | Yes | `1122` | The ID of the line item under which the impression was purchased. |
| `line_item_name` | string | No | `"Line Item 1"` | The name of the line item under which the impression was purchased. |
| `creative_id` | int | Yes | `444` | The ID of the creative that we're reporting on the frequency and/or recency of. |
| `creative_name` | string | No | `"Q1 2017 728x90"` | The name of the creative that we're reporting on the frequency and/or recency of. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order under which the impression was purchased. |
| `device_type` | string | Yes | `"Desktops and Laptops"` | The type of the device where the impression has occurred. |
| `frequency_cap_type` | string | No | `"Classical"`, `"Advanced"`, or `"None"` | The type of frequency cap used to limit over-delivery to individual users. When an ID was available in the request, `"Classical"` is the default frequency cap type. `"Advanced"` refers to "Advanced Frequency Management" feature. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions. |
| `identified_imps` | int | `234123` | identified_imps | The total number of identified impressions (i.e. those impressions which included a cookie, device id, etc. as part of the ad request). |
| `unidentified_imps` | int | `234212` | unidentified_imps | The total number of unidentified impressions (i.e. those impressions which did not include a cookie, device id, etc. as part of the ad request). |
| `approx_users_count` | int | `5654` | approx_users_count | The approximate unique users count who viewed the impression. |
| `average_impression_frequency` | double | `8898` | imps/approx_users_count | The number of impressions viewed by per unique users. |
| `approximate_consumer_count` | int | `8888` | approximate_consumer_count | The approximate consumer count who viewed the impression due to cross-device audience extension. |
| `average_consumer_impression_frequency` | double | `7999` | imps/approximate_consumer_count | The number of impressions viewed by per unique consumers due to cross-device audience extension. |
| `approximate_incremental_devices` | int | `899` | approximate_incremental_devices | The total number of unique cookies, mobile or other devices reached by the impressions. |
| `cross_device_incremental_imps` | int | `6888` | cross_device_incremental_imps | The number of impressions which are transacted due to cross-device audience extension. This represents the number of impressions which were delivered on devices outside of the targeted segment(s), due to a cross device graph being applied to extend the reach to more devices owned by a consumer. |
| `average_identified_impression_frequency` | double | `1.23` | identified_imps / approx_users_count | The number of identified impressions viewed per unique users. |
| `estimated_people_reach` **(currently available in the US only)** | int | `269,266` | unique devices / device density factor | The estimated number of people reached, deduplicated across the user-specified dimensions. |

> [!NOTE]
> The metric **`estimated_people_reach`** is currently available in the US only. This model considers the unique devices reached at the zip code level, and utilizes publicly available US census data for the total population of each zip code, in order to estimate the number of people reached for that zip code. This zip code level data is then aggregated when a report is pulled by the API so that the buyer can view it at any level of granularity that is provided by the existing dimensions in the report.
>
> [Advanced Frequency Management (AFM)](../invest/advanced-frequency-management.md), which is currently in **beta**, does not take universal identifier (Universal ID) into account. This is subject to change as the feature would move into GA. Line items utilising Universal ID targeting should avoid using AFM until this is completely adapted.

## Examples

### Create the JSON report request

The JSON file should include the `report_type` of `"buyer_approximate_unique_users_hourly"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_approximate_unique_users_hourly

{"report":
    {
        "report_type":"buyer_approximate_unique_users_hourly",
        "columns":[
            "hour",
            "buyer_member_id",
            "media_type",
            "supply_type",
            "creative",
            "line_item_id",
            "imps",
            "average_impression_frequency",
            "cross_device_incremental_imps"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the Report Service

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -X post -d @buyer_approximate_unique_users_hourly "https://api.appnexus.com/report?advertiser_id=789"

{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### `GET` the report status from the Report Service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2016-12-11 19:15:48",
         "json_request": "{\"report\":{\"report_type\":\"buyer_approximate_unique_users_hourly\",
             \"columns\":[\"hour\",\"buyer_member_id\",
             \"media_type\",\"supply_type\",\"creative\",\"line_item_id\",
             \"imps\",\"average_impression_frequency\",\"cross_device_incremental_imps\"],
             \"report_interval\":\"last_48_hours\",\"format\":\"csv\",\"filters\":[{\"advertiser_id\":\"789\"}]}}",
             "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the Report Download Service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/buyer_approximate_unique_users_hourly.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
