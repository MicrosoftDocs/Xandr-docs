---
title: Network Publisher Analytics
description: Use the Network Publisher Analytics report to view granular performance data for specific publishers within a network, only available to network users.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network publisher analytics

The **Network Publisher Analytics** report can be used to view performance data for a specific publisher within your network that is more granular than the data provided in the Network Analytics report. This report is available to network users only. Publisher users can use the [Publisher Analytics](./publisher-analytics.md) report.

For usage instructions, see the [example](#example) below. Note that this report requires that a publisher ID be specified as part of the URL, for example:

```
https://api.appnexus.com/report?publisher_id=PUBLISHER_ID
```

## Time frame

The `report_interval` field can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_2_days
- last_7_days
- last_30_days
- month_to_date
- month_to_yesterday
- quarter_to_date
- last_month
- lifetime

### Data retention period

Data retention period for the report is 428 days.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | date | no | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | date | no | `"2010-02-01"` | The day of the auction. |
| `month` | date | no | `"2010-02"` | The month of the auction. |
| `buyer_member_id` | int | yes | `567` | The ID of the buying member. |
| `buyer_member_name` | string | no | `"Network"` | The name of the buying member.<br><br>**Note**: The name might be `"Default"` or `"Default Error"`, which means that there was no buyer for the impression, and a default creative was served. |
| `buyer_member` | string | no | `"Network (567)"` | **Deprecated**. |
| `seller_member_id` | int | yes | `67` | The ID of the selling member. |
| `advertiser_id` | int | yes | `728` | The ID of the advertiser. |
| `advertiser_name` | string | no | `"Test"` | The name of the advertiser. |
| `advertiser` | string | no | `"Test (123)"` | **Deprecated**. |
| `advertiser_code` | string | no | `"Code"`| The custom code for the advertiser. |
| `line_item_id` | int | yes | `554` | The ID of the line item. |
| `line_item_name` | string | no | `"Q1 Pepsi"` | The name of the line item. |
| `line_item` | string | no | `"Q1 Pepsi (554)"` | **Deprecated**. |
| `line_item_code` | string | no | `"Q1 Pepsi Code"` | The custom code for the line item. |
| `campaign_id` | int | yes | `567` | The ID of the campaign. |
| `campaign_name` | string | no | `"Photos 728x90"` | The name of the campaign. |
| `campaign` | string | no | `"Photos 728x90 (567)"` | **Deprecated**. |
| `campaign_code` | string | no | `"Photos Code"` | The custom code for the campaign. |
| `campaign_priority` | int | no | `5` | The bidding priority of a campaign that targets direct inventory. For more information, see [Bidding Priority](../monetize/bidding-priority.md) in the UI documentation.<br>Possible values: `1` - `10`, where `10` is the highest priority. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `creative_id` | int | yes | `554` | The ID of the creative.<br><br>**Note**:<br> - For impressions older than 100 days, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `brand_id` | int | yes | `3` | The ID of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | no | `"Ace Hardware"` | The name of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand` | string | no | `"Ace Hardware (3)"` | **Deprecated**. |
| `publisher_id` | int | yes | `6787` | The number to identify the publisher. |
| `publisher_code` | string | no | `"Publisher Code"` | The custom code to the identify the publisher. |
| `publisher_currency` | string | yes | `"USD"` | The currency of the publisher. |
| `pub_rule_id` | int | no | `54` | The number to identify the publisher rule. |
| `pub_rule_name` | string | no | `"50% Revshare"` | The name of the publisher rule. |
| `pub_rule` | string | no | `"50% Revshare (54)"` | **Deprecated**. |
| `pub_rule_code` | string | no | `"50% Revshare Code"` | The custom code for the publisher rule. |
| `site_id` | int | yes | `194` | The ID of the site.<br><br>**Note**: For impressions older than 100 days, the `site_id` will be `0` . |
| `site_name` | string | no | `"Site Name"` | The name of the site. |
| `site` | string | no | `"Site Name (593)"` | **Deprecated**. |
| `site_code` | string | no | `"Site Name Code`" | The custom code for the site. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. |
| `geo_country` | string | yes | `"US"` | The geographic country/region code. |
| `geo_country_name` | string | no | `"Unites States"` | The name of the country/region. |
| `size` | string | no | `"300x250"` | The size of the creative served. |
| `placement_id` | int | yes | `546` | The ID of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | no | `"300x250 Business"` | The name of the placement.<br><br>**Note**: For impressions older than 100 days, placements will be aggregated into one row with `"All placement data older than 100 days"` as the `placement_name`. |
| `placement` | string | yes | `"300x250 Business (546)"` | **Deprecated**. |
| `placement_code` | string | no | `"300x250 Business Code"` | The custom code for the placement. |
| `imp_type_id` | int | yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br>`1` ("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `imp_type` | string | yes | `"Kept"` | The type of impression. For possible values, see `imp_type_id`. |
| `buyer_type` | string | yes | `"Reseller"` | The type of buyer, set by Xandr. |
| `supply_type` | string | no | `"web"` | The type of inventory. Possible values: <br> - `"web"` <br> - `"mobile_web"`<br> - `"mobile_app"` |
| `payment_type` | string | yes | `"cpm"`, `"revshare"` | The type of payment to a broker. |
| `revenue_type` | string | yes | `"CPA"` | The basis on which the member gets paid. |
| `revenue_type_id` | int | yes | `4` | The ID of the revenue type. Possible values: <br> `-1` = No Payment <br>`0` = Flat CPM <br>`1` = Cost Plus CPM <br>`2` = Cost Plus Margin <br>`3` = CPC <br>`4` = CPA <br>`5` = Revshare <br> `6` = Flat Fee <br>`7` = Variable CPM <br>`8` = Estimated CPM |
| `external_inv_id` | int | Yes | `4921` | The ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](./external-inventory-code-service.md).<br> For impressions older than 100 days, the `external_inv_id` will be `0`. |
| `external_inv_name`  | string | No | `"External Inv Name"` | The name of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](./external-inventory-code-service.md). |
| `external_inv` | string | No | `"External Inv Name (4921)"` | **Deprecated**. |
| `media_type` | string | no |  `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of the creative. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | yes | `2` | **Read-only**. The ID of the media type to which the subtype belongs. |
| `adjustment_id` | int | yes | `890` | The ID of the adjustment used to make changes to the media cost and/or impressions, clicks, and conversions you see in reporting for a publisher. |
| `venue` | string | yes | `"Venue Name"` | The name of the cluster of domain, site, tag, and user country/region that Xandr' optimization system uses to determine bid valuations. A campaign cannot targeted a venue explicitly. |
| `predict_rev_type` | int | yes | `2` | The optimization phase of a campaign that served on the publisher's inventory. Possible values:<br>`-2` = No predict phase<br>`-1` = Base predict phase<br>`0` = Learn giveup<br>`1` = Learn<br>`2` = Throttled<br>`3` = Optimized<br>`4` = Biased<br>`5` = Optimized 1<br>`8` = Optimized giveup<br>`9` = Base bid below giveup |
| `is_takeover` | boolean | Yes | `"Yes"` | Indicates whether an impression was `Blanked` or `Defaulted` because at least one of the ads in the multi-ad request was a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps_total` | int | `2340` | imps | The total number of impressions (served and resold). |
| `imps_sold` | int | `42500` | imps_sold | The number of impressions you sold to other members. |
| `imps_default` | int | `321` | imps_default | The number of impressions that defaulted. |
| `imps_blank` | int | `3` | imps_blank | The number of impressions served with a blank. |
| `imps_psa` | int | `5` | imps_psa | The number of impressions served with a PSA. |
| `imps_psa_error` | int | `0` | imps_psa_error | The number of impressions served with a PSA due to a default error. |
| `imps_default_error` | int | `0` | imps_default_error | The number of impressions that defaulted due to a timeout issue. |
| `imps_default_bidder` | int | `0` | imps_default_bidder | The number of impressions that defaulted because there were no valid bids. |
| `imps_kept` | int | `0` | imps_kept | The number of impressions kept (direct). |
| `imps_resold` | int | `0` | imps_resold | The number of impressions resold. |
| `imps_rtb` | int | `2332` | imps_rtb | The number of rtb impressions. |
| `external_impression` | int | `0` | external_impression | The number of external impressions. |
| `external_click` | int | `0` | external_click | The number of external clicks. |
| `clicks` | int | `545` | clicks | The total number of clicks across all impressions. |
| `click_thru_pct` | double | `1.12359550561797` | (clicks / imps) * 100 | The rate of clicks to impressions as a percentage. |
| `total_convs` | int | `90` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `post_view_convs_pixel` | int | `23` |  | Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Microsoft Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Microsoft Invest)](../invest/conversion-attribution.md). |
| `post_clicks_convs_pixel` | int | `15` |  | Post click conversions for the pixel. Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `ctr` | double | `0.2327836` | clicks / imps * 100 | The rate of clicks to impressions. |
| `convs_rate` | double | `0.0384413` | total_convs / imps * 100 | The rate of conversions to impressions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `network_revenue` | money | `1201.13` | network_revenue | Network revenue booked through direct advertisers and resold to real time buyers. |
| `total_network_rpm` | money | `2.60548314606741` | (network_revenue / imps) x 1000 | The network revenue per 1000 impressions. |
| `publisher_revenue` | money | `400.05` | publisher_revenue | The revenue paid out to the publisher (based on revshare or cpm). |
| `publisher_revenue_pub_curr` | money | `400.05` | publisher_revenue | The revenue paid out to the publisher (based on revshare or cpm), in the currency of the publisher. |
| `publisher_rpm_pub_curr` | money | `1.71` | (publisher_revenue / imps) x 1000 | The publisher revenue per 1000 impressions, in the currency of the publisher. |
| `network_profit` | money | `801.08` | (booked revenue + reseller revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost. |
| `network_roi` | money |  |  | **To be deprecated**. The return on investment for the network. |
| `network_roi_net_commissions` | double |  |  | **To be deprecated**. |
| `network_rpm` | money | `3.42` | (network_revenue / imps) x 1000 | The network revenue per 1000 impressions. |
| `sold_network_rpm` | double |  |  |  |
| `publisher_rpm` | money | `1.71` | (publisher_revenue / imps) x 1000 | The publisher revenue per 1000 impressions. |
| `total_publisher_rpm` | money |  |  |  |
| `sold_publisher_rpm` | double |  |  |  |
| `network_ppm` | money | `9.23` | (profit / imps) x 1000 | **To be deprecated**. The profit per 1000 impressions. |
| `network_revenue_net_commissions` | money |  |  | **To be deprecated**. |
| `network_profit_net_commissions` | money |  |  | **To be deprecated**. |
| `network_rpm_net_commissions` | money |  |  | **To be deprecated**. |
| `network_ppm_net_commissions` | money |  |  | **To be deprecated**. |
| `media_cost_pub_curr` | money | `16.833378` | media_cost_pub_curr | The total cost of the inventory purchased, in the currency of the publisher. |
| `commissions` | money | `0` | Commissions for standard line items, $0 for ALIs. | Fees that come out of the booked revenue. Commissions for standard line items, $0 for ALIs. |
| `serving_fees` | money | `0.025143` | Serving fees for standard line items, $0 for ALIs. | Fees that are added to the media cost. Serving fees for standard line items, $0 for ALIs. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable per the IAB Viewability definition. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `partner_fees` | money | `123.45` |  | The total amount of third-party costs, budgeted using the [Partner Fee Service](./partner-fee-service.md), that have accrued on an augmented line item over the reported period of time. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `network_profit_ecpm` | money | `123.45` | ((booked_revenue + reseller_revenue - total cost)/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | (booked_revenue + reseller_revenue - total cost)/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | (booked_revenue + reseller_revenue - total cost)/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45` | (booked_revenue + reseller_revenue - total cost)/(booked_revenue + reseller_revenue) | Network profit margin. |
| `buying_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * advertiser_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the buyer used to purchase the inventory.|
| `selling_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * publisher_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the seller used to sell the inventory. |

## Example

### Create JSON formatted report request

```
{code}$ cat network_publisher_analytics
{
    "report":
    {
        "report_type":"network_publisher_analytics",
        "columns":[
            "hour",
            "buyer_member_id",
            "inventory_source",
            "gender",
            "imps_total",
            "imps_sold",
            "imps_default",
            "clicks",
            "total_convs",
            "ctr",
            "convs_rate"
        ],
        "row_per":[
            "hour",
            "buyer_member_id",
            "inventory_source_id",
            "gender"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
{code}
```

### `POST` the request to the reporting service

```
{code}$ curl -b cookies -c cookies -X post -d @network_publisher_analytics "https://api.appnexus.com/report?publisher_id=4642"
{
   "response":{
      "status":"OK",
      "report_id":"f4ebb93755dd01dde4fc157f86198ea9"
   }
}
{code}
```

### `GET` the report status from the report service

Make a `GET` call with the Report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
{code}$ curl -b cookies -c cookies "https://api.appnexus.com/report?id=f4ebb93755dd01dde4fc157f86198ea9"
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:37:31",
         "json_request":"{\"report\":{\"report_type\":\"network_publisher_analytics\",\"columns\":[\"hour\",\"buyer_member_id\",\"inventory_source\",
            \"gender\",\"imps_total\",\"imps_sold\",\"imps_default\",\"clicks\",\"total_convs\",\"ctr\",\"convs_rate\"],
            \"row_per\":[\"hour\",\"buyer_member_id\",\"inventory_source_id\",\"gender\"],\"report_interval\":\"last_48_hours\",
            \"filters\":[{\"publisher_id\":\"4642\"}]}}",
         "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
{code}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the Report ID, but this time to the **report-download** service. You can find the service and Report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/network_publisher_analytics.csv
{code}
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
