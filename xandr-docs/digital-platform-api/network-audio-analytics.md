---
title: Network Audio Analytics
description: Use the Network Audio Analytics report to view audio event metrics for network members.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network audio analytics

The **Network Audio Analytics** report can be used to view audio event metrics for a network member.

For instructions on retrieving a report, please see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field can be set to one of the following:

- last_available_day
- today
- last_24_hours
- yesterday
- last_48_hours
- last_7_days
- last_14_days
- last_7_available_days
- last_14_available_days
- month_to_date
- last_30_available_days
- month_to_yesterday
- last_30_days
- last_month
- last_100_days
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
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `month` | time | No | `"2010-02"` | The month of the auction. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member of the impression. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member of the impression. |
| `buyer_member` | string | No | `"My Network (123)"` | The name and ID of the buying member of the impression. |
| `creative_id` | int | Yes | `554` | The ID of the creative associated with the impression.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The name of the creative associated with the impression.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 728x90 (554)"` | The name and ID of the creative associated with the impression. |
| `member_id` | int | Yes | `767` | The ID of the member. |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member of the impression. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member of the impression. |
| `seller_member` | string | No | `"That Seller (456)"` | The name and ID of the selling member of the impression. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser whose creative served on this impression. If the value is `0`, either the impression was purchased by an external buyer, or a `default` or `PSA` was shown. |
| `advertiser_name` | string | No | `"Verizon Wireless"` | The name of the advertiser whose creative served on this impression. |
| `advertiser` | string | No | `"Verizon Wireless (789)"` | The name and ID of the advertiser whose creative served on this impression. |
| `advertiser_currency` | string | Yes | `"USD"` | The currency of the advertiser whose creative served on this impression. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher on whose inventory this impression occurred. |
| `publisher_name` | string | No | `"Facebook"` | The name of the publisher on whose inventory this impression occurred. |
| `publisher` | string | No | `"Facebook (321)"` | The name and ID of the publisher on whose inventory this impression occurred. |
| `publisher_currency` | string | Yes | `"USD"` | The currency of the publisher on whose inventory this impression occurred. |
| `site_id` | int | Yes | `194` | The ID of the site where the impression is occurred.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site Name"` | The name of the site where the impression is occurred. |
| `site` | string | No | `"Site Name (194)"` | The name and ID of the site where the impression is occurred. |
| `placement_id` | int | Yes | `456` | The ID of the placement through which this impression occurred.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| `placement_name` | string | No | `"Ivillage 160x600"` | The name of the placement through which this impression occurred.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the ID and a generic name. |
| `placement_code` | string | No | `"Ivillage Code"` | The custom code for the placement. |
| `placement` | string | No | `"Ivillage 160x600 (456)"` | The name and ID of the placement through which this impression occurred. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order under which this impression was purchased. |
| `insertion_order_name` | string | No | `"Insertion Order"` | The name of the insertion order under which this impression was purchased. |
| `insertion_order` | string | No | `"Insertion Order (321)"` | The name and ID of the insertion order under which this impression was purchased. |
| `line_item_id` | int | Yes | `111` | The ID of the line item under which this impression was purchased. |
| `line_item_name` | string | No | `"Default Line Item"` | The name of the line item under which this impression was purchased. |
| `line_item` | string | No | `"Default Line Item (111)"` | The name and ID of the line item under which this impression was purchased. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign which purchased this impression. (Does not apply to all advertisers.) |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign which purchased this impression. (Does not apply to all advertisers.) |
| `campaign` | string | No | `"Default Campaign (222)"` | The name and ID of the campaign which purchased this impression. (Does not apply to all advertisers.) |
| `campaign_group_type_id` | int | Yes | `987` | The ID of the campaign group type used in split reporting. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served in the impression. |
| `brand_id` | int | Tes | `3` | The ID of the brand associated with a creative.<br><br>`Note`: For `imp_type_id = 6`, no information is available in the brand_id field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | No | `"Ace Hardware"` | The name of the brand associated with a creative.<br><br>**Note**: For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand` | string | No | `"Ace Hardware (3)"` | The name and ID of the brand associated with a creative. |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country/region in which the impression took place. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country/region in which the impression took place. |
| `deal_id` | int | Yes | `2345` | The ID of the deal associated with the transaction for the impression.<br><br>**Note**: For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal associated with the transaction for the impression. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | The name and ID of the deal associated with the transaction for the impression. |
| `trafficker_for_insertion_order` | string | Yes | `"Maurice Truman"` | The trafficker for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md) for more details. |
| `salesrep_for_insertion_order` | string | Yes | `"Beverly Heller"` | The sales rep for the insertion order. See the `"labels"` field in the [Insertion Order Service](./insertion-order-service.md)e for more details. |
| `creative_recency_bucket_id` | string | no | `"4"` | The ID of the creative recency bucket.<br>See [Creative Recency Bucket](#creative-recency-bucket) to see for possible values. |
| `creative_recency_bucket` | string | yes | `"15-30 minutes"` | The bucket for how recently the creative was displayed.<br>See [Creative Recency Bucket](#creative-recency-bucket) to see for possible values. |
| `creative_frequency_bucket` | string | yes | `"11-20"` | The bucket for how frequently the creative was displayed. See [Creative Frequency Bucket](#creative-frequency-bucket) to see possible values. |
| `creative_frequency_bucket_id` | string | no | `"3"` | The ID of the creative frequency bucket.<br>See [Creative Frequency Bucket](#creative-frequency-bucket) to see possible values. |
| `site_domain` | string | no | `bestsiteever.com` | The site domain associated with an impression. |
| `supply_type_filterable` | string | yes | `"web"` | Whether to filter by supply type. The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `"web"` <br> - `"mobile_app"` <br> - `"mobile_web"` |
| `media_subtype` | int | yes | `3` | The media subtype for the creative which signifies the specific display style of creatives. |
| `creative_duration` | int | yes | `15` | The length of the ad in seconds. |
| `split_id` | int | yes | `889` | The ID of the split of the line item under which this impression was purchased. |
| `split_name` | string | no | `"split1"` | The name of the split of the line item under which this impression was purchased. |
| `split` | string | no | `"split1(889)"` | The name and ID of the split of the line item under which this impression was purchased. |
| `content_duration_secs` | int | yes | `12` | The length of the content duration in seconds. |
| `content_delivery_type_id` | int | yes | `889` | The ID for the type of streaming content delivery. For example, `Live`, `Video On Demand (VOD)`. |
| `content_genre_id` | int | yes | `771` | The ID of the main genre of the program on which the ad will be played. For example, `Game-Show`, `History`, `Music`. |
| `content_program_type_id` | int | yes | `987` | The ID of higher level categorization of the program on which the ad will be played. For example, `Movie`, `Series`, `Special`, `Show`, `Event`, `Clip` |
| `content_rating_id` | int | yes | `322` | The ID of type of rating of the content. For example, `All`, `Children (7+)`, `Teens (13+)`, `Young Adults (14+)`, `Adults (18+)` |
| `deal_alias` | string | No | `"Deal1"` | The alias of the deal, as it will appear in the UI. |
| `mobile_application_id` | int | Yes | `77775` | The ID of the mobile app on the device where the impression occurred. |
| `buying_currency` | string | Yes | `"USD"` | The transaction currency that the buyer used to purchase this impression. |
| `audio_context` | string | Yes | `"pre-roll"` | The type of the audio creative. See [Audio Context](#audio-context) below for possible values. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `cost` | money | `16.833378` | cost | The total amount of media cost for direct publisher and purchased real-time inventory. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue. |
| `profit` | money | `0.084102` | revenue - cost | The total network revenue minus network cost. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `ctr` | double | `0.000221877080097626` | clicks / imps | The rate of clicks to impressions. |
| `total_network_rpm` | money | `2.60548314606741` | (network_revenue / imps) x 1000 | The network revenue per 1000 impressions. |
| `errors` | int | `5` | errors | The total number of times an error occurred. |
| `starts` | int | `360` | starts | The total number of times the first segment of the creative was downloaded and started. |
| `start_rate` | double | `25.85` | starts / imps | The number of creatives starts divided by the number of impressions. |
| `skips` | int | `20` | skips | The total number of times a user skipped the creatives. |
| `skip_rate` | double | `20.5` | skips / imps | The number of video skips divided by the number of impressions. |
| `25_pcts` | int | `780`| 25% complete | The total number of times the creatives completed 25% of the entire duration. |
| `50_pcts` | int | `654` | 50% complete | The total number of times the creatives completed 50% of the entire duration of time. |
| `75_pcts` | int | `567` | 75% complete | The total number of times the creatives completed 75% of the entire duration of time. |
| `completions` | int | `989` | 100% complete | The total number of times the creatives played for the entire duration of time. |
| `completion_rate` | double | `85.45` | completions / imps | The number of creatives completions divided by the number of impressions. |
| `revenue_per_audio_complete` | double | `15.869` | revenue / completions | The revenue per audio creative completion. |
| `cost_per_audio_complete` | double | `2.056` | cost / completions | The cost per audio creative completion. |
| `audio_fill` | double | `7.889` | total imps/audio impressions served | The total number of imps divided by audio served. |
| `ad_responses` | int | `9999` | ad_responses | The total number of audio ad responses. |
| `served` | int | `87649` | audio impressions served | The total number of audio impressions served. |
| `device_type` | string | `"tablets"` | device_type | The type of device on which the impression was served. Possible values are:<br> - `desktops & laptops`<br> - `tablets`<br> - `mobile phones`<br> - `tv`<br> - `game consoles`<br> - `set top box`<br> - `media players`<br> - `other devices` |

### Creative recency bucket

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

### Creative frequency bucket

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

### Audio context

| Method ID | Method |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"pre-roll"` |
| `2` | `"mid-roll"` |
| `3` | `"post-roll"` |
| `4` | `"outstream"` |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` `"audio_analytics_network"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat audio_analytics_network 
{
   "report":{
      "report_type":"audio_analytics_network",
      "columns":[
         "seller_member_name",
         "audio_context",
         "imps",
         "clicks",
         "ctr",
         "convs_rate",
         "starts",
         "25_pcts",
         "50_pcts",
         "75_pcts",
         "completions"
      ],
      "report_interval":"last_48_hours",
      "format":"csv"
   }
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @audio_analytics_network 'https://api.appnexus.com/report' 
{ "response":{ 
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
         "created_on":"2021-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"audio_analytics_network\",\"columns\":[\"hour\",\"seller_member_name\",\"audio_context\", \"imps\",\"clicks\",\"ctr\",\"25_pcts\",\"50_pcts\",\"75_pcts\",\"completions\",\"convs_rate\"], \"row_per\":[\"hour\",\"seller_member_name\"], \"report_interval\":\"last_48_hours\"}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/audio_analytics_network.csv {code} 
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
