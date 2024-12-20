---
title: Network Analytics
description: Use the Network Analytics report to view the buy and sell-side data for network members, including direct advertiser impressions and direct publishers sold across platforms.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network analytics

The Network Analytics report can be used to view both buy and sell-side data for a network member:

- Direct advertiser impressions (bought across direct publishers and real-time inventory)
- Direct publishers (sold across direct advertisers and other platform buyers)

To drill down into more granular analytics for a specific advertiser or publisher, see the [Network Advertiser Analytics](./network-advertiser-analytics.md) and [Network Publisher Analytics](./network-publisher-analytics.md) reports.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

## Time frame

The `report_interval` field can be set to one of the following:

- current_hour
- last_hour
- today
- yesterday
- last_48_hours
- last_7_days
- last_30_days
- month_to_date
- month_to_yesterday
- last_2_days
- quarter_to_date
- last_month
- lifetime

### Data retention period

Most data in this report is maintained permanently (exceptions noted below). After:

- 100 days, you are no longer able to report on hourly data. However, daily, monthly and cumulative intervals are still available.
- 14 months, you are no longer able to report on individual:
  - Creatives
  - Placements
  - Brands

In some cases Analytics reports can show delivery that does not match statistics shown elsewhere in Invest or Monetize for a given advertiser or publisher. This is due to the way that Analytics reporting data older than 100 days and 14 months are aggregated. The data from Billing reports are kept in non-aggregated form indefinitely. For more information, see [Dates and Times in Reporting](../curate/dates-and-times-in-reporting.md) in the UI documentation.

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Time ranges including dates occurring greater than 45 days ago

If you create network analytics reports with the `report_interval` set to `"lifetime"` or `"quarter_to_date"` (where the end date is greater than 45 days from today), your report (regardless of metrics included) will be added to a special queue for `"resource-intensive"` reports. As a result, the report may take longer than usual to complete. In addition, these resource-intensive reports may, due to the amount of data being requested, fail before being completed. If your report fails to complete, you will receive a notification. If your report request fails or is deleted, you can:

- re-run the report at a later time.
- use a report type other than `network_analytics`.
- alter the way you structure your reports (if possible) so they do not include dates greater than 45 days ago.

If you are frequently requesting network analytics reports via the API which include dates longer than 45 days ago, you may need to consider caching data and using [Bulk Reporting Feeds](./bulk-reporting-feeds.md) or [Log-Level Data (LLD) Feeds](../log-level-data/log-level-data-feeds.md).

## Dimensions

> [!NOTE]
> Some dimensions have attributes. Dimension attributes are a more granular element of data about the parent dimension. If a dimension has attributes, the name of its attributes will appear below it using the following syntax: `dimension_name.attribute_name`.

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | No | `"2010-02-01 06:00:00"` | The hour of the auction.<br><br>**Note**: For impressions older than 100 days, the day will be returned rather than the hour. |
| `day` | time | No | `"2010-02-01"` | The day of the auction. |
| `month` | time | No | `"2010-02"` | The month of the auction. |
| `entity_member_id` | int | Yes | `123` | If `imp_type` is `1`, `2`, `3`, `4`, `6`, or `8`, the ID of the buying member; otherwise, the ID of the selling member. |
| `buyer_member_id` | int | Yes | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default. <br><br>This dimension also has an attribute, called bidder, that identifies the ID of the bidder for the impression. The attribute's data type is int. |
| `buyer_member_name` | string | No | `"My Network"` | The name of the buying member.<br><br>**Note**: The name might be `"Default"` or `"Default Error"`, which means that there was no buyer for the impression, and a default creative was served. |
| `external_inv_id` | int | Yes | `123` | The ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](./external-inventory-code-service.md). |
| `external_inv_name` | string | No | `"My external inventory"` | The name of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](./external-inventory-code-service.md). |
| `external_inv` | string | No | `"My external inventory(123)"` | **Deprecated**. |
| `deal_type` | string | Yes | `"programmatic_guaranteed"` | The name for the type of deal. Possible values are: <br> - `"open_auction"` <br> - `"private_auction"` <br> - `"first_look"` <br> - `"programmatic_guaranteed"` <br> - `"curated"` |
| `deal_type_id` | int | Yes | `4` | The ID for the type of deal. Possible values are (associated types in parentheses):<br> - `1` ("open_auction") <br> - `2` ("private_auction") <br> - `3` ("first_look") <br> - `4` ("programmatic_guaranteed") <br> - `5` ("curated") |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |
| `seller_member_name` | string | No | `"That Seller"` | The name of the selling member. |
| `advertiser_id` | int | Yes | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by an external buyer, or a `default` or `PSA` was shown. |
| `advertiser_name` | string | No | `"Verizon Wireless"` | The name of the advertiser. |
| `advertiser_code` | string | No | `"Verizon Wireless Code"` | The custom code for the advertiser. |
| `advertiser_currency` | string | Yes | `"USD"` | The currency of the advertiser. |
| `adjustment_id` | int | Yes | `890` | The ID of the adjustment used to make changes to booked revenue and media cost values. |
| `adjustment_day` | time | Yes | `"2010-02-01"` | The day of the adjustment. |
| `adjustment_hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour of the adjustment. |
| `publisher_id` | int | Yes | `321` | The ID of the publisher. |
| `publisher_name` | string | No | `"Newscorp"` | The name of the publisher. |
| `publisher_code` | string | No | `"Newscorp Code"` | The custom code for the publisher. |
| `pub_rule_id` | int | Yes | `555` | The ID of the publisher rule. |
| `pub_rule_name` | string | No | `"Publisher Rule Name"` | The name of the publisher rule. |
| `pub_rule_code` | string | No | `"Publisher Rule Code"` | The custom code for the publisher rule. |
| `publisher_currency` | string | Yes | `"USD"` | The currency of the publisher. |
| `site_id` | int | Yes | `194` | The ID of the site.<br><br>**Note**: For impressions older than 14 months, the `site_id` will be `0`. |
| `site_name` | string | No | `"Site Name"` | The name of the site. |
| `site_code` | string | No | `"Site Code"` | The custom code for the site. |
| `pixel_id` | int | Yes | `3141` | The ID of the pixel used to track the conversion. For more information, see the [Conversion Pixel Service](./conversion-pixel-service.md). |
| `pixel_name` | string | No | `"My Pixel"` | The name of the pixel used to track the conversion. |
| `flight` | int | Yes | `124785` | The line item flight ID. |
| `flight.start_date` | datetime | No | `2017-02-06 00:00:00 EST5EDT` | The start date of the line item's flight. |
| `flight.end_date` | datetime | No | `2017-02-09 23:00:00 EST5EDT` | The end date of the line item's flight. |
| `flight.booked_impressions_budget_daily` | int | No | `2000` | The daily impression budget for the line item's flight. |
| `flight.booked_impressions_budget_lifetime` | int | No | `200000` | The lifetime impression budget for the line item's flight. |
| `flight.booked_revenue_budget_daily_advertiser_currency` | money | No | `50.00` | The daily budget in revenue for the line item's flight. |
| `flight.booked_revenue_budget_lifetime_advertiser_currency` | money | No | `20000.00` | The lifetime budget in revenue for the line item's flight. |
| `placement_id` | int | Yes | `456` | The ID of the placement.<br><br>**Note**: For impressions older than 14 months, placements will be aggregated into one row with `-1` as the `placement_id`. |
| `placement_name` | string | No | `"Ivillage 160x600"` | The name of the placement.<br><br>**Note**: For impressions older than 14 months, placements will be aggregated into one row with `"All placement data older than 14 months"` as the `placement_name`. |
| `placement_code` | string | No | `"Ivillage Code"` | The custom code for the placement. |
| `insertion_order_id` | int | Yes | `321` | The ID of the insertion order. |
| `insertion_order_name` | string | No | `"Insertion Order"` | The name of the insertion order. |
| `insertion_order_code` | string | No | `"Insertion Order Code"` | The custom code for the insertion order. |
| `insertion_order.type` | string | No | `"Legacy IO"` | The type of insertion order associated with the impression (e.g. Legacy, Seamless). |
| `insertion_order.state` | string | No | `"active"` | The state of the insertion order (e.g., `active`, `inactive`). |
| `insertion_order.start_date` | timestamp | No | `2017-02-06 00:00:00 EST5EDT` | The start date of the non-seamless insertion order associated with the impression. For seamless orders, see `billing_period.start_date`. |
| `insertion_order.end_date` | timestamp | No | `2017-02-09 23:00:00 EST5EDT` | The end date of the non-seamless insertion order associated with the impression. For seamless orders, see `billing_period.end_date`. |
| `insertion_order.booked_impressions_budget_daily` | int | No | `2000` | The daily impression budget for the insertion order. |
| `insertion_order.booked_impressions_budget_lifetime` | int | No | `200000` | The lifetime impression budget for the insertion order. |
| `insertion_order.booked_revenue_budget_daily` | money | No | `200.00` | The daily budget in revenue for the insertion order. |
| `insertion_order.booked_revenue_budget_lifetime` | money | No | `10000.00` | The lifetime budget in revenue for the insertion order. |
| `insertion_order.billing_code` | string | No | `"E4567"` | The billing code associated with the insertion order. |
| `type_for_insertion_order` | string | Yes | `"Retargeting IO"` | A custom reporting field describing the type of insertion order. See the `labels` field in the [Insertion Order Service](./insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `salesrep_for_insertion_order` | string | Yes | `"Patricia Martin"` | A custom reporting field containing the sales representative for the insertion order. See the `labels` field in the [Insertion Order Service](./insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `trafficker_for_insertion_order` | string | Yes | `"George Martin"` | A custom reporting field containing the trafficker for the insertion order. See the `labels` field in the [Insertion Order Service](./insertion-order-service.md) for more information. You may only select one reporting label per report. |
| `external_code` | string | No | `"external code"` | An external custom code associated with the placement (by the Publisher). |
| `line_item_id` | int | Yes | `111` | The ID of the line item. |
| `line_item_name` | string | No | `"Default Line Item"` | The name of the line item. |
| `line_item_code` | string | No | `"Default Line Item Code"` | The custom code for the line item. |
| `line_item.type` | string | No | `"standard"` | The line item type (e.g., `standard`, `augmented`). |
| `line_item.true_line_item_type` | string | No | `"augmented"` | The new line item type that includes augmented line item (ALI), standard etc. |
| `line_item.status` | string | No | `"active"` | The state of the line item (e.g., `active`, `inactive`). |
| `line_item.start_date` | datetime | No | `2017-02-06 00:00:00 EST5EDT` | The start date of the non-augmented line item. For augmented line Items (ALIs), see `flight.start_date`. |
| `line_item.end_date` | datetime | No | `2017-02-09 23:00:00 EST5EDT` | The end date of the non-augmented line item. For augmented line Items (ALIs), see `flight.end_date`. |
| `line_item.booked_impressions_budget_daily` | int | No | `2000` | The daily impression budget for the line item. |
| `line_item.booked_impressions_budget_lifetime` | int | No | `20000` | The lifetime impression budget for the line item. |
| `line_item.booked_revenue_budget_daily_adv_curr` | money | No | `1200.00` | The daily budget in revenue for the line item. |
| `line_item.booked_revenue_budget_lifetime_adv_curr` | money | No | `23000.00` | The lifetime budget in revenue for the line item. |
|`line_item.comments` | string | No | `"extension of Feb spend"` | Any comments related to this line item. |
| `type_for_line_item` | string | Yes | `"Branding IO"` | A custom reporting field describing the type of line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `salesrep_for_line_item` | string | Yes | `"Patricia Martin"` | A custom reporting field containing the sales representative for the line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `trafficker_for_line_item` | string | Yes | `"George Martin"` | A custom reporting field containing the trafficker for the line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. You may only select one reporting label per report. |
| `is_curated` | Yes | Indicates whether an impression was sold involving a Curator Member. Returns `true` if a Curator Member is involved, otherwise `false`. |
| `curator_member` | No | The Curator for the impression. |
| `campaign_id` | int | Yes | `222` | The ID of the campaign. |
| `campaign_name` | string | No | `"Default Campaign"` | The name of the campaign. |
| `campaign_code` | string | No | `"Default Campaign Code"` | The custom code for the campaign. |
| `campaign_priority` | int | No | `5` | The bidding priority for a campaign that targets direct inventory. For more information, see [Bidding Priority](../monetize/bidding-priority.md) in the UI Documentation.<br>Possible values: `1` - `10`, where `10` is the highest priority. |
| `campaign_type` | string | Yes | `"House Ad Campaign"` | The type of campaigns under the line item. See the `labels` field in the [Line Item Service](./line-item-service.md) for more information. |
| `creative_id` | int | Yes | `554` | The ID of the creative.<br><br>**Note**:<br> - For impressions older than 100 days, creatives will be aggregated into one row with `0` as the `creative_id`.<br> - For external click or impression trackers, `creative_id` will be `"External Clicks"` or `"External Imps"`. |
| `creative_name` | string | No | `"Q1 2010 728x90"` | The name of the creative.<br><br>Note:<br> - For impressions older than 100 days, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, `creative_name` will be `"External Clicks"` or `"External Imps"`. |
| `creative_code` | string | No | `"12655"` | The code for the creative.<br><br>**Note**:<br> - For impressions older than 100 days, creatives will be aggregated into one row with `"All creative data older than 100 days"` as the `creative_name`.<br> - For external click or impression trackers, `creative_code` will be `"External Clicks"` or `"External Imps"`. |
| `size` | string | Yes | `"728x90"` | The size of the placement/creative served. |
| `brand_id` | int | Yes | `3` | The ID of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `brand_name` | string | No | `"Ace Hardware"` | The name of the brand associated with a creative. For `imp_type_id = 6`, no information is available in the `brand_name` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `billing_period.start_date` | datetime | No | `"2015-05-25 19:19:53"` | The earliest date of the insertion order's billing period.<br><br>**Note**: <br> **Alpha-Beta Notice**: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period.end_date` | datetime | No | `"2015-05-30 19:19:53"` | The last date of the insertion order's billing period.<br><br>**Note**: **Alpha-Beta Notice**: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `billing_period.booked_imps_budget_daily` | int | No | `3500` | The daily impression budget of the insertion order's billing period. |
| `billing_period.booked_imps_budget_lifetime` | int | No | `300000` | The lifetime impression budget of the insertion order's billing period. |
| `billing_period.booked_revenue_budget_daily_buying_currency` | money | No | `250.00` | The daily revenue budget of the insertion order's billing period. |
| `billing_period.booked_revenue_budget_lifetime_buying_currency` | money | No | `2500.00` | The lifetime revenue budget of the insertion order's billing period. |
| `billing_period.external_code` | string | No | `"houseware245"` | The custom code for the billing period (`budget_interval`). |
| `geo_country` | string | Yes | `"US"` | The code for the geographic country. For impression requests for which we received no indication that the ad was rendered (i.e., non-transacted), country information is not provided. |
| `geo_country_name` | string | No | `"United States"` | The name of the geographic country. For impression requests for which we received no indication that the ad was rendered (i.e., non-transacted), country information may not be provided. |
| `inventory_class` | string | Yes | `"class_1"`, `"class_2"`, `"class_3"`, `"unaudited"`, `"black"` | The class of the inventory. |
| `bid_type` | string | Yes | `"Manual"` | The optimization phase the node was in when it bid for this impression. Note that the term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price".<br>Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `imp_type_id` | int | Yes | `1` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1` ("Blank"): No creative served.<br> - `2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br> - `3` ("Default Error"): A default creative served due to a timeout issue.<br> - `4` ("Default"): A default creative served because there were no valid bids.<br> - `5` ("Kept"): Your advertiser's creative served on your publisher's site.<br> - `6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br> - `7` ("RTB"): Your advertiser's creative served on third-party inventory.<br> - `8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9` ("External Impression"): An impression from an impression tracker.<br> - `10` ("External Click"): A click from a click tracker. |
| `imp_type` | string | Yes | `"Blank"` | The type of impression. For possible values, see `imp_type_id`. |
| `buyer_type` | string | Yes | `"Real Time"` | The type of impression purchased by the buyer member. Possible values: `"Real Time"` or `"Direct"`. |
| `seller_type` | string | Yes | `"Real Time"` | The type of impression sold by the seller member. Possible values: `"Real Time"` or `"Direct"`. |
| `revenue_type` | string | Yes | `"CPA"` | The basis on which the member gets paid. |
| `revenue_type_id` | int | Yes | `4` | Possible values: <br> `-1` = No Payment <br>`0` = Flat CPM <br> `1` = Cost Plus CPM <br> `2` = Cost Plus Margin <br> `3` = CPC <br> `4` = CPA <br> `5` = Revshare <br> `6` = Flat Fee <br> `7` = Variable CPM <br> `8` = Estimated CPM <br> `9` = CPVM. |
| `supply_type` | string | No | `"web"` | The type of inventory. Possible values: <br> - `"web"` <br> - `"mobile_web"` <br> - `"mobile_app"` <br> - `"facebook_sidebar"`. |
| `payment_type` | string | Yes | `"cpm"` | The type of payment to a broker. Possible values: <br> - `"cpm"` <br> - `"revshare"` <br> - `"cpvm"`. |
| `deal_id` | int | Yes | `2345` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `deal_name` | string | No | `"Private deal for buyer 1085 with floor of $2.50"` | The name of the deal. |
| `deal_code` | string | No | `"External seller deal code"` | The custom code for the deal. For deals with external supply partners, this is generally the string that you use to identify the deal. |
| `media_type` | string | No | `"Standard Banner"` | The specific display style of a creative. You can use the [Media Subtype Service](./media-subtype-service.md) to view all possible media subtypes. |
| `media_type_id` | int | Yes | `1` | The ID of the specific display style of a creative. You can use the [Media Subtype Service](./media-subtype-service.md) to view all possible media subtypes. |
| `salesperson_for_advertiser` | string | Yes | `"Michael Sellers"` | The salesperson for the advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `account_manager_for_advertiser` | string | Yes | `"Yvonne Summers"` | The account manager for the advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `advertiser_type` | string | Yes | `"Local"` | The type of advertiser. See the `"labels"` field in the [Advertiser Service](./advertiser-service.md) for more details. |
| `salesperson_for_publisher` | string | Yes | `"Brian Young"` | The salesperson for the publisher. See the `"labels"` field in the [Publisher Service](./publisher-service.md) for more details. |
| `account_manager_for_publisher` | string | Yes | `"Ami Fisher"` | The account manager for the publisher. See the `"labels"` field in the [Publisher Service](./publisher-service.md) for more details. |
| `user_group_for_campaign` | string | Yes | `"Test"` | The test/control user group for the campaign. See the `"labels"` field in the [Campaign Service](./campaign-service.md) for more details. |
| `line_item_type` | string | Yes | `"Performance"` | A field describing the line item, provided by the user. See [Line Item Service](./line-item-service.md) for more information. |
| `insertion_order_type` | string | Yes | `"Client A Insertion Order"` | A field describing the insertion order, provided by the user. See [Insertion Order Service](./insertion-order-service.md) for more information. |
| `buying_currency` | string | Yes | `"EUR"` | The transaction currency used by the buyer to purchase this impression. |
| `selling_currency` | string | Yes | `"EUR"` | The transaction currency used by the seller to sell this impression. |
| `imps_filtered_reason_id` | int | Yes | `"3"` | The numeric ID associated with the reason why the impression request was filtered out by Xandr inventory quality controls and the auction was not held. See `imps_filtered_reason` below for more information. |
| `imps_filtered_reason` | string | Yes | `"Invalid Domain"` | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are:<br> - `"Invalid Domain" (1)` <br> - `"Invalid IP" (2)` <br> - `"Suspected Domain Detection Tampering" (3, 4, 5)` <br> - `"Unknown" (6, 7)` <br> - `“White Ops: General IVT” (17)` - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks.<br> - `“White Ops: Sophisticated IVT” (18)` - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify.<br> - `"Valid Impression" (0)` is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. |
| `marketplace_clearing_event_id` | int | Yes | `2` | The ID of the underlying auction event that was transacted (e.g., impression, viewable impression, completed video). For a list of Clearing Events and their IDs, see [Supported Viewability Standards](../invest/supported-viewability-standards-for-guaranteed-outcomes.md) in the UI documentation. |
| `marketplace_clearing_event_name` | string | Yes | `"Views - Standard Display"` | The name of the underlying auction event that was transacted (e.g., impression, viewable impression, completed video). For more information, see [Guaranteed Outcomes](../monetize/guaranteed-outcomes.md) and [Supported Viewability Standards](../invest/supported-viewability-standards-for-guaranteed-outcomes.md) in the UI documentation. |
| `marketplace_clearing_event` | string | No | `"Views - Standard Display (2)"` | The concatenated value of the name and ID of the underlying auction event that was transacted (e.g., impression, viewable impression, completed video). For more information, see [Guaranteed Outcomes](../monetize/guaranteed-outcomes.md) and [Supported Viewability Standards](../invest/supported-viewability-standards-for-guaranteed-outcomes.md) in the UI documentation. |
| `line_item.trafficker_label` | string | Yes | `"My trafficker"` | A customer reporting label field used to list the trafficker associated with the line item. |
| `line_item.salesrep_label` | string | Yes | `"My salesrep"` | A customer reporting label field used to list the sales representative associated with the line item. |
| `insertion_order.trafficker_label` | string | Yes | `"My trafficker"` | A customer reporting label field used to list the trafficker associated with the insertion order. |
| `insertion_order.sales_rep_label`| string | Yes | `"My salesrep"` | A customer reporting label field used to list the sales representative associated with the insertion order. |
| `insertion_order.lifetime_pacing` | int | No | `11` | The lifetime pacing budget for the insertion order. |
| `line_item.type_label` | string | Yes | `"My LI"` | A custom reporting label field used to list the line item type (e.g., `Retargeting LI`). This is not the same as the `line_item_type` attribute. |
| `insertion_order.type_label` | string | Yes | `"My IO"` | A custom reporting label field used to list the insertion order type (e.g., `Branding IO`). This is not the same as the `insertion_order_type` attribute. |
| `payment_type_id` | int | Yes | `5` | The ID for the payment type i.e. how the buyer is paying for the impression (Flat CPM, CPC, CPA etc.). |
| `bid_type_id` | int | Yes | `7` | The ID for the bid type (`Manual`, `Learn`, `Optimize` etc.). |
| `billing_period_id` | int | Yes | `9` | The ID of the billing period for the insertion order. |
| `viewdef_definition_id` | int | Yes | `11` | The definition id for the custom viewability. |
| `mediatype_id` | int | Yes | `23` | The ID of the media type associated with the creative that served on an impression. |
| `bidder_id/filtered_bidder` | int | Yes | `123` | The bidder ID extracted from the member ID.<br><br>**Note**: The `filtered_bidder` is not a dimension, it is only a filter. |
| `bidder` | string | No | `"My bidder(123)"` | The name and ID of the bidder extracted from the member ID. |
| `bidder_name` | string | No | `"My bidder"` | The name of the bidder extracted from the member ID. |
| `buyer_payment_event_type_id` | int | Yes | `123` | The ID of the market place clearing event that the buyer paid on. |
| `buyer_payment_event_type_name` | string | No | `"My event"` | The name of the market place clearing event that the buyer paid on. |
| `buyer_payment_event_type` | string | No | `"My event(123)"` | The name and ID of the market place clearing event that the buyer paid on. |
| `buyer_payment_event_units` | int | Yes | `133` | The number of the marketplace clearing event units that the buyer paid on. |
| `seller_revenue_event_type_id` | int | Yes | `123` | The ID of the market place clearing event that the seller paid on. |
| `seller_revenue_event_type_name` | string | No | `"My event"` | The name of the market place clearing event that the seller paid on. |
| `seller_revenue_event_type` | string | No | `"My event(123)"` | The name and ID of the market place clearing event that the seller paid on. |
| `seller_revenue_event_units` | int | Yes | `123` | The number of the marketplace clearing event units that the seller paid on. |
| `_realtime_status_batch` | string | No | `"Batch`" | The static batch value for the real time status. |
| `billing_period_external_code`| int | No | `89` | The optional external code supplied for the insertion order's billing period. |
| `flight_id` | int | Yes | `67` | The ID of the line item flight under which the impression was purchased. |
| `line_item.lifetime_pacing` | int | No | `800` | The lifetime pacing budget for the line item. |
| `buyer_seat_code` | string | No | `"My buyer seat(123)"` | The custom buyer seat ID (submitted by DSP) that was used to bid on the impression |
| `buyer_seat_name` | string | No | `"My buyer seat"` | The display name for the buyer seat code |
| `is_curated` | boolean | Yes | `"Yes"` | Boolean value to specify if a deal is curated. |
| `curator_member_id` | int | Yes | `23` | The member ID of the deal curator. |
| `split_id` | int | Yes | `13` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. |
| `split_name` | string | No | `"My split"` | The name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. |
| `split` | string | No | `"My split(123)"` | The ID and name of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. |
| `buyer_seat_id` | int | Yes | `11` | The ID of the buyer seat. |
| `campaign_group_type_id` | int | Yes | `12` | The ID of the campaign group type which purchased this impression. |
| `content_category_id` | int | No | `11` | **Deprecated**. |
| `fold_position_id` | int | No | `10` | **Deprecated**. |
| `fold_position` | string | No | `"My fold"` | **Deprecated**. |
| `inventory_source_id` | int | No | `3` | **Deprecated**. |
| `inventory_source` | string | No | `"My inv source(3)"` | **Deprecated**. |
| `inventory_source_name` | string | No | `"My inv source"` | **Deprecated**. |
| `content_category` | string | No | `"My category(11)"` | **Deprecated**. |
| `content_category_name` | string | No | `"My category"` | **Deprecated**. |
| `buyer_member` | string | No | `"My Network (123)"` | **Deprecated**. |
| `seller_member` | string | No | `"That Seller (456)"` | **Deprecated**. |``
| `advertiser` | string | No | `"Verizon Wireless (789)"` | **Deprecated**. |
| `publisher` | string | No | `"Newscorp (321)"` | **Deprecated**. |
| `deal` | string | No | `"Private deal for buyer 1085 with floor of $2.50 (45)`" | **Deprecated**. |
| `brand` | string | No | `"Ace Hardware (3)"` | **Deprecated**. |
| `creative` | string | No | `"Q1 2010 728x90 (554)"` | **Deprecated**. |
| `campaign` | string | No | `"Default Campaign (222)"` | **Deprecated**. |
| `line_item` | string | No | `"Default Line Item (111)"` | **Deprecated**. |
| `insertion_order` | string | No | `"Insertion Order (321)"` | **Deprecated**. |
| `site` | string | No | `"Site Name (194)"` | **Deprecated**. |
| `placement` | string | No | `"Ivillage 160x600 (456)"` | **Deprecated**. |
| `pub_rule` | string | No | `"Publisher Rule Name (555)"` | **Deprecated**. |
| `code_1` | string | No | `"Code A"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| `code_2` | string | No | `"Code B"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |
| `code_3` | string | No | `"Code C"` | An alias added to the placement object that is reportable as a sub-dimension of Placement. The report shows the current value of the alias and does not reflect historical values. This information is only reportable to Sellers. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `imps_blank` | int | `3` | imps_blank | The number of impressions served with a blank. |
| `imps_psa` | int | `5` | imps_psa | The number of impressions served a PSA. |
| `imps_psa_error` | int | `0` | imps_psa_error | The number of impressions served a PSA due to a timeout issue or lack of a default creative. |
| `imps_default_error` | int | `0` | imps_default_error | The number of impressions that defaulted due to a timeout issue. |
| `imps_default_bidder` | int | `0` | imps_default_bidder | The number of impressions that defaulted because there were no valid bids. |
| `imps_kept` | int | `0` | imps_kept | The number of impressions your advertiser purchased from your publisher. |
| `imps_resold` | int | `0` | imps_resold | The number of impressions your publisher sold to a third party. |
| `imps_rtb` | int | `2332` | imps_rtb | The number of impressions your advertiser bought from a third party. |
| `imp_requests` | int | `10` | imps_requests | The total number of ad calls (impression requests). <br><br>**Warning**: This metric is typically inaccurate for video inventory due to occasional delays in receiving video events, which can lead to inflated request totals based on the assumption that the video has expired. For a better video request metric, you should use Ad Requests in the [Seller Fill and Delivery Network Report](./seller-fill-and-delivery-network-report.md) or the [Network Video Analytics Report](./network-video-analytics.md). |
| `imps_insertion` | int | `10` | imps_insertion | The total number of impressions bought from the insertion order perspective. |
| `external_impression` | int | `0` | external_impression | The number of impressions from an impression tracker. |
| `viewdef_viewed_imps` | int | `2350` | viewdef_viewed_imps | Viewable impressions with a different viewability definition (i.e., different from the viewability definition of IAB). It is equivalent to custom viewability. |
| `viewdef_view_rate` | double | `67%` | viewdef_view_rate | The rate for impressions with a different viewability definition (i.e., different from the viewability definition of IAB). It is equivalent to custom viewability. |
| `clicks` | int | `1` | clicks | The total number of clicks across all impressions. For Microsoft Invest, clicks from all media types are supported. For external DSPs, only clicks from Native and Video media types are supported. |
| `include_adjustments_in_reported_data` | boolean | `Yes` | NA | Check to include adjustments in the report while generating |
| `click_thru_pct` | double | `1.12359550561797%` | (clicks / imps) x 100 | The rate of clicks to impressions as a percentage. |
| `external_click` | int | `0` | external_click | The number of external clicks. |
| `cost` | money | `16.833378` | cost | The total amount of media cost for direct publisher and purchased real-time inventory. |
| `cost_including_fees` | money | `19.281633` | cost + serving_fees | **Deprecated**. |
| `third_party_costs` | money | `19.281633` | third_party_costs | The cost incurred for purchasing of third party inventory. |
| `revenue` | money | `25.767257` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue. |
| `revenue_including_fees` | money | `25.767257` | revenue - commissions | **Deprecated**. |
| `booked_revenue` | money | `25.767257` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `booked_revenue_adv_curr` | money | `25.767257` | booked_revenue_adv_curr | The total revenue booked through a direct advertiser, in the currency of the advertiser. |
| `booked_revenue_vcpm_adv_curr` | money | `25.767257` | booked_revenue_vcpm_adv_curr | The total vcpm revenue booked through a direct advertiser, in the currency of the advertiser. |
| `booked_revenue_ecpc` | money | `25.767257` | booked_revenue_ecpc | Booked revenue per click. |
| `booked_revenue_ecpa` | money | `25.767257` | booked_revenue_ecpa | Booked revenue per acquisition. |
| `booked_revenue_ecpa_buying_currency` | money | `25.767257` | booked_revenue_ecpa_buying_currency | Booked revenue per acquisition in buying currency. |
| `booked_revenue_ecpm` | money | `25.767257` | booked_revenue_ecpm | Booked revenue per thousand impressions. |
| `booked_revenue_ecpm_buying_currency` | money | `25.767257` | booked_revenue_ecpm_buying_currency | Booked revenue per thousand impressions in buying currency. |
| `booked_revenue_vcpm_adv_curr` | money | `25.767257` | booked_revenue_vcpm_adv_curr | Booked revenue per thousand viewable impressions in advertiser currency. |
| `booked_revenue_vcpm` | money | `25.767257` | booked_revenue_vcpm | Booked revenue per thousand viewable impressions. |
| `booked_revenue_ecpc_buying_currency` | money | `25.767257` | booked_revenue_ecpc_buying_currency | Booked revenue per click in buying currency. |
| `media_cost_advertiser_currency` | money | `25.767257` | media_cost_advertiser_currency | The total amount to be paid for media purchases in advertiser currency. |
| `media_cost_vcpm_advertiser_currency` | money | `25.767257` | media_cost_vcpm_advertiser_currency | The total amount to be paid for media purchases of per thousand viewable impressions in advertiser currency. |
| `media_cost_vcpm` | money | `25.767257` | media_cost_vcpm | The total amount to be paid for media purchases of per thousand viewable impressions. |
| `cost_ecpm_advertiser_currency` | money | `25.767257` | cost_ecpm_advertiser_currency | The cost per 1,000 impressions in advertiser currency. |
| `cost_ecpc_advertiser_currency` | money | `25.767257` | cost_ecpc_advertiser_currency | The cost per click in advertiser currency. |
| `cost_ecpa_advertiser_currency` | money | `25.767257` | cost_ecpa_advertiser_currency | The cost per conversion in advertiser currency. |
| `clearing_event_booked_revenue_per_event_buying_currency` | money | `25.767257` | clearing_event_booked_revenue_per_event_buying_currency | Per event booked revenue of clearing events in buying currency. |
| `clearing_event_booked_revenue_per_event` | money | `25.767257` | clearing_event_booked_revenue_per_event | Per event booked revenue of clearing events. |
| `clearing_event_buyer_media_cost_per_event` | money | `25.767257` | clearing_event_buyer_media_cost_per_event | Per event buyer media cost of clearing events. |
| `post_view_convs_pixel` | int | `23` |  | Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_clicks_convs_pixel` | int | `15` |  | Post click conversions for the pixel. Post view conversions for the pixel. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_view_convs_cross_device` | int | `123` | post_view_convs_cross_device | The number of the total post view conversion events that occurred as a result of having cross device enabled. |
| `post_click_convs_cross_device` | int | `123` | post_click_convs_cross_device | The number of the total post click conversion events that occurred as a result of having cross device enabled. |
| `post_view_convs_ip` | int | `123` | post_view_convs_ip | The number of the total post view conversion events that occurred as a result of having IPs enabled. |
| `post_clicks_convs_ip` | int | `123` | post_clicks_convs_ip | The number of the total post click conversion events that occurred as a result of having IPs enabled. |
| `reseller_revenue` | money | `0` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `profit` | money | `0.084102` | booked_revenue - total_cost | Booked revenue minus total cost. |
| `profit_including_fees` | money | `0.058959` | revenue_including_fees - cost - serving_fees | **Deprecated**. |
| `profit (net commissions/gross serving fees)` | money | `0.058959` | revenue - serving_fees - commissions | **Deprecated**. |
| `commissions` | money | `0` | Commissions for standard line items, $0 for ALIs. | Fees that come out of the booked revenue. |
| `cpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `vcpm` | money | `1.66051685393258` | (media_cost / imps_viewable) x 1000 | The media cost per thousand viewable impressions. |
| `cpm_including_fees` | money | `1.94302247191011` | (cost_including_fees / imps) x 1000 | **Deprecated**. |
| `post_click_convs` | int | `3` | post_click_convs | The total number of recorded post-click conversions. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_click_revenue` | money | `24.84` | post_click_revenue | The revenue from post-click conversions. |
| `post_view_convs` | int | `2` | post_view_convs | The total number of recorded post-view conversions. For more information on how we attribute post-view (and other) conversions, see [Conversion Attribution (Monetize)](../monetize/conversion-attribution.md) or [Conversion Attribution (Invest)](../invest/conversion-attribution.md). |
| `post_view_revenue` | money | `12.42` | post_view_revenue | The revenue from post-view conversions. |
| `post_view_cross_device` | int | `5` | post_view_cross_device | The number of post-view Cross Device conversions. |
| `post_click_cross_device` | int | `5` | post_click_ cross_device | The number of post-click Cross Device conversions. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `convs_per_mm` | double | `221.877080097625` | (total_convs / imps) x 1,000,000 | The number of conversions per million impressions. |
| `convs_rate` | double | `0.000221877080097626` | total_convs / imps | The rate of conversions to impressions. |
| `convs_bought` | int | `100` | convs_bought | The number of conversions according to Xandr and the buyer. |
| `clicks_bought` | int | `100` | clicks_bought | The total number of clicks across all impressions according to Xandr and the buyer. |
| `imps_bought` | int | `100` | imps_bought | The total number of impressions (served and resold) according to Xandr and the buyer. |
| `ctr` | double | `0.000221877080097626` | clicks / imps | The rate of clicks to impressions. |
| `total_rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions, including defaults, PSAs, and errors. |
| `rpm` | money |`2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `rpm_including_fees` | money | `2.60548314606741` | (revenue_including_fees / imps) x 1000 | **Deprecated**. |
| `total_network_rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `total_publisher_rpm` | money | `1.66051685393258` | (cost / imps) x 1000 | The cost per 1000 impressions. |
| `sold_network_rpm` | double | `231.888` | (revenue / imps) x 1000 ----- no errors | The revenue per 1000 impressions that were not defaults or errors. |
| `sold_publisher_rpm` | double | `147.786` | (cost / imps) x 1000 ----- no errors | The cost per 1000 impressions that were not defaults or errors. |
| `media_cost_pub_curr` | money | `123.45` | cost | The media cost, expressed in the currency of the publisher.<br><br>**Note**: You must group by `publisher` or `publisher_currency` when pulling this report if you are reporting across publishers who use different currencies. |
| `ppm` | money | `0.944966292134831` | (profit / imps) x 1000 | **Deprecated**. |
| `ppm_including_fees` | money | `0.662460674157303` | (profit_including_fees / imps) x 1000 | **Deprecated**. |
| `serving_fees` | money | `0.025143` | Serving fees for standard line items, $0 for ALIs. | Fees that are added to the media cost. Serving fees for standard line items, $0 for ALIs. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `cpvm` | money | `2.25` | (cost / imps_viewable) x 1000 | The cost per 1000 viewable impressions.<br><br>**Note**: This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. |
| `imps_master_creative` | int | `1276` | imps_master_creative | The total number of impressions from the master creative in page-level roadblocking.<br><br>**Note**: This metric is in alpha testing and not available to all customers. |
| `imps_filtered` | int | `2024` | imps_filtered | The total number of bid requests for which Xandr did not hold an auction due to inventory quality concerns.<br>See `imps_filtered_reason_id` and `imps_filtered_reason` (under Dimensions) for a list of the possible reasons. |
| `avg_bid_reduction` | double | `18%` | avg_bid_reduction | The average bid reduction you gained on the line item or campaign. This value represents the difference (as a percentage) between your bid and the actual media cost you paid for the impression you won (e.g., due to bid reduction). This value is only valid for RTB bidding (i.e., not Managed). Currently, this value is not accurately calculated for line items for which the `payment_auction_event_type` field has been set to `2` . |
| `partner_fees` | money | `123.45` | partner_fees | The total amount of third-party costs, budgeted using the [Partner Fee Service](./partner-fee-service.md), that have accrued on an augmented line item over the reported period of time. |
| `partner_fees_buying_currency` | money | `123.45` | partner_fees_buying_currency | The total amount of third-party costs, budgeted using the [Partner Fee Service](./partner-fee-service.md), that have accrued on an augmented line item over the reported period of time in buying (advertiser) currency. |
| `total_cost_buying_currency` | money | `123.45` | total_cost_buying_currency | The sum of media costs, `total_feature_costs`, `total_segment_data_costs` and partner fees in buying (advertiser) currency. |
| `total_cost_selling_currency` | money | `123.45` | total_cost_selling_currency | The sum of media costs, `total_feature_costs`, `total_segment_data_costs` and partner fees in selling (publisher) currency. |
| `total_segment_data_costs` | money | `123.45` | total_segment_data_costs | This includes all costs related to usage of segments in the data marketplace. Applicable when specific segments are applied in line items and associated pricing is displayed in the platform. |
| `total_feature_costs` | money | `123.45` | total_feature_costs | These are costs incurred when using a platform feature such as cross-device. |
| `total_cost` | money | `123.45` | total_cost = media_cost + total_feature_costs + total_segment_data_costs + partner_fees + commissions + serving_fees + publisher_revenue | The total amount of costs accrued over the reported period of time. This generally includes two types of costs, budgeted costs (media cost, data cost, partner fees, serving fees, commissions) and publisher revenue if you track publisher payouts on the platform.<br><br>**Note**: We have added logic to prevent double counting third-party fees during the breaking change period. |
| `total_cost_ecpm` | money | `123.45` | (total_cost/imps) * 1,000 | The total cost per 1,000 imps. |
| `total_cost_ecpc` | money | `123.45` | total_cost/clicks | The total cost per click. |
| `total_cost_ecpa` | money | `123.45` | total_cost/conversions | The total cost per conversion. |
| `buyer_media_cost` | money | `123.45` | media_cost | The amount of money paid by the buyer to Xandr, in dollars. |
| `buyer_media_cost_ecpm` | money | `123.45` | (media_cost/imps) * 1,000 | The effective cost per thousand impressions (eCPM) based on media cost. |
| `buyer_media_cost_ecpc` | money | `123.45` | media_cost/clicks | The effective cost per click (eCPC) based on media cost. |
| `buyer_media_cost_ecpa` | money | `123.45` | media_cost/conversions | The effective cost per acquisition (eCPA) based on media cost. |
| `network_profit` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost. |
| `network_profit_ecpm` | money | `123.45` | (network_profit/imps) * 1,000 | Network profit per 1,000 imps. |
| `network_profit_ecpc` | money | `123.45` | network_profit/clicks | Network profit per click. |
| `network_profit_ecpa` | money | `123.45` | network_profit/conversions | Network profit per conversion. |
| `network_profit_margin` | money | `123.45` | network_profit/(booked_revenue + reseller_revenue) | Network profit margin. |
| `network_profit_buying_currency` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost in buying (advertiser) currency. |
| `network_profit_selling_currency` | money | `123.45` | (booked_revenue + reseller_revenue) - total_cost | The sum of booked revenue and reseller revenue minus total cost in selling (publisher) currency. |
| `profit_ecpm` | money | `123.45` | ((booked_revenue - total_cost)/imps) * 1,000 | Profit per 1,000 imps.<br><br>**Note**: This field defines "profit" as booked revenue minus total cost. |
| `profit_ecpc` | money | `123.45` | (booked_revenue - total_cost)/clicks | Profit per click.<br><br>**Note**: This field defines "profit" as booked revenue minus total cost. |
| `profit_ecpa` | money | `123.45` | (booked_revenue - total_cost)/conversions | Profit per conversion.<br><br> **Note**: This field defines "profit" as booked revenue minus total cost. |
| `profit_margin` | money | `123.45` | (booked_revenue - total_cost)/booked_revenue | Buyer profit margin.<br><br> **Note**: This field defines "profit" as booked revenue minus total cost. |
| `profit_advertiser_currency` | money | `123.45` | booked_revenue - total_cost | Profit in buying (advertiser) currency. |
| `video_skips` | int | `10` | video_skips | The total number of times a user skipped the video. Use this metric for reporting when buying skippable inventory. |
| `video_starts` | int | `11` | video_starts | The total number of times the first segment of the video creative was downloaded and started. |
| `video_25_pcts` | int | `10` | video_25_pcts | The total number of times the video creatives completed 25% of the entire duration. |
| `video_50_pcts` | int | `7` | video_50_pcts | The total number of times the video creatives completed 50% of the entire duration. |
| `video_75_pcts` | int | `10` | video_75_pcts | The total number of times the video creatives completed 75% of the entire duration. |
| `video_completions` | int | `12` | video_completions | The total number of times the video creatives played for the entire duration. |
| `video_served` | int | `10` | video_served | The total number of video responses served to the player. An ad response occurs when the VAST document (XML) is served in response to a request. An ad response doesn't necessarily indicate a successful impression. For an impression, the first frame of the video must be served. |
| `video_errors` | int | `2`| video_errors | The total number of times a video error occurred. |
| `revenue_per_video_complete` | money | `25.76` | revenue/video_completions | The revenue per video completion. |
| `cost_per_video_complete` | money | `22.76` | cost/video_completions | The cost per video completion. |
| `video_completion_rate` | double | `1.12359550561797%` | (video completions/total impressions) x 100 | The ratio of video completions to impressions, expressed as a percentage. |
| `video_start_rate` | double | `1.12359550561797%` | video_start_rate | The percentage of times the first segment of the video creative was downloaded and started. |
| `video_skip_rate` | double | `1.12359550561797%` | video_skip_rate | The percentage of times the user opted to skip the video. |
| `buying_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * advertiser_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the buyer used to purchase the inventory.|
| `selling_currency_total_segment_data_costs` | money | `123.45` | total_segment_data_costs * publisher_exchange_rate | All costs related to usage of segments in the data marketplace. It is applicable when specific segments are applied in line items and associated pricing is displayed in the platform. It is in the currency the seller used to sell the inventory. |
| **Metrics with local currency support** |  |  |  |  |
| `revenue_buying_currency` | money | `123.45` | (booked_revenue + reseller_revenue) * [buying exchange rate] | The sum of booked revenue and reseller revenue in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `revenue_selling_currency` | money | `123.45` | (booked_revenue + reseller_revenue) * [selling exchange rate] | The sum of booked revenue and reseller revenue in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `booked_revenue_buying_currency` | money | `123.45` | booked_revenue * [buying exchange rate] | The total revenue booked through direct advertisers (line item) in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `booked_revenue_selling_currency` | money | `123.45` | booked_revenue * [selling exchange rate] | The total revenue booked through direct advertisers (line item) in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `reseller_revenue_buying_currency` | money | `123.45` | reseller_revenue * [buying exchange rate] | The total revenue on resold impressions through direct publishers in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `reseller_revenue_selling_currency` | money | `123.45` | reseller_revenue * [selling exchange rate] | The total revenue on resold impressions through direct publishers in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cost_buying_currency` | money | `123.45` | cost * [buying exchange rate] | The total amount of media cost for direct publisher and purchased real-time inventory in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cost_selling_currency` | money | `123.45` | cost * [selling exchange rate] | The total amount of media cost for direct publisher and purchased real-time inventory in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `profit_buying_currency` | money | `123.45` | profit * [buying exchange rate] | Profit (defined as booked revenue minus total cost) in the currency the buyer used to purchase inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `profit_selling_currency` | money | `123.45` | profit * [selling exchange rate] | Profit (defined as booked revenue minus total cost) in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `total_network_rpm_buying_currency` | money | `123.45` | (revenue / imps) x 1000 * [buying exchange rate] | The revenue per 1000 impressions in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `total_network_rpm_selling_currency` | money | `123.45` | (revenue / imps) x 1000 * [selling exchange rate] | The revenue per 1000 impressions in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cpm_buying_currency` | money | `123.45` | (cost / imps) x 1000 * [buying exchange rate] | The cost per 1000 impressions in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `cpm_selling_currency` | money | `123.45` | (cost / imps) x 1000 * [selling exchange rate] | The cost per 1000 impressions in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `rpm_buying_currency` | money | `123.45` | (revenue / imps) x 1000 * [buying exchange rate] | The revenue per 1000 impressions in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `rpm_selling_currency` | money | `123.45` | (revenue / imps) x 1000 * [selling exchange rate] | The revenue per 1000 impressions in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `ppm_buying_currency` | money | `123.45` | (profit / imps) x 1000 * [buying exchange rate] | **To be deprecated**. The profit per 1000 impressions in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `ppm_selling_currency` | money | `123.45` | (profit / imps) x 1000 * [selling exchange rate] | **To be deprecated**. The profit per 1000 impressions in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `sold_network_rpm_buying_currency` | money | `123.45` | (revenue / imps) x 1000 * [buying exchange rate] ----- no errors | The revenue per 1000 impressions that were not defaults or errors in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `sold_network_rpm_selling_currency` | money | `123.45` | (revenue / imps) x 1000 * [selling exchange rate] ----- no errors | The revenue per 1000 impressions that were not defaults or errors in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `commissions_buying_currency` | money | `123.45` | commissions * [buying exchange rate] | Fees that come out of the booked revenue in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `commissions_selling_currency` | money | `123.45` | commissions * [selling exchange rate] | Fees that come out of the booked revenue in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `serving_fees_buying_currency` | money | `123.45` | serving_fees * [buying exchange rate] | Fees that are added to the media cost in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `serving_fees_selling_currency` | money | `123.45` | serving_fees * [selling exchange rate] | Fees that are added to the media cost in the currency the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `data_costs_buying_currency` | money | `123.45` | data_costs * [buying exchange rate] | The total cost of 3rd party data used on the campaign in the currency the buyer used to purchase the inventory.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `data_costs_selling_currency` | money | `123.45` | data_costs * [selling exchange rate] | The total cost of 3rd party data used on the campaign the seller used to sell the impression.<br><br>**Note**: Exchange rates are not yet available in reporting. |
| `marketplace_clearing_event_units` | int | `23` | marketplace_clearing_event_units | The total number of events purchased (for the associated Clearing Event). When buying a Clearing Event other than impression (e.g., viewable impressions), the number of billed events will be less than the number of impressions. |
| `marketplace_clearing_event_units_cpm` | double | `11.2` | CPM/marketplace_clearing_event_units | CPM by marketplace clearing event units |
| `marketplace_clearing_events_booked_revenue_cpm` | double | `2.45` | total revenue/1000 events | The total revenue per 1000 events (for the associated Clearing Event). |
| `marketplace_clearing_event_buyer_media_cost_ecpm` | double | `2.37` | total media cost/1000 events | The total media cost per 1000 events (for the associated Clearing Event). |

## Custom viewable definition metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `viewdef_viewed_imps` | int | `4399` | viewdef_viewed_imps | The number of measured impressions that were viewable, per the member-level custom definition configuration (for more details, contact your Xandr account representative). |
| `viewdef_viewed_rate` | double | `96%` | viewdef_viewed_imps / view_measured_imps | The percentage of impressions that were viewable, per the member-level custom definition configuration, out of the total number of impressions measured for viewability. |

## Example

### Create a JSON formatted report request

The JSON file should include the `report_type` `"network_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`year`, `month`, `day`), and specify the format in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
{code}$ cat network_analytics

{
    "report":
    {
        "report_type":"network_analytics",
        "columns":[
            "hour",
            "seller_member_name",
            "buyer_member_name",
            "advertiser_name",
            "publisher_name",
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
{code}
```

### `POST` the request to the reporting service

```
{code}$ curl -b cookies -X POST -d @network_analytics 'https://api.appnexus.com/report'
{
   "response":{
      "status":"OK",
      "report_id":"097f59fc3ab7d02c5d60db42081d9b69"
   }
}
{code}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the reporting data to a file (described in the next step).

```
{code}$ curl -b cookies 'https://api.appnexus.com/report?id=097f59fc3ab7d02c5d60db42081d9b69'
{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2010-05-25 19:19:53",
         "json_request":"{\"report\":{\"report_type\":\"network_analytics\",\"columns\":[\"hour\",\"seller_member_name\",
            \"buyer_member_name\",\"advertiser_name\",\"publisher_name\",\"imps\",\"clicks\",\"total_convs\",\"ctr\",\"convs_rate\"],
            \"row_per\":[\"hour\",\"seller_member_id\",\"buyer_member_id\",\"advertiser_id\",\"publisher_id\"],
            \"report_interval\":\"last_48_hours\"}}",
         "url": "report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
{code}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the previous `GET` response. When identifying the file that you want to save to, be sure to use the file extension of the `"format"` that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
{code}$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/network_analytics.csv{code}
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
