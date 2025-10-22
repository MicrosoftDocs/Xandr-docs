---
title: Digital Platform API Internal Services - Buyer Untargeted Segment Performance Report
description: In this article, learn about the Buyer Untargeted Segment Performance report, their time frame, data retention period, dimensions, and metrics with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API Internal Services - Buyer Untargeted Segment Performance report

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.
>
> In addition, due to the cost of running this report, it is limited to strategic/large clients only. Contact Steve Truxal to request access for your client and provide details on the revenue opportunity, expected hourly biddable impressions for 1 day, and how you expect the member's seat to scale over the next 6-12 months.

The Buyer Untargeted Segment report can be used for discovery: to identify segments you have access to but may not be targeting. This report is available to members.

For instructions on retrieving a report, see the [examples](#examples) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- `today`
- `yesterday`
- `last_7_days`
- `last_30_days`
- `last_14_days`

## Dimensions

| Column | Type | Description |
|:---|:---|:---|
| `hour` | time | The hour of the auction.<br>**Example:** `"2010-02-01 06:00:00"`<br>**Group:** Yes<br>**Filter:** Yes |
| `day` | time | The day of the auction.<br>**Example:** `"2010-02-01"`<br>**Group:** Yes<br>**Filter:** Yes |
| `month` | time | The month of the auction.<br>**Example:** `"2010-02"`<br>**Group:** Yes<br>**Filter:** Yes |
| `buyer_member_id` | int | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: `229` = PSA, `0` = Blank, or `319` = Default.<br>**Example:** `123`<br>**Group:** Yes<br>**Filter:** Yes |
| `insertion_order_id` | int | The ID of the insertion order.<br>**Group:** Yes<br>**Filter:** Yes |
| `campaign_id` | int | The ID of the campaign.<br>**Example:** `123`<br>**Group:** Yes<br>**Filter:** Yes |
| `advertiser_id` | int | The ID of the advertiser. If the value is 0, either the impression was purchased by an external buyer, or a default or PSA was shown.<br>**Example:** `789`<br>**Group:** Yes<br>**Filter:** Yes |
| `line_item_id` | int | The ID of the line item.<br>**Example:** `111`<br>**Group:** Yes<br>**Filter:** Yes |
| `pixel_id` | int | The ID of the pixel.<br>**Example:** `123`<br>**Group:** Yes<br>**Filter:** Yes |
| `advertiser_name` | string | The name of the advertiser.<br>**Example:** `"Verizon Wireless"`<br>**Group:** No<br>**Filter:** No |
| `advertiser` | string | **Deprecated** (as of October 17, 2016). |
| `line_item_name` | string | The name of the line item.<br>**Example:** `"Default Line Item"`<br>**Group:** No<br>**Filter:** No |
| `line_item` | string | **Deprecated** (as of October 17, 2016). |
| `segment_id` | int | The ID of the segment pixel.<br>**Example:** `220`<br>**Group:** Yes<br>**Filter:** Yes |
| `segment_name` | string | The name of the segment.<br>**Example:** `"Submitted application"`<br>**Group:** No<br>**Filter:** No |
| `segment` | string | **Deprecated** (as of October 17, 2016). |
| `insertion_order_name` | string | The name of the insertion order.<br>**Example:** `"Mobile Insertion Order"`<br>**Group:** No<br>**Filter:** No |
| `insertion_order` | string | **Deprecated** (as of October 17, 2016). |
| `segment_code` | int | The (optional) custom code associated with the user segment present for this impression.<br>**Example:** `12456`<br>**Group:** No<br>**Filter:** No |
| `age_bucket` | string | The age bucket in which the user is contained. For more information, see [Age Bucket](#age-bucket) below.<br>**Group:** Yes<br>**Filter:** Yes |
| `age_bucket_id` | int | The ID of the age bucket.<br>**Group:** Yes<br>**Filter:** Yes |
| `gender` | string | The gender segment.<br>**Group:** Yes<br>**Filter:** Yes |
| `is_targeted` | int | Whether or not the line item targeted the segment.<br>**Group:** Yes<br>**Filter:** Yes |
| `segment_owner_member_id` | int | The ID of the segment owner.<br>**Group:** Yes<br>**Filter:** Yes |
| `segment_owner_member_name` | string | The name of the segment owner.<br>**Group:** No<br>**Filter:** Yes |
| `is_advertiser_segment` | int | Whether or not the segment is an advertiser segment for the buyer running the report.<br>**Group:** Yes<br>**Filter:** Yes |

### Age Bucket

| Bucket ID | Bucket Name |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"13-17"` |
| `2` | `"18-24"` |
| `3` | `"25-34"` |
| `4` | `"35-44"` |
| `5` | `"45-54"`|
| `6` | `"55-64"` |
| `7` | `"65+"` |

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
| `post_view_revenue` | money | Advertiser revenue from post-view conversions. | `150.00` | post_view_revenue |
| `post_click_convs` | int | The total number of recorded post-click conversions. | `4` | post_click_convs |
| `post_click_revenue` | money | Advertiser revenue from post-click conversions. | `300.00` | post_click_revenue |
| `post_view_convs_rate` | double | The rate of post-view conversions to impressions. | `0.0002` | post_view_convs / imps |
| `post_click_convs_rate` | double | The rate of post-click conversion to impressions. | `0.0002` | post_click_convs / imps |
| `media_cost` | money | The total amount spent. | `100.00`| media_cost |
| `profit` | money | The profit per thousand impressions. | `4.14` | profit |
| `profit_ecpm` | money | The profit as a percentage of the revenue. | `0.778` | ((booked_revenue - media_cost) / imps)* 100 |
| `revenue_ecpc` | money | The total revenue per click. | `0.8256` | booked_revenue / clicks |
| `revenue_ecpa` | money | The total revenue per conversion. | `5.00` | booked_revenue / total_convs |
| `cost_ecpc` | money | The cost per click. | `0.1834` | media_cost / clicks |
| `cost_ecpa` | money | The cost per attribution/conversion. | `0.1834` | media_cost / total_convs |
| `commissions` | money | The fees that come out of the booked revenue. | `0` | commissions |
| `serving_fees` | money | The fees that are added to the media cost. | `0/025143` | serving_fees |
| `convs_per_mm` | double | The number of conversions per million impressions. | `221.87708` | (total_convs / imps) x 1,000,000 |
| `rpm` | money | The revenue per thousand impressions. | `100.00` | (booked_revenue / imps) / 1000 |

## Examples

### Step 1: Create the JSON report request

The JSON file should include the following:

- `"report_type"` you want to run.
- `"columns"` (dimensions and metrics) you want to retrieve.
- `"report_interval"` you want to retrieve.

You can also include `filters` for dimensions, define granularity (`year`, `month`, `day`), and specify the `format` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`).

> [!NOTE]
> To filter a dimension by more than one value, use an array. For example:
>
> **Correct:**
>
> `"filters": [{"bid_type": ["learn","optimized"]}, {"geo_country":"US"}]`
>
> **Incorrect:**
>
> `"filters": [{"bid_type":"learn"}, {"bid_type":"optimized"}, {"geo_country":"US"}]`

For more details about the columns that can be included in the request, see [Dimensions](#dimensions) and [Metrics](#metrics) above.

The example below demonstrates how to retrieve the Buyer Untargeted Segment Performance Report. In this example, the report will display data for the `hour`, `campaign_id`, `imps`, `clicks`, `total_convs`, `ctr`, and `convs_rate` columns. This report will pull data from the last 48 hours and will format it as a CSV file.

```
$ cat report_request
{
        "report":{
                "report_type":"buyer_untargeted_segment_performance",
                "columns":[
                        "hour",
                        "campaign_id",
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

### Step 2: `POST` the request to the Report Service

`POST` the JSON request to get back a `report_ID`.

```
$ curl -b cookies -X post -d @report_request "https://api.appnexus.com/report"
 
{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

Alternatively, you can get a `report_id` via a `POST` request using a `saved_report_id`.

```
curl -b cookies -X POST 'https://api.appnexus.com/report?saved_report_id=30'
```

### Step 3: `GET` the report status from the Report Service

Make a `GET` call with the `report_id` to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then, use the `report-download` service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:15:48",
         "json_request":"{\"report\":{\"report_type\":\"network_advertiser_frequency\",\"columns\":
          [\"hour\",\"campaign\",\"imps\",\"clicks\",\"total_convs\",
          \"ctr\",\"convs_rate\"],\"row_per\":[\"hour\",\"campaign_id\"],
          \"report_interval\":\"last_48_hours\",\"filters\":[{\"advertiser_id\":\"690\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### Step 4: `GET` the report data from the Report Download Service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the `"url"` field of the response to your previous `GET` call. When setting the file to which you want to save the report, use the file extension of the `"format"` (e.g., .csv) that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `\-i` or `\-v` in your call to expose the response header.

```
curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' -o /tmp/network_advertiser_frequency.csv
```
