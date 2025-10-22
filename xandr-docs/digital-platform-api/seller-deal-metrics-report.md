---
title: Seller Deal Metrics Report
description: Use the Seller Deal Metrics report to view relevant information on deal metrics, performance, and rejection reasons for sellers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Seller Deal Metrics report

The Seller Deal Metrics report provides key information about deal metrics, performance, and rejection reasons that is relevant to seller.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- today
- yesterday
- last_2_days
- last_7_days (not including today)
- last_14_days
- last_30_days

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 30 days.

## Dimensions

| Column | Filter? | Description |
|:---|:---|:---|
| `hour` | Yes | The hour of the auction. <br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | Yes | The day of the auction. |
| `month` | Yes | The month of the auction. |
| `buyer_member` | Yes | The ID and name of the member whose advertiser purchased the impression. |
| `buyer_member_id` | Yes | The ID of the buyer that purchased the impression. |
| `buyer_member_name` | Yes | The specific buyer that purchased the impression. |
| `buyer_seat_id` | Yes | The ID of the buyer seat. |
| `buyer_seat_name` | No | The display name for the buyer seat code. |
| `buyer_seat_code` | No | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| `seller_member_id` | Yes | The member ID of the seller whose inventory you're interested in. |
| `deal` | Yes | The deal associated with the impression. |
| `deal_id` | Yes | The ID of the deal to which the settings apply. |
| `deal_name` | Yes | The deal associated with the transaction for the impression. |
| `ask_price` | Yes | The ask price for the deal. |
| `start_date` | Yes | The day and time when the deal starts being available to the buyer. |
| `end_date` | Yes | The day and time when the deal stops being available to the buyer. |
| `metric_type` | Yes | The type of the metric used to measure the performance of campaigns. |
| `deal_auction_type_name` | Yes | The auction type for the deal. A deal can have the following auction types: first price, second price, and fixed price. |
| `deal_type_name` | Yes | Whether the deal is a public deal, private deal, or programmatic guaranteed deal. |
| `deal_alias` | No | The alias of the deal. |
| `package_id` | Yes | The ID of the Package that the deal was created from. This value will be `0` if the deal was not created from a package. |
| `priority` | Yes | For a private auction only, the priority the seller assigned to the deal. |

## Metrics

| Column | Type | Filter | Description |
|:---|:---|:---|:---|
| `imps_matched` | int | Yes | The total number of impressions that match the seller's settings (not the buyer's) on the deal. |
| `bid_requests` | int | Yes | The number of bid requests. |
| `bids` | int | Yes | The number of times a buyer bid. |
| `final_bids` | int | Yes | The number of auctions in which a buyer bid. |
| `imps_won` | int | Yes | The total number of impressions won. |
| `seller_revenue` | currency | Yes | The seller revenue on the deal. |
| `seller_revenue_ecpm` | currency | Yes | The seller revenue on the deal, represented in eCPM. |
| `average_net_bid` | currency | Yes | The average net bid on the deal. This is the bid price that is net of all fees and used in determining seller revenue (prior to any bid price reduction that may take place). |
| `average_floor_price` | currency | Yes | The average floor price for the deal. |
| `bid_rate` | int | Yes | The percentage of auctions in which the buyer bid. |
| `ineligible_bid_rate` | int | Yes | The rate of ineligible bids on the deal. |
| `gross_win_rate` | int | Yes | The gross win rate for the deal. |
| `net_win_rate` | int | Yes | The net win rate for the deal. |
| `reject_count` | int | Yes | The total number of rejected bids. |
| `reject_bidder_error_count` | int | Yes | The number of bids rejected due to bidder errors. |
| `reject_blocked_by_ad_profile_count` | int | Yes | The sum of all bids rejected by the Ad Profile. |
| `reject_below_floor_count` | int | Yes | The number of bids rejected because they are below the reserve price set on the auction. |
| `reject_blocked_by_deal_count` | int | Yes | The sum of all bids rejected due to constraints of the deal. |
| `reject_invalid_creative_count` | int | Yes | The number of bids rejected due to invalid creatives that the buyer bid with. |
| `reject_blocked_by_dynamic_adserver_count` | int | Yes | The number of bids rejected due to adserver constraints dynamically passed in by the seller at the time of the impression request. |
| `reject_other_count` | int | Yes | The number of bids rejected for reasons not listed here. |
| `reject_bidder_error_deal_not_available_count` | int | Yes | The number of bids rejected because the deal was no longer available. |
| `reject_blocked_by_ad_profile_creative_count` | int | Yes | The number of bids rejected because the creative ad server was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_language_count` | int | Yes | The number of bids rejected because the language of the ad was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_tech_attribute_count` | int | Yes | The number of bids rejected because a technical attribute of the ad was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_category_count` | int | Yes | The number of bids rejected because the ad profile does not allow the category of the creative. |
| `reject_blocked_by_ad_profile_brand_count` | int | Yes | The number of bids blocked by the ad profile due to brand exclusions. |
| `reject_blocked_by_ad_profile_adserver_count` | int | Yes | The number of bids rejected because an ad server associated to the creative that the buyer bid with is blocked. |
| `reject_blocked_by_ad_profile_member_count` | int | Yes | The number of bids rejected because the member was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_audit_status_count` | int | Yes | The number of bids blocked by the Ad Profile due to their audit status. This typically happens when the buyer is bidding with an unaudited creative and the seller has blocked unaudited creatives in ad quality. |
| `reject_below_floor_ym_count` | int | Yes | The number of bids rejected because they are below the yield management floor applicable for the auction. |
| `reject_invalid_creative_not_ssl_count` | int | Yes | The number of bids rejected due to the creative not being SSL approved for a secure auction. |
| `reject_blocked_by_deal_creative_count` | int | Yes | The number of bids blocked by the deal due to their creative count. |
| `reject_blocked_by_deal_language_count` | int | Yes | The number of bids blocked by the deal due to their language settings. |
| `reject_blocked_by_deal_tech_attribute_count` | int | Yes | The number of bids rejected because a technical attribute was blocked by the deal. |
| `reject_blocked_by_deal_category_count` | int | Yes | The number of bids rejected because the deal does not allow the category of the creative. |
| `reject_blocked_by_deal_brand_count` | int | Yes | The number of bids rejected because their brand was blocked by the deal. |
| `reject_blocked_by_deal_below_floor_count` | int | Yes | The number of bids rejected because they were below the floor applicable for the auction. |
| `reject_blocked_by_deal_media_subtype_count` | int | Yes | The number of bids rejected due to their media subtypes. |
| `reject_blocked_by_deal_size_count` | int | Yes | The number of bids rejected because they did not match the size requirements for the deal. |
| `reject_blocked_by_deal_payment_type_count` | int | Yes | The number of bids rejected because their payment type was not allowed by the deal. |
| `reject_blocked_by_deal_adserver_count` | int | Yes | The number of bids blocked by due to adserver constraints on the Deal. |
| `reject_blocked_by_dynamic_brand_count` | int | Yes | The number of bids rejected because the brand is blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_language_count` | int | Yes | The number of bids rejected because the language is blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_tech_attribute_count` | int | Yes | The number of bids rejected because their techincal attributes are blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_category_count` | int | Yes | The number of bids rejected because the creative category is blocked dynamically by the bid request passed in by the seller. |
| `reject_other_data_protection_count` | int | Yes | The total number of bids rejected for data security reasons not listed here. |
| `reject_other_advertiser_exclusion_count` | int | Yes | The total number of bids rejected due to advertiser exclusions not listed above. |
| `reject_blocked_by_deal_advertiser_exclusion_count` | int | Yes | The number of deals rejected due to advertiser exclusions not listed here. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"seller_deal_metrics_report"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_deal_metrics_report
 
{
    "report": {
        "report_type": "seller_deal_metrics_report",
        "columns": [
            "hour",
            "buyer_member_name",
            "deal_name",
            "start_date",
            "end_date",
            "bids",
            "average_net_bid",
            "imps_won",
            "seller_revenue",
            "reject_count"
        ],
        "report_interval": "last_7_days",
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @seller_deal_metrics_report 'https://api.appnexus.com/report'
{
    "response": {
        "report_id": "2630ab93193a0b14257f154b7912ac5f",
        "status": "OK",
        "dbg_info": {
            "user::read_limit": 100,
            "user::write_limit": 60,
            "read_limit": 100,
            "write_limit": 60,
            "user::read_limit_seconds": 60,
            "user::write_limit_seconds": 60,
            "read_limit_seconds": 60,
            "write_limit_seconds": 60,
            "instance": "50.bm-report-processor.prod.nym2",
            "version": "1.73.249",
            "time": 280.62701225281,
            "start_microtime": 1694609672,
            "warnings": [],
            "api_cache_hit": "0",
            "output_term": "report_id"
        }
    }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=2630ab93193a0b14257f154b7912ac5f'
{
    "response": {
        "status": "OK",
        "report": {
            "id": "2630ab93193a0b14257f154b7912ac5f",
            "name": "",
            "created_on": "2023-09-13 12:54:32",
            "cache_hit": true,
            "fact_cache_hit": false,
            "fact_cache_error": "",
            "json_request": "{\"report\":{\"report_type\":\"seller_deal_metrics_report\",\"columns\":[\"hour\",\"buyer_member_name\",\"deal_name\",\"start_date\",\"end_date\",\"bids\",\"average_net_bid\",\"imps_won\",\"seller_revenue\",\"reject_count\"],\"report_interval\":\"last_7_days\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"seller_member_id\":\"958\"},{\"metric_type\":{\"value\":[\"0\"],\"operator\":\"=\"}}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1694563200,\"start_date\":1693958400,\"user_id\":\"4814\"}",
            "header_info": "Report type: seller_deal_metrics_reports\nReport ID: 2630ab93193a0b14257f154b7912ac5f\nRun at: 2023-09-13 12:55:17 UTC\nRequested Start date: 2023-09-06 00:00:00 UTC\nRequested End date: 2023-09-13 00:00:00 UTC\nTimezone: UTC\n",
            "user_id": "4814",
            "member_id": "958",
            "bidder_id": "2",
            "entity_id": "958",
            "row_count": 29112,
            "report_size": 3271276,
            "url": "report-download?id=2630ab93193a0b14257f154b7912ac5f"
        },
        "execution_status": "ready",
        "_was_this_status_cached_": 0,
        "dbg_info": {
            "user::read_limit": 100,
            "user::write_limit": 60,
            "read_limit": 100,
            "write_limit": 60,
            "user::read_limit_seconds": 60,
            "user::write_limit_seconds": 60,
            "read_limit_seconds": 60,
            "write_limit_seconds": 60,
            "instance": "47.bm-report-processor.prod.nym2",
            "version": "1.73.249",
            "time": 550.46796798706,
            "start_microtime": 1694609717,
            "warnings": [],
            "api_cache_hit": "0",
            "output_term": "report"
        }
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the`"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=2630ab93193a0b14257f154b7912ac5f' > /tmp/seller_deal_metrics_report.csv
```
