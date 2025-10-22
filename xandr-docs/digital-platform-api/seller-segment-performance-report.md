---
title: Digital Platform API - Seller Segment Performance Report
description: Use the Seller Segment Performance Report to track targeted segments' impact on overall performance and transacted impressions to understand usage per segment.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Seller Segment Performance report

The Seller Segment Performance Report provides sellers insights into how their targeted segments are contributing to the overall performance of their line items. The report provides data on all targeted segments (includes and excludes) that contributed towards transacted impressions.This reporting helps sellers in the following ways:

- by providing data on the usage per segment, so they can understand how often they used each segment and thus enable them to bill their data providers and/or advertisers appropriately

- by providing data of performance per segment, so they can analyze which segments are performing well or not well and optimize appropriately

- facilitating data clearing, so that instead of them being responsible for billing their data providers each month, Xandr can do it for them.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_hour
- last_48_hours
- today
- yesterday
- last_7_days
- month_to_date
- quarter_to_date
- last_month
- last_30_days

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 100 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `bidder_id` | int | Yes | `99000` | The ID of the bidder associated with the impression. |
| `bidder_name` | string | No | `"123.com"` | The name of the bidder associated with the impression. |
| `bidder` | string | No | `"123.com (99000)"` | The name and ID of the bidder associated with the impression. |
| `buyer_member_id` | int | Yes | `11100` | The ID of the buyer who buys the impression. |
| `buyer_member_name` | string | No | `"Accenture LLP"` | The name of the buyer who buys the impression. |
| `buyer_member` | string | No | `"Accenture LLP (11100)"` | The name and ID of the buyer who buys the impression. |
| `deal_id` | int | Yes | `165888` | The ID of the deal associated with the transaction for the impression. |
| `deal_name` | string | No | `"5StarsCine"` | The name of the deal associated with the transaction for the impression. |
| `deal` | string | No | `"5StarsCine (165888)"` | The name and ID of the deal associated with the transaction for the impression. |
| `curator_member_id` | int | Yes | `123` | Member ID of the curator account. |
| `curator_member_name` | string | No | `"My Account"` | Member name of the curator account. |
| `day` | date | Yes | `"2020-02-01"` | The day of the auction |
| `device_type` | string | Yes | `"desktops & laptops"` | Device type on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"` |
| `device_type_id` | int | Yes | `1` | Device type ID on which the impression was served. Possible values are:<br>`0` (other devices)<br>`1` (desktops & laptops)<br>`2` (mobile phones)<br>`3` (tablets)<br>`4` (tv)<br>`5` (game consoles)<br>`6` (media players)<br>`7` (set top box) |
| `device_type_name` | string | Yes | `"desktops & laptops"` | Device type name on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"` |
| `geo_country_code` | string | Yes | `"US"` | The country/region code in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. |
| `geo_country_name` | string | No | `"United States"` | The country/region name in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. |
| `hour` | date | Yes | `"2020-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `media_type` | string | No | `"banner"` | The media type associated with the creative that served on an impression. Possible values are:<br> - `"banner"`<br> - `"pop"`<br> - `"interstitial"`<br> - `"video"`<br> - `"text"`<br> - `"expandable"`<br> - `"skin"`<br> - `"facebook"`<br> - `"image and text"`<br> - `"high impact"`<br> - `"native"`<br> - `"audio"`<br> - `"Unknown"` |
| `media_type_id` | int | Yes | `1` | Media type ID associated with the creative that served on this impression. Possible values are:<br>`1` (banner)<br>`2` (pop)<br>`3` (interstitial)<br>`4` (video)<br>`5` (text)<br>`6` (expandable)<br>`8` (skin)<br>`9` (facebook)<br>`10` (image and text)<br>`11` (high impact)<br>`12` (native)<br>`13` (audio) |
| `month` | date | Yes | `"2020-02"` | The month of the auction. |
| `segment_id` | int | Yes | `123456` | The ID of a segment that targeted the impression. |
| `segment_name` | string | No | `"That Segment"` | The name of a segment that targeted the impression. |
| `segment` | string | No | `"That Segment(123456)"` | The name and ID of a segment that targeted the impression. |
| `segment_owner_id` | int | Yes | `789` | Member ID of the segment owner that owns the targeted segment(s). |
| `segment_owner_name` | string | No | `"That Segment Owner"` | Member name of the segment owner that owns the targeted segment(s). |
| `seller_member_id` | int | Yes | `4567` | Member ID of the seller of the impression. |
| `seller_member_name` | string | No | `"That Seller"` | Member name of the seller of the impression. |
| `seller_member` | string | No | `"That Seller"` | Member ID and name of the seller of the impression. |
| `supply_type_id` | int | Yes | `0` | ID of the supply type of the ad that was rendered. Possible values are:<br>`0` (web)<br>`1` (mobile_web)<br>`2` (mobile_app) |
| `supply_type_name` | string | Yes | `"web"` | Name of the supply type of the ad that was rendered. Possible values are:<br> - `"web"`<br> - `"mobile_web"`<br> - `"mobile_app"` |
| `targeting_type` | string | Yes | `"Inclusion"` | Whether the segment contributed to the line item targeting by being included or excluded. Possible values are:<br> - `"Inclusion"`<br> - `"Exclusion"` |
| `publisher_id` | int | Yes | `1825156` | The ID of the publisher on whose inventory this impression occurrs. |
| `publisher_name` | string | No | `"12up.com"` | The name of the publisher on whose inventory this impression occurrs. |
| `publisher` | string | No | `"12up.com (1825156)"` | The name and ID of the publisher on whose inventory this impression occurred. |
| `line_item_id` | int | Yes | `314` | The ID of the line item associated with the impression. |
| `line_item_name` | string | No | `"Kansas City Winter Commuters"` | The name of the line item associated with the impression. |
| `line_item` | string | No | `"Kansas City Winter Commuters (314)"` | The name and ID of the line item associated with the impression. |
| `sales_channel` | string | Yes | `"Managed"` | The sales channels of the line item for the impression. For example, `Managed`, `Open Exchange`, `Curated`, `Deals`, `Programmatic Guaranteed`, etc. |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `targeted_revenue` | money | `48.4185` | Targeted revenue of the segment which is sum of booked revenue and seller revenue. |
| `targeted_revenue_ecpm` | money | `2.5588` | The targeted revenue, expressed as eCPM. For definitions of eCPM and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| `targeted_revenue_ecpc` | money | `2.5588` | The targeted revenue, expressed as eCPC. For definitions of eCPC and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| `targeted_revenue_ecpa` | money | `2.5588` | The targeted revenue, expressed as eCPA. For definitions of eCPA and other terms, see the [Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). |
| `targeted_impressions` | int | `18922` | The number of transacted impressions that the segment targeted. |
| `targeted_clicks` | int | `17000` | The number of transacted clicks that the segment targeted. |
| `targeted_view_measured_impressions` | int | `17867` | The number of transacted impressions that Xandr measured viewability on that the segment targeted. |
| `targeted_viewable_impressions` | int | `14135` | The number of viewed impressions that the segment targeted. |
| `targeted_conversions` | int | `11211` | The number of targeted conversions of a segment. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"seller_segment_performance"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat curator_segment_performance

{
    "report": {
        "report_type": "seller_segment_performance",
        "columns": [
            "deal_id",
            "deal_name",
            "segment_id",
            "segment_name",
            "targeting_type",
            "targeted_impressions",
            "targeted_revenue"
        ],
        "report_interval": "today",
        "format": "csv"
    }
}
```

### `POST`the request to the report service

```
$ curl -b cookies -X POST -d @seller_segment_performance 'https://api.appnexus.com/report'

{
    "response": {
        "status": "OK",
        "report_id": "a2c95fcff2d8759e69cec123364f9b32"
    }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=a2c95fcff2d8759e69cec123364f9b32'
{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2020-09-04 12:46:08",
            "json_request": "{\"report\":{\"report_type\":\"seller_segment_performance\",\"columns\":[\"deal_id\",\"deal_name\",\"segment_id\",\"segment_name\",\"targeting_type\",\"targeted_impressions\",\"targeted_revenue\"],\"report_interval\":\"today\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"curator_member_id\":\"12025\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1599264000,\"start_date\":1599177600,\"user_id\":\"123456\"}",
            "url": "report-download?id=a2c95fcff2d8759e69cec123364f9b32"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=a2c95fcff2d8759e69cec123364f9b32' > /tmp/seller_segment_performance.csv
```
