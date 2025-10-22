---
title: Network Advertiser Analytics
description: Use the Network Advertiser Analytics report to get detailed performance data for specific advertisers. It is only available to network users.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Network advertiser analytics

The **Network Advertiser Analytics** report is used to view performance data for a specific advertiser that is more detailed than the data provided in the [Network Analytics](./network-analytics.md) report. This report is available to network users only. Advertiser users can use the [Advertiser Analytics](./advertiser-analytics.md) report.

> [!NOTE]
> For usage instructions, see below. Note that this report requires that an advertiser ID be specified as part of the URL, for example:
>
> ```
> https://api.appnexus.com/report?advertiser_id=ADVERTISER_ID
> ```

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

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

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data. However, daily, monthly and cumulative intervals are still available.
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match statistics shown elsewhere in Invest or Monetizes for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months are aggregated. The data from Billing reports are kept in non-aggregated form indefinitely.

## Dimensions

Some dimensions have attributes. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: `dimension_name.attribute_name`.

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | date | No | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | date | No |`2010-02-01` | Day of the month. |
| `month` | date | No | `2010-02` | Month of the year. |
| `advertiser_code` | string | No | `"Advertiser Code"` | The custom code for the advertiser. |
| `buyer_member_id` | int | Yes | `123` | The internal ID of the buying member in the impression. |
| `bidder_id` | int | No | `436537` | The ID of the bidder or DSP (demand side platform) that the buyer used to purchase this impression. |
| `bidder_name` | string | No | `"Bidder's name"` | The name of the bidder or DSP (demand side platform) that the buyer used to purchase this impression. |
| `seller_member_id` | int | Yes | `567` | The internal ID of the selling member. |
| `seller_member_name` | string | No | `"AdMeld"` | The display name of the selling member. |
| `seller_member` | string | No | `"AdMeld (567)"` | **Deprecated**. |
| `advertiser_id` | int | Yes | `344` | The internal ID of the advertiser whose campaign and creative served in the impression. |
| `campaign_id` | int | Yes | `728` | Number to identify the campaign. |
| `campaign_name` | string | No | `"Test"` | Display name of the campaign |
| `campaign` | string | No | `"Test (123)"` | **Deprecated**. |
| `campaign_code` | string | No | `"Campaign Code"` | The custom code for the campaign |
| `campaign_priority` | int | No | `5` | The bidding priority for a campaign that targets direct inventory.<br>Possible values: `1` - `10,` where `10` is the highest priority. |
| `split_id` | int | Yes | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |
| `split_name` | string | Yes | `"Mobile Split A"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_name` (if included) will be `null`. |
| `creative_id` | int | Yes | `554` | The ID of the creative.<br><br>**Note**: <br> - For impressions older than 14 months, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The name of the creative.<br><br>**Note**: <br> - For impressions older than 14 months, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative_code` | string | No | `"12655"` | The code for the creative.<br><br>**Note**: <br> - For impressions older than 100 days, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, `creative_code` will be `"External Clicks"` or `"External Imps"`. |
| `creative` | string | No | `"Q1 2010 728x90 (554)"` | **Deprecated**. |
| `site_id` | int | Yes | `194` | The ID of the site.<br><br>**Note**: For impressions older than 14 months, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site Name"` | The name of the site. |
| `site` | string | No | `"Site Name (593)"` | **Deprecated**. |
| `placement_id` | int | Yes | `567` | The ID of the placement.<br><br>**Note**: For impressions older than 14 months, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No | `"Photos 728x90"` | The name of the placement.<br><br>**Note**: For impressions older than 14 months, placements will be aggregated into one row with `"All placement data older than 14 months"` as the `placement_name`. |
| `placement` | string | No | `"Photos 728x90 (123)"` | **Deprecated**. |
| `placement_code` | string | No | `"Placement Code"` | The custom code for the placement. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)"` | **Deprecated**. |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. For deals with external supply partners, this is generally the string that you use to identify the deal. |
| `size` | string | Yes | `"728x90"` | Size of the creative/placement |
| `geo_country` | string | Yes | `"US"` | Geographic country/region code |
| `geo_country_name` | string | No | `"Unites States"` | Name of the country/region |
| `creative_recency_bucket` | string | Yes | `"11-20"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative recency data. |
| `creative_recency_bucket_id` | string | No | `"4"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative recency data. |
| `creative_frequency_bucket` | string | Yes | `"15-30 minutes"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative frequency data. |
| `creative_frequency_bucket_id` | string | No | `"3"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative frequency data. |
| `insertion_order_id` | int | Yes | `654` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"Insertion Order Name"` | The name of the insertion order. |
| `insertion_order` | string | No | `"Insertion Order Name (654)"` | **Deprecated**. |
| `insertion_order_code` | string | No | `"Insertion Order Code"` | The custom code for the insertion order. |
| `insertion_order.type` | string | No | `"Legacy IO"` | The type of insertion order associated with the impression (e.g. Legacy, Seamless). |
| `insertion_order.state` | string | No | `"active"` | The state of the insertion order associated wih the impression. |
| `insertion_order.start_date` | date | No |  | The start date of the non-seamless insertion order associated with the impression. For seamless orders, see `billing_period.start_date`. |
| `insertion_order.end_date` | date | No |  | The end date of the non-seamless insertion order associated with the impression. For seamless orders, see `billing_period.end_date`. |
| `insertion_order.booked_impressions_budget_daily` | int | No | `2000` | The daily impression budget for the insertion order. |
| `insertion_order.booked_impressions_budget_lifetime` | int | No | `20000` | The lifetime impression budget for the insertion order. |
| `insertion_order.booked_revenue_budget_daily` | money | No | `200.00` | The daily budget in revenue for the insertion order. |
| `insertion_order.booked_revenue_budget_lifetime` | money | No | `10000.00` | The lifetime budget in revenue for the insertion order. |
| `insertion_order.billing_code` | string | No | `"E4567"` | The billing code associated with the insertion order. |
| `type_for_insertion_order` | string | Yes | `"Retargeting IO"` | A custom reporting field describing the type of insertion order. See the `labels` field in the [Insertion Order Service](../yield-analytics-api/insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `salesrep_for_insertion_order` | string | Yes | `"Patricia Martin"` | A custom reporting field containing the sales representative for the insertion order. See the `labels` field in the [Insertion Order Service](../yield-analytics-api/insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `trafficker_for_insertion_order` | string | Yes | `"George Martin"` | A custom reporting field containing the trafficker for the insertion order. See the `labels` field in the [Insertion Order Service](../yield-analytics-api/insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `billing_period.start_date` | datetime | No | `"2015-05-25 19:19:53"` | The earliest date of the insertion order's billing period.<br><br>**Note**:<br>**Alpha-Beta Notice**: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period.end_date` | datetime | No | `"2015-05-30 19:19:53"` | The last date of the insertion order's billing period.<br><br>**Note**: **Alpha-Beta Notice**: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period.booked_imps_budget_daily` | int | No | `3500` | The daily impression budget of the insertion order's billing period. |
| `billing_period.booked_imps_budget_lifetime` | int | No | `30000` | The lifetime impression budget of the insertion order's billing period. |
| `billing_period.booked_revenue_budget_daily_buying_currency` | money | No | `250.00` | The daily revenue budget of the insertion order's billing period. |
| `billing_period.booked_revenue_budget_lifetime_buying_currency` | money | No | `2500.00` | The lifetime revenue budget of the insertion order's billing period. |
| `billing_period.external_code` | string | No | `"houseware245"` | The custom code for the billing period (`budget_interval`). |
| `payment_type` | string | Yes | `"CPM"` | How the buyer is paying for the impression. Possible values:<br> - `"No payment"`<br> - `"CPM"`<br> - `"CPC"`<br> - `"CPA"`<br> - `"Owner CPM"`<br> -  `"Owner revshare"` |
| `supply_type` | string | No | `"web"` | The type of supply in the impression. Possible values:<br> - `"web"`: A site viewed on a desktop browser.<br> - `"mobile_web"`: A site viewed on a mobile browser.<br> - `"mobile_app"`: An app running on a mobile device. |
| `line_item_id` | int | Yes | `932` | Number to identify the line item. |
| `line_item_name` | string | No | `"$3 CPM Verizon Remarketing"` | Display name of the line item. |
| `line_item` | string | No | `"$3 CPM Verizon Remarketing (932)"` | **Deprecated**. |
| `line_item_code` | string | No | `"Line Item Code"` | The custom code for the line item. |
| `line_item.type` | string | No | `"standard"` | The line item type (e.g., standard, augmented). |
| `line_item.status` | string | No | `"active"` | The state of the line item (e.g., `active`, `inactive`). |
| `line_item.start_date` | datetime | No | `2017-02-06 00:00:00 EST5EDT` | The start date of the non-augmented line item. For augmented line Items (ALIs), see `flight.start_date`. |
|`line_item.end_date` | datetime | No | `2017-02-09 23:00:00 EST5EDT` | The end date of the non-augmented line item. For augmented line Items (ALIs), see `flight.end_date`. |
|`line_item.booked_impressions_budget_daily` | int | No | `2000` | The daily impression budget for the line item. |
| `line_item. booked_impressions_budget_lifetime` | int | No | `20000` | The lifetime impression budget for the line item. |
| `line_item.booked_revenue_budget_daily_adv_curr` | money | No | `1200.00` | The daily budget in revenue for the line item. |
| `line_item.booked_revenue_budget_lifetime_adv_curr` | money | No | `23000.00` | The lifetime budget in revenue for the line item. |
| `line_item.comments` | string | No | `"extension of Feb spend"` | Any comments related to this line item. |
| `type_for_line_item` | string | Yes | `"Branding IO"` | A custom reporting field describing the type of line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `salesrep_for_line_item` | string | Yes | `"Patricia Martin"` | A custom reporting field containing the sales representative for the line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `trafficker_for_line_item` | string | Yes | `"George Martin"` | A custom reporting field containing the trafficker for the line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `pixel_id` | int | Yes | `1942` | The ID of the conversion pixel.<br><br>**Note**: This dimension will return a maximum of 10 conversion pixels. Also, you can filter by No more than 10 conversion pixels. |
| `flight` | int | Yes | `123475` | The line item flight ID. |
| `flight.start_date` | datetime | No | `2017-02-06 00:00:00 EST5EDT` | The start date of the line item's flight. |
| `flight.end_date` | datetime | No | `2017-02-09 23:00:00 EST5EDT` | The end date of the line item's flight. |
| `flight.booked_impressions_budget_daily` | int | No | `20000` | The daily impression budget for the line item's flight. |
| `flight.booked_impressions_budget_lifetime` | int | No | `200000` | The lifetime impression budget for the line item's flight. |
| `flight.booked_revenue_budget_daily_advertiser_currency` | money | No | `200.00` | The daily budget in revenue for the line item's flight. |
| `flight.booked_revenue_budget_lifetime_advertiser_currency` | money | No | `20000.00` | The lifetime budget in revenue for the line item's flight. |
| `publisher_id` | int | Yes | `321` | Number to identify the publisher. |
| `publisher_name` | string | No | `"Test"` | Display name of the publisher. |
| `publisher` | string | No | `"Test (123)"` | **Deprecated**. |
| `publisher_code` | string | No | `"Publisher Code"` | The custom code for the publisher. |
| `imp_type_id` | int | Yes | `1` | The type of impression. Integer value which translates as follows: <br> - `1` = Blank <br> - `2` = PSA <br> - `3` = Default Error <br> - `4` = Default <br> - `5` = Kept <br> - `6` = Resold <br> - `7` = RTB <br> - `8` = PSA Error <br> - `9` = External Impression <br> - `10` = External Click. |
| `imp_type` | string | Yes | `"Kept"` | The type of impression. See `imp_type_id` above for the correspondence between descriptions and numeric values. |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for this impression. Note that the term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price". Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `seller_type` | string | Yes | `"Real Time"`, `"Direct"` | The type of media sold by the seller. |
| `media_type` | string | Yes | `"Banner"`, `"Pop"`, `"Interstitial"`, `"Video"`, `"Text"`, `"Expandable"`, `"Skin"` | The general display style of the creative. You can use the [Media Type Service](./media-type-service.md) to view the complete list of media types. |
| `mediatype_id` | int | yes | `2` | **Read-only**. The ID of the media type to which the subtype belongs. |
| `venue_id` | int | Yes | `1805` | The ID of the cluster of domain, site, tag, and user country/region that the Xandr optimization system uses to determine bid valuations. |
| `venue` | string | Yes | `"Venue Name"` | The name of the cluster of domain, site, tag, and user country/region that the Xandr optimization system uses to determine bid valuations. |
| `predict_type_rev` | int | Yes | `2` | The optimization phase of the campaign. Possible values:<br>`-2` = No predict phase<br>`-1` = Base predict phase<br>`0` = Learn giveup<br>`1` = Learn<br>`2` = Throttled<br>`3` = Optimized<br>`4` = Biased<br>`5` = Optimized 1<br>`8` = Optimized giveup<br>`9` = Base bid below giveup |
| `advertiser_type` | string | Yes | `"Local"` | The type of advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `user_group_for_campaign` | string | Yes | `"Test"` | The test/control user group for the campaign. See the `"labels"` field in the [Campaign Service](./campaign-service.md) for more details. |
| `line_item_type` | string | Yes | `"Performance"` | A field describing the line item, provided by the user. See the the `"labels"` field in the [Line Item Service](./line-item-service.md) for more information. |
| `insertion_order_type` | string | Yes | `"Client A Insertion Order"` | A field describing the insertion order, provided by the user. See the `"labels"` field in the [Insertion Order Service](../yield-analytics-api/insertion-order-service.md) for more information. |
| `adjustment_id` | int | Yes | `890` | The ID of the adjustment used to make changes to the media cost and/or impressions, clicks, and conversions you see in reporting for a advertiser. |
| `revenue_type` | string | No | `"CPA"` | The basis on which the member gets paid. |
| `revenue_type_id` | int | Yes | `4` | The ID of the revenue type. Possible values: <br> `-1` = No Payment <br> `0` = Flat CPM <br> `1` = Cost Plus CPM <br> `2` = Cost Plus Margin <br> `3` = CPC <br> `4` = CPA <br> `5` = Revshare <br> `6` = Flat Fee <br> `7` = Variable CPM <br> `8` = Estimated CPM. |
| `is_takeover` | boolean | Yes | `"Yes"` | Indicates whether an impression was `Blanked` or `Defaulted` because at least one of the ads in the multi-ad request was a takeover. Returns `true` if the impression is part of a takeover request; otherwise, returns `false`.|

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `234123` | imps | The total number of impressions served. |
| `clicks` | int | `545` | clicks | The the total number of clicks across all impressions. |
| `post_view_convs` | int | `75` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_revenue` | money | `150.00` | post_view_revenue | The total amount of recorded post-view conversion revenue. |
| `post_click_convs` | int | `15` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_revenue` | money | `300.00` | post_click_revenue | The total amount of recorded post-click conversion revenue. |
| `total_revenue` | money | `450.00` | booked_revenue | The total revenue. |
| `total_revenue_adv_curr` | money | `300.00` | total_revenue_adv_curr | The total revenue in the advertiser's currency |
| `total_convs` | int | `90` | post_click_convs + post_view_convs | The total number of post-view and post-click conversions. |
| `convs_rate` | double | `0.0003844` | total_convs / imps | The rate of conversions to impressions. |
| `post_view_convs_rate` | double | `0.000320` | post_view_convs / imps | The rate of post-view conversions to impressions. |
| `post_click_convs_rate` | double | `0.000064` | post_click_convs / imps | The rate of post-click conversions to impressions. |
| `ctr` | double | `0.2327836` | clicks / imps | The rate of clicks to impressions. |
| `profit` | money | `0.084102` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `click_convs_rate` | double | `0.1651376` | total_convs / clicks | The rate of conversions to clicks. |
| `advertiser_currency` | string | `Yes` | advertiser_currency | The advertiser's preferred currency. This preference can be set using the [Advertiser Service](./advertiser-service.md). |
| `revenue_ecpm` | money | `1.9221` | booked_revenue / clicks | The total revenue per 1000 impressions. |
| `revenue_ecpm_adv_curr` | money | `1.50` | revenue_ecpm_adv_curr | The total revenue per 1000 impressions in the advertiser's currency. |
| `cost_ecpm` | money | `0.4271259` | media_cost / imps * 1000 | The cost per 1000 impressions. |
| `profit_ecpm` | money | `0.4949` | profit / imps * 1,000 | The profit per 1000 impressions. "Profit" is defined as booked revenue minus total cost. |
| `revenue_ecpc` | money | `0.8256` | booked_revenue / clicks | The total revenue per click. |
| `revenue_ecpc_adv_curr` | money | `0.50` | revenue_ecpc_adv_curr | The total revenue per click in the advertiser's currency. |
| `revenue_ecpa` | money | `5.00` | booked_revenue / total_convs | The total revenue per conversion. |
| `revenue_ecpa_adv_curr` | money | `3.00` | revenue_ecpa_adv_curr | The total revenue per conversion in the advertiser's currency. |
| `cost_ecpc` | money | `0.1834` | media_cost / clicks | The cost per click. |
| `cost_ecpa` | money | `1.1111` | media_cost / total_convs | The cost per acquisition/conversion. |
| `profit_margin` | money | `0.7778` | profit/booked_revenue | Buyer profit margin. "Profit" is defined as booked revenue minus total cost. |
| `media_cost` | money | `100.00` | media_cost | The total amount spent. |
| `media_cost_buying_currency` | money | `120.00` | media_cost_buying_currency | The total amount spent expressed in buying currency. |
| `convs_per_mm` | double | `384.4` | (total_convs/imps) * 1,000,000 | The number of conversions per million impressions. |
| `click_thru_pct` | double | `2.756%` | (clicks / imps) * 100 | The rate of clicks to impressions, expressed as a percentage. In other words, the percentage of impressions that resulted in clicks. |
| `commissions` | money | `0` | Commissions for standard line items, $0 for ALIs. | Fees that come out of the booked revenue. Commissions for standard line items, $0 for ALIs. |
| `serving_fees` | money | `0.025143` | Serving fees for standard line items, $0 for ALIs. | Fees that are added to the media cost. Serving fees for standard line items, $0 for ALIs. |
| `profit_including_fees` | money | `250.00` | booked_revenue_dollars - commissions - media_cost_dollars - serving fees | **To be deprecated**. Profit minus commissions and serving fees. |
| `total_revenue_including_fees` | money | `450.00` | booked_revenue_dollars - commissions | **To be deprecated**. Total revenue after commissions. |
| `total_revenue_including_fees_adv_currency` | money | `370.00` | booked_revenue_adv_curr - commissions_adv_curr | **To be deprecated**. Total revenue after commissions, in the advertiser's currency. |
| `revenue_ecpa_including_fees` | money | `2.50` | If (post_click_convs + post_view_convs) > 0, then (booked_revenue_dollars - commissions) / (post_click_convs + post_view_convs)<br><br>If (post_click_convs + post_view_convs) = 0, then (booked_revenue_dollars - commissions) / 1 | **To be deprecated**. Revenue per conversion after commissions. |
| `revenue_ecpa_including_fees_adv_currency` | money | `3.25` | If (post_view_convs + post_click_convs) > 0, then (booked_revenue_adv_cur - commissions_adv_revenue) / (post_view_convs + post_click_convs)<br>If (post_view_convs + post_click_convs) = 0, then (booked_revenue_adv_cur - commissions_adv_revenue) / 1 | **To be deprecated**. Revenue per conversion after commissions, in the advertiser's currency. |
| `revenue_ecpc_including_fees` | money | `0.7256` | If clicks > 0, then (booked_revenue_dollars - commissions / clicks<br>If clicks = 0, then (booked_revenue_dollars - commissions / 1 | **To be deprecated**. Revenue per click after commissions. |
| `revenue_ecpc_including_fees_adv_currency` | money | `0.7256` | If clicks > 0, then (booked_revenue_adv_curr - commissions_adv_curr) / clicks<br><br>If clicks = 0, then (booked_revenue_adv_curr - commissions_adv_curr) / 1 | **To be deprecated**. Revenue per click after commissions, in the advertiser's currency. |
| `revenue_ecpm_including_fees` | money | `1.3131` | If imps > 0, then (booked_revenue_dollars - commissions) / (imps) * 1000<br>If imps = 0, then (booked_revenue_dollars - commissions) / 1000 | **To be deprecated**. Revenue per thousand impressions after commissions. |
| `revenue_ecpm_including_fees_adv_currency` | money | `1.3456` | If imps > 0, then (booked_revenue_dollars_adv_curr - commissions_adv_curr) / (imps) * 1000<br>If imps = 0, then (booked_revenue_dollars_adv_curr - commissions_adv_curr) / 1000 | **To be deprecated**. Revenue per thousand impressions after commissions, in the advertiser's currency. |
| `cost_ecpa_including_fees` | money | `1.1111` | If (post_click_convs + post_view_convs) > 0, then (media_cost_dollars + serving_fees) / (post_click_convs + post_view_convs)<br>If (post_click_convs + post_view_convs) = 0, then (media_cost_dollars + serving_fees) / 1 | **To be deprecated**. Cost per conversion including serving fees. |
| `cost_ecpc_including_fees` | money | `0.7925` | If clicks > 0, then (media_cost_dollars + serving fees) / clicks<br>If clicks = 0, then (media_cost_dollars + serving fees) / 1 | **To be deprecated**. Cost per click including serving fees. |
| `cost_ecpm_including_fees` | money | `0.4271259` | If imps > 0, then (media_cost_dollars + serving_fees) / imps<br>If imps = 0, then (media_cost_dollars + serving_fees) / 1 | **To be deprecated**. Gross serving fees per thousand impressions. |
| `profit_net_including_fees` | money | `200.00` | booked_revenue_dollars - commissions - media_cost_dollars - serving fees | **To be deprecated**. Net profit after commissions and serving fees. |
| `profit_ecpm_including_fees` | money | `0.4141` | If imps > 0, then (booked_revenue_dollars - commissions - media_cost_dollars - serving_fees) / imps * 1000<br><br>If imps = 0, then (booked_revenue_dollars - commissions - media_cost_dollars - serving_fees) / 1000 | **To be deprecated**. Profit per thousand impressions after commissions and serving fees. |
| `profit_margin_including_fees` | money | `0.7778` | If (booked_revenue_dollars - commissions) > 0, then (booked_revenue_dollars - commissions - media_cost_dollars - serving_fees) / (booked_revenue_dollars - commissions)<br>If (booked_revenue_dollars - commissions) = 0, then (booked_revenue_dollars - commissions - media_cost_dollars - serving_fees) / 1 | **To be deprecated**. Profit margin after commissions and serving fees. |
| `post_view_convs_pixel` | int | `23` |  | Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_clicks_convs_pixel` | int | `15` |  | Post click conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see Conversion Attribution (Monetize) or Conversion Attribution (Invest). |
| `total_revenue_pixel` | money | `118.50` |  | Total revenue for the pixel. |
| `total_revenue_including_fees_pixel` | money | `94.80` |  | **To be deprecated**. Total revenue for the pixel after commissions |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable per the IAB Viewability definition. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `cost_ecpvm` | money | `2.25` | (media_cost / imps_viewed) * 1000 | The cost per 1000 viewable impressions. |
| `avg_bid_reduction` | double | `18%` |  | The average bid reduction you gained on the line item or campaign. This value represents the difference (as a percentage) between your bid and the actual media cost you paid for the impression you won (e.g., due to bid reduction). This value is only valid for RTB bidding (i.e., not Managed). Currently, this value is not accurately calculated for line items for which the `payment_auction_event_type` field has been set to `2`. |
| `partner_fees` | money | `123.45` |  | **Forthcoming**. The total amount of third-party costs, budgeted using the Partner Fee Service, that have accrued on an augmented line item over the reported period of time. |
| `total_cost` | money | `123.45` | total_cost = media_cost + data_costs + partner_fees + commissions + serving_fees + publisher_revenue | Forthcoming. The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period (July 17-After the breaking change period ). |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | **Forthcoming**. The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | **Forthcoming**. The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | **Forthcoming**. The total cost per conversion. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | **Forthcoming**. Profit per click. |
| `profit_ecpa` | money | `123.45` | ( booked_revenue - total_cost)/conversions | **Forthcoming**. Profit per conversion. |
| `buying_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * advertiser_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the buyer used to purchase the inventory.|
| `selling_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * publisher_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the seller used to sell the inventory. |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"network_advertiser_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat network_advertiser_analytics

{"report":
    {
        "report_type":"network_advertiser_analytics",
        "columns":[
            "hour",
            "seller_member_id",
            "campaign_id",
            "imps",
            "clicks",
            "total_convs",
            "ctr",
            "convs_rate"
        ],
        "report_interval":"last_48_hours",
        "format":"csv"
    }
}
```

### `POST` the request to the [Report Service](./report-service.md)

You `POST` the JSON request and get back a report ID.

```
$ curl -b cookies -X post -d @network_advertiser_analytics "https://api.appnexus.com/report?advertiser_id=690"

{
  "response":{
   "status":"OK",
   "report_id":"09b6979a6a4c3805bdac8921378d3622"
  }
}
```

### `GET` the report status from the report service

Make a  `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the reporting data to a file (described in the next step).

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
  "response":{
   "status":"OK",
   "report":{
     "name":null,
     "created_on":"2010-05-25 19:15:48",
     "json_request":"{\"report\":{\"report_type\":\"network_advertiser_analytics\",\"columns\":
     [\"hour\",\"seller_member_id\",\"campaign_id\",\"imps\",\"clicks\",\"total_convs\",
     \"ctr\",\"convs_rate\"],\"row_per\":[\"hour\",\"seller_member_id\",\"campaign_id\"],
     \"report_interval\":\"last_48_hours\",\"filters\":[{\"advertiser_id\":\"690\"}]}}",
     "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
   },
   "execution_status":"ready"
  }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!NOTE]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/network_advertiser_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

## Related topic

[Report Service](./report-service.md)
