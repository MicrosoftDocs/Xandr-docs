---
title: Advertiser Frequency Report
description: Use the Advertiser Frequency report to view how frequently users are viewing a specific advertiser's creatives.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Advertiser Frequency report

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Advertiser Frequency report can be used to view how frequently users are viewing a specific advertiser's creatives. This report shows data at the advertiser level and is available to members.

For instructions on retrieving a report, see the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- `last_48_hours`
- `today`
- `yesterday`
- `last_7_days`
- `month_to_date`
- `last_24_hours`
- `last_30_days`

## Dimensions

| Column | Type | Description |
|:---|:---|:---|
| `hour` | time | The hour of the auction.<br>Example: `"2010-02-01 06:00:00"`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `day` | time | The day of the auction.<br>Example: `"2010-02-01"`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `month` | time | The month of the auction.<br>Example: `"2010-02"`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `buyer_member_id` | int | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default.<br>Example: `123`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `insertion_order_id` | int | The ID of the insertion order.<br><br>**Group**: Yes<br>**Filter**: Yes |
| `advertiser_id` | int | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown.<br>Example: `789`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `line_item_id` | int | The ID of the line item.<br>Example: `111`<br><br>**Grou**p: Yes<br>**Filter**: Yes |
| `pixel_id` | int | The ID of the pixel.<br>Example: `123`<br><br>**Group**: Yes<br>**Filter**: Yes |
| `advertiser_name` | string | The name of the advertiser.<br>Example: `"Verizon Wireless"`<br><br>**Group**: No<br>**Filter**: No |
| `advertiser` | string | **Deprecated** (as of October 17, 2016). |
| `insertion_order_name` | string | The name of the insertion order.<br><br>**Group**: No<br>**Filter**: No |
| `insertion_order_code` | string | The custom code for the insertion order.<br>**Group**: No<br>**Filter**: No |
| `line_item_name` | string | The name of the line item.<br>Example: `"Default Line Item"`<br><br>**Group**: No<br>**Filter**: No |
| `line_item_code` | string | The custom code for the line item.<br><br>**Group**: No<br>**Filter**: No |
| `insertion_order` | string | **Deprecated** (as of October 17, 2016). |
| `line_item` | string | **Deprecated** (as of October 17, 2016). |
| `advertiser_frequency_bucket` | string | The bucket for how frequently the advertiser's creatives were displayed. See [Advertiser Frequency Buckets](#advertiser-frequency-buckets).<br><br>**Group**: Yes<br>**Filter**: Yes |
| `advertiser_frequency_bucket_id` | int | The ID of the advertiser frequency bucket. See [Advertiser Frequency Buckets](#advertiser-frequency-buckets) below for possible values.<br><br>**Group**: No<br>**Filter**: No |

### Advertiser frequency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-data"` |
| `-1` | `"no-cookie"` |
| `0` | `"0"` |
| `1` - `21` | Bucket name is the number of times the advertiser's creatives have been viewed. |
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
| `33` | `"201-300`" |
| `34` | `"301-400"` |
| `35` | `"401-500"` |
| `36` | `"501+"` |

## Metrics

| Column | Type | Description | Example | Formula |
|:---|:---|:---|:---|:---|
| `imps` | int | The total number of impressions (served and resold). | `2437` | imps |
| `clicks` | int | The total number of clicks across all impressions. | `1` | clicks |
| `booked_revenue` | money | The total revenue booked through direct advertisers (line item). | `25.6788` | booked_revenue |
| `cpm` | money | The cost per 1000 impressions | `1.6605` | (cost / imps) x 1000 |
| `total_convs` | int | The total number of post-view and post-click conversions. | `9` | post_click_convs + post_view_convs |
| `convs_rate` | double | The rate of conversions to impressions. | `0.0002218770` | total_convs / imps |
| `ctr` | double | The rate of clicks to impressions. | `0.0002218777` | clicks / imps |
| `post_view_convs` | int | The total number of recorded post-view converstions. | `5` | post_view_convs |
| `post_click_convs` | int | The total number of recorded post-click conversions. | `4` | post_click_convs |
| `post_click_convs_rate` | double | The rate of post-click conversion to impressions. | `0.0002` | post_click_convs / imps |
| `media_cost` | money | The total amount spent. | `100.00` | media_cost |
| `profit_ecpm` | money | The profit as a percentage of the revenue. | `0.778` | ((booked_revenue - media_cost) / imps) * 100 |
| `revenue_ecpc` | money | The total revenue per click. | `0.8256` | booked_revenue / clicks |
| `revenue_ecpa` | money | The total revenue per conversion. | `5.00` | booked_revenue / total_convs |
| `cost_ecpc` | money | The cost per click. | `0.1834` | media_cost / clicks |
| `cost_ecpa` | money | The cost per attribution/conversion. | `0.1834` | media_cost / total_convs |
| `convs_per_mm` | double | The number of conversions per million impressions. | `221.87708` | (total_convs / imps) x 1,000,000 |

## Example

### Step 1. Create a JSON report request

The JSON file should include the following:

- `"report_type"` you want to run.
- `"columns"` (dimensions and metrics) you want to retrieve.
- `"report_interval"` you want to retrieve.

You can also include `filters` for dimensions, define granularity (`year`, `month`, `day`), and specify the  `format` in which the data should be returned ( `"csv"` ,  `"excel"` , or  `"html"` ).

To filter a dimension by more than one value, use an array. For example:

> [!NOTE]
> **Correct:**
>
> `"filters": [{"bid_type": ["learn","optimized"]}, {"geo_country":"US"}]`
>
> **Incorrect:**
>
> `"filters": [{"bid_type":"learn"}, {"bid_type":"optimized"}, {"geo_country":"US"}]`

See [Dimensions](#dimensions) and [Metrics](#metrics) above for more details about the columns that can be included in the request.

The example below demonstrates how to retrieve the Advertiser Frequency Report. In this example, the report will display data for the `hour`, `campaign`, `imps`, `clicks`, `total_convs`, `ctr`, and `convs_rate` columns. This report will pull data from the last 48 hours and will format it as a CSV file.

```
$ cat report_request
{
        "report":{
                "report_type":"advertiser_frequency",
                "columns":[
                        "hour",
                        "line_item_id",
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

### Step 2.`POST` the request to the report service

`POST` the JSON request to get back a `report_ID`.

```
$ curl -b cookies -X post -d @report_request "http://api.appnexus.com/report"
 
{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

Alternatively, you can get a `report_id` via a `POST` request using a `saved_report_id`.

```
$ curl -b cookies -X POST 'http://api.appnexus.com/report?saved_report_id=30'
```

### Step 3.`GET` the report status from the report service

Make a `GET` call with the `report_id` to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then, use the `report-download` service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'http://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:15:48",
         "json_request":"{\"report\":{\"report_type\":\"network_advertiser_frequency\",\"columns\":
          [\"hour\",\"line_item_id\",\"imps\",\"clicks\",\"total_convs\",
          \"ctr\",\"convs_rate\"],\"row_per\":[\"hour\",\"campaign_id\"],
          \"report_interval\":\"last_48_hours\",\"filters\":[{\"advertiser_id\":\"690\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### Step 4. `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the `"url"` field of the response to your previous `GET` call. When setting the file to which you want to save the report, use the file extension of the `"format"` (e.g., .csv) that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `\-i` or `\-v` in your call to expose the response header.

```
$ curl -b cookies 'http://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' -o /tmp/network_advertiser_frequency.csv
```
