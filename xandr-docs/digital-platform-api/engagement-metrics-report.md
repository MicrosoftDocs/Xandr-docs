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

| Column | Type | Filter? | Description |
|---|---|---|---|
| `buyer_member_id` | int | Yes | The ID of the buying member of the impressions. |
| `seller_member_id` | int | Yes | The ID of the selling member. |
| `buyer_member_name` | string | No | The name of the buying member of the impressions. |
| `seller_member_name` | string | No | The name of the selling member. |
| `advertiser_id` | int | Yes | The ID of the advertiser object associated to the served impressions. |
| `advertiser_name` | string | No | The name of the advertiser object associated to the served impressions. |
| `line_item_id` | int | Yes | The ID of the line item under which the impressions were purchased. The buy-side hierarchy is **Line Item** > **Campaign**. |
| `line_item_name` | string | No | The name of the line item under which the impressions were purchased. The buy-side hierarchy is **Line Item** > **Campaign**. |
| `campaign_id` | int | Yes | The ID of the campaign that purchased the impressions. |
| `campaign_name` | string | No | The name of the campaign that purchased the impressions. |
| `imp_type` | int | Yes | The name of the impression type which was occurred.  |
| `imp_type_id` | int | Yes | The ID of the impression type which was occurred.  |
| `insertion_order_id` | int | Yes | The ID of the insertion order under which the impressions were purchased. The buy-side hierarchy is **Insertion Order** > **Line Item** > **Campaign**. |
| `insertion_order_name` | string | No | The name of the insertion order under which the impressiond were purchased. The buy-side hierarchy is **Insertion Order** > **Line Item** > **Campaign**. |
| `publisher_id` | int | Yes | The ID of the  publisher object on which the the   impressions were occurred. |
| `publisher_name` | string | No | The name of the  publisher object on which the the impressions were occurred. |
| `placement_id` | int | Yes | The ID of the placement or the open slot on publisher website where the advertiser's   creative with matching specifications was served. |
| `placement_name` | string | No | The name of the placement or the open slot on publisher website where the advertiser's   creative with matching specifications was served. |
| `member_id` | int | Yes | The ID of the member for which report is generated. |
| `creative_id` | int | No | The ID of the creative served for the impression. |
| `creative_name` | string | No | The name of the creative served for the impression. |
| `mediatype` | string | No | The name of the media type associated with the creative that served on the impression. |
| `media_type_id` | int | Yes | The ID of the media type associated with the creative that served on the impression. |
| `device_type` | string | Yes | The type of device on which the impression was served. Possible values:  <br>  - Desktops & Laptops  <br> - Tablets  <br> - Mobile Phones <br> - TV  <br> - Game Consoles <br> - Set Top Box   <br> - Media Players  <br> - Other Devices |
| `day` | date | Yes | The day of the auction. |
| `operating_system_family_id` | int | Yes | The ID of the operating system family associated with the device where the impression was   served on. |
| `operating_system_family_name` | string | No | The name of the operating system family associated with the device where the impression was served on. |
| `split_id`| int | Yes | The ID of the split that purchased the impressions in this data set. Splits are   only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be null. |
| `split_name` | string | No | The name of the split that purchased the impressions in this data set. Splits are   only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be null. |
|`campaign_group_type_id` | int | Yes | The ID of the campiagn group of which the campaign that purchaed the impression is a part of. |

## Metrics

> [!NOTE]
> When values of a metric are displayed as percentages in the UI, they will be displayed as decimals when you export the report.

| Column | Type | Formula | Description |
|---|---|---|---|
| `imps` | int | imps | The total number of impressions (served and resold). |
| `viewed_imps` | int | viewed_imps | The number of measured impressions that were viewable according to the IAB   Viewability definition, which states that an impression is viewable if 50% of the pixels are in view for 1 continuous second. |
| `view_measurable_rate` | double | view_measurable_imps/imps | The percentage of impressions measured for viewability out of the total number of impressions. |
| `view_rate` | double | viewed_imps/view_measurable_imps | The percentage of impressions that were viewable out of the total number of impressions measured for viewability.  |
| `viewed_imps` | int | viewed_imps | The total number of impressions that were measured for viewability. |
| `nvt_unknown_imps` | int | nvt_unknown_imps | The number of impressions not viewed because of unknow reasons. |
| `nmt_not_initialised_imps` | int | nmt_not_initialised_imps | The number of impressions not measured because the measurement script did not initialize. This could occur for very short sessions when a user leaves a page before the other component (like the OS in mobile apps) can provide feedback on viewability. |
| `nmt_unknown_imps` | int | nmt_unknown_imps | The number of impressions not measured because of unknow reasons. |
| `view_iab_durat`ion | double | view_iab_duration | The average duration (in seconds) measured for which impressions met the IAB Viewability   definition. |
| `nvt_crea_not_loaded_imps` | int | nvt_crea_not_loaded_imps | The number of impressions not viewed because the creative could not be loaded by the viewability script on the page. For example, this could occur if the div   is being replaced or the creative isn't located within five seconds. |
| `nvt_sdk_imps` | int | nvt_sdk_imps | The number of impressions not viewed because in-app SDK responded with a not visible signal. For example, the Open Measurement Software Development Kit (OM SDK) reported the ad as non-viewable. |
| `nvt_hidden_crea_imps` | int | nvt_hidden_crea_imps | The number of impressions not viewed because the creative was explicitly hidden   by CSS or HTML on the webpage. For more details, check your ads' recent style   changes. |
| `nvt_out_viewport_imps` | int | nvt_out_viewport_imps | The number of impressions not viewed because the creative was outside the visible area of a webpage on a display device. Ensure that the creative is visible and not at the bottom of the page. |
| `nvt_surface_imps` |int | nvt_surface_imps | The number of impressions not viewed because the surface threshold based on IAB   definition was not met. |
| `nvt_duration_imps` |int | nvt_duration_imps | The number of impressions not viewed because time threshold based on IAB   definition was not met. |
| `nmt_imp_type_imps` |int | nmt_imp_type_imps | The number of impressions not measured because the impression  type is not supported. Please visit the   Viewability FAQ to learn about supported media types. |
| `nmt_media_type_imps` |int | nmt_media_type_imps | The   number of impressions not measured because the media type is not supported. Please visit the Viewability FAQ to learn about supported media types. |
| `nmt_supply_type_imps` |int | nmt_supply_type_imps | The number of impressions not measured because the supply type is not supported. Please visit the Viewability FAQ to learn about supported supply types. |
| `nmt_cross_domain_imps` | int | nmt_cross_domain_imps | The number of impressions not measured because the creative cannot be measured because the ad was served in a cross-domain iframe and the browser was not   supported. All modern browsers are supported but certain old versions may not be supported. |
| `nmt_no_crea_imps` | int | nmt_no_crea_imps | The number of impressions not measured because the creative could not be found by   the viewability script on the page. For example, this could occur if the div   is being replaced or the creative isn't located within five seconds. |
| `nmt_sdk_imps` | int | nmt_sdk_imps | The number of impressions not measured because the in-app SDK for the specific   inventory is not supported. Please visit the Viewability FAQ to learn about supported in-app SDKs. |
| `nmt_no_callback_imps` | int | nmt_no_callback_imps | The number of impressions not measured because no callback was received from the   measurement script. For example, this could occur if the script hasn't executed. |
| `nmt_native_imps` | int | nmt_native_imps | The number of impressions not measured because the specific type of native   inventory is not supported. |
| `nvt_hidden_browser_imps` | int | nvt_hidden_browser_imps | The number of impressions not viewed because either the browser was not in focus, or the browser tab was hidden. |
| `view_duration_gt_0pct` | double | view_duration_gt_0pct | The average duration (in seconds) for which impressions displaying greater than 0% of the pixels in the creative remained in view. |
| `view_duration_gt_25pct` | double | view_duration_gt_25pct | The average duration (in seconds) for which impressions displaying greater than 25% of the pixels in the creative remained in view. |
| `view_duration_gt_25pct`| double | view_duration_gt_25pct | The average duration (in seconds) for which impressions displaying greater than 50% of the pixels in the creative remained in view. |
| `view_duration_gt_75pct` | double | view_duration_gt_75pct | The average duration (in seconds) for which impressions displaying greater than 75% of the pixels in the creative remained in view. |
| `view_duration_eq_100pct` | double | view_duration_eq_100pct | The average duration (in seconds) for which impressions displaying 100% of the pixels in the creative remained in view. |

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
            "advertiser_id",
            "insertion_order_id",
            "creative_id",
            "device_type",
            "imps",
            "view_iab_duration  ",
            "view_rate"
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
         "json_request":"{\"report\":{\"report_type\":\"engagement_metrics_network\",\"columns\":[\"advertiser_id\",
            \"insertion_order_id\",\"creative_id\",\"device_type\",\"imps\",\"view_iab_duration\",\"view_rate\"],
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
