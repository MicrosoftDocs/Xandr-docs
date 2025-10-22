---
title: Multi Key Value Analytics Report
description: The Multi Key Value Analytics report provides information on network targeting keys and values, allowing sellers to view different keys associated with the same bid. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Multi Key Value Analytics report

The Multi Key Value Analytics report shows you the information associated with your network's defined targeting keys and values. This report helps seller need to view different keys associated with the same bid as a flat report and enables users to filter the report based on their keys. Currently, it is available to selected partners only (3 partners or 3 keys).

Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the **kw\_** prefix on the key name. For example, a placement tag containing *keyname=value1* will not serve and therefore not be logged, whereas a placement tag containing *kw_keyname=value1* will serve and be logged. This applies to ad calls with the following tag types: `/tt`, `/ttj`, `/fpt`, `/jpt`, `/pt`, `/ptv`, `/ssptv`, `/mtj`, `/map`, and `/mob`.

> [!NOTE]
> **AppNexus Seller Tags**
>
> When using [Seller Tag](../seller-tag/seller-tag.md), omit the **kw\_** prefix. AST has the `keyword` object in the body of the request, so the prefix is not needed.

Not all impressions from key/value targets will be included in reports. To be included, the targets must meet the following criteria:

- Key must be pre-defined. See the [Pre-Defining Targeting Keys and Values](../monetize/pre-defining-targeting-keys-and-values.md) page in the UI for more information.
- Value must be pre-defined OR Value must be targeted by at least one line item or campaign.
- Value is not a numeric range (greater than or less than).
- Value does not include a wildcard.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- today
- last_24_hours
- yesterday
- last_48_hours
- last_7_days
- month_to_date
- quarter_to_date

### Data retention period

Data in this report is retained for 428 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | Yes | `"2010-02"` | The month of the auction. |
| `day` | date | Yes | `"2010-02-01"` | The day of the auction. |  
| `hour` | date | Yes | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default. |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member.<br><br>**Note**: The name might be `"Default"` or `"Default Error"`, which means that there was no buyer for the impression, and a default creative was served. |  
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |  
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |  
| `seller_member` | string | No | `"That Seller (456)"` | The name and ID of the selling member. |  
| `placement_id` | int | Yes | `1212` | The ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id` . |
| `placement_name` | string | No | `"lvillage 160x600"` | The name of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | No | `"lvillage 160x600 (1212)"` | The name and ID of the placement. |
| `placement_group_id` | int | Yes | `765` | The ID of the site.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0`. |
| `placement_group_name` | string | No | `"Site 1"` | The name of the site. |
| `placement_group` | string | No | `"Site 1 (765)"` | The name and ID of the site. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a `default` or `PSA` was shown. |
| `advertiser_name` | string | No | `"AdvertiserA"` | The name of the advertiser. |
| `advertiser` | string | No | `"AdvertiserA (789)"` | The name and ID of the advertiser. |
| `line_item_id` | int | Yes | `1122` | The ID of the line item. |
| `line_item_name` | string | No | `"Line Item 1"` | The name of the line item. |
| `line_item` | string | No | `"Line Item 1 (1122)"` | The name and ID of the line item. |
| `publisher_id` | int | Yes | `555` | The ID of the publisher. |
| `publisher_name` | string | No | `"PublisherA"` | The name of the publisher. |
| `publisher` | string | No | `"PublisherA (555)"` | The name and ID of the publisher. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id`. |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1 ("Blank")`: No creative served.<br> - `2 ("PSA")`: A public service announcement served because there were no valid bids and no default creative was available.<br> - `3 ("Default Error")`: A default creative served due to a timeout issue.<br> - `4 ("Default")`: A default creative served because there were no valid bids.<br> - `5 ("Kept")`: Your advertiser's creative served on your publisher's site.<br> - `6 ("Resold")`: Your publisher's impression was sold to a third-party buyer.<br> - `7 ("RTB")`: Your advertiser's creative served on third-party inventory.<br> - `8 ("PSA Error")`: A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9 ("External Impression")`: An impression from an impression tracker.<br> - `10 ("External Click")`: A click from a click tracker.<br><br>**Note**: RTB auctions are not included in reports. An impression with `imp_type_id = 7` will not be reported. |
| `creative_id` | int | Yes | `444` | The ID of the creative.<br><br>**Note**:<br>- For impressions older than 100 days, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2017 728x90"` | The name of the creative.<br> - For impressions older than 100 days, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2017 728x90 (444)`" | The name and ID of the creative. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `advertiser_currency` | string | Yes | `"USD"` | The currency used by the advertiser. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order associated with the campaign that purchased the impression. |
| `insertion_order_name` | string | No | `"FirstIO"` | The name of the insertion order associated with the campaign that purchased the impression. |
| `insertion_order` | string | No | `"FirstIO(321)"` | The ID and name of the insertion order associated with the campaign that purchased the impression. |
| `publisher_currency` | money | Yes | `"EUR"` | The currency used by the publisher. |
| `revenue_type_id` | int | Yes | `4` | The ID of the revenue type for different impression types. |
| `revenue_type` | string | No | `"CPC"` | See [revenue_type as text for a corresponding revenue_type_id](#revenue_type-as-text-for-a-corresponding-revenue_type_id)|
| `device_type` | string | Yes | `"Desktops and Laptops"` | The type of the device where the impression has occurred. |
| `deal_id` | int | Yes | `123` | The ID of the deal. |
| `deal_name` | string | No | `"MyDeal"` | The name of the deal. |
| `deal` | string | No | `"MyDeal(123)"` | The name and ID of the deal. |
| `reporting_key_1_name` | string | Yes | `"fruit"` | The name of the first targeting key in the multi key-value report. |
| `reporting_key_1_value` | string | Yes | `"apple"` | The value associated with the first targeting key. |
| `reporting_key_1_name_label` | string | Yes | `"fruit eaten by customer"` | The label for the first key. The label can be a more descriptive version of the key name. |
| `reporting_key_1_value_label` | string | Yes | `"green or red apples"` | The label for the first value. The label can be a more descriptive version of the key value. |
| `reporting_key_2_name` | string | Yes | `"pet"` | The name of the second targeting key in the multi key-value report. |
| `reporting_key_2_value` | string | Yes | `"dog"` | The value associated with the second targeting key. |
| `reporting_key_2_name_label` | string | Yes | `"pet owned by customer"` | The label for the second key. The label can be a more descriptive version of the key name. |
| `reporting_key_2_value_label` | string | Yes | `"doberman or german shephard"` | The label for the second value. The label can be a more descriptive version of the key value. |
| `reporting_key_3_name` | string | Yes | `"vehicle"` | The name of the third targeting key in the multi key-value report. |
| `reporting_key_3_value` | string | Yes | `"car"` | The value associated with the third targeting key. |
| `reporting_key_3_name_label` | string | Yes | `"vehicle owned by customer"` | The label for the third key. The label can be a more descriptive version of the key name. |
| `reporting_key_3_value_label` | string | Yes | `"Ford or GM"` | The label for the third value. The label can be a more descriptive version of the key value. |

### `revenue_type` as text for a corresponding `revenue_type_id`

| `revenue_type_id` | `revenue_type` |
|:---|:---|
| `-1` | No Payment |
| `0` | Flat CPM |
| `1` | Cost plus CPM |
| `2` | Cost plus margin |
| `3` | CPC |
| `4` | CPA |
| `5` | Revshare |
| `6` | Flat Fee |
| `7` | Variable CPM |
| `8` | Estimated CPM |
| `9` | vCPM|
| `10` | CPCV|

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions. |
| `clicks` | int | `545` | clicks | The total number of clicks. |
| `booked_revenue` | money | `150.00` | booked_revenue | The total revenue booked through direct advertisers. |
| `reseller_revenue` | money | `100.00` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `revenue` | money | `250.00` | booked_revenue + reseller_revenue | The total revenue. |
| `rpm` | money | `1.25` | revenue / 1000 imps | The revenue per 1000 impressions, including defaults, PSAs, and errors. |
| `total_convs` | int | `5` | total_conversions | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.000221877080097626` | total_conversions / imps | The rate of conversions to impressions. |
| `imps_master_creative` | int | `1276` | imps_master_creative | The total number of impressions from the master creative in page-level roadblocking.<br><br>**Note**: This metric is in alpha testing and not available to all customers. |
| `imps_viewed` | int | `1122` | imps_viewed | The total number of viewed impressions. |
| `view_measured_imps` | int | `1121` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `reseller_revenue_pub_curr` | money | `200.00` | reseller_revenue_pub_curr | The total revenue on resold impressions through direct publishers in publishers' currency. |
| `rpm_pub_curr` | money | `1.23` | revenue / 1000 imps | The revenue per 1000 impressions, including defaults, PSAs, and errors in publishers' currency. |
| `booked_revenue_pub_curr` | money | `150.00` | booked_revenue_pub_curr | The total revenue booked through direct advertisers in publishers' currency. |
| `revenue_pub_curr` | money | `250.00` | booked_revenue + reseller_revenue | The total revenue in publishers' currency. |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"multi_key_value_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the `"format"` in which the data should be returned (`"csv"`, `"excel"`, or `"html"`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat multi_key_value_analytics

{"report":
    {
        "report_type":"multi_key_value_analytics",
        "columns":[
            "hour",
            "seller_member_id",
            "reporting_key_1_name",
            "reporting_key_1_name_label",
            "reporting_key_1_value",
            "reporting_key_1_value_label",
            "imps",
            "clicks",
            "revenue",
            "revenue_pub_curr"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the [report service](./report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -X post -d @multi_key_value_analytics "https://api.appnexus.com/report?advertiser_id=123"

{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2016-12-11 19:15:48",
         "json_request": "{\"report\":{\"report_type\":\"multi_key_value_analytics\",
             \"columns\":[\"hour\",\"seller_member_id\",
             \"reporting_key_1_name\",\"reporting_key_1_name_label\",\"reporting_key_1_value\",\"reporting_key_1_value_label\",
             \"imps\",\"clicks\",\"revenue\",\"revenue_pub_curr\"],
             \"report_interval\":\"last_48_hours\",\"format\":\"csv\",\"filters\":[{\"advertiser_id\":\"123\"}]}}",
             "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/multi_key_value_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
