---
title: Digital Platform API - Multi-Buyer Seller Deal Metrics
description: Use the Multi-Buyer Seller Deal Metrics report to view key information about deal metrics, performance, and rejection reasons that is relevant to seller.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Multi-buyer seller deal metrics

The Multi-Buyer Seller Deal Metrics report provides key information about deal metrics, performance, and rejection reasons that is relevant to seller.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- yesterday
- today
- last_2 \_days
- last_7_days (not including today)
- last_14_Days
- last_30_days

### Data retention period

Data retention period for this report is 30 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Filter? | Description |
|:---|:---|:---|
| `ask_price` | Yes | The ask price for the deal. |
| `bidder_id` | Yes | ID of the bidder (DSP) for the impression. |
| `bidder_name` | No | Name of the bidder (DSP) for the impression. |
| `buyer_member_name` | Yes | The specific buyer that purchased the impression. |
| `buyer_member_id` | Yes | The ID of the buyer that purchased the impression. |
| `deal_auction_type_name` | Yes | The auction type for the deal. A deal can have the following auction types: <br> - `first price` <br> - `second price` <br> - `fixed price` |
| `deal_buyer_type` | Yes | Select to filter by the type of buyer the impression served through. Possible values: <br> - `"Entire Deal"` <br> - `"Bidder"` <br> - `"Buyer Member"` <br> - `"Buyer Seat"`<br><br>**Note**: This dimension is mandatory on the Multi-Buyer Deal Metrics Report. To not see data broken out by deal buyer type, filter by Entire Deal. |
| `deal_name` | Yes | The deal associated with the transaction for the impression. |
| `deal_type_name` | Yes | Whether the deal is a public deal, private deal, or programmatic guaranteed deal. |
| `end_date` | Yes | The day and time when the deal stops being available to the buyer. |
| `package_id` | Yes | The ID of the Package that the deal was created from. This value will be `0` if the deal was not created from a package. |
| `priority` | Yes | For a private auction only, the priority the seller assigned to the deal. |
| `start_date` | Yes | The day and time when the deal starts being available to the buyer. |

## Metrics

| Column | Type | Filter? | Description |
|:---|:---|:---|:---|
| `hour` | time | No | The hour of the auction. <br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | No | The day of the auction. |
| `month` | time | No | The month of the auction. |
| `imps_matched` | int | Yes | The total number of impressions that match the seller's settings (not the buyer's) on the deal. |
| `bid_requests` | int | Yes | The number of bid requests. |
| `bids` | int | Yes | The number of completed bids. |
| `imps_won` | int | Yes | The total number of impressions won. |
| `seller_revenue` | currency | Yes | The seller revenue on the deal. |
| `seller_revenue_ecpm` | currency | Yes | The seller revenue on the deal, represented in eCPM. |
| `average_net_bid` | currency | Yes | The average net bid on the deal. This is the bid price that is net of all fees and used in determining seller revenue (prior to any bid price reduction that may take place). |
| `average_biased_bid` | currency | Yes | The average biased bid for the deal. This is the bid price used for ranking purposes in the auction. |
| `average_floor_price` | currency | Yes | The average floor price for the deal. |
| `deal_type_name` | string | Yes | Whether the deal is a public deal or a private deal. |
| `bid_rate` | int | Yes | The rate of bidding on the deal. |
| `ineligible_bid_rate` | int | Yes | The rate of ineligible bids on the deal. |
| `gross_win_rate` | int | Yes | The gross win rate for the deal. |
| `net_win_rate` | int | Yes | The net win rate for the deal. |
| `ask_price` | currency | Yes | The ask price for the deal |
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
| `reject_blocked_by_deal_creative_count` | int | Yes | The number of bids blocked by the deal due to their language settings. |
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
| `reject_blocked_by_dynamic_tech_attribute_count` | int | Yes | The number of bids rejected because their technical attributes are blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_category_count` | int | Yes | The number of bids rejected because the creative category is blocked dynamically by the bid request passed in by the seller. |
| `reject_other_data_protection_count` | int | Yes | The total number of bids rejected for data security reasons not listed here. |
| `reject_other_advertiser_exclusion_count` | int | Yes | The total number of bids rejected due to advertiser exclusions not listed above. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"multi_buyer_seller_deal_metrics"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat multi_buyer_seller_deal_metrics

{
    "report": {
        "report_type": "multi_buyer_seller_deal_metrics",
        "columns": [
            "hour", 
            "buyer_member_name", 
            "deal_name", 
            "start_date", 
            "end_date", 
            "average_net_bid", 
            "imps_won", 
            "seller_revenue", 
            "reject_count"
        ],
        "filters": [{
            "deal_buyer_type": ["Buyer Member"]
        }],
        "report_interval": "last_7_days",
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @multi_buyer_seller_deal_metrics 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"b97897a7864dd8f34e7457226c7af592"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=b97897a7864dd8f34e7457226c7af592'
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2010-05-25 19:19:53",
            "json_request": "{\"report\":{\"report_type\":\"multi_buyer_seller_deal_metrics\",\"columns\":[\"hour\",\
            "buyer_member_name\",\"deal_name\",\"start_date\",\"end_date\",\"average_net_bid\",\"imps_won\",\"seller_revenue\,\"reject_count\"],\
            "row_per\":[\"hour\",\"buyer_member_id\",\"deal_id\"],\
            "report_interval\":\"last_7_days\"}}",
            "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `i` or `v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/multi_buyer_seller_deal_metrics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
