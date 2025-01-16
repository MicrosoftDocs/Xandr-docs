---
title: Network Publisher Video Analytics
description: Use the Network Publisher Video Analytics report to view granular video event metrics for specific publishers within a network, available to network users only.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network publisher video analytics

The **Network Publisher Video Analytics** report can be used to view video event metrics for specific publisher within your network that is more granular than the data provided in the [Network Video Analytics](network-video-analytics.md) report. This report is available to network users only.

> [!NOTE]
> `video_content_genre` video metrics are recorded for VAST creatives only.

For usage instructions, see the [Example](#example) below. Note that this report requires that a publisher ID be specified as part of the URL, for example:

```
https://api.appnexus.com/report?publisher_id=PUBLISHER_ID
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
- month_to_date
- month_to_yesterday
- last_available_day
- last_7_available_days
- last_14_available_days
- last_30_available_days
- last_month

### Data retention period

Data in this report is retained for 420 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | date | no | `"2010-02-01 06:00:00"` | The hour of the auction<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | date | no | `"2010-02-01"` | The day of the auction. |
| `month` | date | no | `"2010-02"` | The month of the auction. |
| `member_id` | int | Yes | `767` | The ID of the member. |
| `buyer_member_id` | int | yes | `567` | The ID of the buying member. |
| `buyer_member_name` | string | no | `"Network"` | The name of the buying member. |
| `advertiser_id` | int | yes | `728` | The ID of the advertiser. |
| `advertiser_name` | string | no | `"Test"` | The name of the advertiser. |
| `brand_id` | int | yes | `3` | The ID of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | no | `"Ace Hardware"` | The name of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `publisher_id` | int | yes | `6787` | The number to identify the publisher. |
| `publisher_currency` | string | yes | `"USD"` | The currency of the publisher. |
| `site_id` | int | yes | `194` | The ID of the site.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0`. |
| `site_name` | string | no | `"Site Name"` | The name of the site. |
| `deal_code` | string | No | `External seller deal code` | The custom code for the deal. For deals with external supply partners, this string typically identifies the deal. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `geo_country` | string | yes | `"US"` | The geographic country/region code. |
| `geo_country_name` | string | no | `"United States"` | The name of the country/region. |
| `placement_id` | int | yes | `546` | The ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | no | `"300x250 Business"` | The name of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement_code` | string | no | `"300x250 Business Code"` | The custom code for the placement. |
| `site_domain` | string | no | `bestsiteever.com` | The site domain of an impression. |
| `application_id` | string | Yes | `'343200656' (iOS)` or <br> `'com.rovio.angrybirds'(Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app"` <br> - `"mobile_web"` |
| `video_playback_method` | string | Yes | `"1"` | The playback method for the creative. See [Video Playback Method](#video-playback-method) below for possible values. |
| `video_context` | string | Yes | `"3"` | When and where the video creative plays. See [Video Context](#video-context) below for possible values. |
| `video_player_size_id` | string | Yes | `"2"` | The ID of the video player width. See [Player Size](#player-size) below for possible values. |
| `video_delivery_type1` | string | No | `"vod"` | The type of streaming content delivery. For example, `Video On Demand (VOD)` and `Live`. |
| `video_content_genre1` | string | No | `"action"` | The main genre of the program in which the ad will be played. For example, `Action`, `Adventure`, `Biography`, `Business`, `Comedy`, etc. |
| `video_program_type1` | string | No | `"series"` | The higher level categorization of the video program's format on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip`, etc. |
| `video_content_rating1` | string | No | `"teens"` | The publisher-identified audience group for which the content is rated. For example, `All`, `Children (7+)` , `Teens (13+)`, `Young Adults (14+)`, or `Adults (18+)`. |
| `content_duration_secs` | int | Yes | `480` | The length of the video content in seconds. |
| `device_type` | string | Yes | `Desktops & Laptops, Mobile Phones, Tablets, TV, Game Consoles, Media Players, Set Top Box, and Other Devices`. | The type of device where the creative was set to play. |
| `video_content_duration1` | int | Yes | `100` | The length of the video content in seconds. |
| `video_content_language1` | string | No | `"Spanish"` | The language of the video program in which ad will be played. For example, `Spanish`. |
| `video_content_network1` | string | No | `"AMC"` | The network delivering the video content. For example, `9 Story`, `CBC`, `Disney`, `AMC`, `Fox`, etc. |

> [!NOTE]
> The data for the following dimensions is only available if the publisher has implemented video taxonomy.
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
| `imps` | int | `2340` | imps | The total number of impressions. |
| `clicks` | int | `545` | clicks | The total number of clicks across all impressions. |
| `total_convs` | int | `90` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `ctr` | double |`0.2327836` | clicks / imps * 100 | The rate of clicks to impressions. |
| `convs_rate` | double | `0.0384413` | total_convs / imps * 100 | The rate of conversions to impressions. |
| `network_revenue` | money | `1201.13` | network_revenue | Network revenue booked through direct advertisers and resold to real time buyers |
| `total_network_rpm` | money | `2.60548314606741` | (network_revenue / imps) x 1000 | The network revenue per 1000 impressions. |
| `publisher_revenue` | money | `400.05` | publisher_revenue | The revenue paid out to the publisher (based on revshare or cpm). |
| `network_profit` | money | `801.08` | (booked_revenue + reseller_revenue) - total_cost | Network profit minus total cost. |
| `network_roi` | double | `2.94` | (network_revenue / media_cost) - 1 | **To be deprecated**. Network return on investment. Returned as a percentage, e.g., 0.94 = 94% |
| `sold_network_rpm` | double | `231.888` | (revenue / imps) x 1000 ----- no errors | The revenue per 1000 impressions that were not errors. |
| `total_publisher_rpm` | money | `1.6605168`<br>`5393258` | (cost / imps) x 1000 | The cost per 1000 impressions paid to direct and third-party publishers, including errors. |
| `sold_publisher_rpm` | double | `147.786` | (cost / imps) x 1000 ----- no errors | The cost per 1000 impressions paid to direct and third-party publishers, not including errors. |
| `network_ppm` | money | `9.23` | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| `imps_sold` | int | `42500` | imps_sold | The number of impressions you sold to other members. |
| `video_errors` | int | `23` | errors | The total number of errors serving video impressions |
| `ad_responses` | int | `2340` | served | The number of responses delivered to the user's browser (or mediating server). A response can result in an impression, an error in player, or an auction with no impression event.<br><br>**Note**: An imp refers to when the video player loads the video and starts the first frame. Videos Served refers to the VAST document being served in response to a request from the video player. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `network_profit_ecpm` | money | `123.45` | ((booked_revenue + reseller_revenue - total_cost)/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | (booked_revenue + reseller_revenue - total_cost)/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | (booked_revenue + reseller_revenue - total_cost)/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45` | (booked_revenue + reseller_revenue - total_cost)/(booked_revenue + reseller_revenue) | Network profit margin. |
| `Average View Time` | int | `28` | sum (creative_duration * ((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions)) / sum (starts)) | An estimate for the average duration in seconds (rounded to 0 decimal places) of the creative that was viewed. This is calculated by approximating the duration watched as the mid-point between the video events (for example, a start event would estimate that 12.5% of the creative is viewed). |
| `Average View Time Percent` | percentage | `89%` | sum (((0.125 × starts) + (0.25 × first_quartiles) + (0.25 × second_quartiles) + (0.25 × third_quartiles) + (0.125 × completions))∕starts) | The average view time expressed as a percentage of the total possible view time. |

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

## Example

### Create a JSON formatted report request

```
$ cat video_analytics_network_publisher
{
    "report":
    {
        "report_type":"video_analytics_network_publisher",
        "columns":[
            "hour",
            "buyer_member",
            "brand_name",
            "deal_name",
            "deal_id",
            "imps_sold",
            "video_errors",
            "total_convs",
            "served"
        ],
        "row_per":[
            "hour",
            "buyer_member",
            "sold_network_rpm"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X post -d @video_analytics_network_publisher "https://api.appnexus.com/report?publisher_id=4642"
{
   "response":{
      "status":"OK",
      "report_id":"f4ebb93755dd01dde4fc157f86198ea9"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies "https://api.appnexus.com/report?id=f4ebb93755dd01dde4fc157f86198ea9"
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:37:31",
         "json_request":"{\"report\":{\"report_type\":\"video_analytics_network_publisher\",\"columns\":[\"hour\",\"buyer_member\",\"brand_name\",
            \"deal_name\",\"deal_id\",\"imps_sold\",\"video_errors\",\"total_convs\",\"served\"],
            \"row_per\":[\"hour\",\"buyer_member\",\"sold_network_rpm\"],\"report_interval\":\"last_48_hours\",
            \"filters\":[{\"publisher_id\":\"4642\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_analytics_network_publisher.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
