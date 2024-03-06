---
title: Digital Platform API - Engagement Metrics Report
description: Use the Engagement Metrics report to get information about ad viewability and identify problems that might prevent measuring an impression's viewability.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Engagement Metrics report

The Engagement Metrics report provides information about ad viewability, as well as indicating any problems that might be preventing Xandr from measuring an impression's viewability. This report is only available for Xandr Publisher Adserver customers.

## Time frame

All dates and times are given in UTC.

### Time ranges

Time ranges define the time period of the data extracted for the report. The following is a complete list of time ranges available for reports. However, all time ranges are not available for every report.

- custom
- current_hour
- last_available_day
- last_hour
- today
- last_24_hours
- last_48_hours
- yesterday
- last_2_days
- last_7_days
- last_7_available_days
- last_14_days
- last_14_available_days
- last_30_days
- last_30_available_days
- last_month
- last_100_days
- last_365_days
- quarter_to_date
- month_to_date
- month_to_yesterday
- lifetime

### Intervals

Intervals determine how your data is grouped together into rows in the report response. The following is a complete list of intervals available for reports. However, all intervals are not available for every report.

- Hourly: Data is grouped into rows by the hour.
- Daily: Data is grouped into rows by the day.
- Monthly: Data is grouped into rows by the month.
- Cumulative: Data is grouped together in one figure, covering the entire selected time range.

> [!NOTE]
> For more information about how quickly report data is processed, see [Availability of Reporting Data](../monetize/availability-of-reporting-data.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `advertiser` | string | no | `"Verizon Wireless (789)"` | The advertiser whose creative is served on impression. |
| `publisher` | string | no | `"Publisher XYZ 347967"` | The publisher on whose inventory this impression has occurred. |
| `placement` | string | no | `"FP 728x90 (567)"` | A placement is an open slot on a publisher website where an advertiser creative with matching specifications can serve. |
| `insertion_order` | string | no | `"InsertionOrderABC648359"` | The insertion order under which this impression was purchased. The buy-side hierarchy is Insertion Order > Line Item > Campaign. |
| `line_item` | string | no | `"LineItemDEF947764"` | The line item under which this impression was purchased. The buy-side hierarchy is Line Item > Campaign. |
| `campaign` | string | no | `Campaign` | The campaign which purchased this impression. |
| `creative` | string | no | `"Q1 2010 - 728x90 (554)"` | The creative served for the impression. |
| `media_type` | string | no | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The media type associated with the creative that served on this impression. |
| `impression_type` | string | yes | `"External Impression"` | See Impression Types for definitions of the different types of impressions. |
| `device_type` | string | yes | `"Mobile Phones"` | The type of device on which the impression was served. Possible values:<br> - `Desktops & Laptops`<br> - `Tablets`<br> - `Mobile Phones`<br> - `TV`<br> - `Game Consoles`<br> - `Set Top Box`<br> - `Media Players`<br> - `Other Devices` |
| `operating_system_family` | string | yes | `"Android"` | The name of the operating system family associated with the device the impression was served on. |
| `buyer` | string | no |  | The name of the buyer associate with the impression. |
| `seller` | string | no |  | The name of the seller associated with the impression. |
| `minimum_impressions` | int | yes |  | The minimum number of impressions you'd like to filter by. For example, you may want to see only impressions and unique from members whose volume exceeds 100,000 impressions over the selected time range. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `75000` | imps | The total number of impressions (served and resold). |
| `measurable_imps` | int | `6500` |  | The total number of impressions that were measured for viewability. |
| `viewed_imps` | int | `1872` | viewed_impsview_non_measurable_reason | The number of measured impressions that were viewable according to the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in view for 1 continuous second. |
| `viewability_measurement_rate` | double | `45`% | View Measured Imps / Imps | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps). |
| `viewability_rate` | double | `58%` | Viewed Imps / View Measured Imps | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps). |
| `in_view_duration` | time | `35` | not applicable | The `average in_view duration` (in seconds) measured for which impressions met the IAB Viewability definition. |
| `not_measured_imps` (`unsupported_cross-domain_iframe`) | int | `115` | not applicable | The number of impressions not measured because the creative cannot be measured because the ad was served in a cross-domain iframe and the browser was not supported. All modern browsers are supported but certain old versions may not be supported. |
| `not_measured_imps` (`creative_not_found`) | int | `85` | not applicable | The number of impressions not measured because the creative could not be found by the viewability script on the page. For example, this could occur if the div is being replaced or the creative isn't located within five seconds. |
| `not_measured_imps` (`script_not_initialized`) | int | `35` | not applicable | The number of impressions not measured because the measurement script did not initialize. This could occur for very short sessions when a user leaves a page before the other component (like the OS in mobile apps) can provide feedback on viewability. |
| `not_measured_imps` (`no_script_callback`) | int | `200` | not applicable | The number of impressions not measured because no callback was received from the measurement script. For example, this could occur if the script hasn't executed. |
| `not_measured_imps` (`unsupported_in-app_SDK`) | int | `175` | not applicable | The number of impressions not measured because the in-app SDK for the specific inventory is not supported. Please visit the [Viewability FAQ](../monetize/viewability-faq.md) to learn about supported in-app SDKs. |
| `not_measured_imps` (`unsupported_native_integration`) | int | `200` |  | The number of impressions not measured because the specific type of native inventory is not supported. Please visit the [Viewability FAQ](../monetize/viewability-faq.md) to learn about supported native supply. |
| `not_measured_imps` (`unsupported_media_type`) | int | `135` | not applicable | The number of impressions not measured because the media type is not supported. Please visit the [Viewability FAQ](../monetize/viewability-faq.md) to learn about supported media types. |
| `not_measured_imps` (`unsupported_supply_type`) | int | `120` | not applicable | The number of impressions not measured because the supply type is not supported. Please visit the [Viewability FAQ](../monetize/viewability-faq.md) to learn about supported supply types. |
| `not_measured_imps` (`unsupported_impression_type`) | int | `145` | not applicable | The number of impressions not measured because the imp type is not supported. Please visit the [Viewability FAQ](../monetize/viewability-faq.md) to learn about supported impression types. |
| `not_measured_imps` (`unknown`) | int | `115` | not applicable | The number of impressions not measured because of an unknown reason. |
| `not_viewed_imps` (`creative_not_loaded`) | int | `125` | not applicable | The number of impressions not viewed because the creative did not load before the web page was closed. For example, when a user leaves the web page within one second of the creative being loaded. |
| `not_viewed_imps` (`not_visible_per_SDK`) | int | `80` | not applicable | The number of impressions not viewed because in-app SDK responded with not visible signal. For example, the Open Measurement Software Development Kit (OM SDK) reported the ad as non-viewable. |
| `not_viewed_imps` (`hidden_browser`) | int | `60` | not applicable | The number of impressions not viewed because either the browser was not in focus, or the browser tab was hidden. |
| `not_viewed_imps` (`creative_hidden_by _css/html`) | int | `125` | not applicable | The number of impressions not viewed because the creative was explicitly hidden by CSS or HTML on the webpage. For more details, check your ads' recent style changes. |
| `not_viewed_imps` (`out_of_viewport`) | int | `95` | not applicable | The number of impressions not viewed because the creative was outside the visible area of a webpage on a display device. Ensure that the creative is visible and not at the bottom of the page. |
| `not_viewed_imps` (`insufficient_surface_area`) | int | `100` | not applicable | The number of impressions not viewed because the surface threshold based on IAB definition was not met. |
| `not_viewed_imps` (`insufficient_duration`) | int | `50` | not applicable | The number of impressions not viewed because time threshold based on IAB definition was not met. |
| `not_viewed_imps` (`unknown`) | int | `75` | not applicable | The number of impressions not viewed because of an unknown reason. |
| `in_view_duration` (`greater_than_0%_pixels`) | time | `10` | not applicable | The average duration (in seconds) for which impressions displaying greater than 0% of the pixels in the creative remained in view. |
| `in_view_duration` (`greater_than_25%_pixels`) | time | `15` | not applicable | The average duration (in seconds) for which impressions displaying greater than 25% of the pixels in the creative remained in view. |
| `in_view_duration` (`greater_than_50%_pixels`) | time | `35` | not applicable | The average duration (in seconds) for which impressions displaying greater than 50% of the pixels in the creative remained in view. |
| `in_view_duration` (`greater_than_75%_pixels`) | time | `20` | not applicable | The average duration (in seconds) for which impressions displaying greater than 75% of the pixels in the creative remained in view. |
| `in_view_duration` (`equal_to_100%_pixels`) | time | `40` | not applicable | The average duration (in seconds) for which impressions displaying 100% of the pixels in the creative remained in view. |

## Example

### Create a JSON-formatted report request

The JSON file should include the `report_type` of `"engagement_metrics_network"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat engagement_metrics_network
  {
    "report":
    {
        "report_type":"engagement_metrics_network",
        "columns":[
            "advertiser",
            "insertion_order",
            "creative",
            "device_type",
            "imps",
            "in_view_duration",
            "viewability_rate"
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -X POST -d @engagement_metrics_network 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"engagement_metrics_network\",\"columns\":[\"advertiser\",
            \"insertion_order\",\"creative\",\"device_type\",\"imps\",\"in_view_duration\",\"viewability_rate\"],
            \"report_interval\":\"last_7_days\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/engagement_metrics_network.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
