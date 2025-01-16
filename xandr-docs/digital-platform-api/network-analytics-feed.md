---
title: Network Analytics Feed
description: Use the network analytics feed to get detailed information on a network's buy-side and sell-side performance.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Network analytics feed

The Network Analytics Feed offers you extensive data on your network's buy-side and sell-side performance. The `report_type` for this feed is `network_analytics_feed`.

> [!NOTE]
> **How to fetch this feed?**
>
> For instructions on how to fetch this feed, see the example on the [Bulk Reporting Feeds](./bulk-reporting-feeds.md) page.

## Data retention period

This report's data is retained for 30 days, and is available at an hourly time granularity.

## Dimensions

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `hour` | time | `2010-02-01 06:00:00` | The year, month, day, and hour of the auction. |
| `day` | time | `2010-02-01` | The year, month, and day of the auction. |
| `month` | time | `2010-02` | The year and month of the auction. |
| `adjustment_id` | int | `890` | The ID of the adjustment used to make changes to booked revenue and media cost values. |
| `advertiser_id` | int | `789` | The ID of the advertiser. If the value is `0`, either the impression was purchased by third-party buyer, or a `default` or `PSA` was shown. |
| `advertiser_code` | int | `789` | This field returns the same value as `advertiser_id`. To map the ID to the external code for the advertiser, use the [Lookup Service](./lookup-service.md). If the value is `0`, the impression was purchased by third-party buyer. |
| `advertiser_currency` | string | `"USD"` | The currency of the advertiser. |
| `bid_type` | string | `"Manual"` | The optimization phase the node was in when it bid for this impression.<br><br>**Note**: The term "give up" is appended to the bid types below if the valuation for that impression falls below the venue's "give up price".<br><br> For more information, see [What is a Venue?](../monetize/what-is-a-venue.md) and [Give Up](../monetize/give-up-price.md) in the UI documentation. Allowed values:<br> - `"Manual"`: Applies when you are bidding with a CPM goal, whether it's Base, EAP, or ECP.<br> - `"Learn"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we do not yet have enough data to bid optimized.<br> - `"Optimized"`: Applies when you are bidding with optimization (CPA, CPC, or margin) and we have enough data to bid optimized.<br> - `"Unknown"`: The node was in an unknown optimization phase.<br> - `"Optimized give up"`<br> - `"Learn give up"`<br> - `"Manual give up"` |
| `buyer_member_id` | int | `123` | The ID of the buying member. If the impression was not purchased, this field shows one of the following values: <br>`229` = PSA <br>`0` = Blank <br>`319` = Default |
| `buyer_type` | string | `"Real Time"`, `"Direct"` | The type of media purchased by the buyer member. |
| `campaign_id` | int | `222` | The ID of the campaign. |
| `creative_id` | int | `50` | The ID of the creative. For external click or impression trackers, this will be `"External Clicks"` or `"External Imps"`. For `imp_type = 6`, no information is available in the `creative_id` field for this report. See the [Seller Brand Review Report](./seller-brand-review-report.md) instead. |
| `creative_frequency_bucket` | string | `"15-30 minutes"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative frequency data. |
| `creative_recency_bucket` | string | `"11-20"` | **Deprecated**. If you request this dimension, only a default value will be returned. Please use the [Network Creative Frequency & Recency](./network-creative-frequency-and-recency.md) report to view creative recency data. |
| `deal_id` | int | `456` | The ID of the deal. For more information about negotiated deals between buyers and sellers, see [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md). |
| `entity_member_id` | int | `123` | If `imp_type` is `1`, `2`, `3`, `4`, `6`, or `8`, the ID of the buying member; otherwise, the ID of the selling member. |
| `external_inv_id` | int | `8293` | The ID of the external inventory code passed in the ad call and predefined by the publisher. For more details, see [External Inventory Code Service](./external-inventory-code-service.md). |
| `geo_country` | string | `"US"` | The code of the geographic country/region. |
| `height` | int | `720` | The height of the creative/placement. |
| `imp_type` | string | `"Blank"` | The ID for the type of impression. Possible values (associated types in parentheses):<br> - `1 ("Blank")`: No creative served.<br> - `2 ("PSA")`: A public service announcement served because there were no valid bids and no default creative was available.<br> - `3 ("Default Error")`: A default creative served due to a timeout issue.<br> - `4 ("Default")`: A default creative served because there were no valid bids.<br> - `5 ("Kept")`: Your advertiser's creative served on your publisher's site.<br> - `6 ("Resold")`: Your publisher's impression was sold to a third-party buyer.<br> - `7 ("RTB")`: Your advertiser's creative served on third-party inventory.<br> - `8 ("PSA Error")`: A public service announcement served due to a timeout issue or lack of a default creative.<br> - `9 ("External Impression")`: An impression from an impression tracker.<br> - `10 ("External Click")`: A click from a click tracker. |
| `insertion_order_id` | int | `321` | The ID of the insertion order. If the value is `0`, the impression was purchased by a third-party buyer. |
| `insertion_order_code` | int | `321` | This field returns the same value as `insertion_order_id`. To map the ID to the external code for the insertion order, use the [Lookup Service](./lookup-service.md). If the value is `0`, the impression was purchased by a third-party buyer. |
| `line_item_id` | int | `111` | The ID of the line item. If the value is `0`, the impression was purchased by a third-party buyer. |
| `line_item_code` | int | `111` | This field returns the same value as `line_item_id`. To map the ID to the external code for the line item, use the [Lookup Service](./lookup-service.md). If the value is `0`, the impression was purchased by a third-party buyer. |
| `media_type` | string | `"Banner"` | The general display style of a creative, for example, `Banner`, or `Video`. You can use the [Media Type Service](./media-subtype-service.md) to view the complete list of media types. |
| `mediatype_id` | int | `4` | The ID of the general display style of a creative. Possible values: <br> `1` = Banner <br> `2` = Pop <br> `3` = Interstitial <br> `4` = Video <br> `5` = Test <br> `6` = Expandable <br> `8` = Skin |
| `media_subtype` | string | `"Standard Banner"` | The specific display style of a creative, for example, `In-Banner Video`, or `Standard VAST`. You can use the [Media Type Service](./media-subtype-service.md) to view the complete list of media subtypes. |
| `media_subtype_id` | int |  `7`  | The ID of the specific display style of a creative. |
| `pixel_id` | int | `543` | The ID of the pixel. |
| `placement_id` | int | `432` | The ID of the placement. |
| `placement_code` | string | `"Placement Code"` | The external code for the placement. |
| `publisher_id` | int | `772` | The ID of the publisher. |
| `publisher_code` | string | `772` | This field returns the same value as `publisher_id`. To map the ID to the external code for the publisher, use the [Lookup Service](./lookup-service.md). If the value is `0`, the impression was purchased by a third-party buyer. |
| `publisher_currency` | string | `"USD"` | The currency of the publisher. |
| `pub_rule_id` | int | `588` | The ID of the publisher rule. This is the same as `payment_rule_id`. |
| `pub_rule_code` | string | `"Pub Rule Code"` | The external code for the publisher rule. |
| `seller_member_id` | int | `892` | The ID of the selling member. |
| `seller_type` | string | `"Real Time"`, `"Direct"` | The type of media sold by the selling member. |
| `site_id` | int | `673` | The ID of the site. |
| `site_code` | string | `"Site Code"` | The external code for the site. |
| `size` | string | `"720x90"` | The size of the creative/placement. |
| `width` | int | `90` | The width of the creative/placement |
| `revenue_type` | string | `"CPA"` | The basis on which an advertiser pays the member. |
| `payment_type` | string | `"com"`, `"revshare"` | The basis on which the member pays a broker. |
| `split_id` | int | `342` | The ID of the split that purchased the impressions in this data set. Splits are only applicable to augmented line items. For any reports that contain campaigns, the `split_id` (if included) will be `null`. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `booked_revenue` | money | `25.767257` | booked_revenue | The total revenue booked through direct advertisers (line item). |
| `booked_revenue_adv_curr` | money | `25.767257` | booked_revenue_adv_curr | The total revenue booked through a direct advertiser, in the currency of the advertiser. |
| `clicks` | int | `1` | clicks | The total number of clicks across all impression. |
| `commissions` | money | `0` | commissions | Fees that come out of the booked revenue. |
| `imps` | int | `2340` | imps | The total number of impressions (served and resold). |
| `media_cost` | money | `16.833378` | media_cost | The total cost of the inventory purchased. |
| `media_cost_pub_curr` | money | `16.833378` | media_cost_pub_curr | The total cost of the inventory purchased, in the currency of the publisher. |
| `network_advertiser_rpm` | money | `network_advertiser_rpm` | network_advertiser_rpm |  |
| `network_advertiser_rpm_adv_curr` | money | `network_advertiser_rpm_adv_curr` | network_advertiser_rpm_adv_curr |  |
| `network_resold_rpm` | double | `network_resold_rpm` | network_resold_rpm |  |
| `post_click_convs` | int | `3` | post_click_convs | The total number of recorded post-click conversions. |
| `post_click_revenue` | money | `12.90` | post_click_revenue | The total amount of recorded post-click revenue. |
| `post_view_convs` | int | `2` | post_view_convs | The total number of recorded post-view conversions. |
| `post_view_revenue` | money | `150.00` | post_view_revenue | The total amount of recorded post-view revenue. |
| `ppm` | money | `4.14` | (profit / imps) x 1000 | The profit per thousand impressions. |
| `profit` | money | `970.40` | revenue - media_cost | The total network revenue minus the network cost. |
| `publisher_rpm_publisher_currency` | money | `200.22` | publisher_rpm_publisher_currency |  |
| `reseller_revenue` | money | `720.10` | reseller_revenue | The total revenue on resold impressions through direct publishers. |
| `revenue` | money | `1921.23` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue. |
| `revenue_adv_curr` | money | `1921.23` | booked_revenue + reseller_revenue | The sum of booked revenue and reseller revenue, in the currency of the advertiser. |
| `rpm_adv_curr` | double | `8.21` | (revenue / imps) x 1000 | The revenue per thousand impressions, in the currency of the advertiser. |
| `serving_fees` | money | `0.025143` | serving_fees | Fees that are added to the media cost. |
| `total_convs` | int | `5` | total_convs | The total number of post-view and post-click conversions. |
| `total_network_rpm` | money | `2.60548314606741` | (revenue / imps) x 1000 | The revenue per 1000 impressions. |
| `total_publisher_rpm` | double | `1.66051685393258` | (media_cost / imps) x 1000 | The cost per 1000 impressions. |
| `imps_viewed` | int | `30,450` | imps_viewed | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | view_measured_imps | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | view_rate | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | view_measurement_rate | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `imps_master_creative` | int | `100` | imps_for_budget_caps_pacing | The total number of impressions from the master creative in page-level roadblocking. |

## Example

For an example, see the **Example** section in [Bulk Reporting Feeds](./bulk-reporting-feeds.md).

## Related topics

- [Clicktrackers Feed](./clicktrackers-feed.md)
- [Bulk Reporting Feeds](./bulk-reporting-feeds.md)
