---
title: Network Advertiser Video Analytics
description: Use the Network Advertiser Video Analytics report to get detailed video event metrics for specific advertisers. It is only available to network users.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network advertiser video analytics

The **Network Advertiser Video Analytics** report can be used to view video event metrics for a specific advertiser that is more detailed than the data provided in the [Network Video Analytics](./network-video-analytics.md) report. This report is available to network users only.

> [!NOTE]
> Video metrics are recorded for VAST creatives only.

For usage instructions, see the [Example](#example) below. Note that this report requires that an advertiser ID be specified as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame

The `report_interval` field can be set to one of the following:

- today
- yesterday
- last_24_hours
- last_48_hours
- last_2_days
- last_7_days
- last_14_days
- last_30_days
- last_available_day
- last_7_available_days
- last_14_available_days
- last_30_available_days
- month_to_date
- month_to_yesterday
- last_month
- last_365_days


### Data retention period

Data in this report has the following retention period:

- Hourly retention: 100 days
- Daily retention: 500 days


> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | date | No | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | date | No | `2010-02-01` | Day of the month. |
| `month` | date | date | `2010-02` | Month of the year. |
| `seller_member_id` | int | Yes | `567` | The internal ID of the selling member. |
| `seller_member_name` | string | No | `"AdMeld"` | The display name of the selling member. |
| `seller_member` | string | No | `"AdMeld (567)"` | **Deprecated**. |
| `advertiser_id` | int | Yes | `344` | The internal ID of the advertiser whose campaign and creative served in the impression. |
| `campaign_id` | int | Yes | `728` | Number to identify the campaign. |
| `campaign_name` | string | No | `"Test"` | Display name of the campaign |
| `campaign` | string | No | `"Test (123)"` | **Deprecated**. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `creative_id` | int | Yes | `554` | The ID of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"`or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The name of the creative.<br><br>**Note**: For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 728x90 (554)"` | **Deprecated**. |
| `placement_id` | int | Yes | `567` | The ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No | `"Photos 728x90"` | The name of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | No | `"Photos 728x90 (123)"` | **Deprecated**. |
| `placement_code` | string | No | `"Placement Code"` | The custom code for the placement. |
| `deal_code` | string | No | `External seller deal code` | The custom code for the deal. For deals with external supply partners, this string typically identifies the deal. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `size` | string | Yes | `"728x90"` | Size of the creative/placement |
| `geo_country` | string | Yes | `"US"` | Geographic country/region code |
| `geo_country_name` | string | No | `"Unites States"` | Name of the country/region |
| `creative_recency_bucket` | string | Yes | `"11-20"` | The bucket for how recently the creative was displayed. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_recency_bucket_id` | string | No | `"4"` | The ID of the creative recency bucket. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_frequency_bucket` | string | Yes | `"15-30 minutes"` | The bucket for how frequently the creative was displayed. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `creative_frequency_bucket_id` | string | No | `"3"` | The ID of the creative frequency bucket. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `insertion_order_id` | int | Yes | `654` | The ID of the insertion order |
| `insertion_order_name` | string | No | `"Insertion Order Name"` | The name of the insertion order |
| `insertion_order` | string | No | `"Insertion Order Name (654)"` | **Deprecated**. |
| `line_item_id` | int | Yes | 932 | Number to identify the line item |
| `line_item_name` | string | No | `"$3 CPM Verizon Remarketing"` | Display name of the line item |
| `line_item` | string | No | `"$3 CPM Verizon Remarketing (932)"` | **Deprecated**. |
| `publisher_id` | int | Yes | `321` | Number to identify the publisher |
| `publisher_name` | string | No | `"Test"` | Display name of the publisher |
| `publisher` | string | No | `"Test (123)"` | **Deprecated**. |
| `trafficker_for_insertion_order` | string | Yes | `"Chris Mack"` | The trafficker for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `salesrep_for_insertion_order` | string | Yes | `"Jonathan Smith"` | The sales rep for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `site_domain` | string | no | `bestsiteever.com` | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store.<br><br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `application_id` | string | Yes | `'343200656' (iOS)` or <br>`com.rovio.angrybirds'(Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app"` <br> - `"mobile_web"`. |
| `video_playback_method` | string | Yes | `"1"` | The playback method for the creative. See [Video Playback Method](#video-playback-method) below for possible values. |
| `video_context` | string | Yes | `"3"` | The type of the video creative. See [Video Context](#video-context) below for possible values. |
| `video_player_size_id` | string | Yes | `"2"` | The ID of the video player width. See [Player Size](#player-size) below for possible values. |
| `video_content_genre` | string | No | `"action"` | The main genre of the program in which the ad will be played. For example, `Action`, `Adventure`, `Biography`, `Business`, `Comedy`, etc. |
| `video_program_type` | string | No | `"series"` | The higher level categorization of the video program's format on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip`, etc. |
| `video_content_rating` | string | No | `"teens"` | The publisher-identified audience group for which the content is rated. For example, `All`, `Children (7+)` , `Teens (13+)`, `Young Adults (14+)`, or `Adults (18+)`. |
| `content_duration_secs` | int | Yes | `480` | The length of the video content in seconds. |
| `device_type` | string | Yes | `Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles, Media Players, Set Top Box, and Other Devices.` | The type of device where the creative was set to play. |
| `video_content_duration` | int | Yes | `100` | The length of the video content in seconds. |
| `video_content_language` | string | No | `"Spanish"` | The language of the video program in which ad will be played. For example, `Spanish`. |
| `video_content_network` | string | No | `"AMC"` | The network delivering the video content. For example, `9 Story`, `CBC`, `Disney`, `AMC`, `Fox`, etc. |
| `video_delivery_type` | string | No | `"vod"` | The type of streaming content delivery. For example, `Video On Demand (VOD)` and `Live`. |
| `is_takeover` | boolean | Yes | `"Yes"` | Indicates whether an impression was `Blanked` or `Defaulted` because at least one of the ads in the multi-ad request was a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|

> [!NOTE]
> The data for the following dimensions is only available if the publisher has implemented video taxonomy.
>
> - `video_content_genre`
> - `video_program_type`
> - `video_content_rating`
> - `video_content_duration`
> - `video_content_language`
> - `video_content_network`
> - `video_delivery_typ`

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions served. |
| `clicks` | int | `545` | clicks | The the total number of clicks across all impressions. |
| `post_view_convs` | int | `75` | post_view_convs | The total number of recorded post-view conversions. |
| `post_click_convs` | int | `15` | post_click_convs | The total number of recorded post-click conversions. |
| `total_convs` | int | `90` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.0003844` | total_convs / imps | The rate of conversions to impressions. |
| `post_view_convs_rate` | double | `0.000320` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_click_convs_rate` | double | `0.000064` | post_click_convs / imps | The rate of post-click conversions to impressions. |
| `ctr` | double | `0.2327836` | clicks / imps | The rate of clicks to impressions. |
| `profit` | money | `350.00` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `revenue_ecpm` | money | `1.9221` | booked_revenue / clicks | The total revenue per 1000 impressions. |
| `cost_ecpm` | money |`0.4271259` | media_cost / imps * 1,000 | The cost per 1000 impressions. |
| `profit_ecpm` | money | `0.4949` | profit/imps * 1,000 | The profit per 1000 impressions. "Profit" is defined as booked revenue minus total cost. |
| `revenue_ecpc` | money | `0.8256` | booked_revenue / clicks | The total revenue per click. |
| `revenue_ecpa` | money | `5.00` | booked_revenue / total_convs | The total revenue per conversion. |
| `cost_ecpc` | money | `0.1834` | media_cost / clicks | The cost per click. |
| `cost_ecpa` | money | `1.1111` | media_cost / total_convs | The cost per acquisition/conversion. |
| `profit_margin` | money | `0.7778` | profit/booked_revenue | Profit divided by `booked_revenue`. "Profit" is defined as booked revenue minus total cost. |
| `media_cost` | money | `100.00` | media_cost | The total amount spent. |
| `errors` | int | `5` | errors | The total number of times an error occurred. |
| `starts` | int | `360` | starts | The total number of times the first segment of the video creative was downloaded and started. |
| `start_rate` | double | `25.85` | starts / imps | The number of video starts divided by the number of impressions. |
| `skips` | int | `20` | skips | The total number of times a user skipped the video. |
| `skip_rate` | double | `20.5` | skips / imps | The number of video skips divided by the number of impressions. |
| `25_pcts` | int | `780` | 25% complete | The total number of times the video creatives completed 25% of the entire duration. |
| `50_pcts` | int | `654` | 50% complete | The total number of times the video completed 50% of the entire duration of time. |
| `75_pcts` | int | `567` | 75% complete | The total number of times the video completed 75% of the entire duration of time. |
| `completions` | int | `989` | 100% complete | The total number of times the video played for the entire duration of time. |
| `completion_rate` | double | `85.4`5 | completions / imps | The number of video completions divided by the number of impressions. |
| `revenue_per_video_complete` | double | `15.869` | revenue / completions | The revenue per video completion. |
| `cost_per_video_complete` | double | `2.056` | cost / completions | The cost per video completion. |
| `served` | int | `87649` | video impressions served | The total number of video impressions served.<br><br>**Note**: An **Imp** refers to when the video player loads the video and starts the first frame. **Videos Served** refers to the VAST document being served in response to a request from the video player. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `Average View Time` | int | `28` | sum (creative_duration * ((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions)) / sum (starts)) | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| `Average View Time Percent` | percentage | `89%` | sum (((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions))∕ starts) | The average view time expressed as a percentage of the total possible view time. |

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
| `6` | `"41-60"` |
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

### Video playback method

| Method ID | Method |
|:---|:---|
| `0` | `Unknown` |
| `1` | `Auto-play, sound on` |
| `2` | `Auto-play, sound off` |
| `3` | `Click-to-play` |
| `4` | `Mouse-over` |
| `5` | `Auto-play, sound unknown` |

### Video context

| Method ID | Method |
|:---|:---|
| `0` | `Unknown` |
| `1` | `Pre-roll` |
| `2` | `Mid-roll` |
| `3` | `Post-roll` |
| `4` | `Outstream` |

### Player size

| ID | Name |
|:---|:---|
| `0` | `small` |
| `1` | `medium` |
| `2` | `large` |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"video_analytics_network_advertiser"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat video_analytics_network_advertiser

{"report":
    {
        "report_type":"video_analytics_network_advertiser",
        "columns":[
            "hour",
            "seller_member_id",
            "campaign_id",
            "imps",
            "starts",
            "75_pcts",
            "completions",
            "cost_per_video_complete",
            "served"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @video_analytics_network_advertiser "https://api.appnexus.com/report?advertiser_id=690"

{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the reporting data to a file (described in the next step).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:15:48",
         "json_request":"{\"report\":{\"report_type\":\"video_analytics_network_advertiser\",\"columns\":
          [\"hour\",\"seller_member_id\",\"campaign_id\",\"imps\",\"starts\",\"75_pcts\",
          \"completions\",\"cost_per_video_complete\",\"served\"],\"row_per\":
          [\"hour\",\"seller_member_id\",\"campaign_id\"],
          \"report_interval\":\"last_48_hours\",\"filters\":[{\"advertiser_id\":\"690\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_analytics_network_advertiser.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topic

[Report Service](./report-service.md)
