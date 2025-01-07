---
title: Platform Seller Report
description: In this article, find information about the Platform seller report, the metrics and dimensions associated with it, along with an example.
ms.date: 10/28/2023
---

# Platform seller report

The **Platform Seller Report** can be used to invoice buyers or reconcile internal transaction records. Using this report, you can view transaction information at the tag level.

For instructions on retrieving this report, see the [Example](#example) below.

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
|---|---|---|---|---|
| `bidder` | string | No | No | **Deprecated.** |
| `bidder_id` | int | Yes | Yes | The internal ID of the bidder. |
| `bidder_name` | string | No | No | The display name of the bidder. |
| `buyer_member` | string | No | No | **Deprecated.** |
| `buyer_member` | string | No | No | The display name of the buying member followed by the ID (Xandr format). |
| `buyer_member_id` | int | Yes | Yes | The internal ID of the buying member. |
| `buyer_member_name` | string | No | No | The display name of the buying member. |
| `buyer_member_name` | string | No | No | The display name of the buyer member. |
| `cleared_direct` | int | No | Yes | If this is set to 1, then the impression was successfully served on direct inventory. Possible values: <br> - `0` = not direct inventory <br> - `1` = direct inventory |
| `day` | date | Yes | Yes | Day. |
| `gender` | string | No | Yes | The gender of the user. |
| `geo_country` | string | No | Yes | The display name of the country or region followed by the ID (Xandr format). |
| `geo_country_name` | string | No | No | Country or region. |
| `hour` | date | Yes | Yes | The hour of the auction. <br><br> **Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `imp_type` | string | No | Yes | The type of impression served. Possible values: <br> - `1` = blank <br> - `2` = PSA <br> - `3` = default error <br> - `4` = default <br> - `5` = kept <br> - `6` = resold <br> - `7` = RTB <br> - `8` = PSA resulting from a default error <br> - `9` = external impression <br> - `10` = external click |
| `is_delivered` | boolean | No | Yes | If true, the impression was served successfully. |
| `is_dw` | boolean | No | Yes | If true, the impression was served by Xandr. |
| `month` | time | Yes | No | Month. |
| `price_bucket_id` | int | Yes | No | The ID of the price bucket. For more information about price buckets, see the description of the `price_buckets` field on the [Member Service](member-service.md). |
| `publisher` | string | No | No | **Deprecated.** |
| `publisher_code` | string | No | No | The custom code for the publisher, entered to correspond to the publisher code within the external system. |
| `publisher_id` | int | Yes | Yes | The internal ID of the publisher. |
| `publisher_name` | string | No | No | The display name of the publisher. |
| `seller_currency` | string | No | Yes | The seller member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `seller_member` | string | No | No | **Deprecated.** |
| `seller_member_id` | int | Yes | Yes | The internal ID of the member. |
| `seller_member_name` | string | No | No | The display name of the seller member. |
| `site` | string | No | No | **Deprecated.** |
| `site_code` | string | No | No | The custom code for the site, entered to correspond to the site code within the external system. |
| `site_id` | int | Yes | Yes | The internal ID of the site. |
| `site_name` | string | No | No | The display name of the site. |
| `size` | string | No | No | The size of the creative. |
| `supply_type` | string | No | No | The type of inventory. Possible values: <br> - `"web"` <br> - `"mobile_web"` <br> - `"mobile_app"` |
| `tag` | string | No | No | **Deprecated.** |
| `tag_id` | int | Yes | No | The ID of the tag. |
| `tag_name` | string | No | No | The display name of the tag. |
| `year` | date | Yes | Yes | Year. |

## Metrics

| Column | Type | Formula | Description |
|---|---|---|---|
| `auction_service_deduction` | money | `auction_service_deduction` | The deduction on RTB bought impressions specified in the buyer member's contract. For example, with a 10% deduction, if they budget $1000 for their campaign, we take $100 from that, leaving the buyer with $900 that is used to purchase inventory from the seller. |
| `auction_service_fees` | money | `auction_service_fees` | The fee charged on RTB bought impressions specified in the buyer member's contract. For example, with a 10% fee, if the buyer spends $1000 on inventory we then charge them a $100 fee. |
| `buyer_spend` | money | `buyer_spend` | The amount the buyer pays for the cost of media. |
| `clear_fees` | money | `clear_fees` | The fee specified in the buyer member's contract charged on impressions bought from an external or partner seller. |
| `clicks` | int | `clicks` | The total number of clicks. |
| `creative_overage_fees` | money | `creative_overage_fees` | The charge for hosted creatives that exceed the creative size limit specified in the buyer member's contract. |
| `imps` | int | `imps` | The total number of impressions (served and resold). |
| `imps_delivered` | int | `imps_delivered` | The total number of impressions served successfully. |
| `imps_not_delivered` | int | `imps_not_delivered` | The total number of impressions where someone other than Xandr served the impression. |
| `imps_viewed` | int | `imps_viewed` | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `seller_ecpm` | money | ( `seller_revenue` / `imps_delivered` ) * 1000 | The seller's revenue expressed in eCPM. |
| `seller_ecpm_seller_curr` | money | (`seller_revenue` / `imps_delivered`) * 1000, expressed in the seller's currency. | The seller's revenue expressed in eCPM, in the seller's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `seller_revenue` | money | `seller_revenue` | The seller's revenue per impression. |
| `seller_revenue_seller_curr` | money | `seller_revenue`, expressed in the seller's currency. | The seller's revenue per impression in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `view_measurable_rate` | double | `view_measurable_rate` | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `view_measured_imps` | int | `view_measured_imps` | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `view_rate` | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |

## Visible to administrators only

| Column | Type | Formula | Description |
|---|---|---|---|
| `forex_allowance` | money | `forex_allowance` | A foreign currency buffer allowance. |
| `discrepancy_allowance` | money | `discrepancy_allowance` | The deduction on RTB sold impressions specified in the seller member's contract. This is determined based on past discrepancies between what Xandr and the supply partner recorded as won impressions. |

## Example

### Create the JSON-formatted report request

The JSON file should include the `report_type "platform_buyer"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter specific dimensions, define granularity (year, month, day), and specify the format in which the data should be returned (csv, excel, or html). For a full explanation of fields that can be included in the JSON file, see the [Report Service](platform-seller-report.md).

```
$ cat report
{
    "report": {
        "report_type": "platform_seller",
        "timezone": "PST",
        "report_interval": "last_7_days",
        "name": "SSP Monthly Buyer Report",
        "columns": [
            "day",
            "seller_member",
            "publisher_id",
            "publisher_name",
            "publisher_code",
            "buyer_member_id",
            "buyer_member_name",
            "imps",
            "imps_delivered",
            "seller_revenue",
            "buyer_spend"
        ]
    }
}
```

> [!TIP]
> To order by day, insert this object into your JSON file after the "columns" array:
>
> ```
> "orders": ["day"]
> ```
>

### POST the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @report 'https://api.adnxs.com/report'
{
  "response": {
    "status": "OK",
    "report_id": "bfe2ba2ea54a51115db942d591a7b5d9",
  }
}
```

### GET the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `"execution_status"` is `"ready"`. Then use the report-download service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/report?id=bfe2ba2ea54a51115db942d591a7b5d9'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "url": "report-download?id=bfe2ba2ea54a51115db942d591a7b5d9"
      },
      "execution_status":"ready"
   }
}
```

### GET the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the report-download service. You can find the service and Report ID in the "url" field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the "format" that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use "-i" or "-v" in your call to expose the response header.
>
> ```
> $ curl -b cookies -c cookies 'https://api.adnxs.com/report?id=bfe2ba2ea54a51115db942d591a7b5d9' > report.csv
> ```
>
> Use the id that was given in the response from when you initially posted the report.

## Schedule a frequently run report

You can schedule reports that you would like to pull regularly. See the [Saved Report Service](saved-report-service.md) for more information.

## Related topics

- [Report Service](report-service.md)
- [Completed Creative Audits Report](completed-creatives-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Inventory Availability Reporting](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
- [Saved Report Service](saved-report-service.md)
