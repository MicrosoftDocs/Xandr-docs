---
title: Seller Platform Billing Report
description: Learn how Suppliers gather transaction information using the Seller Platform Billing Report to invoice buyers. This page covers an example on retrieving a report.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Seller platform billing report

Learn about Seller Platform Billing Report in this page. Suppliers gather transaction information using the Seller Platform Billing Report to invoice buyers or reconcile their internal transaction records.

For instructions on retrieving a report, see the [Example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- `current_hour`
- `last_hour`
- `today`
- `yesterday`
- `last_48_hours`
- `last_7_days`
- `month_to_yesterday`
- `month_to_date`
- `quarter_to_date`
- `last_month`
- `lifetime`
- `mtd`

## Dimensions

| Column | Type | Group? | Filter? | Description |
|--|--|--|--|--|
| `bidder` | string | No | No | **Deprecated**. |
| `bidder_id` | int | Yes | Yes | The internal ID of the bidder. |
| `bidder_name` | string | No | No | The display name of the bidder. |
| `buyer_currency` | string | No | Yes | The buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `buyer_member` | string | No | No | **Deprecated**. |
| `buyer_member_id` | int | Yes | Yes | The internal ID of the buyer member. |
| `buyer_member_name` | string | No | No | The display name of the buyer member. |
| `cleared_direct` | int | No | Yes | If this is set to 1, then the impression was successfully served on direct inventory. <br>  Possible values: <br> - 0 = not direct inventory <br> - 1 = direct inventory |
| `day` | date | Yes | Yes | Day. |
| `geo_country` | string | No | Yes | The display name of the country or region followed by the ID (Xandr format). |
| `geo_country_name` | string | No | No | Country or region. |
| `hour` | date | Yes | Yes | The hour of the auction. <br> **Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `imp_type` | string | No | Yes | The type of impression served. Possible values: <br> - 1 = blank <br> - 2 = PSA <br> - 3 = default error <br> - 4 = default <br> - 5 = kept <br> - 6 = resold <br> - 7 = RTB <br> - 8 = PSA resulting from a default error  <br> - 9 = external impression <br> - 10 = external click |
| `is_delivered` | boolean | No | Yes | If true, the impression was served successfully. |
| `is_dw` | boolean | No | Yes | If true, the impression was served by Xandr. |
| `month` | time | Yes | No | Month. |
| `publisher` | string | No | No | **Deprecated**. |
| `publisher_code` | string | No | No | The custom code for the publisher, entered to correspond to the publisher code within the external system. |
| `publisher_id` | int | Yes | Yes | The internal ID of the publisher. |
| `publisher_name` | string | No | No | The display name of the publisher. |
| `seller_currency` | string | No | Yes | The seller member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `seller_member` | string | No | No | **Deprecated**. |
| `seller_member_id` | int | Yes | Yes | The internal ID of the seller member. |
| `seller_member_name` | string | No | No | The display name of the seller member. |
| `site` | string | No | No | **Deprecated**. |
| `site_code` | string | No | No | The custom code for the site, entered to correspond to the site code within the external system. |
| `site_id` | int | Yes | Yes | The internal ID of the site. |
| `site_name` | string | No | No | The display name of the site. |
| `year` | date | Yes | Yes | Year. |

## Metrics

| Column | Type | Formula | Description |
|--|--|--|--|
| `imps` | int | `imps` | The total number of impressions (served and resold). |
| `imps_delivered` | int | `imps_delivered` | The total number of impressions served successfully. |
| `imps_not_delivered` | int | `imps_not_delivered` | The total number of impressions where someone other than Xandr served the impression. |
| `imps_appnexus_cleared` | int | `imps_appnexus_cleared` | The total number of impressions where Xandr collects cost of media and pays out seller payment for transactions between this buyer-seller pair. |
| `imps_direct_cleared` | int | `imps_direct_cleared` | The total number of impressions where Xandr does NOT collect cost of media or pay out seller payment for transactions between this buyer-seller pair. |
| `seller_revenue` | money | `seller_revenue` | The seller's revenue per impression. |
| `seller_revenue_appnexus_cleared` | money | `seller_revenue for imps_appnexus_cleared` | The seller's revenue for impressions where Xandr pays out the seller payment. |
| `seller_revenue_direct_cleared` | money | `seller_revenue for imps_direct_cleared` | The seller's revenue for impressions where the seller payment is transacted directly between this buyer-seller pair, not through AppNexus. |
| `seller_ecpm` | money | `seller_revenue x 1000 / imps_delivered` | The seller's revenue expressed in eCPM. |
| `seller_revenue_seller_curr` | money | `seller_revenue, expressed in the seller's currency`. | The seller's revenue per impression in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `seller_revenue_appnexus_cleared_seller_curr` | money | `seller_revenue for imps_appnexus_cleared, expressed in the seller's currency`. | The seller's revenue for impressions where Xandr pays out the seller payment, per impression, in their selected currency. For a list of supported currencies,  [Supported Currencies](supported-currencies.md). |
| `seller_revenue_direct_cleared_seller_curr` | money | `seller_revenue for imps_direct_cleared, expressed in the seller's currency`. | The seller's revenue for impressions where the seller payment is transacted directly between this buyer-seller pair and not through Xandr, per impression, in their selected currency. For a list of supported currencies, see  [Supported Currencies](supported-currencies.md). |
| `seller_revenue_direct_cleared_buyer_curr` | money | `seller_revenue for imps_direct_cleared, expressed in the buyer's currency`. | The seller's revenue for impressions where the seller payment is transacted directly between this buyer-seller pair and not through Xandr, per impression, in the buyer's selected currency. For a list of supported currencies, see  [Supported Currencies](supported-currencies.md). |
| `seller_ecpm_seller_curr` | money | `(seller_revenue / imps_delivered) * 1000, expressed in the seller's currency` | The seller's revenue expressed in eCPM, in the seller's selected currency. For a list of supported currencies, see  [Supported Currencies](supported-currencies.md). |

## Example

### Create the JSON-formatted report request

The JSON file should include the `report_type` `"seller_invoice_report"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filters for specific dimensions, define granularity (year, month, day), and specify the `format` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

``` 
$ cat report {
            "report": { "report_type": "seller_invoice_report", "timezone": "PST",
            "report_interval": "last_7_days", "name": "SSP Monthly Buyer Report", "columns": [
            "day", "seller_member", "publisher_id", "publisher_name", "publisher_code",
            "buyer_member_id", "buyer_member_name", "imps", "imps_delivered", "seller_revenue" ] }
            }
```

> [!NOTE]
> To order by day, insert this object into your JSON file after the "columns" array: `"orders": ["day"]`

### `POST` the request to the Reporting Service

``` 
$ curl -b cookies -c cookies
            -X POST -d @report 'https://api.appnexus.com/report' {
            "response": { "status": "OK", "report_id": "bfe2ba2ea54a51115db942d591a7b5d9" }
            }
```

### `GET` the report status from the Report Service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `{{execution_status}}`is `"ready"`. Then use the \*report-download\* service to save the report data to a file, as described in the next step.

``` 
$ curl -b cookies -c
            cookies 'https://api.appnexus.com/report?id=bfe2ba2ea54a51115db942d591a7b5d9' { "response":{ "status":"OK",
            "report":{ "name":null, "created_on":"2010-05-25 19:19:53", "url":
            "report-download?id=bfe2ba2ea54a51115db942d591a7b5d9" }, "execution_status":"ready" }
            }
```

### `GET` the report data from the Report Download Service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the \*report-download\* service. You can find the service and Report ID in the `{{url}}` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the "format" that you specified in your initial `POST`.

- If an error occurs during download, the response header will include an HTTP error code and message. Use `{{-i}}` or `{{-v}}` in your call to expose the response header.
- Use the ID that was given in the response from when you initially posted the report.

``` 
$ curl -b cookies -c cookies
                  'https://api.appnexus.com/report-download?id=bfe2ba2ea54a51115db942d591a7b5d9' >
               report.csv
```

## Schedule a frequently run report

You can schedule reports that you would like to pull regularly. See the [Saved Report Service](saved-report-service.md) for more information.

## Related topics

- [Report Service](report-service.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Platform Seller Report](platform-seller-report.md)
- [Inventory Availability Reporting](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
- [Saved Report Service](saved-report-service.md)
