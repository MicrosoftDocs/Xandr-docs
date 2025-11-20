---
title: Digital Platform API - Data Usage Report
description: Use the Data Usage report to view details related to third-party data usage and associated costs, as well as campaigns used to target users.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Data Usage report

This report provides gives details related to your usage of data provided by third parties (e.g., user segment providers), the costs of that data usage and line items/campaigns in which that data was used to target users.

This report's data is retained for 60 days. The `time_granularity` of the data is `hourly`. For instructions on retrieving a report, see the [Report Service](./report-service.md) or the [Example](#example) below.

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

To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `geo_country_code` | string | yes | `"CA"` | A two-character string denoting the country/region associated with the impression.|
| `campaign` | string | no | `"Prospect Campaign (31)"` | **Deprecated** (as of October 17, 2016). |
| `data_provider` | string | no | `"Peer 39 (Data Provider) (517)"` | **Deprecated** (as of October 17, 2016). |
| `geo_country` | string | yes | `"US"` | The code of the geographical country/region associated with the impression. |
| `targeted_segment_ids` | string | no | `"935035, 935146"` | The comma-separated list of IDs for each of the segments used when targeting. |
| `day` | date | yes | `"2010-02-01"` | The day at which the auction associated with the impression occurred |
| `hour` | date | yes | `"2010-02-01 05:00:00"` | The hour at which the auction associated with the impression occurred. |
| `campaign_id` | int | yes | `31` | The ID of the campaign associated with the impression that used third-party data targeting. |
| `buyer_member_id` | int | yes | `643` | The ID of the member that used the third-party data. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `data_provider_id` | int | yes | `517` | The ID of the third-party that provided the targeting data. |
| `month` | date | yes | `"2010-02"` | The month at which the auction associated with the impression occurred |
| `data_provider_name` | string | no | `"Peer 39 (Data Provider)"` | The name and ID of the third-party that provided the targeting data. |
| `campaign_name` | string | no | `"Prospect Campaign"` | The name of the campaign associated with the impression that used third-party data targeting. |
| `geo_country_name` | string | no | `"United States"` | The name of the geographical country/region associated with the impression. |
| `line_item_name` | string | no | `"Fall Apparel"` | The name of the line item associated with the impression that used third-party data targeting. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `34534` | imps | The total number of impressions that used third-party data to serve the ad. |
| `data_costs` | money | `3.50` |  | The monetary value of the data segments that were purchased from third-party data providers. |
| `transaction_tax` | money | `.43` |  | Applicable sales, value added, goods and services or similar taxes (Transaction Taxes) will be applied to your transactions with Microsoft based on the Customer’s Account Business Location provided in the onboarding experience. |
| `data_type` | string | `Segment` |  | The available choices are Segment and Cross Device |
| **Metrics available in local currency** |  |  |  |  |
| `data_costs_buying_currency` | money | `3.50` |  | The monetary value of the data segments that were purchased from third-party data providers. Represented in the Advertiser's currency |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"buyer_data_usage_analytics"`, as well as the columns (dimensions and metrics) and report_interval that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`, `hour`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat buyer_data_usage_analytics

{"report":
    {
        "format": "csv",
        "report_interval": "yesterday",
        "row_per": ["geo_country"],
        "columns": ["imps","campaign_id","geo_country"],
        "report_type": "buyer_data_usage_analytics"
    }
}
```

### `POST` the request to the [Report Service](./report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -c cookies -X post -d @seller_brand_review "https://api.appnexus.com/report"

{
   "response":{
      "status":"OK",
      "report_id":"c445bca183a3d338dc1c5b85a3d484f5"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=c445bca183a3d338dc1c5b85a3d484f5'

{
    "response": {
        "status": "OK",
        "report": {
            "name": null,
            "created_on": "2014-11-19 22:33:31",
            "json_request": "{\"report\":{\"format\":\"csv\",\"report_interval\":\"yesterday\",\"row_per\":[\"geo_country\"],\"columns\":[\"imps\",\"campaign_id\",\"geo_country\"],\"report_type\":\"buyer_data_usage_analytics\",\"filters\":[{\"buyer_member_id\":\"958\"}]}}",
            "url": "report-download?id=c445bca183a3d338dc1c5b85a3d484f5"
        },
        "execution_status": "ready"
    }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=c445bca183a3d338dc1c5b85a3d484f5' > /tmp/buyer_data_usage_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
