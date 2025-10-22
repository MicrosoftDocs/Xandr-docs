---
title: Bidder Platform Buyer Report
description: Explore this article to understand the Bidder Platform Buyer report, including its metrics, dimensions, examples, and how to run a report.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder Platform Buyer report

The Bidder Platform Buyer Report provides granular transaction information to buyers (down to the tag level). For instructions on retrieving this report, see the [Examples](#examples) below.

> [!TIP]
> Need more than 90 days of data?
>
> The `bidder_platform_buyer` and `platform_seller` types pull from tables that store the last 90 days worth of data. For data beyond the past 90 days, use the `buyer_platform_billing` and `seller_platform_billing` report types.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

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
- `mtd`
- `month_to_yesterday`

## Dimensions

| Column | Type | Filter? | Description |
|:---|:---|:---|:---|
| `month` | time | Yes | The month of the year in which the event being counted occurred. |
| `day` | date | Yes | The day of the year in which the event being counted occurred. |
| `hour` | date | Yes | The hour in which the event being counted occurred. |
| `year` | date | Yes | The year in which the event being counted occurred. |
| `buyer_member_id` | int | Yes | The internal ID of the buyer member. |
| `seller_member_id` | int | Yes | The internal ID of the seller member. |
| `seller_member_name` | string | Yes | The display name of the seller member. |
| `seller_member` | string | Yes | **Deprecated**. |
| `tag_id` | int | Yes | The ID of the tag. |
| `publisher_id` | int | Yes | The internal ID of the publisher. |
| `publisher_name` | string | Yes | The display name of the publisher. |
| `publisher` | string | Yes | **Deprecated**. |
| `size` | string | Yes | The size of the creative. |
| `geo_country` | string | Yes | The display name of the country or region followed by the ID (Xandr format). |
| `geo_country_name` | string | Yes | The country or region  where the event being counted (e.g., click) occurred. |
| `content_category_id` | int | Yes | The ID of the content category that the inventory where the impression occurred was associated with. For more information about content categories, see the [Content Category Service](content-category-service.md). |
| `content_category_name` | string | Yes | The name of the content category that the inventory where the impression occurred was associated with. For more information about content categories, see the [Content Category Service](content-category-service.md). |
| `content_category` | string | Yes | **Deprecated**. |
| `imp_type` | string | Yes | The type of impression served. Possible values:<br> - 1 = blank<br> - 2 = PSA<br> - 3 = default error<br> - 4 = default<br> - 5 = kept<br> - 6 = resold<br> - 7 = RTB<br> - 8 = PSA resulting from a default error<br> - 9 = external impression<br> - 10 = external click |
| `creative_id` | int | Yes | The ID of the creative that served on the impression where the "event" you're counting occurred. For more information about creatives, see the [Creative Service](creative-service.md). |
| `creative_name` | string | Yes | The name of the creative that served on the impression where the "event" you're counting occurred. For more information about creatives, see the [Creative Service](creative-service.md). |
| `creative` | string | Yes | **Deprecated**. |
| `bidder_id` | int | Yes | The ID of the bidder that purchased the impression where the "event" you're reporting on occurred. For more information about bidders, see the [Bidder Service](bidder-service.md). |
| `bidder_name` | string | Yes | The name of the bidder that purchased the impression where the "event" you're reporting on occurred. For more information about bidders, see the [Bidder Service](bidder-service.md). |
| `bidder` | string | Yes | **Deprecated**. |
| `site_id` | int | Yes | The internal ID of the site. |
| `site_name` | string | Yes | The display name of the site. |
| `site` | string | Yes | **Deprecated**. |
| `tag_name` | string | Yes | The display name of the tag. |
| `tag` | string | Yes | **Deprecated**. |
| `buyer_currency` | string | Yes | The buyer member's selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `supply_type` | string | No | The type of inventory. Possible values:<br>- `"web"`<br> - `"mobile_web"`<br> - `"mobile_app"` |
| `publisher_code` | string | Yes | The custom code for the publisher, entered to correspond to the publisher code within the external system. |
| `site_code` | string | Yes | The custom code for the site, entered to correspond to the site code within the external system. |
| `buyer_member_name` | string | Yes | The display name of the buyer member. |
| `buyer_member` | string | Yes | **Deprecated**. |
| `buyer_seat_code` | string | Yes | The Custom Buyer Seat ID (submitted by DSP) that was used to bid on the impression. |
| `buyer_seat_name` | string | Yes | The display name for the buyer seat code. |

## Metrics

| Column | Type | Formula | Description |
|:---|:---|:---|:---|
| `imps_bought` | int | `imps_bought` | The total number of impressions purchased successfully. |
| `buyer_spend` | money | `buyer_spend` | The amount the buyer pays for the cost of media. |
| `clicks` | int | `clicks` | The total number of clicks.<br><br>**Note:** Clicks are not logged for external demand partners. |
| `click_rate_sold` | double | (`clicks` / `imps_bought`)  | The "click-through rate", or CTR.<br><br>**Note:** Clicks are not logged for external demand partners. |
| `buyer_ecpm` | money | ( `buyer_spend` / `imps_bought` ) * 1000 | The buyer's cost per impression expressed in [eCPM](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| `buyer_spend_buyer_curr` | money | `buyer_spend`, expressed in the buyer's currency. | The buyer's total spend in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `buyer_ecpm_buyer_curr` | money | `buyer_ecpm`, expressed in the buyer's currency. | The buyer's cost per impression in their selected currency. For a list of supported currencies, see [Supported Currencies](supported-currencies.md). |
| `imps_viewed` | int | `imps_viewed` | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `view_measured_imps` | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `view_rate` | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurable_rate` | double | `view_measurable_rate` | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |

## Examples

### Create the JSON-formatted report request

The JSON file should include the `report_type` `bidder_platform_buyer`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat report
{
    "report": {
        "report_type": "bidder_platform_buyer",
        "timezone": "PST",
        "report_interval": "last_7_days",
        "name": "Example Buyer Report",
        "columns": [
            "day",
            "publisher_id",
            "publisher_name",
            "publisher_code",
            "buyer_member_id",
            "buyer_member_name",
            "buyer_ecpm",
            "buyer_spend"
        ]
    }
}
```

> [!NOTE]
> To order by day, insert this object into your JSON file after the "columns" array:
>
> ```
> "orders": ["day"]
> ```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @report 'https://api.adnxs.com/report'
{
  "response": {
    "status": "OK",
    "report_id": "bfe2ba2ea54a51115db942d591a7b5d9",
  }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

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

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use {{-i}} or {{-v}} in your call to expose the response header.

```
curl -b cookies -c cookies 'https://api.adnxs.com/report-download?id=bfe2ba2ea54a51115db942d591a7b5d9' > report.csv
```

> [!NOTE]
> Use the ID that was given in the response from when you initially posted the report.

## Schedule a frequently run report

You can schedule reports that you would like to pull regularly. For more information, see the [Saved Report Service](saved-report-service.md).

## Related topics

- [Report Service](report-service.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
- [Bidder Platform Buyer Report](bidder-platform-buyer-report.md)
- [Bidder Billing Report API](bidder-billing-report-api.md)
- [Platform Seller Report](platform-seller-report.md)
- [Seller Platform Billing Report](seller-platform-billing-report.md)
- [Inventory Availability Report](inventory-availability-report.md)
- [Reporting Timezones](reporting-timezones.md)
- [Saved Report Service](saved-report-service.md)
