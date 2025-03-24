---
title: Advertiser Attributed Conversions
description: Use the Advertiser Attributed Conversions report to view conversion pixel IDs, order IDs, times of attributed clicks or impressions, and other related information.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Advertiser attributed conversions

The Advertiser Attributed Conversions report allows you to view conversion pixel IDs, order IDs, times of attributed clicks or impressions, and other information related to your advertisers' attributed conversions.

> [!NOTE]
> Conversion pixels are used to track actions on advertisers' web pages, such as registering or making a purchase. They can be configured to pass dynamic order ID values, which help networks reconcile with advertisers. Once a conversion pixel fires, Xandr determines if the conversion can be attributed (tied to a creative that the user viewed or clicked previously). A post-click conversion is attributed to the last click on a creative associated with the conversion pixel. A post-view conversion is attributed to the last impression of a creative associated with the conversion pixel. For a hybrid pixel, the conversion is attributed to the last click or, if there were no clicks, the last impression of a creative associated with the conversion pixel.
>
> For more details about our attribution process, see [Conversion Attribution](../invest/conversion-attribution.md) in the UI documentation.

For instructions on retrieving a report, see the [Report Service](./report-service.md) or the [Examples](#examples).

This report is filtered by member ID and advertiser ID. The member ID is detected based on the network user's authentication, but the advertiser ID must be specified as part of the URL, for example:

```
https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
```

## Time frame and time zone

The `report_interval` field in the JSON request can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_7_days
- last_30_days
- month_to_yesterday
- month_to_date
- last_30_days

Alternately, the `start_date` and `end_date` fields can be set to a range within the last 33 days. The `timezone` field in the JSON request can be set only to `UTC`, but this is not necessary, as the timezone defaults to `UTC` if not specified.

### Data retention period

This report can retrieve data for the last 90 days and only in UTC timezone.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | time | yes | `11/1/11` | The month and year when the conversion pixel fired. |
| `day` | time | yes | `11/18/11` | The day of the year when the conversion pixel fired. |
| `hour` | time | yes | `11/18/11 6:00` | The hour of the day when the conversion pixel fired. |
| `datetime` | date | yes | `11/18/11 6:00` | The date and time when the conversion pixel fired. |
| `pixel_id` | int | yes | `9012` | The ID of the conversion pixel. |
| `pixel_name` | string | no | `PixelName` | The name of the conversion pixel. |
| `pixel` | string | no | `PixelName (9012)` | **Deprecated** (as of October 17, 2016). |
| `order_id` | int | yes | `678` | The order ID or SKU optionally passed in the conversion pixel. For information about dynamically passing an order ID in a conversion pixel, see [Conversion Pixels Advanced](../invest/conversion-pixels-advanced.md) in the UI documentation. |
| `external_data` | string | yes | `New York` | Additional data optionally passed in the conversion pixel, for example, the conversion geography, an affiliate code, or other information related to the sale or user. For information about dynamically passing external data in a conversion pixel, see [Conversion Pixels Advanced](../invest/conversion-pixels-advanced.md) in the UI documentation. |
| `post_click_or_post_view_conv` | enum | yes | `Post Click` |  The type of conversion that occurred as a result of having cross-device enabled.<br><br> - **Post-click**: The conversion is attributed to a user clicking a creative.<br> - **Post-view**: Additionally specified, the conversion is attributed to a user viewing a creative.<br> - **Cross-device**: The conversion is attributed to having cross-device enabled.<br> - **IP**: Additionally specified, the conversion is attributed to having IP attribution enabled. |
| `user_id` | int | yes | `433` | The ID of the user that clicked or viewed the creative.<br><br>**Warning**: This field has been deprecated from the API (in compliance with GDPR) and that service has been deprecated. |
| `line_item_id` | int | yes | `12345` | The ID of the line item to which the conversion pixel is assigned. |
| `line_item_name` | string | no | `LineItemName` | The name of the line item. |
| `line_item` | string | no | `LineItemName (12345)` | **Deprecated** (as of October 17, 2016). |
| `creative_id` | int | yes | `890123` | The ID of the creative that was clicked or viewed.<br><br>**Note**: For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | no | `CreativeName` | The name of the creative. |
| `creative` | string | no | `CreativeName (890123)` | **Deprecated** (as of October 17, 2016). |
| `campaign_id` | int | yes | `456789` | The ID of the campaign to which the creative belongs. |
| `campaign_nam`e | string | no | `CampaignName` | The name of the campaign to which the creative belongs. |
| `campaign` | string | no | `CampaignName (456789)` | **Deprecated** (as of October 17, 2016). |
| `split_id` | int | yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be null. |
| `split_name` | string | yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be null. |
| `imp_time` | date | yes | `11/17/11 3:00` | The date and time of the impression (when the creative was served). |
| `imp_type_id` | int | yes | `5` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1 ("Blank")`: No creative served.<br> - `2 ("PSA")`: A public service announcement served because there were no valid bids and no default creative was available.<br> - `3 ("Default Error")`: A default creative served due to a timeout issue.<br> - `4 ("Default")`: A default creative served because there were no valid bids.<br> - `5 ("Kept")`: Your advertiser's creative served on your publisher's site.<br> - `6 ("Resold")`: Your publisher's impression was sold to a third-party buyer.<br> - `7 ("RTB")`: Your advertiser's creative served on third-party inventory.<br> - `8 ("PSA Error")`: A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9 ("External Impression")`: An impression from an impression tracker.<br> - `10 ("External Click")`: A click from a click tracker. |
| `imp_type` | string | yes | `"Kept"` | The type of impression. For possible values, see `imp_type_id`. |
| `advertiser_id` | int | yes | `123` | The ID of the advertiser. |
| `advertiser_name` | string | no | `AdvertiserName` | The name of the advertiser. |
| `advertiser` | string | no | `AdvertiserName (123)` | **Deprecated** (as of October 17, 2016). |
| `buyer_member_id` | int | yes | `4567` | The ID of the member that bought the impression. |
| `auction_id` | int | yes | `6442894461734786633` | The ID of the impression event.<br><br>**Note**: Clients who subscribe to [log-level data feeds](../log-level-data/log-level-data-feeds.md) can use this ID to request additional information about the impression, such as geography and browser. |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `post_click_or_post_view_revenue` | money | `3.00` | The revenue optionally passed in the conversion pixel using the `"value"` parameter. |

## Examples

### Create a JSON-formatted report request

In this example, we set a filter to get information about conversion pixel 9012.

```
$ cat attributed_conversions  {
    "report":
    {
        "report_type": "attributed_conversions",
        "columns": [
            "datetime",
            "pixel_id",
            "order_id",
            "post_click_or_post_view_conv",
            "post_click_or_post_view_revenue",
            "line_item_id",
            "creative_id",
            "campaign_id",
            "imp_time",
            "imp_type_id",
            "advertiser_id",
            "buyer_member_id"
        ],
        "filters": [{"pixel_id": 9012}],
        "report_interval": "last_7_days",
        "emails": ["js@email.com"],
        "format": "csv"
    }
}
```

### `POST` the request to the reporting service

```
$ curl -b cookies -c cookies -X POST -d @attributed_conversions 'https://api.appnexus.com/report?advertiser_id=123'

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
            "created_on": "2011-11-22 23:51:22",
            "cache_hit": false,
            "fact_cache_hit": false,
            "json_request": "{\"report\":{\"report_type\":\"attributed_conversions\",\"columns\":
             [\"datetime\",\"pixel_id\",\"order_id\",\"post_click_or_post_view_conv\",
             \"post_click_or_post_view_revenue\",\"line_item_id\",\"creative_id\",\"campaign_id\",
             \"imp_time\",\"imp_type_id\",\"advertiser_id\",\"buyer_member_id\"],
             \"report_interval\":\"lifetime\",\"emails\":[\"js@email.com\"],\"filters\":
             [{\"buyer_member_id\":\"4567\"},{\"advertiser_id\":\"123\"}]}}",
            "header_info": "Report type:,conversion_pixel\u000d\u000a,\u000d\u000aRun at:,
             2011-11-22 23:51:22\u000d\u000aStart date:,2011-11-15 00:00:00\u000d\u000aEnd date:,
             2011-11-22 00:00:00\u000d\u000aTimezone:,\u000d\u000aUser:,John Smith (1432)
             \u000d\u000a",
            "data": "datetime,pixel_id,order_id,post_click_or_post_view_conv,
             post_click_or_post_view_revenue,line_item_id,creative_id,campaign_id,imp_time,
             imp_type_id,advertiser_id,buyer_member_id\u000d\u000a11704,8225230493273032227,
             123,8.7654A+32,4567,2011-11-18 06:00:13,2011-11-17 03:00:02,5,12345,678,9012,
             Post Click,.3.00\u000d\u000a11704,
             ..."
        },
        "execution_status": "ready",
        "dbg_info": {
            ...
        }
    }
}
```

If necessary, use the [Lookup Service](./lookup-service.md) to map objects IDs to other relevant data, such as names, codes, and statuses.

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the `report-download` service. You can find the service and report ID in the url field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/attributed_conversions.csv 
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
