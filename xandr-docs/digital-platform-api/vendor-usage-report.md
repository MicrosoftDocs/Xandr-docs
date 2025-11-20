---
title: Digital Platform API - Vendor Usage Report
description: Explore the Vendor Usage report, offering details on your data usage or platform powered by third-party vendors.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Vendor Usage report

This network report provides the details on your usage of data or platform powered by third-party vendors (e.g., user segment providers), the costs of that data or feature usage, and the line items/campaigns where vendor costs were applicable.

## Time frame

The `report_interval` field in the JSON request must be set to one of the following:

- today
- yesterday
- last_7_days
- last_30_days
- month_to_date
- quarter_to_date
- last_month
- lifetime

The `time_granularity` of the data is `hourly`. For instructions on retrieving a report, see the [Report Service](report-service.md) or the [Examples](#examples) below.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

### Data retention period

Data retention period for this report is 60 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | yes | `"2010-02"` | The month at which the auction associated with the impression occurred. |
| `day` | date | yes | `"2010-02-01"` | The day at which the auction associated with the impression occurred. |
| `hour` | date | yes | `"2010-02-01 05:00:00"` | The hour at which the auction associated with the impression occurred. |
| `buyer_member_id` | int | yes | `643` | The ID of the member that used the data provided by the third-party vendor (e.g., user segment providers). |
| `geo_country` | string | yes | `"US"` | The code of the geographical country/region associated with the impression. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region associated with the impression. |
| `geo_country_code` | string | yes | `"CA"` | A two-character string denoting the country/region associated with the impression.|
| `campaign_id` | int | yes | `31` | The ID of the campaign associated with the impression that used third-party data targeting. |
| `campaign_name` | string | no | `"Prospect Campaign"` | The name of the campaign associated with the impression that used third-party data targeting. |
| `campaign` | string | no | `"Prospect Campaign (31)"` | The name and ID of the campaign associated with the impression. |
| `campaign_group_type_id` | int | yes | `154` | The ID of the campaign group type which purchased this impression. Used in split reporting. |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | no | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `split` | string | no | `"Mobile Split A (342)"` | The name and ID of the split. |
| `line_item_name` | string | no | `"Fall Apparel"` | The name of the line item associated with the impression that used third-party data targeting. |
| `targeted_segment_ids` | string | no | `"935035, 935146"` | The comma-separated list of IDs for each of the segments used when targeting. |
| `advertiser_currency` | string | yes | `"USD"` | The advertiser's preferred currency. This preference can be set using the [Advertiser Service](advertiser-service.md). |
| `insertion_order_id` | int | yes | `1243` | The ID of the insertion order associated with the impression that used third-party data targeting. |
| `insertion_order_name` | string | no | `"IO001"` | The name of the insertion order associated with the impression that used third-party data targeting. |
| `insertion_order_code` | string | no | `"IOABC-1243"` | The user-defined code associated with the insertion-order. |
| `insertion_order` | string | no | `"IO001 (1243)"` | The name and ID of the insertion order associated with the impression that used third-party data targeting. |
| `advertiser_id` | int | yes | `9843` | The advertiser ID associated with the impression. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `advertiser_name` | string | no | `"ADVUS"` | The name of the advertiser associated with the impression. |
| `advertiser` | string | no | `"ADVUS (9843)"` | The name and ID of the advertiser associated with the impression. |
| `line_item_id` | int | yes | `9865` | The ID of the line item associated with the impression that used third-party data targeting. |
| `line_item_code` | string | no | `"LI001"` | The user-defined code associated with the line item. |
| `line_item` | string | no | `"Fall Apparel (9865)"` | The name and ID of the line item associated with the impression that used third-party data targeting. |
| `vendor_id` | int | yes | `76` | The ID of the third party vendor (e.g., user segment providers) whose data usage and cost comes in this report. |
| `vendor_name` | string | no | `"AXM"` | The name of the third party vendor. |
| `vendor` | string | no | `"AXM (76)"` | The name and ID of the third party vendor. |
| `vendor_type` | string | no | `"Segment Marketplace"` | The type of the vendor depending on the third party data it provides. <br>Allowed values are: <br> - `Segment Marketplace`<br> - `Cross Device Graph`<br> - `Measurement`<br> - `Offline Attribution` <br> -  `Unknown Vendor Type` |
| `cost_type` | string | no | `"Segment Data Costs"` | The type of cost incurred towards the data usage provided by the third party vendors. Allowed values are: <br> - `Segment Data Costs`<br> - `Feature Costs`<br> - `Unknown Vendor Type` |
| `buying_currency` | string | yes | `"USD"` | The transaction currency that the buyer used to purchase this impression. |
| `cpm_usd` | money | yes | `7.8` | Cost per mille, or thousand (mille = thousand in Latin) expressed in USD. A pricing model in which advertisers pay for every 1000 impressions of their advertisement served. |

## Metrics

| Column | Type | Filter | Example | Formula | Description |
|:---|:---|:---|:---|:---|:---|
| `imps` | int | yes | `34534` | imps | The total number of impressions that used third-party data to serve the ad. |
| `third_party_costs` | money | yes | `5.20` | third_party_costs | Total monetary value of data segment costs, feature costs or others. |
| `transaction_tax` | money | no | `.43` | transaction_tax | Applicable sales, value added, goods and services or similar taxes (Transaction Taxes) will be applied to your transactions with Microsoft based on the Customer’s Account Business Location provided in the onboarding experience. |
| `vendor_costs` | money | no | `5.00` | vendor_costs | The total costs, including but not limited to segment data costs, and feature costs.<br>**Feature Costs:** Costs incurred when using a platform feature such as Nielsen Digital Ad Ratings (DAR), Nielsen Catalina Solutions (NCS) and Cross Device.<br>**Segment Data Costs:** All costs related to using segments in the data marketplace. Applicable when specific segments are applied in line items and associated pricing is displayed in the platform. |
| `vendor_costs_buying_currency` | money | no | `1.50` | vendor_costs_buying_currency | The vendor costs expressed in the transaction currency used by the buyer. |

## Examples

### Create JSON formatted report request

The JSON file should include the `report_type` of `"buyer_vendor_usage_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`, `hour`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat buyer_vendor_usage_analytics  
{
    "report": {
        "report_type": "buyer_vendor_usage_analytics",
        "format": "csv",
        "report_interval": "last_7_days",
        "columns": [
            "imps",
            "line_item_id",
            "vendor_costs",
            "sales_tax",
            "vendor_type",
            "vendor"
        ],
        "orders": [
            "line_item_id",
            "vendor_costs",
            "vendor_type"
        ]
    }
}
```

### `POST` the request to the Report service

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @buyer_vendor_usage_analytics "https://api.appnexus.com/report"
{
    "response": {
        "report_id": "d89151942729f768dcac4586288ff7eb",
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
            "version": "1.73.238",
            "time": 712.83793449402,
            "start_microtime": 1686106227,
            "warnings": [],
            "api_cache_hit": "0",
            "output_term": null,
            "edge_forwarded_dbg_info": {
                "user::read_limit": 100,
                "user::write_limit": 60,
                "read_limit": 100,
                "write_limit": 60,
                "user::read_limit_seconds": 60,
                "user::write_limit_seconds": 60,
                "read_limit_seconds": 60,
                "write_limit_seconds": 60,
                "instance": "37.report-processor.prod.nym2",
                "version": "1.73.238",
                "time": 708.98699760437,
                "start_microtime": 1686106227,
                "warnings": [],
                "api_cache_hit": "0",
                "output_term": "report_id"
            },
            "edge_forwarded": true,
            "edge_forwarded_by": "50.bm-report-processor.prod.nym2",
            "edge_forwarded_to": "http://report-processor-edge.adnxs.net/report"
        }
    }
}
```

### `GET` the report status from the Report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `ready`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=d89151942729f768dcac4586288ff7eb'
{
    "response": {
        "status": "OK",
        "report": {
            "id": "d89151942729f768dcac4586288ff7eb",
            "name": "",
            "created_on": "2023-06-07 02:50:27",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "",
            "json_request": "{\"report\":{\"report_type\":\"buyer_vendor_usage_analytics\",\"format\":\"csv\",\"report_interval\":\"last_7_days\",\"columns\":[\"imps\",\"line_item_id\",\"vendor_costs\",\"sales_tax\",\"vendor_type\",\"vendor\"],\"orders\":[{\"order_by\":\"line_item_id\",\"direction\":\"ASC\"},{\"order_by\":\"vendor_costs\",\"direction\":\"ASC\"},{\"order_by\":\"vendor_type\",\"direction\":\"ASC\"}],\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"buyer_member_id\":\"958\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1686096000,\"start_date\":1685491200,\"user_id\":\"4814\"}",
            "header_info": "Report type: buyer_vendor_usage_analyticss\nReport ID: d89151942729f768dcac4586288ff7eb\nRun at: 2023-06-07 04:08:58 UTC\nRequested Start date: 2023-05-31 00:00:00 UTC\nRequested End date: 2023-06-07 00:00:00 UTC\nTimezone: UTC\n",
            "user_id": "4814",
            "member_id": "958",
            "bidder_id": "2",
            "entity_id": "958",
            "row_count": 0,
            "report_size": 61,
            "url": "report-download?id=d89151942729f768dcac4586288ff7eb"
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
            "instance": "50.bm-report-processor.prod.nym2",
            "version": "1.73.238",
            "time": 454.48088645935,
            "start_microtime": 1686110938,
            "warnings": [],
            "api_cache_hit": "0",
            "output_term": null,
            "edge_forwarded_dbg_info": {
                "user::read_limit": 100,
                "user::write_limit": 60,
                "read_limit": 100,
                "write_limit": 60,
                "user::read_limit_seconds": 60,
                "user::write_limit_seconds": 60,
                "read_limit_seconds": 60,
                "write_limit_seconds": 60,
                "instance": "37.report-processor.prod.nym2",
                "version": "1.73.238",
                "time": 448.82392883301,
                "start_microtime": 1686110938,
                "warnings": [],
                "api_cache_hit": "0",
                "output_term": "report"
            },
            "edge_forwarded": true,
            "edge_forwarded_by": "50.bm-report-processor.prod.nym2",
            "edge_forwarded_to": "http://report-processor-edge.adnxs.net/report"
        }
    }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save, be sure to use the file extension of the file `"format"` that you specified in your initial `POST` call, for example, CSV.

```
curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=d89151942729f768dcac4586288ff7eb' > /tmp/buyer_vendor_usage_analytics.csv
```

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `\-i` or `\-v` in your call to expose the response header.
> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
