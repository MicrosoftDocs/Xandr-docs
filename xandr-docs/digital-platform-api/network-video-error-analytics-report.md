---
title: Network Video Error Analytics Report
description: Use the Network Video Error Analytics report to troubleshoot video settings and eliminate errors related to buy-side and sell-side video advertising.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network Video Error Analytics report

The **Network Video Error Report** gives insight into video errors and their cause.

You can use this report to troubleshoot video settings and eliminate errors related to buy-side and sell-side video advertising. [VAST 3 error codes](https://wiki.iabtechlab.com/index.php?title=VAST_Error_Code_Troubleshooting_Matrix) provide further insight into the source of errors.

> [!NOTE]
> For instructions on retrieving a report, please see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field can be set to one of the following:

- last_available_day
- today
- last_24_hours
- yesterday
- last_48_hours
- last_7_days
- last_7_available_days
- last_14_days
- last_14_available_days
- month_to_date
- last_30_available_days
- month_to_yesterday
- last_30_days
- last_month
- custom


### Data retention period

Data in this report has the following retention period:

- Hourly retention: 100 days
- Daily retention: 500 days


> [!NOTE]
> - To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).
>
> - For impressions older than 100 days, the day will be returned rather than the hour.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `month` | time | Yes | `"2010-02"` | The month of the auction. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `advertiser_name` | string | No | `"Verizon Wireless"` | The name of the advertiser. |
| `advertiser` | string | No | `"Verizon Wireless (789)"` | The name and ID of the advertiser. |
| `bidder_name` | string | No | `"ABC Plc"` | The name of a would-be buyer that submitted a bid on the impression. |
| `brand_id` | int | Yes | `3` | The ID of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | No | `"Ace Hardware"` | The name of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand` | string | No | `"Ace Hardware (3)"` | The brand associated with the creative. Xandr keeps a list of advertiser brands in our systems that can be applied to a creative when it's uploaded. For impression type `"Resold"`, no information is available in the `Brand` field for this report. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default <br> This dimension also has an attribute, called bidder, that identifies the ID of the bidder for the impression. The attribute's data type is int. |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member. |
| `buyer_member` | string | No | `"My Network (123)"` | The name and ID of the buying member. |
| `buyer_seat_code` | string | No | `"Custom Seat"` | The Custom Buyer Seat ID (submitted by DSP) which was used to bid on the impression. |
| `buyer_seat_id` | int | Yes | `123` | The id of the buyer seat. |
| `buyer_seat_name` | string | No | `"My Custom Seat"` | The display name for the buyer seat code. |
| `call_type` | string | Yes |  | The type of ad request call. |
| `campaign_id` | int | Yes | `123` | The ID of the campaign. |
| `campaign_name` | string | No | `"My Campaign"` | The name of the campaign. |
| `campaign` | string | No | `"My Campaign(123)"` | The name and ID of the campaign. |
| `campaign_group_type_id` | int | Yes | `123` | The ID for campaign group type used in split reporting. |
| `creative_id` | int | Yes | `123` | The ID of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"My Creative"` | The name of the creative.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"My Creative(123)"` | The name and ID of the creative. |
| `creative_duration` | int | Yes | `30` | The length of the video creative, in seconds. |
| `deal_id` | int | Yes | `123` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"My Deal"` | The name of the deal. |
| `deal` | string | No | `"My Deal(123)"` | The name and ID of the deal. |
| `device_type` | string | Yes | `"Mobile"` | The type of device where the impression occurred. |
| `geo_country` | string | Yes | `001` | The code for the geographic country/region. |
| `geo_country_name` | string | No | `"USA"` | The name of the geographic country/region. |
| `imp_type` | string | Yes | `RTB` | The type of impression. An integer value which translates as follows:<br>`1` = Blank<br>`2` = PSA<br>`3` = Default Error<br>`4` = Default<br>`5` = Kept<br>`6` = Resold<br>`7` = RTB<br>`8` = PSA Error<br>`9` = External Impression<br>`10` = External Click |
| `imp_type_id` | int | Yes | `7` | The ID of the associated impression type. Possible values:<br>`0` = Video event error<br>`1` = Blank: "200 OK" response (blank) served.<br>`2` = PSA: A public service announcement served because no other creative was eligible.<br>`3` = Default Error: A default creative served due to timeout issue.<br>`4` = Default: A default creative served because no campaigns bid or no other creative was eligible.<br>`5` = Kept: One of your managed advertisers served a creative.<br>`6` = Resold: The impression was sold to a third-party buyer.<br>`7` = RTB: Your creative served on third-party inventory.<br>`8` = PSA Error: A public service announcement served due to timeout issue.<br>`9` = External Impression: An impression from an impression tracker.<br>`10` = External Click: A click from a click tracker. |
| `insertion_order_id` | int | Yes | `123` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"My Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | No | `"My Insertion Order(123)"` | The name and ID of the insertion order. |
| `salesrep_for_insertion_order` | string | Yes | `"Beverly Heller"` | The sales rep for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `trafficker_for_insertion_order` | string | Yes | `"Maurice Truman"` | The trafficker for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details |
| `line_item_id` | int | Yes | `123` | The ID of the line item. |
| `line_item_name` | string | No | `"My Line Item"` | The name of the line item. |
| `line_item` | string | No | `"My Line Item(123)"` | The name and ID of the line item. |
| `member_id` | int | Yes | `123` | The ID of the member. |
| `mobile_application_id` | int | Yes | `123` | The ID of the mobile app on the device where the impression occurred. |
| `publisher_id` | int | Yes | `123` | The ID of the publisher. |
| `publisher_name` | string | No | `"My Publisher"` | The name of the publisher. |
| `publisher` | string | No | `"My Publisher(123)"` | The name and ID of the publisher. |
| `seller_member_id` | int | Yes | `123` | The ID of the selling member. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |
| `seller_member` | string | No | `"That Seller (456)"` | The name and ID of the selling member. |
| `site` | string | No | `"That Site(123)"` | The name and ID of the site. |
| `site_id` | int | Yes | `123` | The ID of the site.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0`. |
| `site_domain` | string | Yes | `bestsiteever.com` | The domain where the impression occurred. For mobile applications, this can be the URL of the app's location in the app store. There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed. |
| `site_name` | string | No | `"That Site"` | The name of the site. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `split_id` | int | Yes | `"123"` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | No | `"My Split"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `split` | string | No | `"My Split(123)"` | The name and ID of the split. |
| `supply_type_filterable` | string | Yes | `"web"` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app`" <br> - `"mobile_web"` |
| `tag_id` | int | Yes | `123` | The ID of the tag. |
| `placement_code` | string | No | `"Ivillage Code"` | The custom code for the placement. |
| `video_context` | string | Yes | `"3"` | The type of the video creative. See [Video Context](#video-context) below for possible values. |
| `video_playback_method` | string | Yes | `"1"` | The playback method for the creative. See [Video Playback Method](#video-playback-method) below for possible values |
| `video_player_size` | string | Yes | `"2"` | The ID of the video player width. See [Player Size](#player-size) below for possible values. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `errors` | int | `5` | errors | The total number of times an error occurred. |
| `cost_per_complete` | double | `2.056` | cost/completions | The cost per video completion. |
| `revenue_per_video_complete` | double | `15.869` | revenue/completions | The revenue per video completion. |
| `ad_responses` | int | `100` | ad_responses | The number of video ad responses. |
| `vast_100_error_count` | int | `10` | vast_100_error_count | The number of occurrences of VAST 100 errors. |
| `vast_101_error_count` | int | `10` | vast_101_error_count | The number of occurrences of VAST 101 errors. |
| `vast_102_error_count` | int | `10` | vast_102_error_count | The number of occurrences of VAST 102 errors. |
| `vast_200_error_count` | int | `10` | vast_200_error_count | The number of occurrences of VAST 200 errors. |
| `vast_201_error_count` | int | `10` | vast_201_error_count | The number of occurrences of VAST 201 errors. |
| `vast_202_error_count` | int | `10` | vast_202_error_count | The number of occurrences of VAST 202 errors. |
| `vast_203_error_count` | int | `10` | vast_203_error_count | The number of occurrences of VAST 203 errors. |
| `vast_300_error_count` | int | `10` | vast_300_error_count | The number of occurrences of VAST 300 errors. |
| `vast_301_error_count` | int | `10` | vast_301_error_count | The number of occurrences of VAST 301 errors. |
| `vast_302_error_count` | int | `10` | vast_302_error_count | The number of occurrences of VAST 302 errors. |
| `vast_303_error_count` | int | `10` | vast_303_error_count | The number of occurrences of VAST 303 errors. |
| `vast_400_error_count` | int | `10` | vast_400_error_count | The number of occurrences of VAST 400 errors. |
| `vast_401_error_count` | int | `10` | vast_401_error_count | The number of occurrences of VAST 401 errors. |
| `vast_402_error_count` | int | `10` | vast_402_error_count | The number of occurrences of VAST 402 errors. |
| `vast_403_error_count` | int | `10` | vast_403_error_count | The number of occurrences of VAST 403 errors. |
| `vast_405_error_count` | int | `10` | vast_405_error_count | The number of occurrences of VAST 405 errors. |
| `vast_500_error_count` | int | `10` | vast_500_error_count | The number of occurrences of VAST 500 errors. |
| `vast_501_error_count` | int | `10` | vast_501_error_count | The number of occurrences of VAST 501 errors. |
| `vast_502_error_count` | int | `10` | vast_502_error_count | The number of occurrences of VAST 502 errors. |
| `vast_503_error_count` | int | `10` | vast_503_error_count | The number of occurrences of VAST 503 errors. |
| `vast_600_error_count` | int | `10` | vast_600_error_count | The number of occurrences of VAST 600 errors. |
| `vast_601_error_count` | int | `10` | vast_601_error_count | The number of occurrences of VAST 601 errors. |
| `vast_602_error_count` | int | `10` | vast_602_error_count | The number of occurrences of VAST 602 errors. |
| `vast_603_error_count` | int | `10` | vast_603_error_count | The number of occurrences of VAST 603 errors. |
| `vast_604_error_count` | int | `10` | vast_604_error_count | The number of occurrences of VAST 604 errors. |
| `vast_900_error_count` | int | `10` | vast_900_error_count | The number of occurrences of VAST 900 errors. |
| `vast_901_error_count` | int | `10` | vast_901_error_count | The number of occurrences of VAST 901 errors. |
| `vast_error_rate` | int | `10` | (Number of videos resulted in vast error/Total videos served) x 100 | The percentage of videos served that result in a VAST error. |
| `rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `imps_default_bidder` | int | `0` | imps_default_bidder | The number of impressions that defaulted because there were no valid bids. |
| `imps_kept` | int | `0` | imps_kept | The number of impressions your advertiser purchased from your publisher. |
| `imps_resold` | int | `0` | imps_resold | The number of impressions your publisher sold to a third party. |
| `imps_rtb` | int | `2332` | imps_rtb | The number of impressions your advertiser bought from a third party. |
| `clicks` | int | `654` | clicks | The total number of clicks across all impressions. |
| `cost` | money | `16.833378` | cost | The total amount of media cost for direct publisher and purchased real-time inventory. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The sum of booked revenue and resold revenue. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `ctr` | double | `0.0221877080097626 %` | (clicks / imps) x 100% | The rate of clicks to impressions expressed as a percentage. |

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

The JSON file should include the `report_type` of `video_error_analytics_network`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat video_error_analytics_network

{
    "report":
    {
        "report_type":"video_error_analytics_network",
        "columns":[
            "hour",
            "seller_member_name",
            "buyer_member_name",
            "advertiser_name",
            "publisher_name",
            "vast_error_rate",
            "imps",
            "clicks",
            "ctr",
            "vast_900_error_count"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @network_analytics 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"video_error_analytics_network\",\"columns\":[\"hour\",\"seller_member_name\",
            \"buyer_member_name\",\"advertiser_name\",\"publisher_name\",\"imps\",\"clicks\",\"vast_error_rate\",\"ctr\"],
            \"row_per\":[\"hour\",\"seller_member_id\",\"buyer_member_id\",\"advertiser_id\",\"publisher_id\"],
            \"report_interval\":\"last_48_hours\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/video_error_analytics_network.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
