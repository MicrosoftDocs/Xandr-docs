---
title: Digital Platform API - Curator Segment Performance Report
description: Use the Curator Segment Performance report to get curators insights into how their targeted segments are contributing to the overall performance of their curated deals.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Curator Segment Performance report

> [!NOTE]
> This report is only available to curators.

The Curator Segment Performance Report provides curators insights into how their targeted segments are contributing to the overall performance of their curated deals. The report provides data on all targeted segments (includes and excludes) that contributed towards transacted impressions. For curators, this includes all curated deal activity.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [Example](./report-service.md) below.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- last_hour
- last_48_hours
- today
- yesterday
- last_7_days
- month_to_date
- quarter_to_date
- last_month
- last_30_days

### Data retention period

Data in this report is retained for 429 days.

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `bidder_id` | int | Yes | `456` | ID of the bidder who bought on the transaction |
| `bidder_name` | string | No | `"That Bidder"` | Name of the bidder who bought on the transaction |
| `buyer_member_id` | int | Yes | `789` | Member ID of the buyer who bought on the transaction |
| `buyer_member_name` | string | No | `"That Buyer"` | Member name of the buyer who bought on the transaction |
| `curated_deal_id` | int | Yes | `123` | Curated deal ID |
| `cureated_deal_name` | string | No | `"My Deal Name"` | Curated deal name |
| `curated_line_item_id` | int | Yes | `123` | Line Item ID of the curator member object that owns the deal line item associated with the curated deal |
| `curated_line_item_name` | string | No | `"My Curated LI"` | Line Item name of the curator member object that owns the deal line item associated with the curated deal |
| `curator_member_id` | int | Yes | `123` | Member ID of the curator account |
| `curator_member_name` | string | No | `"My Account"` | Member name of the curator account |
| `day` | date | Yes | `"2020-02-01"` | The day of the auction |
| `device_type` | string | Yes | `"desktops & laptops"` | Device type on which the impression was served. Possible values are:<br>- `"desktops & laptops"`<br>- `"tablets"`<br>- `"mobile phones"`<br>- `"tv"`<br>- `"game consoles"`<br>- `"set top box"`<br>- `"media players"`<br>- `"other devices"` |
| `device_type_id` | int | Yes | `1` | Device type ID on which the impression was served. Possible values are:<br>`0` (other devices)<br>`1` (desktops & laptops)<br>`2` (mobile phones)<br>`3` (tablets)<br>`4` (tv)<br>`5` (game consoles)<br>`6` (media players)<br>`7` (set top box) |
| `device_type_name` | string | Yes | `"desktops & laptops"` | Device type name on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br>- `"tablets"`<br>- `"mobile phones"`<br>- `"tv"`<br>- `"game consoles"`<br>- `"set top box"`<br>- `"media players"`<br>- `"other devices"` |
| `geo_country_code` | string | Yes | `"US"` | The country code in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. |
| `geo_country_name` | string | No | `"United States"` | The country/region name in which the impression took place. For impression requests for which Xandr received no indication that the ad was rendered (i.e., non-transacted), country/region information is not provided. |
| `hour` | date | Yes | `"2020-02-01 06:00:00"` | The hour of the auction<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `media_type` | string | No | `"banner"` | Media type associated with the creative that served on this impression. Possible values are:<br>- `"banner"`<br>- `"pop"`<br>- `"interstitial"`<br>- `"video"`<br>- `"text"`<br>- `"expandable"`<br>- `"skin"`<br>- `"facebook"`<br>- `"image and text"`<br>- `"high impact"`<br>- `"native"`<br>- `"audio"`<br>- `"Unknown"` |
| `media_type_id` | int | Yes | `1` | Media type ID associated with the creative that served on this impression. Possible values are:<br>`1` (banner)<br>`2` (pop)<br>`3` (interstitial)<br>`4` (video)<br>`5` (text)<br>`6` (expandable)<br>`8` (skin)<br>`9` (facebook)<br>`10` (image and text)<br>`11` (high impact)<br>`12` (native)<br>`13` (audio) |
| `media_type_name` | string | No | `"banner"` | Media type name associated with the creative that served on this impression. Possible values are:<br>- `"banner"`<br>- `"pop"`<br>- `"interstitial"`<br>- `"video"`<br>- `"text"`<br>- `"expandable"`<br>- `"skin"`<br>- `"facebook"`<br>- `"image and text"`<br>- `"high impact"`<br>- `"native"`<br>- `"audio"`<br>- `"Unknown"` |
| `month` | date | Yes | `"2020-02"` | The month of the auction |
| `segment_id` | int | Yes | `123456` | ID of a segment that targeted the impression.<br><br>**Note**: Curators running this report will only see segments that they assign to their deal line item objects. For example, a curator pulling this report will not see segments tied to a third-party seller deal that they are buying. |
| `segment_name` | string | No | `"That Segment"` | Name of a segment that targeted the impression.<br><br>**Note**: Curators running this report will only see segments that they assign to their deal line item objects. For example, a curator pulling this report will not see segments tied to a third-party seller deal that they are buying. |
| `segment_owner_id` | int | Yes | `789` | Member ID of the segment owner that owns the targeted segment(s) |
| `segment_owner_name` | string | No | `"That Segment Owner"` | Member name of the segment owner that owns the targeted segment(s) |
| `seller_member_id` | int | Yes | `4567` | Member ID of the seller where the curated transaction served |
| `seller_member_name` | string | No | `"That Seller"` | Member name of the seller where the curated transaction served |
| `supply_strategy` | string | Yes | `"Deals"` | Distinguishes between the different supply channels used to source impressions for the curator.<br><br>**Note**: Only `"Open Exchange"` and `"Deals"` are currently relevant for the curator. |
| `supply_type_id` | int | Yes | `0` | ID of the supply type of the ad that was rendered. Possible values are:<br>`0` (web)<br>`1` (mobile_web)<br>`2` (mobile_app) |
| `supply_type_name` | string | Yes | `"web"` | Name of the supply type of the ad that was rendered. Possible values are:<br>- `"web"`<br>- `"mobile_web"`<br>- `"mobile_app"` |
| `targeting_type` | string | Yes | `"Inclusion"` | Whether the segment contributed to the line item targeting by being included or excluded. Possible values are:<br>- `"Inclusion"`<br>- `"Exclusion"` |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `targeted_curator_media_cost` | money | `31.513709` | The amount of spend (transacted via impressions targeted by the segment) a curator sent to exchange sellers net of curator fees and margins, if applicable |
| `targeted_curator_media_cost_ecpm` | money | `1.6654` | The amount of spend (transacted via impressions targeted by the segment, expressed as an eCPM based on transacted impressions) a curator sent to exchange sellers net of curator fees and margins, if applicable |
| `targeted_curator_revenue` | money | `48.4185` | The amount of spend (transacted via impressions targeted by the segment) a buyer sent to the curator net of buyer fees, if applicable |
| `targeted_curator_revenue_ecpm` | money | `2.5588` | The amount of spend (transacted via impressions targeted by the segment, expressed as an eCPM based on targeted impressions) a buyer sent to the curator net of buyer fees, if applicable |
| `targeted_impressions` | int | `18922` | The number of transacted impressions that the segment targeted |
| `targeted_view_measured_impressions` | int | `17867` | The number of transacted impressions that Xandr measured viewability on that the segment targeted |
| `targeted_viewable_impressions` | int | `14135` | The number of viewed impressions that the segment targeted |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"curator_segment_performance"`, as well as the `columns` (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat curator_segment_performance

{
    "report": {
        "report_type": "curator_segment_performance",
        "columns": [
            "curated_deal_id",
            "cureated_deal_name",
            "segment_id",
            "segment_name",
            "targeting_type",
            "targeted_impressions",
            "targeted_curator_revenue"
        ],
        "report_interval": "today",
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @curator_segment_performance 'https://api.appnexus.com/report'

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
            "json_request": "{\"report\":{\"report_type\":\"curator_segment_performance\",\"columns\":[\"curated_deal_id\",\"cureated_deal_name\",\"segment_id\",\"segment_name\",\"targeting_type\",\"targeted_impressions\",\"targeted_curator_revenue\"],\"report_interval\":\"today\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"curator_member_id\":\"12025\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1599264000,\"start_date\":1599177600,\"user_id\":\"123456\"}",
            "url": "report-download?id=a2c95fcff2d8759e69cec123364f9b32"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=a2c95fcff2d8759e69cec123364f9b32' > /tmp/curator_segment_performance.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
