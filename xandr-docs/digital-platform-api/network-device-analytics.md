---
title: Network Device Analytics
description: Use the Network Device Analytics report to view performance data for buy-side and sell-side ads targeting compatible devices, useful for networks working with in-app advertisers.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network device analytics

The **Network Device Analytics** report enables you to retrieve buy-side and sell-side performance data based on devices where impressions were served. This is especially important for networks working with in-app advertisers who traffic creatives that encourage app installation and who therefore want confirmation that their creatives are targeting devices compatible with their apps. It also helps you answer the following questions:

- How many impressions have you seen for specific device makes and models?
- How many impressions have you seen for specific connection types (i.e., Wifi/Static or Carrier-based)?
- How do certain types of devices perform relative to others (i.e., tablets vs. phones)?
- How do certain makes and models of devices perform relative to others (i.e., Android vs. Apple)?
- How do certain types of connections perform relative to others (i.e., Wifi/Static vs. Carrier-based)?

## Time frame and time zone

The `report_interval` field can be set to one of the following:

- today
- yesterday
- last_2_days
- last_7_days
- last_14_days
- last_30_days
- month_to_date
- month_to_yesterday

Alternately, the `start_date` and `end_date` fields can be set to a range within the last 30 days. However, since hourly data is not available for this report, the `start_date` and `end_date` cannot be identical and must be formatted as `"YYYY-MM-DD"` rather than `"YYYY-MM-DD HH:MM:SS"`. The `timezone` field in the JSON request can be set only to `"UTC"`, but this is not necessary, as the timezone defaults to `"UTC"` if not specified.

### Data retention period

Data in this report has the following retention period:
- Hourly retention: 100 days
- Daily retention: 500 days

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | time | Yes | `"2010-02"` | The month of the auction. |
| `day` | time | Yes | `"2010-02-01"` | The day of the auction. |
| `device_make_id` | int | Yes | `1` | The ID of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). To retrieve a complete list of device make IDs and names, use the [Device Make Service](./device-make-service.md). |
| `device_make_name` | string | No | `"4G Systems"` | The name of the device make on which the impression was served. The make is generally the manufacturer of the device (i.e., Apple). |
| `device_make` | string | No | `"4G Systems (1)"` | **Deprecated**. |
| `device_model_id` | int | Yes | `15` | The ID of the device model on which the impression was served. The model is generally the specific product (i.e., iPhone). To retrieve a complete list of device model IDs and names, use the [Device Make Service](./device-make-service.md). |
| `device_model_name` | string | No | `"DX650"` | The name of the device model on which the impression was served. The model is generally the specific product (i.e., IPhone). |
| `device_model` | string | No | `"DX650 (15)"` | **Deprecated**. |
| `device_type` | string | Yes | `"tablets"` | The type of device on which the impression was served. Possible values are:<br> - `"desktops & laptops"`<br> - `"tablets"`<br> - `"mobile phones"`<br> - `"tv"`<br> - `"game consoles"`<br> - `"set top box"`<br> - `"media players"`<br> - `"other devices"` |
| `connection_type` | string | Yes | `"Carrier-based"` | The type of internet connection at the time of the impression. Possible values:<br> - `"Carrier-based"`<br> - `"Wifi or Static"` |
| `operating_system_id` | int | Yes | `24` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_name` | string | Yes | `"Android 2.3.5 Gingerbread"` | The name of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_id` | int | Yes | `2` | The ID of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_name` | string | Yes | `"Android"` | The name of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `browser_id` | int | Yes |  | The ID of the browser in which the impression was served. To retrieve a complete list of browser IDs and names, use the [Browser Service](./browser-service.md). |
| `browser_name` | string | Yes |  | The ID of the browser in which the impression was served. |
| `browser` | string | Yes |  | **Deprecated**. |
| `entity_member_id` | int | Yes | `123` | If `imp_type` is: <br> `1` (Blank) <br>`2` (PSA) <br> `3` (Default Error) <br> `4` (Default) <br> `6` (Resold) <br> `8` (PSA Resulting from Default Error), the ID of the buying member; otherwise, the ID of the selling member. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member. |
| `buyer_member` | string | No | `"My Network (123)"` | **Deprecated**. |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |
| `seller_member` | string | No | `"That Seller (456)"` | **Deprecated**. |
| `buyer_type` | string | Yes | `"Real Time"` | The type of media purchased by the buyer member. Possible values: `"Real Time"` or `"Direct"`. |
| `seller_type` | string | Yes | `"Real Time"` | The type of media sold by the seller member. Possible values: `"Real Time"` or `"Direct"`. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer or a default or PSA was shown. |
| `advertiser_name` | string | No | `"Mobile Zombies"` | The name of the advertiser. |
| `advertiser` | string | No | `"Mobile Zombies (789)"` | **Deprecated**. |
| `advertiser_code` | string | No | `"MZB1010"` | The custom code for the advertiser. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"Mobile Insertion Order"` | The name of the insertion order. |
| `insertion_order` | string | No | `"Mobile Insertion Order (321)"` | **Deprecated**. |
| `insertion_order_code` | string | No | `"Mobile Insertion Order Code"` | The custom code for the insertion order. |
| `line_item_id` | int | Yes | `111` | The ID of the line item. |
| `line_item_name` | string | No | `"Mobile Line Item"` | The name of the line item. |
| `line_item` | string | No | `"Mobile Line Item (111)"` | **Deprecated**. |
| `line_item_code` | string | No | `"Mobile Line Item Code"` | The custom code for the line item. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `campaign_name` | string | No | `"Mobile Campaign"` | The name of the campaign. |
| `campaign` | string | No | `"Mobile Campaign (222)"` | **Deprecated**. |
| `campaign_code` | string | No | `"Mobile Campaign Code"` | The custom code for the campaign. |
| `deal_name` | string | Yes | `"My New Deal"` | The name of the deal associated with the transaction for the impression. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `deal_id` | int | Yes | `123` | The ID of the deal associated with the transaction for the impression. |
| `pixel_id` | int | Yes | `3849` | The ID of the conversion pixel. |
| `media_type` | string | Yes | `"Banner"` | The media type of the creative. Possible values: <br> - `"Banner"` <br> - `"Pop"` <br> - `"Interstitial"` <br> - `"Video"` <br> - `"Text"` <br> - `"Expandable"` <br> - `"Skin"` <br> To retrieve a complete list of media types, use the [Media Type Service](./media-type-service.md). |
| `mediatype_id` | int | Yes | `1` | The ID of the media type of the creative. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `geo_country` | string | Yes | `"US"` | The code for the country/region. |
| `geo_country_name` | string | No | `"United States"` | The name of the country/region. |
| `payment_type` | string | Yes | `"cpm"`, `"revshare"` | The type of payment to a broker. |
| `revenue_type` | string | No | `"CPA"` | The basis on which the advertiser pays the member. |
| `revenue_type_id` | int | Yes | `4` | The ID of the revenue type. Possible values: <br> `-1` = No Payment <br> `0` = Flat CPM <br> `1` = Cost Plus CPM <br> `2` = Cost Plus Margin <br> `3` = CPC <br> `4` = CPA <br> `5` = Revshare <br> `6` = Flat Fee <br> `7` = Variable CPM <br> `8` = Estimated CPM |
| `publisher_name` | string | No | `"AppSite"` | The name of the publisher. |
| `publisher` | string | Yes | `"AppSite (123)"` | The name of the publisher followed by the ID (Xandr format). |
| `publisher_code` | string | No | `"AS123"` | The custom code for the publisher. |
| `pub_rule_name` | string | No | `"Publisher Rule Name"` | The name of the publisher rule. |
| `pub_rule` | string | No | `"Publisher Rule Name (555)"` | The name of the publisher rule followed by the ID (Xandr format). |
| `pub_rule_code` | string | No | `"AppSitePR123"` | The custom code for the publisher rule. |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for the impression. <br><br>**Note**: The term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `imp_type_id` | int | Yes | `6` | The ID for the type of impression. Possible values (associated types in parentheses):<br>`1` ("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `imp_type` | string | Yes | `"Resold"` | The type of impression. For possible values, see `imp_type_id`. |
| `venue` | string | Yes | `"Venue Name"` | The name of the cluster of domain, site, tag, and user country/region that our optimization system uses to determine bid valuations. A campaign cannot target a venue explicitly. |
| `operating_system_family_id` | int | Yes | `2` | The ID of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_name` | string | Yes | `"Android"` | The name of the operating system family associated with the device the impression was served on.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br>Use the [Operating System Extended service](./operating-system-extended-service.md) to look up which operating system versions are within a given operating system family. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `imps_blank` | int | `3` | imps_blank | The number of impressions served with a blank. |
| `imps_psa` | int | `5` | imps_psa | The number of impressions that served a PSA. |
| `imps_default_error` | int | `0` | imps_default_error | The number of impressions that defaulted due to a timeout issue. |
| `imps_default_bidder` | int | `0` | imps_default_bidder | The number of impressions that defaulted because there were no valid bids. |
| `imps_kept` | int | `0` | imps_kept | The number of impressions your advertiser purchased from your publisher . |
| `imps_resold` | int | `0` | imps_resold | The number of impressions your publisher sold to a third party. |
| `imps_rtb` | int | `2332` | imps_rtb | The number of impressions your advertiser bought from a third party. |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. |
| `click_thru_pct` | double | `1.12359550<br>561797%` | (clicks / imps) x 100 | The rate of clicks to impressions as a percentage. |
| `ctr` | double | `0.00022187`<br>`7080097626` | clicks / imps | The rate of clicks to impressions. |
| `total_convs` | int | `1` | total_convs | The total number of post-view and post-click conversions. |
| `post_view_convs` | int | `15` | post_view_convs | The total number of recorded post-view conversions. |
| `post_click_convs` | int | `15` | post_click_convs | The total number of recorded post-click conversions. |
| `convs_per_mm` | double | `221.877080`<br>`097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `convs_rate` | double | `0.00022187`<br>`7080097626` | total_convs / imps | The rate of conversions to impressions. |
| `cost` | money | `16.833378` | cost | The total amount of media cost for direct publisher and purchased third-party inventory. |
| `cpm` | money | `1.66051685`<br>`393258` | (cost / imps) x 1000 | The media cost per 1000 impressions. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The total revenue booked through direct advertisers (line item) and direct publishers (resold impressions). |
| `booked_revenue` | money | `25.767257` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `reseller_revenue` | money | `0` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `total_rpm` | money | `2.60548314`<br>`606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. This value will be displayed in USD as well as potentially the Buying Currency and Selling Currency (if you've selected those dimensions). |
| `profit` | money | `0.084102` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `ppm` | money | `0.94496629`<br>`2134831` | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| `total_publisher_rpm` | money | `1.6605168`<br>`5393258` | (cost / imps) x 1000 | The cost per 1000 impressions paid to direct and third-party publishers, including errors. |
| `sold_publisher_rpm` | double | `147.786` | (cost / imps) x 1000 ----- no errors | The cost per 1000 impressions paid to direct and third-party publishers, not including errors. |
| `sold_network_rpm` | double | `231.888` | (revenue / imps) x 1000 ----- no errors | The revenue per 1000 impressions that were not errors. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `network_profit` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost. |
| `network_profit_ecpm` | money | `123.45` | (network_profit/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | network_profit/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | network_profit/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45` | network_profit/(booked_revenue + reseller_revenue) | Network profit margin. |
| `profit_ecpm` | money | `123.45` | ((booked_revenue - total_cost)/imps) * 1,000 | Profit per 1,000 imps. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin. |
| `device_type` | string | `Tablets`,`mobile phones` |  | This is the type of device being used. |
| `convs_device_make` | string | `Apple (26)` |  | This is the device that the conversion occurred on. This can be compared against Device Make to determine what device the impression occurred on. |
| `device_make` | string | `Apple (26)` |  | This is the brand name of the device. |
| `convs_device_type` | string | `Tablets`, `mobile phones` |  | This can be compared against Device Type to determine what device the conversion occurred on. |
| `video_skips` | int | `10` |  | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` |  | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` |  | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `10` |  | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` |  | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` |  | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` |  | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2` |  | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` |  | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` |  | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` |  | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` |  | The percentage of times the user opted to skip the video. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` `"network_device_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md). In this example, we want to see performance data about US impressions for advertiser 1459 for each of the last 14 days. Specifically, for each combination of device make, device model, connection type, and impression type, we want the number of impressions, the number of clicks, the total money spent, the money spent per 1000 impressions, the money paid to us by the advertiser, and the total profit (money earned - money spent).

```
$ cat network_device_analytics

{
    "report": {
        "report_type": "network_device_analytics",
        "filters": [
            {
                "advertiser_id": 1459
            },
            {
                "geo_country": "US"
            }
        ],
        "columns": [
            "day",
            "connection_type",
            "imp_type",
            "imps",
            "clicks",
            "cost",
            "cpm",
            "booked_revenue",
            "profit"
        ],
        "report_interval": "last_14_days",
        "format": "csv",
    }
}
```

### `POST` the request to the reporting service

`POST` the JSON request to get back a Report ID.

```
$ curl -b cookies -c cookies -X POST -d @network_device_analytics 'https://api.appnexus.com/report'
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2013-02-01 12:19:53",
            "json_request": "{\"report\":{\"report_type\":\"network_device_analytics\",\"filters\":[{\"advertiser_id\":1459},
             {\"geo_country\":\"US\"}],\"columns\":[\"day\",\"device_make_id\",\"device_model_id\",\"connection_type\",
             \"imp_type\",\"imps\",\"clicks\",\"cost\",\"cpm\",\"booked_revenue\",\"profit\"],\"format\":\"csv\"]}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2013-02-01 12:19:53",
            "json_request": "{\"report\":{\"report_type\":\"network_device_analytics\",\"filters\":[{\"advertiser_id\":1459},
             {\"geo_country\":\"US\"}],\"columns\":[\"day\",\"device_make_id\",\"device_model_id\",\"connection_type\",
             \"imp_type\",\"imps\",\"clicks\",\"cost\",\"cpm\",\"booked_revenue\",\"profit\"],\"format\":\"csv\"]}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/network_device_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topics

- [Report Service](./report-service.md)
- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
