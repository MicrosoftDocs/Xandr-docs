---
title: Network Creative Frequency and Recency
description: Use the Network Creative Frequency and Recency report to view granular creative data for specific advertisers based on user views.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network creative frequency and recency

The **Network Creative Frequency & Recency** report can be used to view creative data for a specific advertiser based on the frequency and recency of user views. This report is more granular than the [Advertiser Creative Frequency and Recency](./advertiser-creative-frequency-and-recency.md) report and is available to network users only.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below. This report requires specifying the advertiser ID as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame

The `report_interval` field can be set to one of the following:

- last_hour
- today
- yesterday
- last_48_hours
- last_2_days
- last_7_days
- last_14_days
- month_to_date
- last_30_days
- last_month
- last_100_days
- custom

### Data retention period

Data retention period for this report is 120 days (no data before February 26, 2017).

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | no | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `day` | time | no | `"2010-02-01"` | The day of the auction. |
| `month` | time | no | `"2010-02"` | The month of the auction. |
| `creative_id` | int | yes | `554` | The ID of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | no | `"Q1 2010 728x90"` | The name of the creative.<br><br>**Note**: For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | no | `"Q1 2010 728x90 (554)"` | **Deprecated**. |
|  | string | yes | `"15-30 minutes"` | The bucket for how recently the creative was displayed. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_recency_bucket_id` | string | no | `"4"` | The ID of the creative recency bucket. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_frequency_bucket` | string | yes | `"11-20"` | The bucket for how frequently the creative was displayed. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `creative_frequency_bucket_id` | string | no | `"3"` | The ID of the creative frequency bucket. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `buyer_member_id` | int | yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br> `0` = Blank <br>`319` = Default |
| `advertiser_id` | int | yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a `default` or `PSA` was shown. |
| `advertiser_name` | string | no | `"Verizon Wireless"` | The name of the advertiser. |
| `advertiser` | string | no | `"Verizon Wireless (789)"` | **Deprecated**. |
| `advertiser_code` | string | no | `"Verizon Wireless Code"` | The custom code for the advertiser. |
| `insertion_order_id` | int | yes | `321` | The ID of the insertion order. |
| `insertion_order_name` | string | no | `"Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | no | `"Insertion Order (321)`" | **Deprecated**. |
| `insertion_order_code` | string | no | `"Insertion Order Code"` | The custom code for the insertion order. |
| `line_item_id` | int | yes | `111` | The ID of the line item. |
| `line_item_name` | string | no | `"Default Line Item"` | The name of the line item. |
| `line_item` | string | no | `"Default Line Item (111)"` | **Deprecated**. |
| `line_item_code` | string | no | `"Default Line Item Code"` | The custom code for the line item. |
| `campaign_id` | int | yes | `222` | The ID of the campaign. |
| `campaign_name` | string | no | `"Default Campaign"` | The name of the campaign. |
| `campaign` | string | no | `"Default Campaign (222)"` | **Deprecated**. |
| `campaign_code` | string | no | `"Default Campaign Code"` | The custom code for the campaign. |
| `campaign_priority` | int | no | `5` | The bidding priority for a campaign that targets direct inventory. For more information, see [Bidding Priority](../monetize/bidding-priority.md) in the UI documentation.<br>Possible values: `1` - `10`, where `10` is the highest priority. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `size` | string | yes | `"728x90"` | The size of the placement/creative served. |
| `is_remarketing` | int | yes | `0`, `1` | If `1`, the campaign is remarketing. If `0`, the campaign is not remarketing. |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for this impression. Note that the term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". For more information, see [What is a Venue?](../monetize/what-is-a-venue.md) and [Give Up Price](../monetize/give-up-price.md) in the UI documentation.<br>Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `media_type` | string | no | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of a creative. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | Yes | `1` | The ID of the general display style of a creative. |
| `trafficker_for_line_item` | string | yes | `"Maurice Truman"` | The trafficker for the line item. See the `"labels"` field in the [Line Item Service](./line-item-service.md) for more details. |
| `salesrep_for_line_item` | string | yes | `"Beverly Heller"` | The sales rep for the line item. See the `"labels"` field in the [Line Item Service](./line-item-service.md) for more details. |
| `user_group_for_campaign` | string | yes | `"Test"` | The test/control user group for the campaign. See the `"labels"` field in the [Campaign Service](./campaign-service.md) for more details. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `total_convs` | int | `9` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `click_convs_rate` | double | `0.1651376` | total_convs / clicks | The rate of conversions to clicks. |
| `click_conv_rate` | double | `0.000064` | total_convs / clicks | The rate of conversions to clicks.<br><br>**Note**: This field is identical to `click_convs_rate`. |
| `ctr` | double | `0.000221877080097626` | clicks / imps | The rate of clicks to impressions. |
| `click_thru_pct` | double | `1.12359550561797%` | (clicks / imps) * 100 | The rate of clicks to impressions as a percentage. |
| `post_click_convs` | int | `4` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_convs_rate` | double | `0.0002` | post_click_convs / imps | The rate of post-click conversion to impressions. |
| `post_click_revenue` | money | `150.00` | post_click_revenue | The total amount of recorded post-click conversion revenue. |
| `post_view_convs` | int | `5` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_convs_rate` | double | `0.00013` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_view_revenue` | money | `300.00` | post_view_revenue | The total amount of recorded post-view conversion revenue. |
| `media_cost` | money | `100` | media_cost | The total amount spent. |
| `cost_ecpm` | money | `0.4271259` | (media_cost / imps) * 1,000 | The cost per 1,000 impressions. |
| `cost_ecpc` | money | `0.1834` | media_cost / clicks | The cost per click. |
| `cost_ecpa` | money | `0.1834` | media_cost / total_convs | The cost per attribution/conversion. |
| `booked_revenue` | money | `25.767257` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `profit_ecpm` | money | `0.7778` | profit/imps * 1,000 | Profit (defined as booked revenue minus total cost) per 1,000 imps. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + `publisher_revenue` | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period . |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit` | money | `123.45` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
| `video_skips` | int | `10` |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` |  | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` |  | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `10` |  | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` |  | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` |  | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2` |  | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` |  | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` |  | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` |  | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` |  | The percentage of times the user opted to skip the video. |

### Creative frequency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-date"` |
| `-1` | `"no-cookie"` |
| `0` | `"0"` |
| `1` | `"1"` |
| `2` | `"2-5"` |
| `3` | `"6-10"` |
| `4` | `"11-20"` |
| `5` | `"21-40"` |
| `6` | `"41-60` |
| `7` | `"61-100"` |
| `8` | `"101-150"` |
| `9` | `"151-250"` |
| `10` | `"251-500"` |
| `11` | `"500+"` |

### Creative recency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-date"` |
| `-1` | `"no-cookie"` |
| `0` | `"< 1 minute"` |
| `1` | `"1-5 minutes"` |
| `2` | `"5-15 minutes"` |
| `3` | `"15-30 minutes"` |
| `4` | `"30-60 minutes"` |
| `5` | `"1-4 hours"` |
| `6` | `"4-12 hours"` |
| `7` | `"12-24 hours"` |
| `8` | `"1-2 days"` |
| `9` | `"2-7 days"` |
| `10` | `"8-14 days"` |
| `11` | `"14-30 days"` |

## Example

### Create a JSON formatted report request

```
$ cat network_advertiser_frequency_recency

{
    "report":
    {
        "report_type": "network_advertiser_frequency_recency",
        "columns": [
            "creative_recency_bucket",
            "creative_frequency_bucket",
            "creative_id",
            "imps",
            "clicks",
            "total_convs",
            "booked_revenue",
            "media_cost",
            "profit_ecpm"
        ],
        "report_interval": "last_7_days",
        "emails": ["jsmith@xandr.com"],
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X post -d @network_frequency_recency 'https://api.appnexus.com/report?advertiser_id=384'

{
    "response": {
        "status": "OK",
        "report_id": "0f148df60ff2760d57014f607f46fce4"
    }
}
```

### Use the report ID to retrieve the report data

The standard response includes the report data and a Download URL that you can use to save the data to a file. If you want to get just the Download URL without the report data, pass `"without_data"` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=0f148df60ff2760d57014f607f46fce4'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2012-02-03 22:00:33",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "did not find any cache table for 2,4,44,30,31,66,32,34,9,17,16,36",
            "json_request": "{\"report\":{\"report_type\":\"network_advertiser_frequency_recency\",
             \"columns\":[\"creative_recency_bucket\",\"creative_frequency_bucket\",\"creative_id\",
             \"imps\",\"clicks\",\"total_convs\",\"booked_revenue\",\"media_cost\",\"profit_ecpm\"],
             \"report_interval\":\"last_7_days\",\"emails\":[\"js@email.com\"],\"filters\":
             [{\"buyer_member_id\":\"541\"},{\"advertiser_id\":\"3610\"}]}}",
            "header_info": "Report type:,network_advertiser_frequency_recency\r\n,\r\nRun at:,
             2012-02-03 22:00:33\r\nStart date:,2012-01-27 00:00:00\r\nEnd date:,2012-02-03 00:00:00
             \r\nTimezone:,\r\nUser:,John Smith (9685)\r\n",
            "data": "creative_recency_bucket,creative_frequency_bucket,creative_id,imps,clicks,
             total_convs,booked_revenue,media_cost,profit_ecpm\r\n7-14 days,6-10,753570,1,0,0,.000000,
             .000000,.000000000000000000000000\r\n15-30 minutes,151-250,753571,3,0,0,.000000,.000000,
             .000000000000000000000000\r\n1-2 days,11-20,1316901,12,0,0,.000000,.004200,-.350000000000
             000000000000\r\n1-2 days,11-20,1316886,6,0,0,.000000,.001900,-.316666666666666666667000\r
             \n7-14 days,21-40,773408,3,0,0,.000000,.000160,-.053333333333333333333000\r\n30-60 minutes,
             500+,700464,35,0,0,.000000,.000000,.000000000000000000000000\r\n30-60 minutes,2-5,1317391,
             ...
            "url": "report-download?id=0f1374f60ff2760d57014f607f46fce4"
        },
        "execution_status": "ready"
    }
}
```

### Use the Download URL to save the report data to a file

You use the `"url"` field in the response to save the report data to a file. Simply make another `GET` call and identify the location and file that you want to save to. Be sure to use the file the extension of the `"format"` that you specified in your initial `POST` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=0f1374f60ff2760d57014f607f46fce4' > /tmp/network_frequency.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
