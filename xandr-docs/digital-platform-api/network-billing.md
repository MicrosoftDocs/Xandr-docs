---
title: Network Billing
description: Use the Network Billing Analytics report to view billing data for direct advertiser impressions and publishers across different platforms.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network billing

> [!WARNING]
> This report has been deprecated. As a result, it should only be used for billing activity **prior** to October 1, 2015. For reports after October 1, 2015, consult the [Buying Billing Report](buying-billing-report.md) and the [Selling Billing Report](./selling-billing-report.md).
>
> The **Network Billing Analytics** report can be used to view billing data across:
>
> - Direct advertiser impressions (bought across direct publishers and real-time inventory)
> - Direct publishers (sold across direct advertisers and other platform buyers)
>
> For instructions on retrieving a report, please see [Report Service](./report-service.md).
> [!NOTE]
> For impressions older than 100 days, the Network Billing Report now returns default values in some columns:
>
> - Creatives are aggregated into one row with `0` as the `creative_id` and a generic `creative_name`.
> - Placements are aggregated into one row with `-1` as the `placement_id` and a generic `placement_name`.
> - `hour` - Hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the  activity happened). This will make it look as though all activity happened at midnight. All daily data older than 100 days will be returned in the UTC time zone.

## Time frame

The `report_interval` field can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_2_days
- last_7_days
- last_30_days
- month_to_date
- month_to_yesterday
- quarter_to_date
- last_month
- lifetime

### Data retention period

Data retention period for this report is 30 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `entity_member_id` | int | Yes | `123` | -- |
| `buyer_member_id` | int | Yes | `123` | Internal ID of the buyer member |
| `buyer_member_name` | string | No | `"My Network"` | Display name of the buyer member |
| `buyer_member` | string | No | `"My Network (123)"` | **Deprecated** (as of October 17, 2016). |
| `buyer_type` | string | Yes | `"Real Time"`, `"Direct"` | The type of buyer |
| `buyer_currency` | string | Yes | `"USD"` | The currency of the buyer. |
| `seller_member_id` | int | Yes | `456` | Internal ID of the seller member |
| `seller_member_name` | string | No | `"That Seller"` | Display name of the seller member |
| `seller_member` | string | No | `"That Seller (456)"` | **Deprecated** (as of October 17, 2016). |
| `seller_type` | string | Yes | `"Real Time"`, `"Direct"` | The type of seller |
| `insertion_order_id` | int | Yes | `451` | Internal ID of the insertion order |
| `insertion_order_name` | string | No | `"Q1-2014"` | Display name for the insertion order |
| `campaign_id` | int | Yes | `728` | Internal ID of the campaign |
| `campaign_name` | string | No | `"Test"` | Display name of the campaign |
| `campaign` | string | No | `"Test (728)"` | **Deprecated** (as of October 17, 2016). |
| `creative_id` | int | Yes | `554` | Internal ID of the creative.<br><br>**Note**: For impressions older than 100 days, creatives are aggregated into one row with `0` as the `creative_id`. For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 - 728x90"` | Display name of the creative.<br><br>**Note**: For impressions older than 100 days, creatives are aggregated into one row with a generic `creative_name`. For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 - 728x90 (554)"` | **Deprecated** (as of October 17, 2016). |
| `placement_id` | int | Yes | `567` | Internal ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements are aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No |`"Photos 728x90"` | Display name of the placement.<br><br>**Note**: For impressions older than 100 days, placements are aggregated into one row with a generic `placement_name`. |
| `placement` | string | No | `"Photos 728x90 (567)"` | **Deprecated** (as of October 17, 2016). |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1` ("Blank"): No creative served.<br> - `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br> - `3` ("Default Error"): A default creative served due to a timeout issue.<br> - `4` ("Default"): A default creative served because there were no valid bids.<br> - `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br> - `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br> - `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br> - `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9` ("External Impression"): An impression from an impression tracker.<br> - `10` ("External Click"): A click from a click tracker. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id`. |
| `revenue_type` | string | Yes | `"CPA"` | The basis on which the member gets paid. |
| `revenue_type_id` | int | Yes | `4` | The ID of the revenue type. Possible values: <br> `-1` = No Payment <br> `0` = Flat CPM <br> `1` = Cost Plus CPM <br> `2` = Cost Plus Margin <br> `3` = CPC <br> `4` = CPA <br> `5` = Revshare <br> `6` = Flat Fee <br> `7` = Variable CPM <br>`8` = Estimated CPM |
| `payment_type` | string | Yes | `"com"`, `"revshare"` | The type of payment to a broker. |
| `cleared_direct` | int | Yes | `0`, `1` | Whether or not the buyer pays the seller directly for the cost of media. If `0`, Xandr collects the cost of media from the buyer and pays the seller. If `1`, the buyer pays the seller directly for the cost of media. <br><br>**Tip**: Buyers can match the cost of media on their invoice by filtering out "cleared direct" transactions. |
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the impression.<br><br>**Note**: For impressions older than 100 days, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight. All daily data older than 100 days is returned in the UTC time zone. |
| `day` | time | No | `"2010-02-01`" | The day of the impression. |
| `month` | time | No | `"2010-02"` | The month of the impression. |
| `advertiser_id` | int | Yes | `789` | Internal ID of the advertiser |
| `advertiser_name` | string | No | `"Verizon"` | Display name of the advertiser |
| `advertiser` | string | No | `"Verizon (789)"` | **Deprecated** (as of October 17, 2016). |
| `advertiser_currency` | string | Yes | `"USD"` | The currency of the advertiser. |
| `line_item_id` | int | Yes | `932` | Internal ID of the line item |
| `line_item_name` | string | No | `"$3 CPM Verizon Remarketing"` | Display name of the line item |
| `line_item` | string | No | `"$3 CPM Verizon Remarketing (932)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_id` | int | Yes | `123` | Internal ID of the publisher |
| `publisher_name` | string | No | `"Microsoft"` | Display name of the publisher |
| `publisher` | string | No | `"Microsoft (123)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_currency` | string | Yes | `Yes` | The currency of the publisher. |
| `salesperson_for_advertiser` | string | Yes | `"Ray Parcino"` | The salesperson for the advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `salesperson_for_publisher` | string | Yes | `"Brian Young"` | The salesperson for the publisher. See the `"labels"` field in the [Publisher Service](./publisher-service.md) for more details. |
| `account_manager_for_advertiser` | string | Yes | `"Rachel Dina"` | The account manager for the advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `account_manager_for_publisher` | string | Yes | `"Ami Fisher"` | The account manager for the publisher. See the `"labels"` field in the [Publisher Service](./publisher-service.md) for more details. |
| `trafficker_for_line_item` | string | Yes | `"Maurice Truman"` | The trafficker for the line item. See the `"labels"` field in the [Line Item Service](./line-item-service.md) for more details. |
| `salesrep_for_line_item` | string | Yes | `"Beverly Heller"` | The sales rep for the line item. See the `"labels"` field in the [Line Item Service](./line-item-service.md) for more details. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | Total number of impressions |
| `clicks` | int | `545` | clicks | Total number of clicks across all impressions |
| `convs` | int | `205` | total_convs | Total number of conversions across all impressions |
| `media_cost` | money | `304.36` | media_cost | The total cost of the inventory purchased. |
| `media_cost_pub_curr` | money | `201.34` | media_cost_pub_curr | The total cost of the inventory purchased, in the currency of the publisher. |
| `media_cost_adv_curr` | money | `201.34` | media_cost_adv_curr | The total cost of the inventory purchased, in the currency of the advertiser.<br><br>**Note**: If you are not tracking revenue through Xandr, this will be `0`. |
| `net_media_cost` | money | `211.23` | media_cost - auction_service_deduction | The total cost of inventory purchased, less the buyer's auction service charge deductions. |
| `net_media_cost_adv_curr` | money | `211.23` | media_cost_adv_curr - auction_service_deduction_adv_curr | The total cost of inventory purchased, less the buyer's auction service charge deductions, in the currency of the advertiser.<br><br>**Note**: If you are not tracking revenue through Xandr, this will be `0`. |
| `ecpm` | money | `1.30` | (spend / imps) x 1000 | Amount of money spent per 1000 impressions. |
| `ecpm_pub_curr` | money | `1.30` | (spend / imps) x 1000 | Amount of money spent per 1000 impressions, in the currency of the publisher. |
| `ctr` | double | `0.002327` | clicks / imps | The rate of clicks to impressions |
| `convs_rate` | double | `0.000856` | total_convs / imps | The rate of conversions to impressions |
| `network_revenue` | money | `1201.13` | network_revenue | Network revenue booked through direct advertisers and resold to real-time buyers |
| `booked_revenue` | money | `1201.13` | booked_revenue | Network revenue booked through direct advertisers. |
| `booked_revenue_adv_curr` | money | `970.24` | booked_revenue_adv_curr | Network revenue booked through direct advertisers, in the currency of the advertiser. |
| `network_profit` | money | `801.08` | network_revenue - media_cost | Network profit booked through direct advertisers and resold to real-time buyers. |
| `network_rpm` | money | `5.13` | (network_revenue / imps) x 1000 | Network revenue per Mille (1000 imps) |
| `network_ppm` | money | `3.42` | (network_profit / imps) x 1000 | Network profit per Mille (1000 imps) |
| `network_roi` | double | `2.94` | (network_revenue / media_cost) - 1 | Network return on investment. Returned as a percentage, e.g., 0.94 = 94% |
| `advertiser_revenue` | money |  | advertiser_revenue | The revenue recorded for the advertiser. |
| `advertiser_profit` | money |  | advertiser_revenue - media_cost | Advertiser profit |
| `advertiser_rpm` | money |  | (advertiser_revenue / imps) x 1000 | Advertiser revenue per Mille (1000 imps) |
| `advertiser_ppm` | money |  | (advertiser_profit / imps) x 1000 | Advertiser profit per Mille (1000 imps) |
| `advertiser_roi` | money |  | (advertiser_revenue / media_cost) x 1000 | Advertiser return on investment |
| `spend` | money | `304.36` | media_cost |  |
| `creative_overage_fees` | money |  | creative_overage_fees | Total fees charged for hosted creatives that exceed the creative size limit. |
| `creative_overage_fees_adv_curr` | money |  | creative_overage_fees_adv_curr | Total fees charged for hosted creatives that exceed the creative size limit, in the currency of the advertiser.<br><br>**Note**: If you are not tracking revenue through Xandr, this will be `0`. |
| `auction_service_fees` | money |  | auction_service_fees | Total fees charged for impressions bought from third parties. These fees are charged in addition to the buyer's media cost. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md) in the Monetize documentation. |
| `auction_service_fees_adv_curr` | money |  | auction_service_fees_adv_curr | Total fees charged for impressions bought from third parties, in the currency of the advertiser. These fees are charged in addition to the buyer's media cost. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md) in the Monetize documentation.<br><br>**Note**: If you are not tracking revenue through Xandr, this will be `0`. |
| `auction_service_deduction` | money |  | auction_service_deduction | The total deductions charged for impressions bought from third parties. These deductions are included in the buyer's media cost and deducted when calculating the seller's payment. |
| `auction_service_deduction_adv_curr` | money |  | auction_service_deduction_adv_curr | The total deductions charged for impressions bought from third parties, in the currency of the advertiser. These deductions are included in the buyer's media cost and deducted when calculating the seller's payment.<br><br>**Note**: If you are not tracking revenue through Xandr, this will be `0`. |
| `reseller_revenue` | money | `304.23` | reseller_revenue | The revenue generated through sales to external (RTB) buyers. |
| `reseller_revenue_pub_curr` | money | `304.23` | reseller_revenue_pub_curr | The revenue generated through sales to external (RTB) buyers, in the currency of the publisher. |

## Example

### Create a JSON formatted report request

The JSON file should include the report_type `"network_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat network-billing-request.json

{
    "report": {
        "format": "csv",
        "report_interval": "last_48_hours",
        "columns": [
            "seller_member_id",
            "buyer_member_id",
            "imps",
            "clicks",
            "convs_rate"
        ],
        "report_type": "network_billing"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @network-billing-request.json 'https://api.appnexus.com/report'

{
    "response": {
        "status": "OK",
        "report_id": "a2add615a52f0ca4ed13f64ce9d94a5c",
        "existing": false
    }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the reporting data to a file (described in the next step).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'

{
    "response": {
        "status": "OK",
        "report": {
            "name": "",
            "created_on": "2014-04-07 15:51:19",
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"last_48_hours\",\"columns\":[\"seller_member_id\",\"buyer_member_id\",\"imps\",\"clicks\",\"convs_rate\"],\"report_type\":\"network_billing\",\"filters\":[{\"entity_member_id\":\"1309\"}]}}",
            "url": "https://hb.nym1.sand-08.adnxs.net/report-download?id=a2add615a52f0ca4ed13f64ce9d94a5c"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=a2add615a52f0ca4ed13f64ce9d94a5c > /tmp/network-billing-report.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
