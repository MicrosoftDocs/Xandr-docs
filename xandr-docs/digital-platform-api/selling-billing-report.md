---
title: Digital Platform API - Selling Billing Report
description: Use the Selling Billing report to view billing data across direct publishers, advertisers, and platform buyers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Selling Billing report

> [!WARNING]
> This report should only be used for data after September 30, 2015.

The Selling Billing Report can be used to view billing data across direct publishers (sold across direct advertisers and other platform buyers).

For instructions on retrieving a report, consult the [Report Service](./report-service.md).

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

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 1095 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the impression.<br><br>**Note**: For impressions older than 100 days, hourly data is aggregated into one row with 'YYYY-MM-DD 00:00:00' as the hour ('YYYY-MM-DD' is the UTC day in which the activity happened). This will make it look as though all activity happened at midnight. All daily data older than 100 days is returned in the UTC time zone. |
| `day` | time | No | `"2010-02-01"` | The day of the impression. |
| `month` | time | No | `"2010-02"` | The month of the impression. |
| `buyer_member_id` | int | Yes | `123` | Internal ID of the buyer member |
| `buyer_member_name` | string | No | `"My Network"` | Display name of the buyer member. |
| `seller_member_id` | int | Yes | `456` | Internal ID of the seller member. |
| `seller_member_name` | string | No | `"That Seller"` | Display name of the seller member. |
| `advertiser_id` | int | Yes | `789` | Internal ID of the advertiser. |
| `advertiser_name` | string | No | `"Verizon"` | Display name of the advertiser. |
| `publisher_id` | int | Yes | `321` | Internal ID of the publisher. |
| `publisher_name` | string | No | `"Test"` | Display name of the publisher. |
| `publisher_code` | int | Yes | `123` | External ID of the publisher. |
| `selling_currency` | string | Yes | `Yes` | The transaction currency used by the seller to sell this impression. |
| `buying_currency` | string | Yes | `"USD"` | The transaction currency used by the buyer to purchase this impression. |
| `deal_id` | int | Yes | `123` | Internal ID of the deal |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated IDs in parentheses):<br> - "Blank" (`1`): No creative served.<br> - "PSA" (`2`): A public service announcement served because there were no valid bids and no default creative was available.<br> - "Default Error" (`3`): A default creative served due to a timeout issue.<br> - "Default" (`4`): A default creative served because there were no valid bids.<br> - "Kept" (`5`): Your advertiser's creative served on your publisher's site.<br> - "Resold" (`6`): Your publisher's impression was sold to a third-party buyer.<br> - "RTB" (`7`): Your publisher's impression was sold to a third-party buyer.<br> - "PSA Error" (`8`): A public service announcement served due to a timeout issue or lack of a default creative.<br> - "External Impression" (`9`): An impression from an impression tracker.<br> - "External Click" (`10`): A click from a click tracker. |
| `selling_imp_type` | string | Yes | `"Resold"` | The type of impression. For possible values, see `imp_type_id`. |
| `cleared_direct` | int | Yes | `0`, `1` | Whether or not the buyer pays the seller directly for the cost of media. If `0`, Xandr collects the cost of media from the buyer and pays the seller. If `1`, the buyer pays the seller directly for the cost of media.<br><br>**Tip**: Buyers can match the cost of media on their invoice by filtering out "cleared direct" transactions. |
| `pricing_media_type_id` | int | No | `0`, `1` | ID of the video-specific media type classification (for billing only). If you don't have video-specific pricing, this field is irrelevant. Possible values are `0`, `1`, `2`, `3`. |
| `pricing_media_type_name` | string | No | `"Non Video"` | Name of the video-specific media type classification (for billing only). If you don't have video-specific pricing, this field is irrelevant. Possible values are <br> - `"--"` <br> - `"Non-Video"` <br> - `"Video (Hosted)"` <br> - `"Video (Non-Hosted)"`|
| `deal_type` | string | Yes | `"Open Auction"` | The deal type for a particular deal. Deal type options are: <br> - `Open Auction` <br> - `Private Auction` - <br> `Curated` <br> - `First Look` <br> - `Programmatic Guaranteed` |
| `auction_charges_available` | string | Yes | `"Yes"` | Identifies billable activity where the seller deductions can be disclosed. If the value is `“yes”`, the SASC Deductions column will be populated. |
| `is_claims_activity` | string | Yes | `"No"` | Identifies billable activity that won’t be paid because a successful Invalid Traffic claim was processed against it. |
| `is_cross_seat_activity` | string | Yes | `"No"` | Only relevant if you have more than one member/seat on the Xandr platform. If you do, this field allows you to know whether the activity was associated with transactions between members you manage and therefore simplify the reconciling of their invoices. |
| `buyer_cleared` | int | Yes | `0` | Whether or not the buyer pays the seller or curator directly for the cost of media. Acceptable values are:<br>`0`: Xandr acts as the clearing house, collecting the cost of media from the buyer and paying the seller.<br>`1`: Xandr does not clear cash; the buyer pays the seller directly for the cost of media.<br>`-1`: Dummy value for unbilled activity. |
| `curator_cleared` | int | Yes | `1` | Whether or not the seller receives the reseller revenue from Xandr or the curator. Acceptable values are:<br>`0`: The seller receives the reseller revenue from Xandr.<br>`1`: The seller receives the reseller revenue from the curator.<br>`-1`: Dummy value for unbilled activity. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `seller_billable_imps` | int | `123456` | imps | Total number of billable impressions. |
| `imps_filtered` | int | `2365` | imps_filtered | The total number of impressions which have been filtered out by Xandr's inventory quality review (e.g., impressions from a blocked buyer). |
| `clicks` | int |  | clicks | Total number of clicks across all impressions. |
| `convs` | int | `123456` | total_convs | Total number of conversions across all impressions. |
| `reseller_revenue` | money | `123.45` | seller_revenue | The revenue generated through sales to external (RTB) buyers, in USD. |
| `reseller_revenue_selling_currency` | money | `123.45` | reseller_revenue_selling_currency | The revenue generated through sales to external (RTB) buyers, in the transaction currency the seller used to sell the impression. |
| `seller_media_cost` | money | `123.45` | seller_media_cost | The amount owed to the publisher, in USD. |
| `seller_media_cost_selling_currency` | money | `123.45` | seller_media_cost_selling_currency | The amount owed to the publisher, in the transaction currency the seller used to sell the impression. |
| `gross_seller_revenue` | money | `123.45` | gross_seller_revenue | Seller revenue before SASC Deductions. |
| `SASC_deduction` | money | `122` | SASC_deduction | Seller Auction Service Charge, also known as Seller Revenue Share in some contracts, SASC is the charge for selling inventory to third-party buyers. It is quoted as a percentage of the buyer's media cost, and deducted prior to the calculation of seller revenue. Deducted from the bid at the time of auction. |
| `SASC_fees` | money | `111` | SASC_fees | Charged as a cost-plus model where the fees aren’t deducted from the bid and are billed to the client. |
| `bad_debt_fees` | money | `124` | bad_debt_fees | An agreed amount we charge to guarantee payment to the seller regardless of whether or not we get paid by the buyer. Charged as a cost-plus model where the fees aren’t deducted from the bid and are billed to the client. |
| `bad_debt_deductions` | money | `155` | bad_debt_deductions | An agreed amount we charge to guarantee payment to the seller regardless of whether or not we get paid by the buyer. Deducted from the bid at the time of auction. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"seller_pricing_report"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat seller_pricing_report.json

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
        "report_type": "seller_pricing_report"
    }
}
```

### `POST` the request to the reporting service specifying a member ID by replacing `INSERT_DESIRED_MEMBER_ID`

```
$ curl -b cookies -c cookies -X POST -d @seller_pricing_report_request.json 'https://api.appnexus.com/report?member_id=INSERT_DESIRED_MEMBER_ID'

{
  "response": {
    "status": "OK",
    "report_id": "9282cde2a86670d9861b77b8fc0954ad", <=== COPY THIS report_id as you will need it to check the status of your report and to download your report
    "existing": false,
    "cached": true
    }
  }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=9282cde2a86670d9861b77b8fc0954ad'

{
  "response": {
    "status": "OK",
    "report": {
      "name": null,
      "created_on": "2015-11-17 22:15:52",
      "cache_hit": true,
      "fact_cache_hit": true,
      "fact_cache_error": null,
      "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"last_48_hours\",\"columns\":[\"seller_member_name\",\"buyer_member_name\",\"imps\",\"clicks\",\"convs\"],\"report_type\":\"seller_pricing_report\",\"filters\":[{\"seller_member_id\":\"2414\"},{\"is_delivered\":{\"value\":[\"1\"],\"operator\":\"=\"}},{\"is_valid_seller\":{\"value\":[\"1\"],\"operator\":\"=\"}}]}}",
      "header_info": "Report ID:,6adf8e4e075f93f7dfba164fe8cddab3\r\nRun at:,2015-11-17 22:15:30\r\nStart date:,2015-11-15 22:00:00\r\nEnd date:,2015-11-17 20:00:00\r\nTimezone:,\r\nUser:,Huanqing Liu (171989)\r\n",
      "row_count": "0",
      "report_size": "56",
      "internal_info": "{\"report_id\":\"9282cde2a86670d9861b77b8fc0954ad\",\"cache_hit_using\":\"6adf8e4e075f93f7dfba164fe8cddab3\",\"cache_cause\":1,\"controller_cache_hit\":true}",
      "user_id": "171989",
      "entity_id": "0",
      "started_on": "1970-01-01 00:00:01",
      "finished_on": "2015-11-17 22:15:52",
      "query_time": null,
      "url": "report-download?id=9282cde2a86670d9861b77b8fc0954ad"
    },
    "execution_status": "ready"
    }
  }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=9282cde2a86670d9861b77b8fc0954ad' > seller_pricing_report.csv
```
