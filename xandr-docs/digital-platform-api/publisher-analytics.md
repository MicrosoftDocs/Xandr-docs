---
title: Digital Platform API - Publisher Analytics
description: Explore the Publisher Analytics report to view revenue and profit data across a specific publisher's sites and placements.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Publisher Analytics

The Publisher Analytics report can be used to view revenue and profit data across a specific publisher's sites and placements. This report is available to both network and publisher users.

For instructions on retrieving a report, see the [Report Service](report-service.md) or the [examples](#examples) below. This report requires that a publisher ID be specified as part of the URL as follows:

```
https://api.appnexus.com/report?publisher_id=PUBLISHER_ID
```

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
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

In some cases Analytics reports can show delivery that does not match Lifetime QuickStats for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months are aggregated. The data from Billing reports are kept in non-aggregated form indefinitely.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | no | `"2010-02-01 06:00:00"` | The hour of the auction. <br><br>**Note:** For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | no | `"2010-02-01"` | The day of the auction. |
| `month` | time | no | `"2010-02"` | The month of the auction. |
| `publisher_id` | int | yes | `923` | The ID of the publisher. |
| `publisher_code` | string | no | `"My Publisher Code"` | The custom code for the publisher. |
| `publisher_currency` | string | no | `"USD"` | The currency of the publisher. |
| `pub_rule_id` | int | yes | `736` | The ID of the publisher rule. |
| `pub_rule_name` | string | no | `"My Publisher Rule"` | The name of the publisher rule. |
| `pub_rule` | string | no | `"My Publisher Rule (736)"` | **Deprecated** (as of October 17, 2016). |
| `pub_rule_code` | string | no | `"My Publisher Rule Code"` |  |
| `seller_member_id` | int | yes | `456` | The ID of the selling member. |
| `geo_country` | string | yes | `"US"` | The code of the geographical country/region. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region. |
| `size` | string | yes | `"728x90"` | The size of the placement/creative served. |
| `placement_id` | int | yes | `546` | The ID of the placement. <br><br>**Note:** For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | no | `"300x250 Business"` | The name of the placement. Note that, for impressions older than 100 days, placements will be aggregated into one row with "All placement data older than 100 days" as the placement_name. |
| `placement` | string | no | `"Photos 728x90 (567)"` | **Deprecated** (as of October 17, 2016). |
| `placement_code` | string | no | `"Photos Code"` |  |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about deals you have negotiated with buyers, see [Deal Service](deal-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated** (as of October 17, 2016). |
| `deal_code` | string | No | `"Custom code"` | The custom code for the deal. |
| `brand_id` | int | yes | `3` | The ID of the brand associated with a creative served on the publisher's inventory. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Publisher Brand Review Report](publisher-brand-review-report.md) instead. |
| `brand_name` | string | no | `"Ace Hardware"` | The name of the brand associated with a creative served on the publisher's inventory. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Publisher Brand Review Report](publisher-brand-review-report.md) instead. |
| `brand` | string | no | `"Ace Hardware (3)"` | **Deprecated** (as of October 17, 2016). |
| `supply_type` | string | no |  | The type of inventory. Possible values:<br>- `"web"`<br>- `"mobile_web"`<br>- `"mobile_app"` |
| `imp_type_id` | int | yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br>- `1` ("Blank"): No creative served.<br>- `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>- `3` ("Default Error"): A default creative served due to a timeout issue.<br>- `4` ("Default"): A default creative served because there were no valid bids.<br>- `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>- `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>- `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>- `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>- `9` ("External Impression"): An impression from an impression tracker. |
| `imp_type` | name | yes | `"Kept"` | The type of impressions. For possible values see `imp_type_id`. |
| `media_type` | string | no | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of a creative served on the publisher's inventory. You can use the [Media Type Service](media-type-service.md) to view the complete list of media types. |
| `adjustment_id` | int | yes | `22` | The ID of an adjustment you have set using the [Adjustment Service](adjustment-service.md). Networks use adjustments to help display their actual revenue in Xandr reporting. |
| `site_id` | int | yes | `555` | The ID of the site. For more information, see the [Site Service](site-service.md). |
| `site_name` | string | yes | `"My Site"` | The name of the site. For more information, see the [Site Service](site-service.md). |
| `site` | string | yes | `"My Site (555)"` | **Deprecated** (as of October 17, 2016). |
| `venue` | string | yes | `"Venue 55"` | The word Venue followed by the ID of the inventory's associated venue. |
| `mediatype_id` | int | yes | `444` | The ID of the media type associated with the creative that was served. For more information, see the [Media Type Service](media-type-service.md). |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps_total` | int | `234223` | imps | The total number of impressions (including defaults). |
| `imps_requests` | int | `234300` | imps_requests | The total number of ad calls (impression requests).<br><br>**Warning:** This metric is typically inaccurate for video inventory due to occasional delays in receiving video events, which can lead to inflated request totals based on the assumption that the video has expired. For a better video request metric, you should use Ad Requests in the [Seller Fill and Delivery Network Report](seller-fill-and-delivery-network-report.md) or the [Network Video Analytics Report](network-video-analytics.md). |
| `imps_sold` | int | `234123` | imps_sold | The total number of impressions sold to direct and real-time advertisers. |
| `imps_default` | int | `100` | imps_default | The total number of impressions not sold (default creative served). |
| `imps_blank` | int | `12` | imps_blank | The number of impressions which were served with a blank. |
| `imps_psa` | int | `10` | imps_psa | The number of impressions which were served with a PSA. |
| `imps_default_error` | int | `3` | imps_default_error | The number of impressions which defaulted due to a timeout error. |
| `imps_default_bidder` | int | `5` | imps_default_bidder | The number of impressions which defaulted because there were no valid bids. |
| `imps_kept` | int | `405` | imps_kept | The number of impressions your advertiser purchased from your publisher. |
| `imps_resold` | int | `506` | imps_resold | The number of impressions your publisher sold to a third party. |
| `imps_rtb` | int | `94` | imps_rtb | The number of impressions your advertiser bought from a third party. |
| `imps_filled` | int | `4900` | imps_filled | The number of blank, PSA, default, kept, resold, and external impressions. |
| `external_impression` | int | `0` | external_impression | The number of external impressions. |
| `external_click` | int | `0` | external_click | The number of external clicks. |
| `clicks` | int | `545` | clicks | The total number of clicks across all impressions. |
| `post_view_convs_pixel` | int | `23` |  | Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution](../monetize/conversion-attribution.md) (Microsoft Monetize) or [Conversion Attribution](../invest/conversion-attribution.md) (Microsoft Invest). |
| `post_clicks_convs_pixel` | int | `15` |  | Post click conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution](../monetize/conversion-attribution.md) (Microsoft Monetize) or [Conversion Attribution](../invest/conversion-attribution.md) (Microsoft Invest). |
| `publisher_revenue` | money | `400.05` | publisher_revenue | The revenue paid out to the publisher (based on revshare or CPM). |
| `publisher_revenue_pub_curr` | money | `400.05` | publisher_revenue_pub_curr | The revenue paid out to the publisher (based on revshare or CPM), in the currency of the publisher. |
| `publisher_filled_revenue` | money | `350.02` | publisher_filled_revenue | The revenue paid out to the publisher (based on revshare or CPM) for filled impressions. |
| `publisher_filled_revenue_publisher_curr` | money | `350.02` | publisher_filled_revenue | The revenue paid out to the publisher (based on revshare or CPM) for filled impressions, in the currency of the publisher. |
| `publisher_default_revenue` | money | `350.02` | publisher_default_revenue | The revenue paid out to the publisher (based on revshare or CPM) for default impressions. |
| `publisher_default_revenue_publisher_curr` | money | `350.02` | publisher_default_revenue | The revenue paid out to the publisher (based on revshare or CPM) for default impressions, in the currency of the publisher. |
| `total_convs` | int | `205` | total_convs | The total number of post view and post click conversions. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions. |
| `click_thru_pct` | double | `1.12359550561797` | (clicks / imps) * 100 | The rate of clicks to impressions as a percentage. |
| `convs_rate` | double | `0.000856` | total_convs / imps | The rate of conversions to impressions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `publisher_rpm` | money | `1.71` | (publisher_revenue / imps) x 1000 | The publisher revenue per 1000 impressions. |
| `publisher_rpm_pub_curr` | money | `1.71` | (publisher_revenue / imps) x 1000 | The publisher revenue per 1000 impressions, in the currency of the publisher. |
| `publisher_filled_rpm` | money |  | (publisher_revenue / imps_filled) x 1000 | The publisher revenue per 1000 filled impressions. |
| `publisher_filled_rpm_publisher_currency` | money |  | (publisher_revenue / imps_filled) x 1000 | The publisher revenue per 1000 filled impressions, in the publisher's currency. |
| `publisher_default_rpm` | money | `1.71` | (publisher_revenue / imps_default) x 1000 | The publisher revenue per 1000 default impressions. |
| `publisher_default_rpm_publisher_curr` | money | `1.71` | (publisher_revenue / imps_default) x 1000 | The publisher revenue per 1000 default impressions, in the currency of the publisher. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `video_skips` | int | `10` |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` |  | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` |  | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `10` |  | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` |  | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` |  | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` |  | The total number of video responses served to the player.An ad response occurs when the VAST document (XML) is served in response to a request.An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2` |  | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` |  | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` |  | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` |  | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` |  | The percentage of times the user opted to skip the video. |

### Age buckets

| Bucket ID | Bucket Name |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"13-17"` |
| `2` | `"18-24"` |
| `3` | `"25-34"` |
| `4` | `"35-44"` |
| `5` | `"45-54"` |
| `6` | `"'55-64"` |
| `7` | `"65+"` |

## Examples

### Step 1: Prepare your report request

```
$ cat the-file.json

{
    "report": {
        "format": "csv",
        "report_interval": "yesterday",
        "columns": [
            "publisher_id",
            "imp_type",
            "geo_country",
            "placement_id",
            "imps_total",
            "imps_kept",
            "imps_resold",
            "publisher_filled_revenue",
            "total_convs"
        ],
        "report_type": "publisher_analytics"
    }
}
```

### Step 2: `POST` the request JSON to the report service

```
$ curl -b cookies -c cookies -X POST -d @the-file.json 'https://api.appnexus.com/report?publisher_id=5555'

{
    "response": {
        "status": "OK",
        "report_id": "f589854c1697da8ff9ead66825c9bc04"
    }
}
```

### Step 3: Check the status of your request

```
$ curl -b cookies 'https://api.appnexus.com/report?id=f589854c1697da8ff9ead66825c9bc04'

{
    "response": {
        "status": "OK",
        "report": {
            "name": "",
            "created_on": "2013-10-30 21:15:36",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "",
            "header_info": "",
            "row_count": "",
            "report_size": "",
            "internal_info": "",
            "user_id": "2027",
            "entity_id": "0",
            "started_on": "1970-01-01 00:00:01",
            "finished_on": "1970-01-01 00:00:01",
            "query_time": ""
        },
        "execution_status": "pending"
    }
}
```

### Step 4: Download your data

```
curl -b cookies 'https://api.appnexus.com/report-download?id=f589854c1697da8ff9ead66825c9bc04' > /tmp/publisher_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
