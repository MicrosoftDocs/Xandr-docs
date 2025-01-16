---
title: Digital Platform API - Identifiers - ID Combinations Report
description: Explore the ID Combinations Identifiers report, providing insights on the breakout and overlap of cookies and IDs across impressions.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Identifiers - ID Combinations report

Platform Reporting on Industry IDs provides an insight into the delivery, performance and unique reach across Industry IDs (RampID, NetID, UID2) alongside device based IDs. The Identifiers-ID Combination Report allows you to understand the breakout and overlap of cookies and IDs across impressions. This view allows you to view impressions and associated metrics per combination of ID types.

You can use the report to determine the following:

- The type of IDs present on your purchased impressions.
- The clear distribution of impressions.
- The performance metrics for various combinations of ID types.

> [!NOTE]
> This report does not generate any information on uniques.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_7_days
- month_to_date
- quarter_to_date
- lifetime

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

## Data retention period

This report's data is retained for 90 days. For more information about how quickly reporting data is processed, see [Availability of Reporting Data](../monetize/availability-of-reporting-data.md).

## Dimensions

> [!IMPORTANT]
>
> - The **Filter?** column shows whether a dimension can be used as a filter as well as being used to group by.
> - Some dimensions have attributes. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: `"Dimension_Name:Attribute_Name"`.
> - For all revenue fields, the currency is defined by the `Buying Currency` field.

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `advertiser_currency` | string | Yes | `"USD"` | The advertiser currency. |
| `advertiser_exchange_rate` | numeric | No | `3.4` | The advertiser exchange rate |
| `advertiser_id` | int | Yes | `123` | The id of the advertiser for which impression was purchased. |
| `advertiser_name` | string | no | `"My advertiser"` | The name of the advertiser for which impression was purchased. |
| `bidder` | string | Yes | `"My bidder(123)"` | The bidder that bought the impression. |
| `billing_period_id` | int | No | `1234` | The insertion order's billing period. |
| `buyer` | string | Yes | `"My Network"` | The buyer of the impression. |
| `creative_id` | int | Yes | `123` | The creative that we're reporting on the frequency and/or recency of. |
| `datetime` | time | No | `"2010-02-01 06:00:00"` | Time is rounded by the hour. |
| `deal_alias` | string | No | `"My deal"` | The Deal Alias associated with the given Deal. |
| `deal_id` | int | Yes | `123` | The Deal delivered against. |
| `device_type` | string | Yes | `"tablet"` | The device type on which creative is displayed to the end-users such as mobiles, laptops, tablets, etc. |
| `flight_id` | int | No | `123456` | The start and end date of flight in a billing period under an insertion order. |
| `geo_country` | string | Yes | `"US"` | The targeted country/region of the advertisement. |
| `id_types` | string | No |  | The individual identifier combinations that are available in the auction. See [possible values](#id_types-possible-values) below. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. |
| `insertion_order` | string | No | `"My Insertion Order"` | The name of insertion order under which the impression was purchased. |
| `insertion_order_id` | int | Yes | `648359` | The id of insertion order under which the impression was purchased. |
| `line_item` | int | Yes | `12345` | The id of line item under which the impression was purchased. For more information about line items, see [Working with Line Items](../monetize/working-with-line-items.md). |
| `line_item_name` | string | No | `"My Line Item"` | The name of line item under which the impression was purchased. For more information about line items, see [Working with Line Items](../monetize/working-with-line-items.md). |
| `media_type` | int | No | - `"Banner"`<br>- `"Pop"`<br>- `"Interstitial"`<br>- `"Video"`<br>- `"Text"`<br>- `"Expandable"`<br>- `"Skin"` | The media type is the general display style of the creative. |
| `publisher` | string | No | `"Newscorp (321)"` | The publisher on whose inventory this impression occurred. |
| `placement` | string | No | `"Ivillage 160x600 (456)"` | The name and ID of the placement through which this impression occurred. |
| `placement_group` | string | Yes | `My Placement Group` | The placement group name. |
| `seller` | string | Yes |  | The seller of the impression. |
| `split_id` | int | No | `1234` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| `split_name` | string | No | `"My Split"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any rows with a campaign name, the Split column (if included) will be null. |
| `supply_type` | string | Yes | `"web"` | The supply type is the method of rendering the creative on a device. For example, for mobiles or tablets, the supply type is a mobile app whereas for laptops or desktops it is a web app. |

### `id_types` possible values

| Dimension Options | Rules |
|:---|:---|
| `UID2` | UID2 is available on the ad request. |
| `RampID` | Ramp ID is available on the ad request. |
| `NetID` | Net ID is available on the ad request. |
| `Device ID` | Traditional device ID and cookie available on the ad requests. |
| `UID2-RampID` | Both UID2 and Ramp ID are available on the ad request. |
| `UID2-NetID` | Both UID2 and NetID are available on the ad request. |
| `RampID-NetID` | Both RampID and NetID are available on the ad request. |
| `UID2-Cookie/Device ID` | Both UID2 and Cookie/Device ID are available on the ad request. |
| `RampID-Cookie/Device ID` | Both RampID and Cookie/Device ID are available on the ad request. |
| `NetID-Cookie/Device ID` | Both NetID and Cookie/Device ID are available on the ad request. |
| `UID2-RampID-NetID` | UID2, RampID and NetID are available on the ad request. |
| `UID2-RampID-Cookie/Device ID` | UID2, RampID and Cookie/Device ID are available on the ad request. |
| `UID2-NetID-Cookie/Device ID` | UID2, NetID and Cookie/Device ID are available on the ad request. |
| `RampID-NetID-Cookie/Device ID` | RampID, NetID and Cookie/Device ID are available on the ad request. |
| `Device ID` (or Cookie Only) | Traditional device ID and cookie available on the ad requests. |
| `UID2-RampID-NetID-Cookie` | UID2, RampID, NetID and Cookie/Device ID are available on the ad request. |
| `No ID` | No industry ID or ANID at time of auction or opt out. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Filter? | Formula | Example | Description |
|:---|:---|:---|:---|:---|:---|
| `media_cost` | money | Yes | MEDIA_COST_DOLLARS | `$450.00` | **Default:** `True`<br>The total media cost. |
| `imps` | int | Yes |  | `125,000` | **Default:** `True`<br>The total number of impressions. |
| `clicks` | int | Yes |  | `123456` | **Default:** `True`<br>The total number of clicks. |
| `reseller_revenue` | money | Yes | reseller_revenue | `0` | The revenue from resold impressions. This is only populated when the impression type is resold. |
| `revenue` | money | Yes | booked revenue + reseller revenue |  | The sum of booked revenue and reseller revenue. |
| `booked_revenue_cpm` |  |  | booked revenue / imps * 1000 |  | The booked revenue per 1000 impressions. |
| `resold_cpm` |  |  | reseller_revenue / imps * 1000 |  | The resold revenue per 1000 impressions. |
| `media_cost_cpm` |  |  |  |  | The media cost per 1000 impressions. |
| `revenue_cpm` |  |  | reseller_revenue + booked_revenue / imps * 1000 |  | The revenue per 1000 impressions. |
| `eCPC` | money | Yes | (MEDIA_COST_DOLLARS / CLICKS) | `$1.4` | **Default:** `True`<br>The average CPC. |
| `eCTR` | double | Yes | (eCTR: clicks / total imps) | `0.0002` | **Default:** `True`<br>The average Click-Through Rate. |

## Examples

The JSON file should include the `report_type` of `seller_slot_video_report_network`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

### Create the JSON report request

```
$ cat identity_reporting_combination
  
{
    "report": {
        "report_type":"identity_reporting_combination",
        "columns": [
                            "id_type_combinations",
                            "imps",
                            "clicks",
                            "cost",
                            "eCPC",
                            "eCPM",
                            "eCTR"
                        ],
        "report_interval": "last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the JSON request to get back a report ID

```
$ curl -b cookie -c cookie -s -d  @identity_reporting_combination "https://api.appnexus.com/report"
{
    "response": {
        "report_id": "52bf975d78de81b6f73035424d3d7b3d",
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
            "instance": "49.bm-report-processor.prod.nym2",
            "version": "1.73.242",
            "time": 895.90907096863,
            "start_microtime": 1688482631,
            "warnings": [],
            "api_cache_hit": "0",
            "output_term": "report_id"
        }
    }
}
```

### Retrieve the status of the report

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookie -c cookie -s "https://api.appnexus.com/report?id=52bf975d78de81b6f73035424d3d7b3d"
{
    "response": {
        "status": "OK",
        "report": {
            "id": "52bf975d78de81b6f73035424d3d7b3d",
            "name": "",
            "created_on": "2023-07-04 14:57:11",
            "cache_hit": false,
            "fact_cache_hit": false,
            "fact_cache_error": "",
            "json_request": "{\"report\":{\"report_type\":\"identity_reporting_combination\",\"columns\":[\"id_type_combinations\",\"imps\",\"clicks\",\"cost\",\"eCPC\",\"eCPM\",\"eCTR\"],\"report_interval\":\"last_48_hours\",\"format\":\"csv\",\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"filters\":[{\"member_id\":\"668\"}],\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1688479200,\"start_date\":1688306400,\"user_id\":\"200537\"}",
            "header_info": "Report type: identity_reporting_combinations\nReport ID: 52bf975d78de81b6f73035424d3d7b3d\nRun at: 2023-07-04 15:00:03 UTC\nRequested Start date: 2023-07-02 15:00:00 UTC\nRequested End date: 2023-07-04 15:00:00 UTC\nTimezone: UTC\n",
            "user_id": "200537",
            "member_id": 0,
            "bidder_id": 0,
            "entity_id": 0,
            "row_count": 47,
            "report_size": 5795,
            "started_on": null,
            "finished_on": null,
            "query_time": null,
            "url": "report-download?id=52bf975d78de81b6f73035424d3d7b3d"
        },
        "execution_status": "ready",
...
```

### Download the report

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

```
curl -b cookie -c cookie -s "https://api.appnexus.com/report-download?id=52bf975d78de81b6f73035424d3d7b3d" > identity_reporting_combination.csv
```

> [!NOTE]
>
> - If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.
> - There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
