---
title: Digital Platform API - Offline Attribution Report
description: Use the Offline Attribution report to track in-store purchases. It is only available to clients with offline sales attribution enabled for their line items.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Offline Attribution report

The Offline Attribution report is used to analyze your line item's performance in influencing in-store purchases among your target audiences. The Offline Attribution report is only accessible to clients who have Offline Sales Attribution enabled for their line items.

For instructions on retrieving a report, please see [Report Service](./report-service.md) or the [example](#example) below. This report requires specifying the advertiser ID as part of the URL, for example:

```
 https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_7_available_days
- last_14_available_days
- last_30_available_days
- last_365_days

### Data retention period

This report has a daily time granularity and can retrieve data from the past 100 days.

> [!NOTE]
>
> - To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).
> - You can't make a specific time zone selection because NCS data uses the time zone(s) from where sales take place.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `day` | date |  | `"2021-10-10"` | The day on which NCS generated the report. The date displayed for this dimension will match the date displayed for the `analysis_start_date`. |
| `insertion_order_id` | string | Yes | `"5533431"`| The ID of the insertion order. |
| `insertion_order_name` | string | Yes | `"My IO"` | The name of the insertion order. |
| `line_item_id` | string | Yes | `"14545960"` | The ID of the line item. |
| `line_item_name` | string | Yes | `"NCS Line Item"` | The name of the line item. |
| `flight_id` | string |  | `"12396335"` | The ID of the flight. |
| `flight.start_date` | date |  | `"2021-04-16 00:00:00 UTC"` | The start date of the flight. |
| `flight.end_date` | date |  | `"2021-04-30 23:59:59 UTC"` | The end date of the flight. |
| `split_id` | string | Yes | `"1234"` | The ID of a split. |
| `split_name` | string | Yes | `"my split"` | The name of a split. |
| `analysis_end_date` | date |  | `"2021-10-10"` | The last day of the purchase interval being reported for each cohort. |
| `analysis_rejection_reason` | string |  | `"DMA minimum not met, Retailer minimum not met"` | The error that identifies which of the requirements for measurement weren't met. |
| `analysis_start_date` | date |  | `"2021-10-03"` | The first day of the purchase interval being reported for each cohort. |
| `frequency_type` | string |  | `"weekly"` | The reporting frequency selected for this line item or split. |
| `lookback_hours` | string |  | `"flight_lifetime"` | The lookback window selected for this line item or split. |
| `product_id` | string |  | `"10096"` | The product selection ID used to describe the product or products being reported. |
| `product` | string |  | `"BAKING SUPPLIES \| MARS INCORPORATED \| M&M MARS"` | The product selection name used to describe the product or products being reported. |

## Metrics

| Column | Type | Description |
|:---|:---|:---|
| `imps` | int | The total number of impressions served. |
| `clicks` | int | The total number of clicks recorded. |
| `booked_revenue` | int | The revenue received from the advertiser. |
| `media_cost` | int | The cost to the buying member for this inventory. |
| `total_cost` | int | The total amount of costs accrued over the reported period of time. This generally includes two types of costs: budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform. |
| `imps_viewed` | int | Impressions that are considered viewable as defined by the Interactive Advertising Bureau (IAB): For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must render on a screen. |
| `all_outlet_adjusted_number_of_trips` | int | The number of trips to the store by households that have been during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US. |
| `all_outlet_adjusted_penetration%` | int | The penetration percentage for the product, category, or brand during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US.<br><br>**Note**: Penetration measures brand or category popularity. It is calculated by dividing the number of people who've purchased a specific brand or category of goods at least once in a given time period by the size of the relevant market's total population. |
| `all_outlet_adjusted_total_spend` | int | The number of dollars spent by households on the product, category, or brand during the analysis's start and end dates. NCS only has data for some stores (outlets) within the US, so it adjusts sales metrics to account for sales that occurred across all outlets in the US. |
| `video_completions` | int | For a video creative, the number of times the video creative was viewed to completion. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` of `"offline_attribution"`, as well as the columns (dimensions and metrics) and the `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat report-request.json

{
    "report": {
        "report_type": "offline_attribution",
        "format": "csv",
        "report_interval": "last_365_days",
        "columns": [
            "month",
            "member_id",
            "line_item_id",
            "split_id",
            "all_outlet_adjusted_total_spend",
            "imps",
            "analysis_rejection_reason"
        ],
        "orders": [
            "member_id",
            "line_item_id",
            "split_id"
        ],
        "filters": [{
            "line_item_id": [14545960, 14545978]
        }]
    }
}
```

### `POST` the request to the reporting service

In this example, we request execution of the report for advertiser 660.

```
$ curl -b cookies -c cookies -X POST -d @offline_attribution 'https://api.appnexus.com/report?advertiser_id=660'

{
    "response":{
        "status":"OK",
        "report_id":"07af1282c9485adcef49c95fa5d7496b"
    }
}
```

### Use the report ID to retrieve the report data

The standard response includes the report data and a Download URL that you can use to save the data to a file. If you want to get just the Download URL without the report data, pass `"without_data"` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=07af1282c9485adcef49c95fa5d7496b'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2011-11-16 23:51:14",
            "cache_hit": false,
            "fact_cache_hit": false,
            "json_request": "{\"report\":{\"report_type\":\"offline_attribution\",\"format\":\"csv\",\"report_interval\":\"last_365_days\",\"columns\":[\"month\",\"member_id\",\"line_item_id\",\"split_id\",\"all_outlet_adjusted_total_spend\",\"imps\",\"analysis_rejection_reason\"],\"orders\":[{\"order_by\":\"member_id\",\"direction\":\"ASC\"},{\"order_by\":\"line_item_id\",\"direction\":\"ASC\"},{\"order_by\":\"split_id\",\"direction\":\"ASC\"}],\"filters\":[{\"line_item_id\":[14545960,14545978]},{\"member_id\":\"958\"}],\"grouping\":{\"additional_grouping_sets\":[],\"unselected_implicit_groupings\":[],\"additional_groups_on_bottom\":true},\"timezone\":\"UTC\",\"reporting_decimal_type\":\"decimal\",\"use_cache\":true},\"extraction_version\":\"refactored\",\"end_date\":1622678400,\"start_date\":1591142400,\"user_id\":\"46052\"}",
            "header_info": "Report type: offline_attributions\nReport ID: 5dd162b83a0417e13859e5e243844329\n",
            "data": "day,campaign,booked_revenue,imps,clicks,click_thru_pct,site_domain\u000d\u000a2011-11-12,ExampleCampaign - 1
             (123456),.000000,24,0,.000000000000000000%,aaaa.com\u000d\u000a2011-11-13,ExampleCampaign - 2 (789012),.000000,9,0,
             .000000000000000000%,bbbb.net\u000d\u000a2011-11-12,ExampleCampaign - 3 (345678),.000000,2,0,.000000000000000000%,
             ccc.com\u000d\u000a2011-11-13,ExampleCampaign - 3 (345678),.000000,2,0,.000000000000000000%,cccc.de\u000du000a
             2011-11-14,ExampleCampaign - 3 (345678),.000000,10,0,.000000000000000000%,dddd.com\u000d\u000a2011-11-13,
             ExampleCampaign - 4 (901234), 2.574900,22,3,13.636363636363636364%,aaaa.com\u000d\u000a2011-11-15,ExampleCampaign - 3
             (345678),8.583000,2431,10,.411353352529823118%,abab.com\
             ...
            "url": "report-download?id=495d03a7667bac467bb488043ae336e9"
        },
        "execution_status": "ready"
    }
}
```

### Use the download URL to save the report data to a file

You use the `"url"` field in the response to save the report data to a file. Simply make another `GET` call and identify the location and file that you want to save to. Be sure to use the file the extension of the `"format"` that you specified in your initial `POST` request.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=495d03a7667bac467bb488043ae336e9' > /tmp/site_domain.csv
```
