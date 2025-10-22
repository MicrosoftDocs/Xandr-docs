---
title: Advertiser Creative Frequency and Recency
description: Use the Advertiser Creative Frequency and Recency report to view creative data for a specific advertiser based on the frequency and recency of user views.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Advertiser creative frequency and recency

The Advertiser Creative Frequency & Recency report can be used to view creative data for a specific advertiser based on the frequency and recency of user views. This report is available to advertiser and network users.

For instructions on retrieving a report, please see [Report Service](./report-service.md) or see the [example](#example) below. For an advertiser user, the advertiser ID is detected based on the user's authentication. For a network user, however, this report requires specifying the advertiser ID as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

> [!NOTE]
> **Lookback window**
>
> Frequency and recency data is available for 120 days (no data before February 26, 2017).

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

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

Data retention period for this report is 120 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the auction. |
| `day` | time | No | `"2010-02-01"` | The day of the auction. |
| `month` | time | No | `"2010-02"` | The month of the auction. |
| `creative_id` | int | yes | `554` | The ID of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | no | `"Q1 2010 728x90"` | The name of the creative.<br><br>**Note**: For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | no | `"Q1 2010 728x90 (554)"` | **Deprecated** (as of October 17, 2016). |
| `creative_recency_bucket` | string | yes | `"15-30 minutes"` | The bucket for how recently the creative was displayed. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_recency_bucket_id` | string | no | `"4"` | The ID of the creative recency bucket. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_frequency_bucket` | string | yes | `"11-20"` | The bucket for how frequently the creative was displayed. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `creative_frequency_bucket_id` | string | no | `"3"` | The ID of the creative frequency bucket. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
|`buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br> `319` = Default. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| a`dvertiser_name` | string | No | `"Verizon Wireless"` | The name of the advertiser. |
| `advertiser` | string | No | `"Verizon Wireless (789)"` | **Deprecated** (as of October 17, 2016). |
| `advertiser_code` | string | No | `"Virizon Wireless Code"` | The custom code for the advertiser. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | No | `"Insertion Order (321)"` | **Deprecated** (as of October 17, 2016). |
| `insertion_order_code` | string | No | `"Insertion Order Code"` | The custom code for the insertion order. |
| `line_item_id` | int | Yes | `111` | The ID of the line item. |
| `line_item_name` | string | No | `"Default Line Item"` | The name of the line item. |
| `line_item` | string | No | `"Default Line Item (111)"` | **Deprecated** (as of October 17, 2016). |
| `line_item_code` | string | No | `"Default Line Item Code"` | The custom code for the line item. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign. |
| `campaign` | string | No | `"Default Campaign (222)"` | **Deprecated** (as of October 17, 2016). |
| `campaign_code` | string | No | `"Default Campaign Code"` | The custom code for the campaign. |
| `campaign_priority` | int | No | `5` | The bidding priority for a campaign that targets direct inventory.<br>Possible values: `1` - `10`, where `10` is the highest priority. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `is_remarketing` | int | yes | `0`, `1` | Whether or not the campaign is remarketing |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for this impression.<br><br>**Note**: The term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". <br>Allowed values are:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `media_type` | string | No | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of a creative. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | Yes | `1` | The ID of the general display style of a creative. |
| `user_group_for_campaign` | string | Yes | `"Test"` | The test/control user group for the campaign. See the `"labels"` field in the [Campaign Service](./campaign-service.md) for more details. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `total_convs` | int | `9` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `click_convs_rate` | double | `0.1651376` | total_convs / clicks | The rate of conversions to clicks. |
| `click_conv_rate` | double | `0.000064` | total_convs / clicks | The rate of conversions to clicks.<br><br>**Note**: This field is identical to `click_convs_rate`. |
| `ctr` | double |`0.000221877080097626` | clicks / imps | The rate of clicks to impressions. |
| `click_thru_pct` | double | `1.12359550561797%` | (clicks / imps) x 100 | The rate of clicks to impressions as a percentage. |
| `post_click_convs` | int | `4` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_convs_rate` | double | `0.0002` | post_click_convs / imps | The rate of post-click conversion to impressions. |
| `post_click_revenue` | money | `150.00` | post_click_revenue | The total amount of recorded post-click conversion revenue. |
| `post_view_convs` | int | `5` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_convs_rate` | double | `0.00013` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_view_revenue` | money | `300.00` | post_view_revenue | The total amount of recorded post-view conversion revenue. |
| `media_cost` | money | `100` | media_cost | The total amount spent |

### Creative frequency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-data"` (cookie lookup failed) |
| `-1` | `"no-cookie"` (user does not have cookies enabled) |
|`0` | `"0"` |
| `1` | `"1"` |
| `2` | `"2-5"` |
| `3` | `"6-10"` |
| `4` | `"11-20"` |
| `5` | `"21-40"` |
| `6` | `"41-60"` |
| `7` | `"61-100"` |
| `8` | `"101-150"` |
| `9` | `"151-250"` |
| `10` | `"251-500"` |
| `11` | `"500+"` |

### Creative recency buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `-2` | `"no-cookie-data"` (cookie lookup failed) |
| `-1` | `"no-cookie"` (user does not have cookies enabled) |
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

### Create a JSON-formatted report request

```
$ cat network_advertiser_frequency_recency {
    "report":
    {
        "report_type": "network_advertiser_frequency_recency",
        "columns": [
            "creative_recency_bucket",
            "creative_frequency_bucket",
            "creative_id",
            "imps",
            "clicks",
            "total_convs"
        ],
        "report_interval": "last_7_days",
        "emails": ["js@email.com"],
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @network_advertiser_frequency_recency "https://api.appnexus.com/report?advertiser_id=384"

{
    "response": {
        "status": "OK",
        "report_id": "c458f71c084a2a3b51dcd749132bcf87",
        "dbg_info": {
            ...
        }
    }
}
```

### Use the report ID to retrieve the report data

The standard response includes the report data and a Download URL that you can us to save the data to a file. If you want to get just the Download URL without the report data, pass `"without_data"` in the query string.

```
$ curl -b cookies -c cookies "https://api.appnexus.com/report?id=c458f71c084a2a3b51dcd749132bcf87"

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2012-02-03 21:43:27",
            "cache_hit": true,
            "fact_cache_hit": false,
            "fact_cache_error": null,
            "json_request": "{\"report\":{\"report_type\":\"network_advertiser_frequency_recency\",
             \"columns\":[\"creative_recency_bucket\",\"creative_frequency_bucket\",\"creative_id\",
             \"imps\",\"clicks\",\"total_convs\"],\"report_interval\":\"last_7_days\",\"emails\":
             [\"js@email.com\"],\"filters\":[{\"buyer_member_id\":\"541\"},{\"advertiser_id\":
             \"3610\"}]}}",
            "header_info": null,
            "data": "creative_recency_bucket,creative_frequency_bucket,creative_id,imps,clicks,
             total_convs\r\nno-cookie,no-cookie,700454,47,0,0\r\n2-7 days,2-5,773422,31,0,
             0\r\n5-15 minutes,6-10,1298720,1,0,0\r\n14-30 days,151-250,700464,8,0,0\r\n7-14 days,
             21-40,711929,5,0,0\r\n1-4 hours,6-10,1317518,826,2,0\r\n1-4 hours,1,1317473,996,14,
             0\r\n12-24 hours,11-20,1317436,139,0,0\r\n15-30 minutes,6-10,773408,12,0,0\r\nno-cookie,
             no-cookie,1318994,3,0,0\r\n1-5 minutes,101-150,711932,898,0,0\r\n2-7 days,2-5,773408,45,
             0,0\r\n1-5 minutes,2-5,610381,7990,23,0\r\n12-24 hours,1,1316895,4790,30,0\r\n1-4 hours,
             ...
             "url": "report-download?id=c447d71c084a2a3b51dcd749132bcf87"
        },
        "execution_status": "ready",
        "dbg_info": {
            ...
        }
    }
}
```

### Use the download URL to save the report data to a file

You use the `"url"` field in the response to save the report data to a file. Simply make another `GET` call and identify the location and file that you want to save to. Be sure to use the file the extension of the `"format"` that you specified in your initial `POST` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c447d71c084a2a3b51dcd749132bcf87' > /tmp/network_advertiser_frequency_recency.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
