---
title: Network Video Analytics
description: Use the Network Video Analytics report to view video event metrics for network members and granular analytics for specific advertisers/publishers.
ms.date: 08/01/2023
ms.custom: digital-platform-api
---

# Network video analytics

The **Network Video Analytics** report can be used to view video event metrics for a network member. To drill down into more granular analytics for a specific advertiser or publisher, see the [Network Video Advertiser Analytics](./network-advertiser-video-analytics.md) and [Network Video Publisher Analytics](./network-publisher-video-analytics.md) reports.

> [!NOTE]
>
> - Video metrics are recorded for VAST creatives only.
> - For instructions on retrieving a report, see [Report Service](./report-service.md) or the [examples](#examples) below.

## Time frame

The `report_interval` field can be set to one of the following:

- today
- yesterday
- last_hour
- last_24_hours
- last_48_hours
- month_to_date
- month_to_yesterday
- last_2_days
- last_7_days
- last_14_days
- last_30_days
- last_7_available_days
- last_14_available_days
- last_30_available_days
- last_365_days

### Data retention period

Data in this report is retained for 420 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `month` | time | No | `"2010-02"` | The month of the auction. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member. |
| `buyer_member` | string | No | `"My Network (123)"` | **Deprecated** (as of October 17, 2016). |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `creative_id` | int | Yes | `554` | The ID of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The name of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 728x90 (554)"` | **Deprecated** (as of October 17, 2016). |
| `member_id` | int | Yes | `767` | The ID of the member. |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |
| `seller_member` | string | No | `"That Seller (456)"` | **Deprecated** (as of October 17, 2016). |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `advertiser_name` | string | No | `"Verizon Wireless"` | The name of the advertiser. |
| `advertiser` | string | No | `"Verizon Wireless (789)"` | **Deprecated** (as of October 17, 2016). |
| `advertiser_currency` | string | Yes | `"USD"` | The currency of the advertiser. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher. |
| `publisher_name` | string | No | `"Test"` | The name of the publisher. |
| `publisher` | string | No | `"Test (123)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_currency` | string | Yes | `"USD"` | The currency of the publisher. |
| `site_id` | int | Yes | `194` | The ID of the site.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site Name"` | The name of the site. |
| `site` | string | No | `"Site Name (194)"` | **Deprecated** (as of October 17, 2016). |
| `placement_id` | int | Yes | `456` | The ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No | `"Ivillage 160x600"` | The name of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement_code` | string | No | `"Ivillage Code"` | The custom code for the placement. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | No | `"Insertion Order (321)"` | **Deprecated** (as of October 17, 2016). |
| `line_item_id` | int | Yes | `111` | The ID of the line item. |
| `line_item_name` | string | No | `"Default Line Item"` | The name of the line item. |
| `line_item` | string | No | `"Default Line Item (111)"` | **Deprecated** (as of October 17, 2016). |
| `line_item_code` | string | No | `"Default Line Item Code"` | The custom code for the line item. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign. |
| `campaign` | string | No | `"Default Campaign (222)"` | **Deprecated** (as of October 17, 2016). |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `brand_id` | int | Tes | `3` | The ID of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | No | `"Ace Hardware"` | The name of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand` | string | No | `"Ace Hardware (3)"` | **Deprecated** (as of October 17, 2016). |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country/region. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country/region. |
| `deal_code` | string | No | `External seller deal code` | The custom code for the deal. For deals with external supply partners, this string typically identifies the deal. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated** (as of October 17, 2016). |
| `trafficker_for_insertion_order` | string | Yes | `"Maurice Truman"` | The trafficker for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `salesrep_for_insertion_order` | string | Yes | `"Beverly Heller"` | The sales rep for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `creative_recency_bucket_id` | string | no | `"4"` | The ID of the creative recency bucket. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_recency_bucket` | string | yes | `"15-30 minutes"` | The bucket for how recently the creative was displayed. See [Creative Recency Buckets](#creative-recency-buckets) below for possible values. |
| `creative_frequency_bucket` | string | yes | `"11-20"` | The bucket for how frequently the creative was displayed. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `creative_frequency_bucket_id` | string | no | `"3"` | The ID of the creative frequency bucket. See [Creative Frequency Buckets](#creative-frequency-buckets) below for possible values. |
| `site_domain` | string | no | `bestsiteever.com` | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store.<br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `mobile_application_id` | int | Yes | `343200656` | A targetable Apple App Store ID, Android application ID, or Windows application ID. |
| `supply_type` | string | Yes | `"mobile_web"` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app"` <br> - `"mobile_web"` |
| `video_playback_method` | string | Yes | `"1"` | The playback method for the creative. See [Video Playback Method](#video-playback-method) below for possible values. |
| `video_context` | string | Yes | `"3"` | The type of the video creative. See [Video Context](#video-context) below for possible values. |
| `video_player_size_id` | string | Yes | `"2"` | The ID of the video player width. See [Player Size](#player-size) below for possible values. |
| `imp_type_id` | int | Yes | `3` | The ID of the associated impression type. Possible values: An integer value which translates as follows:<br>`0` = Video Event Error<br>`1` = Blank: "200 OK" response (blank) served.<br>`2` = PSA : A public service announcement served because no other creative was eligible.<br>`3` = Default Error: A default creative served due to timeout issue.<br>`4` = Default: A default creative served because no campaigns bid or no other creative was eligible.<br>`5` = Kept: One of your managed advertisers served a creative.<br>`6` = Resold: The impression was sold to a third-party buyer.<br>`7` = RTB: Your creative served on third-party inventory.<br>`8` = PSA Error: A public service announcement served due to timeout issue.<br>`9` = External Impression: An impression from an impression tracker.<br>`10` = External Click: A click from a click tracker. |
| `bidder_id` | int | Yes | `45` | The ID of the associated bidder. |
| `creative_duration` | int | Yes | `30` | The duration of the video creative in seconds. |
| `video_delivery_type` | string | No | `"vod"` | The type of streaming content delivery. For example, `Video On Demand (VOD)` and `Live`. |
| `video_content_genre` | string | No | `"action"` | The main genre of the program in which the ad will be played. For example, `Action`, `Adventure`, `Biography`, `Business`, `Comedy`, etc. |
| `video_program_type` | string | No | `"series"` | The higher level categorization of the video program's format on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip`, etc. |
| `video_content_rating` | string | No | `"teens"` | The publisher-identified audience group for which the content is rated. For example, `All`, `Children (7+)` , `Teens (13+)`, `Young Adults (14+)`, or `Adults (18+)`. |
| `content_duration_secs` | int | Yes | `480` | The length of the video content in seconds. |
| `device_type` | string | Yes | - `Desktops & Laptops`<br> - `Mobile Phones`<br> - `Tablets`<br> - `TV`<br> - `Game Consoles`<br> - `Media Players`<br> - `Set Top Box`<br> - `Other Devices` | The type of device where the creative was set to play. |
| `video_content_duration` | int | Yes | `100` | The length of the video content in seconds. |
| `video_content_language` | string | No | `"Spanish"` | The language of the video program in which ad will be played. For example, `Spanish`. |
| `video_content_network` | string | No | `"AMC"` | The network delivering the video content. For example, `9 Story`, `CBC`, `Disney`, `AMC`, `Fox`, etc. |
| `code_1` | string | No | `"Code A"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| `code_2` | string | No | `"Code B"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| `code_3` | string | No | `"Code C"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| `is_takeover` | boolean | Yes | `"Yes"` | Indicates whether an impression was `Blanked` or `Defaulted` because at least one of the ads in the multi-ad request was a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|

> [!NOTE]
> The data for the following dimensions is only available if the publisher has implemented video taxonomy.
>
> - `video_delivery_type`
> - `video_content_genre`
> - `video_program_type`
> - `video_content_rating`
> - `video_content_duration`
> - `video_content_language`
> - `video_content_network`

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `ad_requests` | int | `1234` | ad_requests | The number of ad requests associated with the placement. |
| `ad_responses` | int | `2340` | ad_responses | The number of responses delivered to the user's browser (or mediating server). A response can result in an impression, an error in player, or an auction with no impression event.<br><br>**Note**: An imp refers to when the video player loads the video and starts the first frame. Videos Served refers to the VAST document being served in response to a request from the video player. |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `cost` | money | `16.833378` | cost | The total amount of media cost for direct publisher and purchased real-time inventory. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue. |
| `profit` | money | `0.084102` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `ctr` | double | `0.000221877080097626` | clicks / imps | The rate of clicks to impressions. |
| `rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `rpm_including_fees` | money | `2.60548314606741` | (revenue_including_fees / imps) x 1000 | **To be deprecated**. The revenue minus commissions per 1000 impressions. |
| `total_network_rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `ppm` | money | `0.944966292134831` | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| `ppm_including_fees` | money | `0.662460674157303` | (profit_including_fees / imps) x 1000 | **To be deprecated**. The profit including additional fees per 1000 impressions. |
| `cpm_including_fees` | money | `2.60548314606741` | (cost_including_fees / imps) x 1000 | **To be deprecated**. The cost including additional fees per 1000 impressions. |
| `errors` | int | `5` | errors | The total number of times an error occurred. |
| `starts` | int | `360` | starts | The total number of times the first segment of the video creative was downloaded and started. |
| `start_rate` | double | `25.85` | starts / imps | The number of video starts divided by the number of impressions. |
| `skips` | int | `20` | skips | The total number of times a user skipped the video. |
| `skip_rate` | double | `20.5` | skips / imps | The number of video skips divided by the number of impressions. |
| `25_pcts` | int | `780` | 25% complete | The total number of times the video creatives completed 25% of the entire duration. |
| `50_pcts` | int | `654` | 50% complete | The total number of times the video completed 50% of the entire duration of time. |
| `75_pcts` | int | `567` | 75% complete | The total number of times the video completed 75% of the entire duration of time. |
| `completions` | int | `989` | 100% complete | The total number of times the video played for the entire duration of time. |
| `completion_rate` | double | `85.45` | completions / imps | The number of video completions divided by the number of impressions. |
| `render_rate` | double | `60%` | render_rate | The percentage of videos delivered based on the number of ad responses delivered to the user's browser. (Impressions / Ad responses) |
| `revenue_per_video_complete` | double | `15.869` | revenue / completions | The revenue per video completion. |
| `cost_per_video_complete` | double | `2.056` | cost / completions | The cost per video completion. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 2 consecutive seconds. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `started_video_completion_rate` | double | `85.45` | completions / video_starts | The number of video completions divided by the number of video starts. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `network_profit` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost. |
| `network_profit_ecpm` | money | `123.45` | (network_profit/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | network_profit/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | network_profit/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45` | network_profit/(booked_revenue + reseller_revenue) | Network profit margin. |
| `profit_ecpm` | money | `123.45` | ((booked_revenue - total_cost)/imps) * 1,000 | Profit per 1,000 imps. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
| `Average View Time` | int | `28` | sum (creative_duration * ((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions)) / sum (starts)) | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| `Average View Time Percent` | percentage | `89%` | sum (((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions))∕starts) | The average view time expressed as a percentage of the total possible view time. |
| `fill_rate` | double |`85.00` |(imps_resold+imps_kept)/total_ad_requests |The percentage of total impressions (both resold and retained) out of the total number of ad requests sent to Xandr for auction. |
<!-- | `served` | int | `87649` | video impressions served | The total number of video impressions served.<br><br>**Note**: An `Imp` refers to when the video player loads the video and starts the first frame. **Videos Served** refers to the VAST document being served in response to a request from the video player. | -->

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
| `0` | Unknown |
| `1` | Auto-play, sound on |
| `2` | Auto-play, sound off |
| `3` | Click-to-play |
| `4` | Mouse-over |
| `5` | Auto-play, sound unknown |

### Video context

| Method ID | Method |
|:---|:---|
| `0` | Unknown |
| `1` | Pre-roll |
| `2` | Mid-roll |
| `3` | Post-roll |
| `4` | Outstream |

### Player size

| ID | Name |
|:---|:---|
| `0` | small |
| `1` | medium |
| `2` | large |

## Examples

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"video_analytics_network"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat video_analytics_network

{
    "report":
    {
        "report_type":"video_analytics_network",
        "columns":[
            "hour",
            "seller_member_id",
            "buyer_member_id",
            "advertiser_id",
            "publisher_id",
            "imps",
            "ad_requests",
            "ad_responses",
            "25_pcts",
            "completions",
            "completion_rate",
            "convs_rate"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @video_analytics_network 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the reporting data to a file (described in the next step).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"video_analytics_network\",\"columns\":[\"hour\",\"seller_member_id\",
   \"buyer_member_id\",\"advertiser_id\",\"publisher_id\",\"imps\",\"25_pcts\",\"completions\",\"completion_rate\",\"convs_rate\"],
            \"row_per\":[\"hour\",\"seller_member_id\",\"buyer_member_id\",\"advertiser_id\",\"publisher_id\"],
            \"report_interval\":\"last_48_hours\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_analytics_network.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
