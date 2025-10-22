---
title: Digital Platform API - Key Value Analytics Report
description: Explore the Key Value Analytics report, offering insights into the information associated with your network's designated targeting keys and values.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Key Value Analytics report

The Key Value Analytics report shows you the information associated with your network's defined targeting keys and values.

Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the **kw\_** prefix on the key name. For example, a placement tag containing *keyname=value1* will not serve and therefore not be logged, whereas a placement tag containing *kw_keyname=value1* will serve and be logged. This applies to `GET`-based query-string ad calls with the following tag types: `/tt`, `/ttj`, `/fpt`, `/jpt`, `/pt`, `/ptv`, `/ssptv`, `/mtj`, `/map`, `/mob`, `/prebid/amp`, `/vmap`, `/ssvmap`.

> [!NOTE]
> **AppNexus Seller Tags**
>
> When using [Seller Tag](../seller-tag/seller-tag.md), omit the **kw\_** prefix. AST has the keyword object in the body of the (ut/v3) request, so the prefix is not needed. The same holds true for other `POST`-based request body ad calls from Prebid (ut/v3/prebid, openrtb2/prebid, prebid/lfv) and OpenRTB (openrtb2).

Not all impressions from key/value targets will be included in reports. To be included, the targets must meet the following criteria:

- Key must be pre-defined. For more information, see the [Pre-Defining Targeting Keys and Values](../monetize/pre-defining-targeting-keys-and-values.md) page in the UI.
- Value must be pre-defined OR Value must be targeted by at least one line item or campaign.
- Value is not a numeric range (greater than or less than).
- Value does not include a wildcard.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- today
- yesterday
- last_24_hours
- last_48_hours
- last_7_days
- last_month
- month_to_date
- quarter_to_date

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](report-service.md).

### Dates occurring greater than 45 days ago

If you create a Key Value Analytics report with the Range field set to Custom (where the end date is greater than 45 days from today), your report (regardless of metrics included) will be added to a special queue for "resource-intensive" reports. As a result, the report may take longer than usual to complete. In addition, this resource-intensive report may, due to the amount of data being requested, fail before being completed. If your report fails to complete, you will receive a notification. If your report request fails, you can:

- Rerun the report at a later time.
- Use a report type other than Key Value Analytics.
- Alter the way you structure your reports (if possible) so they do not include dates greater than 45 days ago.

If you are frequently requesting Key Value Analytics reports which include dates longer than 45 day ago, you may need to consider running
these reports via the API, caching the data and using [Bulk Reporting Feeds](bulk-reporting-feeds.md) or a [Log Level Data Feeds - Archive](../log-level-data/log-level-data-feeds.md). For more details on how to alter your reports to avoid these issues, see the [Dimensions, Metrics, Filtering, and Grouping](../invest/dimensions-metrics-filtering-and-grouping.md) page in the UI.

### Data retention period

Data in this report has the following retention period:
- Hourly retention: 100 days
- Daily retention: 500 days

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | No | `"2010-02"` | The month of the auction. |
| `day` | date | No | `"2010-02-01"` | The day of the auction. |
| `hour` | date | No | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note:** For impressions older than 100 days, the day will be returned rather than the hour. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: `229` = PSA, `0` = Blank, or `319` = Default. |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member.<br><br>**Note:** The name might be `"Default"` or `"Default Error"`, which means that there was no buyer for the impression, and a default creative was served. |
| `buyer_member` | string | No | `"My Network (123)"` | **Deprecated** (as of October 17, 2016). |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |
| `seller_member` | string | No | `"That Seller (456)"` | **Deprecated** (as of October 17, 2016). |
| `placement_id` | int | Yes | `1212` | The ID of the placement.<br><br>**Note:** For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id` . |
| `placement_name` | string | No | `"lvillage 160x600"` | The name of the placement.<br><br>**Note:** For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | No | `"lvillage 160x600 (1212)"` | **Deprecated** (as of October 17, 2016). |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a default or PSA was shown. |
| `advertiser_name` | string | No | `"AdvertiserA"` | The name of the advertiser. |
| `advertiser` | string | No | `"AdvertiserA (789)"` | **Deprecated** (as of October 17, 2016). |
| `line_item_id` | int | Yes | `1122` | The ID of the line item. |
| `line_item_name` | string | No | `"Line Item 1"` | The name of the line item. |
| `line_item` | string | No | `"Line Item 1 (1122)"` | **Deprecated** (as of October 17, 2016). |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign. |
| `campaign` | string | No | `"Default Campaign (789)"` | **Deprecated** (as of October 17, 2016). |
| `split_id` | Int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null` . |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `publisher_id` | int | Yes | `555` | The ID of the publisher. |
| `publisher_name` | string | No | `"PublisherA"` | The name of the publisher. |
| `publisher` | string | No | `"PublisherA (555)"` | **Deprecated** (as of October 17, 2016). |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country/region. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id`. |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1` ("Blank"): No creative served.<br>- `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br> - `3` ("Default Error"): A default creative served due to a timeout issue.<br> - `4` ("Default"): A default creative served because there were no valid bids.<br> - `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br> - `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br> - `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br> - `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9` ("External Impression"): An impression from an impression tracker.<br> - `10` ("External Click"): A click from a click tracker.<br><br>**Note:** RTB auctions are not included in reports. An impression with `imp_type_id` = `7` will not be reported. |
| `creative_id` | int | Yes | `444` | The ID of the creative.<br><br>**Note:**<br> - For impressions older than 100 days, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2017 728x90"` | The name of the creative.<br> - For impressions older than 100 days, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, creative_name will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2017 728x90 (444)"` | **Deprecated** (as of October 17, 2016). |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `advertiser_currency` | string | Yes | `"USD"` | The currency used by the advertiser. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order associated with the campaign that purchased the impression. |
| `campaign_group_id` | int | Yes | `432` | The campaign group ID of the impression. |
| `site_id` | int | Yes | `765` | The ID of the site.<br><br>**Note:** For impressions older than 100 days, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site 1"` | The name of the site. |
| `site` | string | No | `"Site 1 (765)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_currency` | money | Yes | `"EUR"` | The currency used by the publisher. |
| `key_name` | string | Yes | `"fruit"` | The name of the targeting key. |
| `key_value` | string | Yes | `"apple"` | The value associated with the targeting key. |
| `key_name_label` | string | Yes | `"fruit eaten by customer"` | The label for the key. The label can be a more descriptive version of the key name. |
| `key_value_label` | string | Yes | `"green or red apples"` | The label for the value. The label can be a more descriptive version of the key value. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions. |
| `clicks` | int | `545` | clicks | The total number of clicks. |
| `ctr` | double | `0.2327836` | clicks / imps | The click-through rate – the ratio of clicks to impressions, expressed as a percentage. |
| `booked_revenue` | money | `150.00` | booked_revenue | The total revenue booked through direct advertisers. |
| `reseller_revenue` | money | `100.00` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `revenue` | money | `250.00` | booked_revenue + reseller_revenue | The total revenue. |
| `rpm` | money | `1.25` | revenue / 1000 imps | The revenue per 1000 impressions, including defaults, PSAs, and errors. For more information about these impression types, see `imp_type_id`. |
| `booked_revenue_dollars` | money | `500.00` | booked_revenue_dollars | The dollar amount earned by this network on the impression. |
| `imps_blocklisted` | int | `20` | imps_blocklisted | The number of impressions that didn't serve because a site was in a blocklist. |
| `total_conversions` | int | `5` | total_conversions | The total number of post-view and post-click conversions. |
| `conversions_rate` | double | `0.000221877080097626` | total_conversions / imps | The rate of conversions to impressions. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `post_view_convs` | int | `2` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_convs_rate` | double | `0.00013` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_click_convs` | int | `3` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_convs_rate` | double | `0.0002` | post_click_convs / imps | The rate of post-click conversions to impressions. |
| `imps_master_creative` | int | `1276` | imps_master_creative | The total number of impressions from the master creative in page-level roadblocking. <br><br>**Note:** This metric is in alpha testing and not available to all customers. |

## Examples

### Create the JSON report request

The JSON file should include the `report_type` of `"key_value_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](report-service.md).

```
$ cat key_value_analytics

{"report":
    {
        "report_type":"key_value_analytics",
        "columns":[
            "hour",
            "seller_member_id",
            "key_name",
            "key_name_label",
            "key_value",
            "key_value_label",
            "imps",
            "clicks",
            "revenue",
            "ctr"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the [Report service](report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -X post -d @key_value_analytics "https://api.appnexus.com/report?advertiser_id=123"

{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### `GET` the report status from the Report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2016-12-11 19:15:48",
         "json_request": "{\"report\":{\"report_type\":\"key_value_analytics\",
             \"columns\":[\"hour\",\"seller_member_id\",
             \"key_name\",\"key_name_label\",\"key_value\",\"key_value_label\",
             \"imps\",\"clicks\",\"revenue\",\"ctr\"],
             \"report_interval\":\"last_48_hours\",\"format\":\"csv\",\"filters\":[{\"advertiser_id\":\"123\"}]}}",
             "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the Report Download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/key_value_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
