---
title: Digital Platform API - Buyer Deal Metrics
description: In this article, learn about the Buyer Deal Metrics report and the dimensions and metrics associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Buyer deal metrics

The Buyer Deal Metrics report provides key information about deal metrics, performance, and rejection reasons that is relevant to buyers.

For instructions on retrieving a report, see [Report Service](report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- yesterday
- last_2_days
- last_7_days (not including today)
- last_14_days
- last_30_days

### Data retention period

Data retention period for this report is 30 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Filter? | Description |
|---|---|---|
| `ask_price` | Yes | The ask price for the deal. |
| `deal_alias` | No | A name assigned to a deal by a buyer with buyer-specific naming conventions which is typically owned and named by a seller. |
| `deal_auction_type_name` | Yes | The auction type for the deal. A deal can have the following auction types: first price, second price, and fixed price. |
| `deal_id` | Yes | The ID of the deal associated with the transaction for the impression. |
| `deal_name` | Yes | The deal associated with the transaction for the impression. |
| `deal_type_name` | Yes | The deal type for a particular deal. Deal type options are Open Auction, Private Auction, Curated, First Look, or Programmatic Guaranteed. |
| `end_date` | Yes | The day and time when the deal stops being available to the buyer. |
| `line_item_id` | Yes | The ID of the line item. |
| `package_id` | Yes | The ID of the package, if the deal is associated with a package. The integer value of the package that the deal was created from. This value will be 0 if the deal was not created from a package. |
| `priority` | Yes | For a private auction only, the priority the seller assigned to the deal. |
| `seller_member_id` | Yes | The ID of the seller that sold the deal. |
| `seller_member_name` | Yes | The seller that sold the deal. |
| `start_date` | Yes | The day and time when the deal starts being available to the buyer. |

## Metrics

| Column | Type | Filter? | Description |
|---|---|---|---|
| `ask_price` | currency | Yes | The ask price for the deal |
| `bid_rate` | int | Yes | The rate of bidding on the deal. |
| `bid_requests` | int | Yes | The number of bid requests. |
| `bids` | int | Yes | The number of completed bids. |
| `buyer_media_cost` | currency | Yes | The total cost to the buyer. |
| `buyer_cost_ecpm` | int | Yes | The cost of the deal to the buyer in eCPM. |
| `buyer_member_id` | int | Yes | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: `229` = PSA, `0` = Blank, or `319` = Default. |
| `buyer_member_name` | string | No | The name of the buying member. <br><br> **Note**: The name might be `"Default"` or `"Default Error"`, which means that there was no buyer for the impression, and a default creative was served. |
| `day` | time | No | The day of the auction. |
| `deal_type_name` | string | Yes | The deal type for a particular deal. Deal type options are Open Auction, Private Auction, Curated, First Look, or Programmatic Guaranteed. |
| `gross_win_rate` | int | Yes | The gross win rate for the deal. |
| `hour` | time | No | The hour of the auction. <br><br> **Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `imps_matched` | int | Yes | The total number of impressions that match the seller's settings (not the buyer's) on the deal. |
| `imps_won` | int | Yes | The total number of impressions won. |
| `ineligible_bid_rate` | int | Yes | The rate of ineligible bids on the deal. |
| `month` | time | No | The month of the auction. |
| `net_win_rate` | int | Yes | The net win rate for the deal. |
| `reject_below_floor_count` | int | Yes | The number of bids rejected because they are below the reserve price set on the auction. |
| `reject_below_floor_ym_count` | int | Yes | The number of bids rejected because they are below the yield management floor set for the deal. |
| `reject_bidder_error_count` | int | Yes | The number of bids rejected due to bidder errors. |
| `reject_bidder_error_deal_not_available_count` | int | Yes | The number of bids rejected because the deal was no longer available. |
| `reject_blocked_by_ad_profile_adserver_count` | int | Yes | The number of bids rejected because an ad server associated to the creative that the buyer bid with is blocked. |
| `reject_blocked_by_ad_profile_audit_status_count` | int | Yes | The number of bids blocked by the Ad Profile due to their audit status. This typically happens when the buyer is bidding with an unaudited creative and the seller has blocked unaudited creatives in ad quality. |
| `reject_blocked_by_ad_profile_brand_count` | int | Yes | The number of bids blocked by the ad profile due to brand exclusions. |
| `reject_blocked_by_ad_profile_category_count` | int | Yes | The number of bids rejected because the ad profile does not allow the category of the creative. |
| `reject_blocked_by_ad_profile_count` | int | Yes | The sum of all bids rejected by the Ad Profile. |
| `reject_blocked_by_ad_profile_creative_count` | int | Yes | The number of bids rejected because the creative ad server was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_language_count` | int | Yes | The number of bids rejected because the language of the ad was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_member_count` | int | Yes | The number of bids rejected because the member was blocked by the ad profile. |
| `reject_blocked_by_ad_profile_tech_attribute_count` | int | Yes | The number of bids rejected because a technical attribute of the ad was blocked by the ad profile. |
| `reject_blocked_by_deal_adserver_count` | int | Yes | The number of bids blocked due to adserver constraints on the deal. |
| `reject_blocked_by_deal_below_floor_count` | int | Yes | The number of bids rejected because they are below the deal's floor price. |
| `reject_blocked_by_deal_brand_count` | int | Yes | The number of bids rejected because their brand was blocked by the deal. |
| `reject_blocked_by_deal_category_count` | int | Yes | The number of bids rejected because the deal does not allow the category of the creative. |
| `reject_blocked_by_deal_count` | int | Yes | The sum of all bids rejected due to constraints of the deal. |
| `reject_blocked_by_deal_creative_count` | int | Yes | The number of bids blocked by the deal due to their language settings. |
| `reject_blocked_by_deal_language_count` | int | Yes | The number of bids blocked by the deal due to their language settings. |
| `reject_blocked_by_deal_media_subtype_count` | int | Yes | The number of bids rejected due to their media subtypes. |
| `reject_blocked_by_deal_payment_type_count` | int | Yes | The number of bids rejected because their payment type was not allowed by the deal. |
| `reject_blocked_by_deal_size_count` | int | Yes | The number of bids rejected because they did not match the size requirements for the deal. |
| `reject_blocked_by_deal_tech_attribute_count` | int | Yes | The number of bids rejected because a technical attribute was blocked by the deal. |
| `reject_blocked_by_dynamic_adserver_count` | int | Yes | The number of bids rejected due to adserver constraints dynamically passed in by the seller at the time of the impression request. |
| `reject_blocked_by_dynamic_brand_count` | int | Yes | The number of bids rejected because the brand is blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_category_count` | int | Yes | The number of bids rejected because the creative category is blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_language_count` | int | Yes | The number of bids rejected because the language is blocked dynamically by the bid request passed in by the seller. |
| `reject_blocked_by_dynamic_tech_attribute_count` | int | Yes | The number of bids rejected because their techincal attributes are blocked dynamically by the bid request passed in by the seller. |
| `reject_count` | int | Yes | The total number of rejected bids. |
| `reject_invalid_creative_count` | int | Yes | The number of bids rejected due to invalid creatives that the buyer bid with. |
| `reject_invalid_creative_not_ssl_count` | int | Yes | The number of bids rejected due to the creative not being SSL approved for a secure auction. |
| `reject_other_advertiser_exclusion_count` | int | Yes | The total number of bids rejected due to advertiser exclusions not listed above. |
| `reject_other_count` | int | Yes | The number of bids rejected for reasons not listed here. |
| `reject_other_data_protection_count` | int | Yes | The total number of bids rejected for data security reasons not listed here. |
| `submitted_bids` | int | Yes | The number of submitted bids. |

## Example

### Create the JSON-formatted report request

The JSON file should include the `report_type` `"buyer_deal_metrics_report"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (year, month, day), and specify the format in which the data should be returned (csv, excel, or html). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_deal_metrics_report

{
    "report":
    {
        "report_type":"buyer_deal_metrics_report",
        "columns":[
            "hour",
            "seller_member_name",
            "deal_name",
            "start_date",
            "end_date",
            "bids",
            "imps_won",
            "reject_count",
            "media_cost"
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @buyer_deal_metrics_report 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"buyer_deal_metrics_report\",\"columns\":[\"hour\",
            \"buyer_member_name\",\"deal_name\",\"start_date\",\"end_date\",\"bids\",\"imps_won\",\"media_cost\"],
            \"row_per\":[\"hour\",\"buyer_member_id\",\"deal_id\"],
            \"report_interval\":\"last_7_days\"}}",
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
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/buyer_deal_metrics_report.csv
```

> [!TIP]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
