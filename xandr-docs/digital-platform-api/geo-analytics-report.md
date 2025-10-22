---
title: Geo Analytics Report
description: Use the Geo Analytics report to break down campaign delivery and performance by geographic area.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Geo Analytics report

The **Geo Analytics** report allows you to break down campaign delivery and performance by geographic area. Sample use cases for this report include:

- Buyers who would like to optimize their campaigns
- Buyers who need to report to their client advertisers or agencies on campaign delivery

This report can break down campaign performance along the following geographic boundaries:

- **Country**: The user's [country](./country-service.md) location.
- **Region**: The user's [regional](./region-service.md) location.
- **DMA**: The user's [designated market area](./designated-market-area-service.md).

For more information on the available data fields and their definitions, see [Dimensions](#dimensions) and [Metrics](#metrics) below.

For instructions on running this report, see the [Examples](#examples).

> [!NOTE]
> **On the accuracy of determining user geography by IP address**
>
> There is a limitation to how accurate the geo data is, particularly on impressions bought from external supply partners. Since some external supply partners (such as Google Ad Manager) truncate the last octet of the user's IP, we have a less precise IP to use when performing an IP geo-lookup. As a result, our geo data may not always be completely accurate at granular levels (such as region and DMA) for impressions bought from these supply sources.

## Time frame

The `report_interval` field in the request can be set to one of the following:

- today
- yesterday
- last_7_days

### Data retention period

Data retention period for this report is 45 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Description |
|:---|:---|:---|:---|
| `month` | date | Yes | The year and month in which the auction took place. |
| `day` | date | Yes | The year, month, and day in which the auction took place. |
| `hourly` | date | Yes | The hour at which the auction took place. |
| `member_id` | int | Yes | The ID of the member. |
| `advertiser_currency` | string | Yes | The type of currency used by the advertiser. |
| `insertion_order_id` | int | Yes | The insertion order ID. |
| `campaign_id` | int | Yes | The campaign ID. |
| `campaign_name` | string | No | The name of the campaign associated with the auction. |
| `campaign` | string | No | **Deprecated**. |
| `advertiser_id` | int | Yes | The advertiser ID. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `line_item_id` | int | Yes | The line item ID. |
| `advertiser_name` | string | No | The name of the advertiser. |
| `advertiser` | string | No | **Deprecated**. |
| `split_id` | int | Yes | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `campaign_code` | string | No | The user-assigned code used to identify the campaign. |
| `advertiser_code` | string | No | The user-assigned code associated with the advertiser. |
| `geo_country_code` | string | Yes | The country code of the user's location as defined by the [Country Service](./country-service.md). |
| `geo_country_id` | int | Yes | The country ID of the user's location as defined by the [Country Service](./country-service.md). `250` is shown in cases where we don't know the country or if the country doesn't map correctly to a location in our database. |
| `geo_region_code` | string | No | The region code of the user's location as defined by the [Region Service](./region-service.md). |
| `geo_region_id` | int | Yes | The region ID of the user's location as defined by the [Region Service](./region-service.md). `4291` is shown in cases where we don't know the region or if the region doesn't map correctly to a location in our database. |
| `geo_dma_id` | int | Yes | The ID of the user's designated market area location as defined by the [Designated Market Area Service](./designated-market-area-service.md).<br><br>**Note**: **Why am I seeing a DMA ID of `1`**?<br>Our reporting derives DMA from the city logged for the auction. However, our geo provider is sometimes unable to determine a city from the IP address associated with the impression, even when DMA **is** determined. Therefore, there are cases where a campaign targeting a specific DMA has impressions in reporting showing a DMA of `1`. |
| `geo_dma_name` | string | No | The name of the user's designated market area location as defined by the [Designated Market Area Service](./designated-market-area-service.md). |
| `geo_postal_code` | string | Yes | The postal code of the user's location. For postal codes, see [Postal Code Service](./postal-code-service.md). |
| `geo_city_id` | int | Yes | The ID of the user's city location. For city IDs, see [City Service](./city-service.md). |
| `geo_city_name` | string | Yes | The name of the user's city location. For city names, see [City Service](./city-service.md). |
| `insertion_order_name` | string | No | The name of the insertion order. |
| `insertion_order_code` | string | No | The user-defined code associated with the insertion order. |
| `line_item_name` | string | No | The name of the line item. |
| `line_item_code` | string | No | The user-defined code associated with the line item. |
| `geo_country_name` | string | No | The name of the user's country, as defined by the [Country Service](./country-service.md). |
| `geo_region_name` | string | No | The name of the region of the user's location as defined by the [Region Service](./region-service.md). |
| `insertion_order` | string | No | **Deprecated**. |
| `line_item` | string | No | **Deprecated**. |
| `geo_country` | string | No | **Deprecated**. |
| `geo_region` | string | No | **Deprecated**. |
| `geo_dma` | string | No | **Deprecated**. |
| `pixel_id` | int | Yes | The unique identification number of the conversion pixel.<br><br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by no more than 10 conversion pixels. Although `pixel_id` is groupable, we do not recommend that you group by this dimension since doing so will cause conversion events to then be shown in separate rows from impression and click events. We generally assume you want to view all of these events in a single row so as to be able to retrieve accurate and aggregated values for conversion rate and cost-per-conversion calculations. As a result, we instead recommend that you filter by `pixel_id` so you can retrieve conversion counts and related metrics for your most relevant pixel IDs. |
| `buying_currency` | string | Yes | The transaction currency used by the buyer to purchase this impression. |
| `uk_constituent_country` | string | No | The constituent country of the user. This is applicable for United Kingdom. Possible values include:<br> - `England`<br> - `Scotland`<br> - `Wales`<br> - `Northern Ireland` |
| `congressional_district_id` | int | Yes | The ID of the congressional district |
| `congressional_district_name` | string | No | The name of the congressional district |
| `state_house_district_id` | int | Yes | The ID of the state house district |
| `state_senate_district_id` | int | Yes | The ID of the state senate district |
| `state_house_district_name` | string | No | The name of the state house district |
| `state_senate_district_name` | string | No | The ID of the state senate district |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int |  | imps | The total number of impressions (served and resold). |
| `clicks` | int |  | clicks | The total number of clicks across all impressions. |
| `cost` | money |  | cost | The total cost of the inventory purchased. |
| `booked_revenue` | money |  | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `cpm` | money |  | cpm | The cost per one thousand impressions. |
| `total_convs` | int |  | total_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double |  | total_convs / imps | The ratio of conversions to impressions. |
| `post_view_convs` | int |  | post_view_convs | The total number of recorded post-view conversions. |
| `post_click_convs` | int |  | post_click_convs | The total number of recorded post-click conversions. |
| `profit` | money |  | booked_revenue - total_cost | Booked revenue minus total cost. |
| `click_thru_pct` | double |  | (clicks / imps) x 100 | The rate of clicks to impressions, expressed as a percentage. |
| `external_imps` | int |  | external_imps | The number of external (non-network) impressions. |
| `external_clicks` | int |  | external_clicks | The number of external (non-network) clicks. |
| `booked_revenue_adv_curr` | money |  | booked_revenue_adv_curr | The total revenue booked through a direct advertiser, expressed in the currency of that advertiser. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `profit_ecpm` | money | `123.45` | ((booked_revenue - total_cost)/imps) * 1,000 | Profit per 1,000 imps. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
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
| `booked_revenue_buying_currency` | money |  |  | The revenue booked by the buyer to purchase this impression. |
| `cost_buying_currency` | money |  |  | The amount of media cost for direct publisher and purchased real-time inventory in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cpm_buying_currency` | money |  |  | The cost per 1000 impressions in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cost_ecpa_buying_currency` | money |  |  | The cost per acquisition/conversion in the currency the buyer used to purchase the inventory. |
| `cost_ecpc_buying_currency` | money |  |  | The cost per click in the currency the buyer used to purchase the inventory. |
| `revenue_ecpm_buying_currency` | money |  |  | The revenue per 1,000 impressions in the buying currency. |
| `revenue_ecpc_buying_currency` | money |  |  | The revenue per click in the buying currency. |
| `revenue_ecpa_buying_currency` | money |  |  | The revenue per conversion in the buying currency. |
| `total_cost_buying_currency` | money |  |  | The total sum of media costs, data costs and partner fees in buying (advertiser) currency |

## Examples

### Create a JSON-formatted report request

The file should contain the `report_type` of `"geo_analytics"` as well as the columns and report_interval that you want to retrieve. For a full explanation of the fields that can be included in the file, see the [Report Service](./report-service.md).

Note that the more dimensions you group by, the larger the data set being returned will be. Larger data sets may take substantially longer to process, so be sure to group by only those dimensions you require.

```
$ cat geo_analytics

{
    "report":{
        "report_type":"geo_analytics",
        "timezone":"EST5EDT",
        "report_interval":"last_7_days",
        "groups":[
            "advertiser_id"
        ],
        "columns":[
            "advertiser_id",
            "imps",
            "clicks",
            "click_thru_pct",
            "total_convs",
            "convs_rate",
            "booked_revenue",
            "cost",
            "profit",
            "cpm"
        ],
        "orders":[
            "advertiser_id",
            "imps",
            "clicks",
            "click_thru_pct",
            "total_convs",
            "convs_rate",
            "booked_revenue",
            "cost",
            "profit",
            "cpm"
        ]
    }
}
```

### `POST` the request to the [report service](./report-service.md)

```
$ curl -b cookies -X POST -d @geo_analytics 'https://api.appnexus.com/report'
{
  "response": {
    "status": "OK",
    "report_id": "58e7a1db8d0ccf222e21ffc7c3cd01fb"
  }
}
```

### `GET` the report status from the [report service](./report-service.md)

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call periodically until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file as shown in the next step.

```
$ curl -b cookies "https://api.appnexus.com/report?id=58e7a1db8d0ccf222e21ffc7c3cd01fb"

{
    "response": {
        
        "execution_status": "ready",
        "report": {
            "url": "https://hb.nym1.sand-08.adnxs.net/report-download?id=58e7a1db8d0ccf222e21ffc7c3cd01fb",
            "query_time": "0",
            "finished_on": "2013-02-19 18:28:51",
            "started_on": "2013-02-19 18:28:48",
            "entity_id": "0",
            "user_id": "2027",
            "report_size": "93",
            "row_count": "0",
            "header_info": "Report ID:,58e7a1db8d0ccf222e21ffc7c3cd01fb
Run at:,2013-02-19 18:28:46
Start date:,2013-02-12 05:00:00
End date:,2013-02-19 05:00:00
Timezone:,EST5EDT
User:,Ursula Nimbus (2027)
",
            "json_request": "{"report":{"report_type":"geo_analytics","timezone":"EST5EDT","report_interval":"last_7_days","groups":["advertiser_id"],"columns":["advertiser_id","imps","clicks","click_thru_pct","total_convs","convs_rate","booked_revenue","cost","profit","cpm"],"pivot_report":false,"fixed_columns":[],"orders":["advertiser_id","imps","clicks","click_thru_pct","total_convs","convs_rate","booked_revenue","cost","profit","cpm"],"name":" Report - 02\/19\/2013","ui_columns":["advertiser_id","imps","clicks","click_thru_pct","total_convs","convs_rate","booked_revenue","cost","profit","cpm"]}}",
            "fact_cache_error": "did not find any cache table for 30,31,36,66,32,34",
            "fact_cache_hit": false,
            "cache_hit": false,
            "created_on": "2013-02-19 18:28:46",
            "name": " Report - 02/19/2013"
        },
        "status": "OK"
    }
}
```

### `GET` the report data from the report download service

Use the **report-download** service to download your data to a file. The service name and report ID can be extracted from the `url` field in the response.

```
$ curl -b cookies "https://api.appnexus.com/report-download?id=58e7a1ddb80ccf222e21ffc7c3cd01fb" > /tmp/geo_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
