---
title: Bidder Billing Report API
description: Explore this article to understand the Bidder Billing report API, including its metrics, dimensions, and a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder Billing report API

Buyers can gather transaction information using the Bidder Billing Report to invoice their advertisers.

For instructions on retrieving a report, see [Report Service](report-service.md).

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- `current_hour`
- `last_hour`
- `last_48_hours`
- `today`
- `yesterday`
- `last_7_days`
- `month_to_date`
- `quarter_to_date`
- `last_month`
- `lifetime`
- `month_to_yesterday`
- `custom`  

## Dimensions

| Column | Type | Group? | Filter? | Example | Description |
|:---|:---|:---|:---|:---|:---|
| `hour` | time | Yes | Yes | `"2010-02-01 06:00:00"` | The hour of the impression.<br><br>**Note:** For impressions older than 100 days, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight. All daily data older than 100 days is returned in the UTC time zone. |
| `day` | time | Yes | Yes | `"2010-02-01"` | The day of the impression. |
| `month` | time | Yes | Yes | `"2010-02"` | The month of the impression. |
| `buyer_member_id` | int | Yes | Yes | `123` | Internal ID of the buyer member. |
| `buyer_member_name` | string | No | No | `"My Buyer"` | Display name of the buyer member. |
| `seller_member_id` | int | Yes | Yes | `456` | Internal ID of the seller member. |
| `seller_member_name` | string | No | No | `"That Seller"` | Display name of the seller member. |
| `publisher_id` | int | Yes | Yes | `321` | Internal ID of the publisher. |
| `geo_country` | string | Yes | Yes | `"US"` | The code for the geographic country or region. |
| `geo_country_name` | string | No | No | `"United States"` | The name of the geographic country or region. |
| `deal_id` |  int | Yes | Yes  | `123`  | The internal ID of the deal. |
| `deal_name` | string | No | No | `"Deal A"` | The display name of the deal. |
| `direct_cleared` | int | Yes | Yes | `0`, `1` | Whether or not the buyer pays the seller directly for the cost of media. If `0`, Xandr collects the cost of media from the buyer and pays the seller. If `1`, the buyer pays the seller directly for the cost of media.<br><br>**Tip:** Buyers can match the cost of media on their invoice by filtering out "cleared direct" transactions. |
| `buying_currency` | string | Yes | Yes | `"USD"` | The transaction currency used by the buyer to purchase this impression. |
| `selling_currency` | string | Yes | Yes | `"EUR"` | The transaction currency used by the seller to sell this impression. |
| `imp_type_id` | int | Yes | Yes | `7` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - 7 ("RTB"): Your buyers's creative served on third-party inventory.<br> - 9 ("External Impression"): An impression from an impression tracker.<br> - 10 ("External Click"): A click from a click tracker. |
| `buyer_seat_code` | string | Yes | No | `"1234"` | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| `buyer_seat_name` | string | Yes | No | `"test seat"` | The display name for the buyer seat code. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `100` | imps_delivered | The total number of impressions served successfully. |
| `imps_direct_cleared` | int | `100` | imps_direct_cleared | The total number of impressions where Xandr does NOT collect buyer media cost or pay out seller payment for transactions between this buyer-seller pair. |
| `imps_appnexus_cleared` | int | `100` | imps_appnexus_cleared | The total number of impressions where Xandr collects buyer media cost and pays out seller payments for transactions between this buyer-seller pair. |
| `buyer_media_cost` | money | `123.45` | buyer_media_cost | The total cost of the inventory purchased. |
| `buyer_media_cost_direct_cleared` | money | `123.45` | buyer_media_cost on imps_direct_cleared | The buyer's spend for impressions where the seller payment is transacted directly between this buyer-seller pair, not through Xandr. |
| `buyer_media_cost_direct_cleared_buying_currency` | money | `123.45` | buyer_media_cost_direct_cleared_buying_currency | The buyer's spend for impressions where the seller payment is transacted directly between this buyer-seller pair, not through Xandr, in the transaction currency the buyer used to buy the impression. |
| `buyer_media_cost_appnexus_cleared` | money | `123.45` | buyer_media_cost on imps_appnexus_cleared | The buyer's spend for impressions where Xandr pays out the seller payment. |
| `buyer_media_cost_direct_cleared_buying_currency` | money | `123.45` | buyer_media_cost_direct_cleared_buying_currency | The buyer's spend for impressions where Xandr pays out the seller payment, in the transaction currency the buyer used to buy the impression. |
| `buyer_media_cost_buying_currency` | money | `123.45` | buyer_media_cost_buying_currency | The total cost of the inventory purchased, in the transaction currency the buyer used to buy the impression. |
| `creative_overage_fees` | money | `123.45` | creative_overage_fees | Total fees charged for hosted creatives that exceed the creative size limit. |
| `creative_overage_fees_buying_currency` | money | `123.45` | creative_overage_fees_buying_currency | Total fees charged for hosted creatives that exceed the creative size limit, in the transaction currency the buyer used to buy the impression. |
| `auction_service_fees` | money | `123.45` | auction_service_fees | The fee charged on RTB bought impressions specified in the buyer member's contract. For example, with a 10% fee, if the buyer spends $1,000 on inventory, Xandr charges them a $100 fee. They will receive an invoice for $1,000 of Media Cost and $100 for Buyer Auction Service Charge (BASC) for a total of $1,100.<br><br>There are two types:<br> - For rows that are direct_cleared, your direct clear fee would be recorded in this field.<br> - If you have your Buyer Auction Service Charge (BASC) set as a fee rather than a deduction, a value will be recorded here as well. You can differentiate by grouping by the direct_cleared dimension when you pull the report. |
| `auction_service_fees_buying_currency` | money | `123.45` | auction_service_fees_buying_currency | The fee charged on RTB bought impressions specified in the buyer member's contract, in the transaction currency the buyer used to buy the impression. |
| `auction_service_deduction` | money | `123.45` | auction_service_deduction | The deduction on RTB bought impressions specified in the buyer member's contract. For example, with a 10% deduction, if they budget $1,000 for their campaign, Xandr takes $100 from that, leaving the buyer with $900 that is used to purchase inventory from the seller. Broker Auction Service Change (BRASC) will also be represented here. For the example above, the buyer will receive an invoice for $1,000 of Media Cost, which is inclusive of the deduction Xandr charges.<br><br>**Warning:** This field matches auction_service_fees if your contract has a Buyer Auction Service Charge (BASC) rate of greater than 0%. |
| `auction_service_deduction_buying_currency` | money | `123.45` | auction_service_deduction_buying_currency | The deduction on RTB bought impressions specified in the buyer member's contract, in the transaction currency the buyer used to buy the impression. |
| `buyer_ecpm` | money | `123.45` | buyer_media_cost / imps_delivered * 1000 | The buyer's cost per impression, expressed in eCPM. |
| `buyer_ecpm_buying_currency` | money | `123.45` | buyer_ecpm, expressed in the buyer's currency | The buyer's cost per impression in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |

## Examples

### Create the JSON-formatted report request

The JSON file should include the `report_type` `bidder_pricing_report`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_invoice_report_request.json
{
    "report": {
        "format": "csv",
        "report_interval": "last_48_hours",
        "columns": [
            "seller_member_name",
            "buyer_member_name",
            "imps"
        ],
        "report_type": "bidder_pricing_report"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @bidder_pricing_report_request.json 'https://api.adnxs.com/report'
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
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/report?id=39c4855a07e92433947886b5aabd267d'
{
 "response": {
   "status": "OK",
   "report": {
     "name": null,
     "created_on": "2015-11-17 21:27:21",
     "cache_hit": false,
     "fact_cache_hit": false,
     "fact_cache_error": null,
     "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"last_48_hours\",\"columns\":[\"seller_member_name\",\"buyer_member_name\",\"imps\",\"report_type\":\"bidder_pricing_report\"}}",
     "header_info": "Report ID:,39c4855a07e92433947886b5aabd267d\r\nRun at:,2015-11-17 21:27:21\r\nStart date:,2015-11-15 21:00:00\r\nEnd date:,2015-11-17 20:00:00\r\nTimezone:,\r\nUser:,Huanqing Liu (171989)\r\n",
     "row_count": "309",
     "report_size": "15583",
     "internal_info": "{...}",
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
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use \\i or \\v in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/report-download?id=39c4855a07e92433947886b5aabd267d' > bidder_pricing_report.csv
```

## Related topics

- [Report Service](report-service.md)
- [Completed Creative Audits Report](completed-creatives-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Platform Seller Report](platform-seller-report.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Inventory Availability Report](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
- [Saved Report Service](saved-report-service.md)
