---
title: Digital Platform API - Buying Billing Report
description: In this article, learn about the Buying Billing report, their time frame, data retention period, dimensions, and metrics with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Buying Billing report

> [!WARNING]
> This report should only be used for data after September 30, 2015.

The Buying Billing Report can be used to view billing data across direct advertiser impressions (bought across direct publishers and real-time inventory).

For instructions on retrieving a report, see [Report Service](report-service.md).

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- today
- yesterday
- last_48_hours
- last_7_days
- last_30_days
- month_to_date
- quarter_to_date
- last_month
- lifetime
- custom

### Data retention period

Data retention period for this report is 1095 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the impression.<br><br>**Note:** For impressions older than 100 days, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight. All daily data older than 100 days is returned in the UTC time zone. |
| `day` | time | No | `"2010-02-01"` | The day of the impression. |
| `month` | time | No | `"2010-02"` | The month of the impression. |
| `buyer_member_id` | int | Yes | `123` | Internal ID of the buyer member. |
| `buyer_member_name` | string | No | `"My Network"` | Display name of the buyer member. |
| `seller_member_id` | int | Yes | `456` | Internal ID of the seller member. |
| `seller_member_name` | string | No | `"That Seller"` | Display name of the seller member. |
| `advertiser_id` | int | Yes | `789` | Internal ID of the advertiser. |
| `advertiser_name` | string | No | `"Verizon"` | Display name of the advertiser. |
| `advertiser_code` | string  | No |`"Advertiser Code"`  | The external code associated with an advertiser. |
| `insertion_order_id` | int | Yes | `451` | Internal ID of the insertion order.|
| `insertion_order_name` | string | No | `"Q1-2014"` | Display name for the insertion order. |
| `insertion_order_code` | string | No | `"Insertion Order Code"` | The external code associated with an insertion order. |
| `line_item_id` | int | Yes | `932` | Internal ID of the line item. |
| `line_item_name` | string | No | `"$3 CPM Verizon Remarketing"` | Display name of the line item. |
| `line_item_code` | string | No | `"Line Item Code"`  | The external code associated with a line item. |
| `campaign_id` | int | Yes | `728` | Internal ID of the campaign. |
| `campaign_name` | string | No | `"Test"` | Display name of the campaign. |
| `campaign_code` | string | No | `"Campaign Code"` | The external code associated with a campaign. |
| `publisher_id` | int | Yes | `321` | Internal ID of the publisher. |
| `publisher_name` | string | No | `"Test"` | Display name of the publisher. |
| `deal_id` | int | Yes | `123` | The internal id of the deal. |
| `deal_name` | string | No | `"Deal A"` | The display name of the deal. |
| `buying_currency` | string | Yes | `"USD"` | The transaction currency used by the buyer to purchase this impression. |
| `selling_currency` | string | Yes | `"EUR"` | The transaction currency used by the seller to sell this impression. |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1 ("Blank")`: No creative served.<br> - `2 ("PSA")`: A public service announcement served because there were no valid bids and no default creative was available.<br> - `3 ("Default Error")`: A default creative served due to a timeout issue.<br> - `4 ("Default")`: A default creative served because there were no valid bids.<br> - `5 ("Kept")`: Your advertiser's creative served on your publisher's site.<br> - `6 ("Resold")`: Your publisher's impression was sold to a third-party buyer.<br> - `7 ("RTB")`: Your advertiser's creative served on third-party inventory.<br> - `8 ("PSA Error")`: A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9 ("External Impression")`: An impression from an impression tracker.<br> - `10 ("External Click")`: A click from a click tracker. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id`. |
| `cleared_direct` | int | Yes | `0`, `1` | Whether or not the buyer pays the seller directly for the cost of media. If `0`, Xandr collects the cost of media from the buyer and pays the seller. If `1`, the buyer pays the seller directly for the cost of media.<br><br>**Tip:** Buyers can match the cost of media on their invoice by filtering out "cleared direct" transactions. |
| `marketplace_clearing_event` | string | Yes | `"Views - Standard Display"` | The name of the underlying auction event that was transacted (e.g., impression, viewable impression, completed video). For more information, see [Guaranteed Outcomes](../invest/guaranteed-outcomes.md) and [Supported Viewability Standards](../invest/supported-viewability-standards-for-guaranteed-outcomes.md) in the UI documentation. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `123456` | imps | Total number of impressions. |
| `clicks` | int | `123456` | clicks | Total number of clicks across all impressions. |
| `convs` | int | `123456` | total_convs | Total number of conversions across all impressions. |
| `booked_revenue` | money | `123.45` | booked_revenue | Network revenue booked through direct advertisers. |
| `booked_revenue_dollars_buying_currency` | money | `123.45` | booked_revenue_dollars_buying_currency | Network revenue booked through direct advertisers, in the transaction currency the buyer used to buy the impression. |
| `buyer_media_cost` | money | `123.45` | buyer_media_cost | The total cost of the inventory purchased. |
| `buyer_media_cost_buying_currency` | money | `123.45` | buyer_media_cost_buying_currency | The total cost of the inventory purchased, in the transaction currency the buyer used to buy the impression. |
| `auction_service_deduction` | money | `123.45` | auction_service_deduction | The total deductions charged for impressions bought from third parties.<br>These deductions are included in the buyer's media cost and deducted when calculating the seller's payment. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md). |
| `auction_service_deduction_buying_currency` | money | `123.45` | auction_service_deduction_buying_currency | The total deductions charged for impressions bought from third parties, in the transaction currency the buyer used to buy the impression.<br>These deductions are included in the buyer's media cost and deducted when calculating the seller's payment. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md). |
| `net_media_cost` | money | `123.45` | net_media_cost | The total amount to be paid for media purchases, less the Auction Service Deduction. |
| `net_media_cost_buying_currency` | money | `123.45` | net_media_cost_buying_currency | The total amount to be paid for media purchases, less the Auction Service Deduction, in the transaction currency the buyer used to buy the impression. |
| `creative_overage_fees` | money | `123.45` | creative_overage_fees | Total fees charged for hosted creatives that exceed the creative size limit. |
| `creative_overage_fees_buying_currency` | money | `123.45` | creative_overage_fees_buying_currency | Total fees charged for hosted creatives that exceed the creative size limit, in the transaction currency the buyer used to buy the impression. |
| `auction_service_fees` | money | `123.45` | auction_service_fees | Total fees charged for impressions bought from third parties.<br>These fees are charged in addition to the buyer's media cost. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md). |
| `auction_service_fees_buying_currency` | money | `123.45` | auction_service_fees_buying_currency | Total fees charged for impressions bought from third parties, in the transaction currency the buyer used to buy the impression.<br>These fees are charged in addition to the buyer's media cost. For more information, see [Buyer Auction Service Charge Mechanics](../monetize/buyer-auction-service-charge-mechanics.md). |
| `marketplace_clearing_event_units` | int | `23` | marketplace_clearing_event_units | The total number of events purchased (for the associated Clearing Event). When buying a Clearing Event other than impression (e.g., viewable impressions), the number of billed events will be less than the number of impressions. For more information, see [Guaranteed Outcomes](../invest/guaranteed-outcomes.md) in the UI documentation. |
| `exchange_cost` | money | `4.32` | exchange_cost | The amount taken out of the exchange to give to the seller. If you aren't using a line item with a guaranteed outcomes payment model, this metric's value equals **Net Media Cost**. |
| `ecpm_conversion_deduction` | money | `3.2` | ecpm_conversion_deduction | The amount that Xandr takes out of a guaranteed outcomes bid/payment to cover eCPM conversion and post-auction outcome prediction services. If you aren't using a line item with a guaranteed outcomes payment model, this field's value equals `0`.<br>For more information on how this fee is calculated, see [Understanding Payment Conversion Rates](../invest/understanding-payment-conversion-rates.md). |
| `go_market_making_fee` | money | `0.48` | go_market_making_fee | The percentage-based fee that Xandr takes out of a guaranteed outcomes bid/payment to cover the risk incurred when providing guaranteed outcomes. This field's value equals `0` when not using a guaranteed outcomes line item. If you aren't using a line item with a guaranteed outcomes payment model, this field's value equals `0`.<br>The target for this fee is 10%, but the actual percentage used varies based on continuously shifting prediction accuracy:<br>GO Market Making Fee Percentage = Fixed Percentage (10%) ± Prediction Variability (a positive or negative percentage that changes based on shifting prediction accuracy)<br><br>For more information on how this fee is calculated, see [Understanding Payment Conversion Rates](../invest/understanding-payment-conversion-rates.md). |

## Examples

### Create the JSON-formatted report request

The JSON file should include the `report_type` `"buyer_invoice_report"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_invoice_report.json

{
    "report": {
        "format": "csv",
        "report_interval": "last_48_hours",
        "columns": [
            "seller_member_name",
            "buyer_member_name",
            "imps",
            "clicks",
            "convs"
        ],
        "report_type": "buyer_invoice_report"
    }
}
```

### `POST` the request to the Reporting Service specifying a member ID by replacing `INSERT_DESIRED_MEMBER_ID`

```
$ curl -b cookies -c cookies -X POST -d @buyer_invoice_report.json 'https://api.appnexus.com/report?member_id=INSERT_DESIRED_MEMBER_ID'

{
 "response": {
   "status": "OK",
   "report_id": "39c4855a07e92433947886b5aabd267d", <=== COPY THIS report_id as you will need it to check the status of your report and to download your report
   "existing": false,
   "dbg_info": {
     ...
     }
   }
}
```

### `GET` the report status from the Report Service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=39c4855a07e92433947886b5aabd267d'

{
 "response": {
   "status": "OK",
   "report": {
     "name": null,
     "created_on": "2015-11-17 21:27:21",
     "cache_hit": false,
     "fact_cache_hit": false,
     "fact_cache_error": null,
     "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"last_48_hours\",\"columns\":[\"seller_member_name\",\"buyer_member_name\",\"imps\",\"clicks\",\"convs\"],\"report_type\":\"buyer_invoice_report\",\"filters\":[{\"buyer_member_id\":\"668\"},{\"is_delivered\":{\"value\":[\"1\"],\"operator\":\"=\"}},{\"is_valid_buyer\":{\"value\":[\"1\"],\"operator\":\"=\"}},{\"is_valid_buying_imp_type\":{\"value\":[\"1\"],\"operator\":\"=\"}}]}}",
     "header_info": "Report ID:,39c4855a07e92433947886b5aabd267d\r\nRun at:,2015-11-17 21:27:21\r\nStart date:,2015-11-15 21:00:00\r\nEnd date:,2015-11-17 20:00:00\r\nTimezone:,\r\nUser:,Huanqing Liu (171989)\r\n",
     "row_count": "309",
     "report_size": "15583",
     "internal_info": "{\"report_id\":\"39c4855a07e92433947886b5aabd267d\",\"expected_query_cost\":\"1\",\"processor\":\"20.bm-report-processor.prod.nym2\",\"last_processor_run_on\":\"20.bm-report-processor.prod.nym2\",\"cache_miss\":1,\"query\":\" SELECT seller_member_id AS alias_1,CASE WHEN transaction_type = 1 THEN 'Blank' WHEN transaction_type = 3 THEN 'Default Error' WHEN transaction_type = 4 THEN 'Default' WHEN transaction_type = 2 THEN 'PSA' WHEN transaction_type = 8 THEN 'PSA Error' WHEN transaction_type IN (5,6,7,9,10,11) THEN CAST(BUYER_MEMBER_ID AS VARCHAR(7)) ELSE 'Unknown' END AS alias_2,SUM(IMPS) AS alias_3,SUM(CLICKS) AS alias_4,sum(convs) AS alias_5  FROM agg_combined_billing fact  WHERE 1=1  AND ymdh >= '2015-11-15 21:00:00' AND ymdh < '2015-11-17 20:00:00' AND buyer_member_id IN ('668') AND is_delivered IN ('1') AND CASE WHEN has_dw_buy=1 OR is_dw_buyer=0 THEN 1 ELSE 0 END IN ('1') AND CASE WHEN transaction_type in (7, 9, 10, 11) THEN 1 ELSE 0 END IN ('1')  GROUP BY alias_1, alias_2 LIMIT 1000000001\\n-- [member_id] \\n-- [report_id] 39c4855a07e92433947886b5aabd267d\"}",
     "user_id": "171989",
     "entity_id": "0",
     "started_on": "2015-11-17 21:27:22",
     "finished_on": "2015-11-17 21:27:24",
     "query_time": "0",
     "url": "report-download?id=39c4855a07e92433947886b5aabd267d"
   },
   "execution_status": "ready",
   "_was_this_status_cached_": 0,
   "dbg_info": {
     ...
     }
   }
}
```

### `GET` the report data from the Report Download Service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=39c4855a07e92433947886b5aabd267d' > buyer_invoice_report.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
