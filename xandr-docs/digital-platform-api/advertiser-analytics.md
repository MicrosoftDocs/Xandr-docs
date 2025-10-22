---
title: Advertiser Analytics
description: Use the Advertiser Analytics report to view performance, revenue, and profit data across a specific advertiser's creatives and campaigns.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Advertiser analytics

The Advertiser Analytics report can be used to view performance, revenue, and profit data across a specific advertiser's creatives and campaigns. This report is available to network and advertiser users.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#examples) below. This report requires specifying the advertiser ID as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_2_days
- last_7_days
- last_30_days
- month_to_date
- month_to_yesterday
- quarter_to_date
- last_month
- lifetime

### Data retention period

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data. However, daily, monthly and cumulative intervals are still available.
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match statistics shown elsewhere in Microsoft Invest or Microsoft Monetize for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months are aggregated. The data from Billing reports are kept in non-aggregated form indefinitely. For more information, see [Dates and Times in Reporting](../invest/dates-and-times-in-reporting.md) in the UI documentation.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | No | `"2010-02-01"` | The day of the auction. |
| `month` | time | No | `"2010-02"` | The month of the auction. |
| `adjustment_id` | int | Yes | `890` | The unique identification number of the adjustment used to make changes to the media cost and/or impressions, clicks, and conversions you see in reporting for a publisher. |
| `advertiser_code` | string | No | `"Advertiser Code"` | The custom code for the advertiser. |
| `advertiser_currency` | string | Yes | `"USD"` | The type of money used by the advertiser. |
| `advertiser_id` | int | Yes | `3` | The unique identification number for each advertiser. |
| `buyer_member_id` | int | Yes | `210` | The unique identification number for the buyer member. |
| `seller_member_id` | int | Yes | `765` | The unique identification number of the selling member. |
| `seller_member_name` | string | No | `"AdMeld"` | The name of the selling member. |
| `seller_member` | string | No | `"AdMeld (765)"` | **Deprecated** (as of October 17, 2016). |
| `campaign_id` | int | Yes | `728` | The unique identification number of the campaign. |
| `campaign_name` | string | No | `"Test"` | The name of the campaign. |
| `campaign` | string | No | `"Test (123)"` | **Deprecated** (as of October 17, 2016). |
| `campaign_code` | string | No | `"Campaign Code"` | The custom code for the campaign. |
| `campaign_priority` | int | No | `4` | The bid priority of a campaign that is targeting direct inventory. The scale is from 1-10, with 1 being lowest and 10 being highest. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be null. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `creative_id` | int | Yes | `554` | The unique identification number of the creative.<br><br>**Note**:<br> - For impressions older than 14 months, creatives will be aggregated into one row with `0` as the `creative_id`.<br><br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The display name of the creative.<br>**Note**:<br> - For impressions older than 14 months, creatives will be aggregated into one row with `"All creative data older than 14 months"` as the `creative_name`.<br> - For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 - 728x90 (554)"` | **Deprecated** (as of October 17, 2016). |
| `placement_id` | int | Yes | `546` | The unique identification number of the placement.<br><br>**Note**:<br> - For impressions older than 14 months, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No | `"300x250 Business"` | The name of the placement.<br><br>**Note**: For impressions older than 14 months, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | No | `"FP 728x90 (567)"` | **Deprecated** (as of October 17, 2016). |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about deals you have negotiated with sellers, see [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated** (as of October 17, 2016). |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. For deals with external supply partners, this is generally the string that you use to identify the deal. |
| `placement_code` | string | No | `"FP 728x90"` | The custom code for the placement. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country or region. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country or region. |
| `creative_recency_bucket` | string | Yes | `"15-30 minutes"` | **Deprecated**. If you request this dimension, only a default value will be returned. Use the [Advertiser Creative Frequency & Recency report](./advertiser-creative-frequency-and-recency.md) to view creative recency data. |
| `creative_recency_bucket_id` | string | No | `3` | **Deprecated**. If you request this dimension, only a default value will be returned. Use the [Advertiser Creative Frequency & Recency report](./advertiser-creative-frequency-and-recency.md) to view creative recency data. |
| `creative_frequency_bucket` | string | Yes | `"11-20"` | **Deprecated**. If you request this dimension, only a default value will be returned. Use the [Advertiser Creative Frequency & Recency report](./advertiser-creative-frequency-and-recency.md) to view creative frequency data. |
| `creative_frequency_bucket_id` | string | No | `4` | **Deprecated**. If you request this dimension, only a default value will be returned. Use the [Advertiser Creative Frequency & Recency report](./advertiser-creative-frequency-and-recency.md) to view creative frequency data. |
| `gender` | string | Yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note**:<br>For impressions older than 100 days, the gender will be `"u"`.<br>The value of the gender is defined by the publisher in the bid request. Xandr does not have control over it apart from processing the value. |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1 ("Blank")`: No creative served.<br> - `2 ("PSA")`: A public service announcement served because there were no valid bids and no default creative was available.<br> - `3 ("Default Error")`: A default creative served due to a timeout issue.<br> - `4 ("Default")`: A default creative served because there were no valid bids.<br> - `5 ("Kept")`: Your advertiser's creative served on your publisher's site.<br> - `6 ("Resold")`: Your publisher's impression was sold to a third-party buyer.<br> - `7 ("RTB")`: Your advertiser's creative served on third-party inventory.<br> - `8 ("PSA Error")`: A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9 ("External Impression")`: An impression from an impression tracker.<br> - `10 ("External Click")`: A click from a click tracker. |
| `imp_type` | string | Yes | `"Kept"` | The type of impression. For possible values, see `imp_type_id`. |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for this impression.<br><br>**Note**: The term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `insertion_order_id` | int | Yes | `648359` | The unique identification number of the insertion order. |
| `insertion_order_name` | string | No | `"InsertionOrderABC"` | The name of the insertion order. |
| `insertion_order` | string | No | `"InsertionOrderABC648359"` | **Deprecated** (as of October 17, 2016). |
| `insertion_order_code` | string | No | `"Insertion Order Code"` | The custom code for the insertion order. |
| `line_item_id` | int | Yes | `947764` | The unique identification number of the line item. |
| `line_item_nam`e | string | No | `"LineItemDEF"` | The name of the line item. |
| `line_item` | string | No | `"LineItemDEF947764"` | **Deprecated** (as of October 17, 2016). |
| `line_item_code` | string | No | `"Line Item Code"` | The custom code for the line item. |
| `supply_type` | string | No | `"web"` | The type of inventory. Possible values: <br> - `"web"` <br> - `"mobile_web"` <br> - `"mobile_app"`. |
| `pixel_id` | int | Yes | `1942` | The unique identification number of the conversion pixel.<br><br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. |
| `publisher_id` | int | Yes | `374967` | The unique identification number of the publisher. |
| `publisher_name` | string | No | `"Publisher XYZ"` | The name of the publisher. |
| `publisher` | string | No | `"Publisher XYZ 347967"` | **Deprecated** (as of October 17, 2016). |
| `publisher_code` | string | No | `"Publisher Code"` | The custom code for the publisher. |
| `seller_type` | string | Yes | `"Real Time"`, `"Direct"` | The seller type. |
| `supply_type` | string | Yes | `"web"` | The type of inventory. Possible values: <br> - `"web"` <br> - `"mobile_web"` <br> - `"mobile_app"`. |
| `media_type` | string | No | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of the creative. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | Yes | `2` | The unique identification number of the media type to which the subtype belongs. |
| `user_group_for_campaign` | string | Yes | `"Test"` | The test/control user group for the campaign. See the `"labels"` field in the [Campaign Service](./campaign-service.md) for more details. |
| `venue` | int | Yes | `321512` | The name of the cluster of domain, site, tag, and user country/region that Xandr' optimization system uses to determine bid valuations. A campaign cannot target a venue explicitly. |
| `billing_period_start_date` | datetime | No | `"2015-05-25 19:19:53"` | The earliest date of the insertion order's billing period.<br><br>**Note: Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period_end_date` | datetime | No | `"2015-05-30 19:19:53"` | The last date of the insertion order's billing period.<br><br>**Note: Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period_external_code` | string | No | `"houseware245"` | The custom code for the billing period (`budget_interval`). |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions served. |
| `attributed_revenue` | money | `10.45` | post_view_revenue + post_click_revenue | The amount of revenue from all recorded post views and post clicks. |
| `attributed_pc_revenue` | money | `121.68` | post_click_revenue | The amount of revenue from all recorded post views. |
| `attributed_pv_revenue` | money | `14` | post_view_revenue | The amount of revenue from all recorded post clicks. |
| `clicks` | int | `545` | clicks | The total number of clicks across all impressions. |
| `click_convs_rate` | double | `0.057` | total_convs / clicks | The rate of conversions to clicks. |
| `click_conv_rate` | double | `0.000064` | total_convs / clicks | The rate of conversions to clicks.<br><br>**Note**: This field is identical to `click_convs_rate`. |
| `click_thru_pct` | double | `0.000%` | clicks / imps | The percentage of users viewing a creative that clicked on it. |
| `cpa` | money | `1.25` | booked_revenue_dollars / (post_view_convs + post_click_convs) | The cost per acquisition. |
| `cpc` | money | `0.45` | booked_revenue_dollars / clicks | The cost per click. |
| `cpm` | money | `0.18` | (booked_revenue_dollars / imps) * 1000 | The cost per 1,000 impressions. |
| `post_view_convs` | int | `75` | post_view_convs | The total number of recorded post view conversions. |
| `post_view_revenue` | money | `150.00` | post_view_revenue | The total amount of recorded post view revenue. |
| `post_click_convs` | int | `15` | post_click_convs | The total number of recorded post click conversions. |
| `post_click_revenue` | money | `300.00` | post_click_revenue | The total amount of recorded post click revenue. |
| `total_revenue` | money | `450.00` | post_view_revenue + post_click_revenue | The total amount of post view and post click revenue. |
| `total_convs` | int | `90` | post_view_convs + post_click_convs | The total number of post view and post click conversions. |
| `conv_rate` | double | `0.018654` | (post_click_convs + post_view_convs) / imps | The rate of post click and post view conversions to impressions. |
| `convs_rate` | double | `0.0003844` | total_convs / imps | The rate of conversions to impressions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `ecpa_adv_curr` | money | `1.13` | booked_revenue_adv_curr / (post_view_convs + post_click_convs) | The cost per acquisition in the advertiser currency type. |
| `ecpc_adv_curr` | money | `0.16` | booked_revenue_adv_curr / clicks | The cost per click in the advertiser currency type. |
| `ecpm_adv_curr` | money | `0.014` | booked_revenue_adv_curr / imps * 1000 | The cost per 1,000 impressions in the advertiser currency type. |
| `post_view_convs_rate` | double | `0.000320` | post_view_convs / imps | The rate of post view conversions to impressions. |
| `post_click_convs_rate` | double | `0.000064` | post_click_convs / imps | The rate of post click conversions to impressions. |
| `post_click_conversion_pixel` | int | `52` | post_click_convs for that pixel_id | The number of post click conversions for a specific pixel. For more information on how we attribute post-view (and other) conversions, [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_click_revenue_pixel` | money |`184.25` | post_click_revenue for that pixel_id | The amount of revenue earned for a specific pixel. |
| `post_view_conversion_pixel` | int | `174` | post_view_convs for that pixel_id | The number of post view conversions for a specific pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_view_revenue_pixel` | money | `303.54` | post_view_revenue for that pixel_id | The amount of revenue earned for a specific pixel. |
| `ppm` | money | `0.944966292134831` | (profit / imps) x 1000 | The profit per 1000 impressions. |
| `rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `spend_adv_curr` | money | `357.18` | booked_revenue_adv_curr | The total amount spent by the advertiser in the advertiser's preferred currency. |
| `total_revenue_pixel` | money | `41.253` | post_click_revenue + post_view_revenue for that pixel_id | The total revenue earned for a specific pixel. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions. |
| `spend` | money | `304.36` | spend | The total marketer spend across both direct and real time media buys. |
| `media_cost` | money | `2.15` | media cost | The total amount spent to purchase all impressions. |
| `ecpm` | money | `1.30` | (spend / imps) x 1000 | The effective advertiser spend per 1000 impressions. |
| `ecpc` | money | `1.25` | spend / clicks | The effective advertiser spend per click. |
| `ecpa` | money | `1.20` | spend / total_convs | The effective advertiser spend per conversion/acquisition. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `avg_bid_reduction` | double | `18%` | avg_bid_reduction | The average bid reduction you gained on the line item or campaign. This value represents the difference (as a percentage) between your bid and the actual media cost you paid for the impression you won (e.g., due to bid reduction). This value is only valid for RTB bidding (i.e., not Managed). Currently, this value is not accurately calculated for line items for which the `payment_auction_event_type` field has been set to `2`. |
| `video_skips` | int | `10` | video_skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` | video_starts | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` | video_25_pcts | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `10` | video_50_pcts | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` | video_75_pcts | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` | video_completions | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` | video_served | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2` | video_errors | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` | revenue_per_video_complete | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` | cost_per_video_complete | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` | video_start_rate | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` | video_skip_rate | The percentage of times the user opted to skip the video. |

## Examples

### Create a JSON-formatted report request

```
$ cat advertiser_analytics 
 
{ 
    "report": { 
        "report_type":"advertiser_analytics", 
        "columns": [ 
            "hour", 
            "seller_member_id", 
            "campaign_id", 
            "gender", 
            "imps", 
            "clicks", 
            "total_convs", 
            "ctr", 
            "convs_rate"
        ], 
        "report_interval": "last_48_hours", 
        "format":"csv" 
    } 
}
```

### `POST` the request to the reporting service

You `POST` the JSON request and get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @advertiser_analytics "https://api.appnexus.com/report?advertiser_id=690" 
 
{
    "response": {
        "status": "OK",
        "report_id": "2790c6627d058cd467f4267add49bedc",
        "existing": true,
        "dbg_info": {
            ...
        }
    }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the `report-download` service to save the reporting data to a file (described in the next step).

```
$ curl -b cookies -c cookies "https://api.appnexus.com/report?id=dc0314bda06597582518c5fc3e1c47ef" 
 
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-04-17 01:26:00",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "did not find any cache table for 1,3,6,44,30,31,32,34,15",
            "json_request": "{\"report\":{\"report_type\":\"advertiser_analytics\",\"columns\":[\"hour\",\"seller_member_id\",\"campaign_id\",\"gender\",\"imps\",\"clicks\",\"total_convs\",\"ctr\",\"convs_rate\"],\"report_interval\":\"last_48_hours\",\"format\":\"csv\",\"filters\":[{\"buyer_member_id\":\"948\"},{\"advertiser_id\":\"78216\"},{\"imp_type_id\":{\"operator\":\"!=\",\"value\":6}}]}}",
            "header_info": "Report ID:,2790c6627d058be467f4267add49bedc\r\nRun at:,2014-04-17 01:26:00\r\nStart date:,2014-04-15 01:00:00\r\nEnd date:,\r\nTimezone:,\r\nUser:,Jesse Seldess (9685)\r\n",
            "row_count": "0",
            "report_size": "75",
            "user_id": "9685",
            "entity_id": "0",
            "started_on": "2014-04-17 01:26:03",
            "finished_on": "2014-04-17 01:28:02",
            "query_time": "118",
            "url": "report-download?id=2790c6627d058be467f4267add49bedc"
        },
        "execution_status": "ready",
        "dbg_info": {
            ...
        }
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the url field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/advertiser_analytics.csv 
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
