---
title: Digital Platform API - Buyer Segment Performance Report
description: In this article, learn about the Buyer Segment Performance report, their time frame, data retention period, dimensions, and metrics with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Buyer Segment Performance report

This report provides buyers with segment performance across campaigns and multiple advertisers.

The `time_granularity` of the data is `hourly`. For instructions on retrieving a report, see the [Report Service](report-service.md) or the [examples](#examples).

> [!NOTE]
> **Impressions across user segments:** Since this report aggregates impressions served by user segment, impressions associated with users who are present in multiple segments will be counted more than once. As a result, be sure to group by `segment_id` when running the report.

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- today
- yesterday
- last_7_days
- last_14_days
- last_30_days

### Data retention period

Data retention period for this report is 45 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Examples | Description |
|:---|:---|:---|:---|:---|
| `month` | time | no | `"2010-02"` | The month of the auction. |
| `day` | date | yes | `"2010-02-01"` | The day of the auction. |
| `hour` | time | no | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `insertion_order_id` | int | yes | `321` | The ID of the insertion order. If the value is `0`, the impression was purchased by a third-party buyer. |
| `campaign_id` | int | yes | `222` | The ID of the campaign that purchased the impression. |
| `campaign_name` | string | no | `"Fall Wares"` | The name of the campaign that purchased the impression. |
| `campaign` | string | no | `"Fall Wares (222)"` | **Deprecated**. |
| `advertiser_id` | int | yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by third-party buyer, or a default or PSA was shown. |
| `line_item_id` | int | yes | `111` | The ID of the line item. If the value is `0`, the impression was purchased by a third-party buyer. |
| `advertiser_name` | string | no | `"Amco"` | The name of the advertiser. |
| `advertiser` | string | no | `"Amco (789)"` | **Deprecated**. |
| `line_item_name` | string | no | `"Kitchen"` | The name of the line item. |
| `line_item` | string | no | `"Kitchen (111)"` | **Deprecated**. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `campaign_code` | string | no | `"Mobile Campaign Code"` | The custom code for the campaign. |
| `segment_id` | int | yes | `220` | The ID of the segment pixel. |
| `segment_name` | string | no | `"Submitted application"` | The name of the segment. |
| `segment` | string | no | `"Submitted application (220)"` | **Deprecated**. |
| `insertion_order_name` | string | no | `"Mobile Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | no | `"Mobile Insertion Order (321)"` | **Deprecated**. |
| `segment_code` | string | no | `"Mobile Insertion Order Code"` | The (optional) custom code associated with the user segment present for this impression. |
| `pixel_id` | int | yes | `1942` | The unique identification number of the conversion pixel.<br><br>**Note:** This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. Although `pixel_id` is groupable, we do not recommend that you group by this dimension since doing so will cause conversion events to then be shown in separate rows from impression and click events. We generally assume you want to view all of these events in a single row so as to be able to retrieve accurate and aggregated values for conversion rate and cost-per-conversion calculations. As a result, we instead recommend that you filter by `pixel_id` so you can retrieve conversion counts and related metrics for your most relevant pixel IDs. |
| `gender` | string | yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note:** For impressions older than 100 days, the gender will be `"u"`. |
| `age_bucket` | string | yes | `"18-24`, `"45-54"` | The age bucket in which the user is contained. For more information, see [Age Bucket](#age-bucket) below. |
| `age_bucket_id` | int | yes | `1`, `3`, `0` | The ID of the age bucket. For more information, see [Age Bucket](#age-bucket) below. |

### Age bucket

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

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `34534` | imps | The total number of impressions (including defaults). |
| `clicks` | int | `345` | clicks | The total number of clicks across all impressions. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions. |
| `booked_revenue` | money | `450.00` | post_view_revenue + post_click_revenue | The total revenue booked through direct advertisers. |
| `booked_revenue_buying_currency` | money | `145.00` | (post_view_revenue + post_click_revenue) in buying currency | The total revenue booked through direct advertisers expressed in buying currency. |
| `post_view_convs` | int | `15` | post_view_convs | The number of post-view conversions. |
| `post_view_revenue` | money | `150.00` | post_view_revenue | Advertiser revenue from post-view conversions. |
| `post_click_convs` | int | `10` | post_click_convs | The number of post-click conversions that occurred. |
| `post_click_revenue` | money | `300.00` | post_click_revenue | Advertiser revenue from post-click conversions. |
| `post_view_convs_rate` | double | `0.00013` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_click_convs_rate` | double | `0.0002` | post_click_convs / imps | The rate of post-click conversions to impressions. |
| `spend` | money | `304.36` | spend | The total marketer spend across both direct and real time media buys for this segment. |
| `media_cost` | money | `100.00` | media_cost | The total cost of the inventory purchased. |
| `cpm` | money | `5.00` | media_cost / imps * 1000 | The cost per thousand impressions. |
| `revenue_ecpm` | money | `1.9221` | (booked_revenue / impressions) x 1000 | The total revenue per 1000 impressions. |
| `profit` | money | `4.14` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `profit_ecpm` | money | `0.4949` | (booked_revenue - total_cost)/imps * 1,000 | The profit (defined as booked revenue minus total cost) per 1,000 impressions. |
| `revenue_ecpc` | money | `0.8256` | booked_revenue / clicks | The total revenue per click. |
| `revenue_ecpa` | money | `5.00` | booked_revenue / total_convs | The total revenue per conversion. |
| `cost_ecpc` | money | `0.1834` | media_cost / clicks | The cost per click. |
| `cost_ecpa` | money | `1.1111` | media_cost / total_convs | The cost per acquisition/conversion. |
| `commissions` | money | `0` | Commissions for standard line items, $0 for ALIs. | Fees that come out of the booked revenue. |
| `serving_fees` | money | `0.025143` | Serving fees for standard line items, $0 for ALIs. | Fees that are added to the media cost. |
| `convs_per_mm` | double | `384.4` | (total_convs / imps) * 1,000,000 | The number of conversions per million impressions. |
| `partner_fees` | money | `123.45` | partner_fees | The total amount of third-party costs, budgeted using the [Partner Fee Service](partner-fee-service.md), that have accrued on an augmented line item over the reported period of time. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note:** We have added logic to prevent double counting third-party fees during the breaking change period (August 6-After the breaking change period). |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
| `video_skips` | int | `10` | video_skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` | video_starts | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` | video_25_pcts | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `10` | video_50_pcts | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` | video_75_pcts | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` | video_completions | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` | video_served | The total number of video responses served to the player.An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2` | video_errors | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` | revenue_per_video_complete | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` | cost_per_video_complete | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` | video_start_rate | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` | video_skip_rate | The percentage of times the user opted to skip the video. |

## Examples

### Create the JSON report request

The JSON file should include the `report_type` of `"buyer_segment_performance"`, as well as the columns (dimensions and metrics) and `{{report_interval}}` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_segment_performance

{"report": 
    {
        "format": "csv",
        "report_interval": "yesterday",
        "row_per": ["campaign_id"],
        "columns": ["campaign_id", "segment_id", "advertiser_id", "advertiser_name","line_item_id"],
        "report_type": "buyer_segment_performance"
    }
}
```

### `POST` the request to the Report Service

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X POST -d @buyer_segment_performance "https://api.appnexus.com/report"

{
   "response":{
      "status":"OK",
      "report_id":"71816ec6d09b32a5140730afe5cf6af5"
   }
}
```

### `GET` the report status from the Report Service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=71816ec6d09b32a5140730afe5cf6af5'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-11-19 21:15:10",
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"campaign_id\"],\"columns\":[\"campaign_id\",\"segment_id\",\"advertiser_id\",\"advertiser_name\",\"line_item_id\"],\"report_type\":\"buyer_segment_performance\",\"filters\":[{\"member_id\":\"1234\"}]}}",
            "url": "report-download?id=71816ec6d09b32a5140730afe5cf6af5"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the Report Download Service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=71816ec6d09b32a5140730afe5cf6af5' > /tmp/buyer_segment_performance.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topic

[Report Service](report-service.md)
