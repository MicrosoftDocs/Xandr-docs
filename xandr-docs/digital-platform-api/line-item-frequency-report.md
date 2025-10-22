---
title: Line Item Frequency Report
description: Learn about the Line Item Frequency report, providing the ability to view how frequently users are viewing a specific line item's creatives.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Line Item Frequency report

The Line Item Frequency report can be used to view how frequently users are viewing a specific line item's creatives. This report shows data at the line item and is available to members. For instructions on retrieving a report, see the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_48_hours
- today
- yesterday
- last_7_days
- month_to_date
- last_24_hours
- last_30_days

### Data retention period

Data retention period for this report is 45 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Description | Group | Filter |
|:---|:---|:---|:---|:---|
| `hour` | time | The hour of the auction.<br>**Example:** `"2010-02-01 06:00:00"` | Yes | Yes |
| `day` | time | The day of the auction.<br>**Example:** `"2010-02-01"` | Yes | Yes |
| `month` | time | The month of the auction.<br>**Example:** `"2010-02"` | Yes | Yes |
| `buyer_member_id` | int | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: `229` = PSA, `0` = Blank, or `319` = Default.<br>**Example:** `123` | Yes | Yes |
| `insertion_order_id` | int | The ID of the insertion order. | Yes | Yes |
| `advertiser_id` | int | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown.<br>**Example:** `789` | Yes | Yes |
| `line_item_id` | int | The ID of the line item.<br>**Example:** `111` | Yes | Yes |
| `pixel_id` | int | The ID of the pixel.<br>**Example:** `123` | Yes | Yes |
| `advertiser_name` | string | The name of the advertiser.<br>**Example:** `"Verizon Wireless"` | No | No |
| `advertiser` | string | The name of the advertiser followed by the ID (Xandr format).<br>**Example:** `"Verizon Wireless (789)"` | Yes | No |
| `insertion_order_name` | string | The name of the insertion order. | No | No |
| `insertion_order_code` | string | The custom code for the insertion order. | No | No |
| `line_item_name` | string | The name of the line item.<br>**Example:** `"Default Line Item"` | No | No |
| `line_item_code` | string | The custom code for the line item. | No | No |
| `insertion_order` | string | The name of the insertion order followed by the ID (Xandr format). | Yes | No |
| `line_item` | string | The name of the line item followed by the ID (Xandr format).<br>**Example:** `"Default Line Item (111)"` | Yes | No |
| `line_item_frequency_bucket` | string | The bucket for how frequently the line item's creatives were displayed. See [Line Item Frequency Buckets](#line-item-frequency-buckets) below. | Yes | Yes |
| `line_item_frequency_bucket_id` | int | The ID of the line item frequency bucket. For possible values, see [Line Item Frequency Buckets](#line-item-frequency-buckets) below.  | No | No |

### Line item frequency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-date"` |
| `-1` | `"no-cookie"` |
| `0` | `"0"` |
| `1-20` | Bucket name is the number of times the line item's creatives have been viewed. |
| `21` | `"21-25"` |
| `22` | `"26-30"` |
| `23` | `"31-35"` |
| `24` | `"36-40"` |
| `25` | `"41-45"` |
| `26` | `"46-50"` |
| `27` | `"51-60"` |
| `28` | `"61-70"` |
| `29` | `"71-80"` |
| `30` | `"81-90"` |
| `31` | `"91-100"` |
| `32` | `"101-200"` |
| `33` | `"201-300"` |
| `34` | `"301-400"` |
| `35` | `"401-500"` |
| `36` | `"501+"` |

## Metrics

| Column | Type | Description | Example | Formula |
|:---|:---|:---|:---|:---|
| `imps` | int | The total number of impressions (served and resold). | `2437` | imps |
| `clicks` | int | The total number of clicks across all impressions. | `1` | clicks |
| `booked_revenue` | money | The total revenue booked through direct advertisers (line item). | `25.6788` | booked_revenue |
| `cpm` | money | The cost per 1000 impressions. | `1.6605` | (cost / imps) x 1000 |
| `total_convs` | int | The total number of post-view and post-click conversions. | `9` | post_click_convs + post_view_convs |
| `convs_rate` | double | The rate of conversions to impressions. | `0.0002218770` | total_convs / imps |
| `ctr` | double | The rate of clicks to impressions. | `0.0002218777` | clicks / imps |
| `post_view_convs` | int | The total number of recorded post-view converstions. | `5` | post_view_convs |
| `post_click_convs` | int | The total number of recorded post-click conversions. | `4` | post_click_convs |
| `post_click_convs_rate` | double | The rate of post-click conversion to impressions. | `0.0002` | post_click_convs / imps |
| `media_cost` | money | The total amount spent. | `100.00` | media_cost |
| `profit` |  |  |  |  |
| `profit_ecpm` | money | The profit as a percentage of the revenue. | `0.778` | ((booked_revenue - media_cost) / imps) * 100 |
| `revenue_ecpc` | money | The total revenue per click. | `0.8256` | booked_revenue / clicks |
| `revenue_ecpa` | money | The total revenue per conversion. | `5.00` | booked_revenue / total_convs |
| `cost_ecpc` | money | The cost per click. | `0.1834` | media_cost / clicks |
| `cost_ecpa` | money | The cost per attribution/conversion. | `0.1834` | media_cost / total_convs |
| `convs_per_mm` | double | The number of conversions per million impressions. | `221.87708` | (total_convs / imps) x 1,000,000 |

## Examples

### Create the JSON report request

```
$ cat insertion_order_frequency  {
    "report":{
        "report_type":"insertion_order_frequency",
        "columns":[
            "hour",
            "campaign",
            "imps",
            "clicks",
            "total_convs",
            "ctr",
            "convs_rate"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the Report service

`POST` the JSON request to get back a `report_ID`.

```
$ curl -b cookies -X post -d @insertion_order_frequency "https://api.appnexus.com/report"
 
{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

Alternatively, you can get a `report_id` via a `POST` request using a `saved_report_id`.

```
curl -b cookies -X POST 'https://api.appnexus.com/report?saved_report_id=30'
```

### `GET` the report status from the Report service

Make a `GET` call with the `report_id` to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then, use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:15:48",
         "json_request":"{\"report\":{\"report_type\":\"insertion_order_frequency\",\"columns\":
          [\"hour\",\"campaign\",\"imps\",\"clicks\",\"total_convs\",
          \"ctr\",\"convs_rate\"],\"row_per\":[\"hour\",\"campaign_id\"],
          \"report_interval\":\"last_48_hours\",\"filters\":[{\"advertiser_id\":\"690\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the `"url"` field of the response to your previous `GET` call. When setting the file to which you want to save the report, use the file extension of the `"format"` (e.g., .csv) that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `\-i` or `\-v` in your call to expose the response header.

```
curl -b cookies 'http://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' -o /tmp/insertion_order_frequency.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
