---
title: Line Item Service - ALI
description: Explore the Line Item Service for Augmented Line Items (ALI), which defines your financial relationship with an advertiser.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Line Item service - ALI

> [!NOTE]
> This page describes the Line Item Service for augmented line items. It links to other API documentation that is designed for legacy line items and may mention fields and objects that are not used with augmented line items. Most importantly, augmented line items can only be used with seamless insertion orders, not legacy insertion orders, which don't support budget intervals (i.e., don't use the `budget_intervals` array).
>
> To create an augmented line item, you must set the `line_item_type` field to `'standard_v2'` and associate the line item with a seamless insertion order via the `insertion_orders` array.

A line item defines your financial relationship with an advertiser, including budget, revenue type, performance goals, bidding strategies, and inventory targeting. The augmented line item must be used with the seamless insertion order. We suggest that you streamline your setup for long-standing advertiser relationships by adding budget intervals to your insertion orders.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>(line item JSON) | Add a new line item. |
| `PUT` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE)<br>(line item JSON) | Modify an existing line item. |
| `GET` | - [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE) | View all of an advertiser's line items. |
| `GET` | [https://api.appnexus.com/line-item?id=1,2,3](https://api.appnexus.com/line-item?id=1,2,3)<br><br>**Note:**<br>**Helpful Query String Filters**<br>- You can filter for line items based on when they first and last served. This is particularly useful when you are approaching your object limit and need to identify line items that can be deleted from the system. For more details, see [First Run/Last Run](#first-runlast-run).<br>- You can filter for line that are not serving due to various conditions. For more details, see [Alerts](#alerts) below. | View multiple line items by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/line-item?search=SEARCH_TERM](https://api.appnexus.com/line-item?search=SEARCH_TERM) | Search for line items with IDs or names containing certain characters. |
| `DELETE` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE)<br><br>**Warning:**<br>**Deletion is Recursive and Permanent**<br>Deleting a line item will also delete all of its impression trackers, click trackers, associated budget intervals, and splits. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., revenue budget, tracking, cost budget and targeting). | Delete a line item. |

> [!NOTE]
> **About Performance Goals**
>
> Goal Pixels are used to track and measure performance when the `revenue_type` and the `goal_type` are not measured the same way. For example, a `revenue_type` of `"cpm"` might be matched with a `goal_type` of `"cpa"` because the advertiser wants to measure goal achievement in terms of conversions but pay in CPM.
>
> - **CPA**: To set performance goals for line items with `goal_type` `"cpa"`, use both the [Goal Pixels](#goal-pixels) array of objects and the [Valuation](#valuation) object below. The `goal_pixels` array contains information about CPA goal targets and thresholds. See **CPC** below for a basic explanation of the `valuation` object.
> - **CPC**: To set performance goals for line items with the `goal_type` `"cpc"`, use the `valuation` object. The `valuation` object contains the performance goal threshold, which determines the bid/no bid cutoff on optimized line items, and the performance goal target, which represents the desired clicks or click-through rate. For more details on which fields to set, see the description of the `valuation` object below.
>
> **About Geography Targeting**
>
> For Augmented Line Item, it is mandatory to set at least one country/region as geography targeting. To add geography targeting, see **Country Targets** under **Targeting** section in the **[Profile Service](profile-service.md)** page.

## JSON fields

### General

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item.<br>**Required On:** `PUT`, in query string. |
| `code` | string (100) | A custom code for the line item. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No 2 objects at the same level (e.g., insertion orders or line items) can use the same code per advertiser. For example, 2 line items cannot both use code "XYZ", but a single insertion order and its child line item can.<br>**Default:** `null` |
| `name` | string (255) | The name of the line item.<br>**Required On:** `POST` |
| `advertiser_id` | int | The ID of the advertiser to which the line item belongs. |
| `state` | enum | The state of the line item. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `line_item_type` | enum | The type of line item. Possible values are:<br>- `"standard_v1"`: Standard line item (non-ALI).<br>- `"standard_v2"`: Augmented line item (ALI).<br>- `"guaranteed_delivery"`: Guaranteed line item (GDLI).<br> - `"curated"`: Curated line item.<br><br>**Note:**<br>Ensure this field is set to `"standard_v2"` for ALIs.<br>**Default:** `"standard_v2"` |
| `start_date` | timestamp | Do not use this field. Instead, use the `start_date` and `end_date` fields within the `budget_intervals` array to designate when the line item should run.<br>**Default:** `null` (immediately) |
| `end_date` | timestamp | Do not use this field. Instead, use the `start_date` and `end_date` fields within the `budget_intervals` array to designate when the line item should run.<br>**Default:** `null` (indefinitely) |
| `timezone` | enum | The timezone by which budget and spend are counted. For details and accepted values, see [API Timezones](api-timezones.md).<br><br>**Note:**<br>For ALIs, be sure to use this field (and not the one in the `budget_intervals` array) to set the line item's time zone.<br>**Default:** `"UTC"` or advertiser's timezone. |
| `ad_types` | array of strings | The type of creative used for this line item. Possible values:<br>- `"banner"`<br>- `"video"`<br>- `"native"`<br>- `"audio"`<br><br>The array should only have a single value. This value determines how auction items are tracked for the line item's buying strategy, paying strategy, optimization options, creative association, and targeting options.<br><br>**Note:**<br>All creatives associated to a line item must have the same ad type, which should match the `ad_types` selected here.<br>**Default:** `"banner"`<br>**Required On:** `POST`/`PUT` |
| `discrepancy_pct` | double | **Deprecated.** |
| `publishers_allowed` | string | **Deprecated.** Use the values of the `supply_strategies` array to set the supply types (e.g., RTB/Open Exchange, Deals, Managed). |
| `revenue_value` | double | The amount paid to the network by the advertiser.<br><br>**Note:** Depending on what you set the `revenue_type` field to, this field must be set to the actual value of that revenue type (e.g., the desired CPC). If your `revenue_type` is `"cost_plus_margin"`, set this field to the percentage margin your client pays you (e.g., `.20` for 20%).<br>**Required On:** `POST`/`PUT` |
| `revenue_type` | enum | The way the advertiser has agreed to pay you (also called Booked Revenue). Possible values are listed below.<br>- `"cpm"`: Select this value if you are being paid flat payment for 1000 impressions (CPM), per click (CPC) or per view (Viewable CPM):<br>&nbsp; - If CPM, set this to `"cpm"`, the `revenue_value` field to the CPM value and set the `max_avg_cpm` and `min_avg_cpm` fields to `null`.<br>&nbsp; - If CPC, set this to `"cpm"`, the `revenue_value` field to the CPC value and set `"revenue_auction_event_type"` to `"click"`, `"revenue_auction_event_type_code"` to `"click"`, and `"revenue_auction_type_id"` to `3`.<br>&nbsp; - If Viewable CPM, set this to `"cpm"`, the `revenue_value` field to the Viewable CPM value, the `revenue_auction_event_type` field to `"view"`, the `revenue_auction_event_type_code` field to `"view_display_50pv1s_an"`, and `"revenue_auction_type_id"` to `2`. Only measured viewable impressions will be counted, according to the Xandr viewability measurement, using the IAB definition.<br>&nbsp; - If CPCV, set this to `"cpm"`, the `ad_types` field to `"video"`, `"revenue_auction_event_type"` to `"video"`, `"revenue_auction_event_type_code"` to `"video_completion"`, and `"revenue_auction_type_id"` to `10`.<br> - `"vcpm"`: A dynamic CPM (where Booked Revenue is equal to the cost of the impression before bid reduction). If `"vcpm"` is selected here, `goal_type` has been set to `'none'`, and no `'expected_value'` model has been attached, you must set a `'max_avg_cpm'` value.<br><br>**Note:**<br>If `programmatic_guaranteed` (in `supply_strategies`) is set to `true`, `revenue_type` must be set to `cost_plus_margin` or `cost_plus_cpm`.<br> - `"cost_plus_margin"`: Media cost (what you spend on inventory) plus a percentage of what you spend. If selected, you must also set the `revenue_value` to a percentage margin you receive (e.g., `.2` for 20%). Data costs will also be added if you participate in third-party data clearing (e.g., segments). If you disable optimization for Cost Plus (via the `goal_type` field), you must set a flat CPM for Cost Plus via the `max_avg_cpm` field (in the `valuation` object).<br>- `"cost_plus_cpm"`: Media cost (what you spend on inventory) plus a service fee that you charge the advertiser based on CPM revenue. If selected, you must also set the `revenue_value` to a flat CPM margin you receive (e.g., `1` for a $1 CPM). Data costs will also be added if you participate in third-party data clearing (e.g., segments). If you disable optimization for Cost Plus (via the `goal_type` field), you must set a flat CPM for Cost Plus via the `max_avg_cpm` field (in the `valuation` object).<br><br>**Note:**<br>If the `lifetime_budget_imps` or `daily_budget_imps` fields are set or the line item's parent insertion order's `budget_type` is set to `impression`, then `revenue_type` may not be set to `"CPC"`.<br>**Default:** `"none"` |
| `goal_type` | enum | For line items that make use of performance goals. Possible values: `null`, `"cpc"`, `"cpa"`, `"ctr"`, or `"custom"`.<br> - If you want to optimize to a CPA performance goal for both post-click and post-view conversions, set this field to `"cpa"`. You must also set the `post_click_goal_threshold` and `post_videw_goal_threshold` fields (in the `goal_pixels` array of objects) to your CPA goal. These values must be the same, since Xandr will optimize to one value. Additionally, you must set `campaign_group_valuation_strategy` to "`retargeting"` or `"prospecting"`. For details, see `campaign_valuation_strategy` in [Valuation](#valuation) below.<br>- If you want to optimize to a CPA performance goal for only post-click conversions, set this field to `"cpa"`. You must also set the `post_click_goal_target` and `post_click_goal_threshold` fields (in the `goal_pixels` array of objects) to your CPA goal.<br> - If you want to optimize to a CPC goal, set this field to `"cpc"`. You must also set the `goal_target` and `goal_threshold` fields (in the `valuation` object) to your CPC goal and set `goal_pixel` to `null`.<br> - If you want to optimize to a Viewable CPM goal, set this field to `null`. You must also set the `goal_target` and `goal_threshold` fields (in the valuation object) and `goal_pixels` to `null`. In addition, you must also set the following fields in the `auction_event` object: `kpi_auction_event_type`, `kpi_auction_event_type_code`, `kpi_auction_type_id`, and `kpi_value`.<br>- If you want to optimize to a CTR goal, set this field to `"ctr"`. In addition, you must also set the `goal_target` and the `goal_threshold` in the `valuation` object to the desired clickthrough rate (a decimal value between `0` and `1`).<br> - If you want to upload your own custom EV model (Expected Valuation), as opposed to a `click_imp` or `ev_click` model, set this field to `"custom"`. For details, see [Custom Models](../data-science-toolkit/custom-models.md).<br>- If you want to disable optimization, set this field to `null`. In addition, for `PUT` calls, if the line item was previously set to optimize to a Viewable CPM, you must also set the following fields (in the `auction_event` object) as follows:<br>&nbsp; - `"kpi_auction_event_type"`: `"impression"`<br>&nbsp; - `"kpi_auction_event_type_code"`: `"impression"`<br>&nbsp; - `"kpi_auction_type_id"`: `1`<br>&nbsp; - `"kpi_value"`: `null`<br><br>**Default:** `"none"` |
| `goal_value` | double | **Deprecated.** Use `valuation` object instead. For details, see [Valuation](#valuation) below. |
| `last_modified` | timestamp | The time of last modification to this line item.<br>**Read Only.** |
| `click_url` | string (1000) | The click URL to apply at the line item level. |
| `currency` | string (3) | The currency used for this line item. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Note:**<br>Once the line item has been created, the currency cannot be changed.<br><br>**Tip:**<br>As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience.<br><br>**Default:** Default currency of the advertiser. |
| `require_cookie_for_tracking` | boolean | Indicates whether you want to serve only to identified users for conversion-tracking purposes. If set to `true`, you won't serve to anonymous users because they have a lower potential for conversion attribution. If set to `false`, this indicates that you'll serve to anonymous users and accept only IP-based conversion attribution for those users (if turned on). This field's setting is only relevant when a conversion pixel has been applied, so setting this to `true` won't require identifiers for a line item that has no conversion pixels. <br><br> - If `true`, an identifier is required for conversion tracking. <br> - If `programmatic_guaranteed` (in `supply_strategies`) is set to `true`, `require_cookie_for_tracking` must be set to `false`. <br><br> **Default:** `true` |
| `profile_id` | int | You may associate an optional `profile_id` with this line item. A profile is a generic set of rules for targeting inventory. For details, see the [Profile Service](profile-service.md). |
| `member_id` | int | ID of the member that owns the line item. |
| `comments` | string | Comments about the line item. |
| `remaining_days` | int | The number of days between today and the `end_date` for the line item. <br><br>**Note:** This will be `null` if the `start_date` is in the future or if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `total_days` | int | The number of days between the `start_date` and `end_date` for the line item. <br><br>**Note:** This will be `null` if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `advertiser` | object | An object describing the advertiser with which this line item is associated. For details, see [Advertiser](#advertiser) below.<br><br>**Read Only.** |
| `labels` | array | The optional labels applied to the line item. Currently, the labels available are: `"Trafficker"` and `"Sales Rep"`. For more details, see [Labels](#labels) below.<br><br>**Note:**<br>You can report on line item labels with the [Network Analytics](network-analytics.md) and [Network Advertiser Analytics](./network-advertiser-analytics.md) reports. For example, if you use the `"Trafficker"` label to specify the name of the trafficker responsible for each line item, you could run the Network Analytics report filtered by `"trafficker_for_line_item"` to focus on the line items that a particular trafficker is responsible for, or grouped by `"trafficker_for_line_item"` to rank the performance of your traffickers. |
| `broker_fees` | array | **Deprecated.** Use `partner_fees` instead. |
| `pixels` | array of objects | The conversion pixels used to track CPA revenue. Both post-click and post-view revenue may be specified. You may only attach 20 pixels to a line item. If you need to attach more, speak with your Xandr Implementation Consultant or Support. For more details, see [Pixels](#pixels) and the example below for a sample of the format.<br>**Default:** `null` |
| `broker_fees` | array | **Deprecated.** Use `partner_fees` instead. |
| `pixels` | array of objects | The conversion pixels used to track CPA revenue. Both post-click and post-view revenue may be specified. You may only attach 20 pixels to a line item. If you need to attach more, speak with your Xandr Implementation Consultant or Support. For more details, see [Pixels](#pixels) and the example below for a sample of the format.<br>**Default:** `null` |
| `insertion_orders` | array of objects | Objects containing metadata for the insertion orders this line item is associated with. For more information, see [Insertion Orders](#insertion-orders) below.<br><br>**Note:**<br>Once a line item is associated with a seamless insertion order, it cannot be associated to a legacy insertion order. |
| `goal_pixels` | array of objects | For a line item with the `goal_type` `"cpa"`, the pixels used for conversion tracking, as well as the post-view and post-click revenue. For more details, see [Goal Pixels](#goal-pixels) and the example below for a sample of the format. |
| `imptrackers` | array of objects | The third-party impression trackers associated with the line item. For more details, see [Impression Tracker Service](impression-tracker-service.md).<br>**Read Only.** |
| `clicktrackers` | array of objects | The third-party click trackers associated with the line item. For more details, see [Click Tracker Service](click-tracker-service.md).<br>**Read Only.** |
| `valuation` | object | For a line item with the `goal_type` `"cpc"` or `"cpa"`, the performance goal threshold, which determines the bid/no bid cutoff on optimized line items, and the performance goal target, which represents the desired clicks (conversions for `"cpa"` are set in the [Goal Pixels](#goal-pixels) array of objects). For more details, see [Valuation](#valuation) below. |
| `creatives` | array of objects | The creatives that are associated with the line item. For more details, see [Creatives](#creatives) below. |
| `budget_intervals` | array of objects | Budget intervals enable multiple date intervals to be attached to a line item, each with corresponding budget values. For more details, see [Budget Intervals](#budget-intervals) below.<br><br>**Note:**<br>If you use `budget_intervals`, the following fields should not be used on the line-item object:<br> - `lifetime_pacing`<br> - `lifetime_budget`<br> - `lifetime_budget_imps`<br> - `enable_pacing`<br> - `lifetime_pacing_span`<br> - `allow_safety_pacing`<br> - `daily_budget`<br> - `daily_budget_imps`<br> - `lifetime_pacing_pct`<br> - `subflights` |
| `lifetime_budget` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited) |
| `lifetime_budget_imps` | int | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited) |
| `daily_budget` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited) |
| `daily_budget_imps` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited) |
| `enable_pacing` | boolean | If `true`, the daily budgeted spend is spread out evenly throughout a day. Only applicable if there is a daily budget. That's why it defaults to `true` if daily budget is set; otherwise, it defaults to `null`.<br>**Default:** `null` |
| `allow_safety_pacing` | boolean | **Deprecated.** This field may not be set. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to spend its overall lifetime budget evenly over the line item flight dates. If `true`, you cannot set a `daily_budget`, you cannot set `enable_pacing` to `false`, and you must first establish a `lifetime_budget`, a `start_date`, and an `end_date` for the line item.<br>**Default:** `null` |
| `lifetime_pacing_span` | int | **Note:** Do not use or edit the value of this field.<br>**Default:** `null` (3 days) |
| `lifetime_pacing_pct` | double | A double integer between-- and including-- 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between `50` and `150` on the following scale:<br> - `50`: Pace behind schedule.<br>- `100`: Pace evenly.<br>- `150`: Pace ahead of schedule.<br>**Default:** `100` |
| `payout_margin` | double | The payout margin on performance offer line items. |
| `insertion_order_id` | int | The ID of the current active insertion order (when applicable). Must append `include_insertion_order_id=true` to return this field in a `GET` call. For details, see the [Insertion Order Service](insertion-order-service.md). |
| `stats` | object | The stats object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `all_stats` | array | To show Rapid Reports for all available intervals (today, yesterday, the last 7 days, life time), pass `all_status=true` in the query string of a `GET` request.<br>**Read Only.** |
| `first_run` | timestamp | The date and time when the line item had its first impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they first served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `last_run` | timestamp | The date and time when the line item had its last impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they last served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `expected_pacing` | double | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `total_pacing` | double | **Deprecated.**<br><br>**Note:**<br>The `stats` and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_dollars` | enum | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_imps` | enum | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `imps_pacing_percent` | int | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `rev_pacing_percent` | int | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `alerts` | object | The conditions that are preventing the line item from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional. To retrieve line items based on pauses, you must pass certain query string parameters in the `GET` request. For more details, including a complete list of possible pauses, see [Alerts](#alerts) below.<br>**Read Only.** |
| `inventory_type` | enum | **Deprecated.**<br>The type of inventory targeted by this line item. Possible values: `"real_time"`, `"direct"`, or `"both"`. `"Real-time"` includes all third-party inventory not managed by your network that has been enabled for reselling (including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager). `"Direct"` includes only inventory managed by your network.<br><br>**Note:** Although you can continue to use this field, the fields within `supply_strategies` object are the preferred mechanism for designating inventory supply sources. However, once you set any of the boolean fields within `supply_strategies` object to `true`, the value of the `inventory_type` field will be permanently ignored and unsettable for that augmented line item.<br>**Default:** `"real_time"` |
| `supply_strategies` | object | An object containing several boolean fields used to designate which inventory supply sources you would like to target. The values of this object's boolean fields supersede the setting of the `inventory_type` field and once set will cause the `inventory_type` field to be permanently locked and ignored. For more details, see [Supply Strategies](#supply-strategies) below. |
| `creative_distribution_type` | enum | When multiple creatives of the same size are trafficked via a line item, this field's setting is used to determine the creative rotation strategy that will be used. Allowed values:<br> - `even`: Even rotation is handled automatically by our system. Also select this if you want creative rotation to be handled at the splits level.<br> - `weighted`: Creative rotation is based on a user-supplied weight.<br> - `ctr-optimized`: The creative in the size bucket with the highest CTR delivers the most.<br>**Default:** `null`<br><br>**Note:** If a specific `creative_distribution_type` is not passed through the API (`null` value is passed), then value of `creative_distribution_type` is set to `even`. |
| `prefer_delivery_over_performance` | boolean | This field is used to indicate your goal priority (whether you wish to give greater priority to delivery, performance, or margin). Options are:<br>- `true`: This option (delivery) prioritizes impression volume by multiplying bids up to 2x in response to delivery. When you optimize to clicks, it also allows line items to discover inventory with historical CPCs up to 10x the goal.<br><br>**Warning:**<br>This may cause margin and performance to be deprioritized, possibly resulting in a negative margin.<br><br>- `false`: Select this option to do one of the following:<br>&nbsp; - Prioritize performance (e.g., clicks). This prioritizes your advertiser goal over impression volume and profit. If you select this option, you must also set `min_margin_pct` (in the `valuation` object) to `null`.<br>&nbsp; - Prioritize margin. This reduces optimized bids by your desired profit margin. Additional margin may be earned through Adaptive Pacing if your revenue type is CPM, Dynamic CPM, Viewable CPM, or CPC. If you select this option, you must also set the `min_margin_pct` field (in the `valuation` object) to your desired margin (e.g. `10` for 10%)<br>**Default:** `false` |
| `use_ip_tracking` | boolean | Determines whether IP Attribution is enabled or not for a given line item. |
| `viewability_vendor` | string | This field determines what provider measures the viewability of the ad unit. The only value that is currently valid is `"appnexus"`.<br>**Default:** `"appnexus"` |
| `is_archived` | boolean | **Read-only.** Indicates whether the line item has been automatically archived due to not being used. Once set to `true`, the value can't be changed and the only calls that can be made on the line item object are `GET` and `DELETE`.<br><br>**Note:**<br>If a line item is automatically archived, its profile will also be archived and the only calls that may be made on either of those objects are `GET` and `DELETE`. In addition, once archived, the line item may not be associated with any insertion orders.<br>**Default:** `false` |
| `archived_on` | timestamp | The date and time on which the line item was archived (i.e., when the `is_archived` field was set to `true`).<br>**Default:** `null`<br>**Read Only.** |
| `partner_fees` | Array | An array of partner fees applied to this line item. You can create or view third-party partner fees with the [Partner Fee Service](partner-fee-service.md). For more details, see [Partner Fees](#partner-fees) below. |
| `line_item_subtype` | enum | The subtype of the line item. The `line_item_subtype` field cannot be changed after the line item is created. For Invest buyers, the supported values are as follows:<br> - `standard_buying`: Augmented line item eligible to serve on managed, RTB, or deals. Omitting the line_item_subtype on `POST` requests will default to this subtype behaviour.<br>- `pg_buying`: Eligible only to transact on PG deals. If the subtype is passed on the `POST`, the `line_item_type`, `bid_object_type`, `delivery_model_type`, and `supply_strategies` fields are not required.<br>- `standard_curated`: For curated deal line items. For more details, see `line_item_subtype` in [Curated Deal Line Item API Setup Guide](curated-deal-line-item-api-setup-guide.md).<br><br>**Default:** `standard_buying` |

### Budgeting/pricing

| Field | Type | Description |
|:---|:---|:---|
| `lifetime_budget` | double | The lifetime budget in dollars (media cost). `Null` corresponds to `"unlimited"`.<br><br>**Warning:**<br>If `lifetime_budget` is set to `null` (unlimited), and the line item and insertion order lifetime budgets are also set to `null`, severe overspend can occur.<br><br>**Default:** `null` |
| `lifetime_budget_imps` | int | The lifetime budget in impressions. `Null` corresponds to `"unlimited"`.<br>**Default:** `null` |
| `daily_budget` | double | The daily budget in dollars (revenue). `Null` corresponds to `"unlimited"`.<br>**Default:** `null` |
| `daily_budget_imps` | int | The daily budget in impressions. `Null` corresponds to `"unlimited"`.<br>**Default:** `null` |
| `learn_budget` | double | **Deprecated.**<br>**Default:** `null` |
| `learn_budget_imps` | int | **Deprecated.**<br>**Default:** `null` |
| `learn_budget_daily_cap` | double | **Deprecated.**<br>**Default:** `null` |
| `learn_budget_daily_imps` | int | **Deprecated.**<br>**Default:** `null` |
| `enable_pacing` | boolean | If `true`, the line item's daily budgeted spend is spread out evenly throughout each day. This is only applicable if `daily_budget` is set.<br>**Default:** `false` |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to spend its overall lifetime budget evenly over the line item flight dates. If `true`, you cannot set a `daily_budget`, you cannot set `enable_pacing` to `false`, and you must first establish a `lifetime_budget`, a `start_date`, and an `end_date` for the line item.<br>**Default:** `false` |
| `lifetime_pacing_span` | int | In the event of an underspend event, this indicates the number of days across which the underspent amount will be distributed. The default value of `null` indicates a value of three (3) days.<br>**Default:** `null` |
| `priority` | int | For a line item targeting managed inventory (`inventory_type` is `"direct"`), since you have already paid for inventory, there is no need to input a buying strategy. However, you can set the line item's priority to weight the line item against other direct line items within your account. The line item with the highest priority will always win, even if a lower priority line item bids more.<br>**Default:** `5` |
| `expected_pacing` | double | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `total_pacing` | double | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_dollars` | enum | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_imps` | enum | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `imps_pacing_percent` | int | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `media_cost_pacing_percent` | int | **Deprecated.**<br><br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |

### Supply strategies

The `supply_strategies` object is used to designate which supply source you wish to target when buying inventory. You can target any combination of the `rtb` (Open Exchange), `managed`, or `deals` fields by setting each to `true` or `false`. If you are targeting a programmatic guaranteed deal, set the `programmatic_guaranteed` field to `true` and the `rtb`, `managed`, and `deals` fields to `false`. At least one of these `supply_strategies` object fields must be set to `true`.

> [!NOTE]
> For deals, in addition setting the `deals` field to `true` within this object, you must also ensure that you both provide a list of deals to target or exclude in the `deal_targets` array and set the `deal_action_include` field to `true` or `false` (depending on inclusion or exclusion) in the [Profile Service](profile-service.md).
> [!WARNING]
> The values of this object's boolean fields supersede the setting of the `inventory_type` field. Once any of these fields are set to `true` on an ALI, the `inventory_type` field will be ignored and unsettable for that line item. If you attempt to make a `PUT` call on the value of the `inventory_type` field after one or more of these fields have been set to `true` , the following error message will be generated: `"inventory_type cannot be updated once supply_strategies has been set"`.
> [!NOTE]
> The Line Item API Service supports Roadblocks only if the `supply_strategy` is `managed`.

| Field | Type | Description |
|:---|:---|:---|
| `rtb` | boolean | Designates whether you wish to target inventory on the Open Exchange. This includes all third-party inventory not managed by your network that has been enabled for reselling (including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager). |
| `managed` | boolean | Designates whether you wish to target managed inventory. This only includes inventory managed by your network. |
| `deals` | boolean | Designates whether you wish to target deal inventory. This includes any deals which you are are eligible to bid on. |
| `programmatic_guaranteed` | boolean | Designates whether you wish to target a programmatic guaranteed deal with this line item. If this is set to `true`, then the `rtb`, `managed`, and `deals` fields must be set to `false`. |

#### Target open exchange and 2 deals but *not* managed inventory

```
{code} $ cat LI-supply-strategies.json

{
    "line-item": {
      ...
      "supply_strategies": {
          "managed": false,
          "rtb": true,
          "deals": true
      }
      ...
    }
}
 
$ cat profile-supply-strategies.json 
{
    "profile": {
      "deal_action_include": true,
      "deal_targets": [
          {
              "id": 44,
              "name": "Deal with external supply partner",
              "code": "APN-1234-2200f"
          },
          {
              "id": 45,
              "name": "Deal with Console seller",
              "code": null
          }
      ]
  }
}
{code}
```

### Advertiser

You can use the [Advertiser Service](advertiser-service.md) to create or view advertisers.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for this advertiser. |
| `name` | string | The name of the advertiser associated with the unique ID above. |

### Labels

You can use the read-only [Label Service](label-service.md) to view all possible labels for line items, advertisers, insertion orders, and publishers. This service also allows you to view the labels that have already been applied to your objects.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the label. <br>Possible values: `7`, `8`, `11`. |
| `name` | enum | **Read-only.** The name of the label.<br>Possible values: `"Trafficker"` or `"Sales Rep"`. |
| `value` | string (100) | The value assigned to the label. For example, for the `"Sales Rep"` label, this could be a name such as `"Michael Sellers"`. |

### Broker fees

Broker fees are deprecated for augmented line items. Create partner fees and apply them to the line item using the [Partner Fee Service](partner-fee-service.md).

### Partner fees

If you need to reserve a portion of your budget for third-party costs—costs owed to parties other than the publisher—you can define this information with the [Partner Fee Service](partner-fee-service.md). Fees can be tracked on a CPM, cost share, or revenue share basis, and can be applied to multiple advertisers and line items, if desired. A single advertiser or line item can have multiple fees applied.

The `partner fee` array includes the following field:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of a partner fee applied to this line item. |

#### Apply a fee to a line item

```
$cat LI-update.json

{
    "line-item": {
        "partner_fees": [
            {"id": 4401
            },
            { "id": 4402
            }
    ]
}

$curl -b cookie -X PUT -d @LI-update.json "https://api.appnexus.com/line-item?id=2345432"

{
    "response": {
        "status" : "OK",
        "id": 2345432
    }
}
```

#### Remove a fee from a line item

> [!NOTE]
> You cannot remove a fee from a line item if `required` on the [partner fee](partner-fee-service.md) is `true`. You must first set `required` to `false` and then remove the fee from the line item.

```
$curl -b cookie -x GET "https://api.appnexus.com/line-item?id=2345432"

 {
    "line-item": {
        ...,
        "partner_fees": [
            {
                "id": 1
            },
            {"id": 2
            }, 
            {"id": 3
            }
        ],
        ...
    }
}

$cat LI-update.json

{
    "line-item": {
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 3
            }, 
    ]
                }
}

$curl -b cookie -X PUT -d @LI-update.json "https://api.appnexus.com/line-item?id=2345432"

{
    "line-item": {
        ...,
        "partner_fees": [
            {
                "id": 1
            },
            {
                "id": 3
            }
        ],
        ...
    }
}
```

### Pixels

Each object in the `pixels` array includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the conversion pixel. |
| `state` | enum | The state of the pixel. Possible values: `"active"` or `"inactive"`. |
| `post_click_revenue` | double | The post click revenue value for the pixel. This field can only be set when the line item's `revenue_type` field has been set to `cpa` (as a result, this field can't be used with augmented line items). |
| `post_view_revenue` | double | The post view revenue value for the pixel. This field cab only be set when the line item's `revenue_type` field has been set to `cpa` (as a result, this field can't be used with augmented line items). |
| `name` | string | The name of the conversion pixel.<br>**Read Only.** |
| `trigger_type` | enum | The type of event required for an attributed conversion. <br>Possible values: `"view"`, `"click"`, or `"hybrid"`.<br>**Read Only.** |

### Insertion orders

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of the insertion order.<br><br>**Note:** Once a line item is associated with a seamless insertion order, it cannot be associated to a legacy insertion order. |
| `state` | enum | The state of this insertion order: `"active"` or `"inactive"`. |
| `code` | string | An optional custom code used to identify this insertion order. |
| `name` | string | The name of this insertion order. |
| `advertiser_id` | int | The unique identifier of the advertiser associated with this insertion order. |
| `start_date` | date | The start date for this insertion order. |
| `end_date` | date | The end date for this insertion order. |
| `timezone` | enum | The timezone that this insertion order is associated with. For a list of allowed values, see [API Timezones](api-timezones.md). |
| `last_modified` | date | The date at which this insertion order object was last updated. |
| `currency` | enum | The currency type associated with this insertion order. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Note:** For best results, set the currency on the parent insertion order. For more information, see [Insertion Order Service](insertion-order-service.md). |
| `budget_intervals` | array of objects | The metadata for the budget intervals from the associated insertion order. Budget intervals enable multiple date intervals to be attached to an insertion order, each with corresponding budget values. For more information, see [Insertion Order Service](insertion-order-service.md). |

### Valuation

The valuation object is used to set performance goals for line items with the `goal_type` of `"cpc"` or `"cpa"`. It contains the performance goal threshold, which determines the bid/no bid cutoff on optimized line items, and the performance goal target, which represents the desired clicks or conversions.

The `valuation` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `min_margin_pct` | decimal | Only set this field if you have set `prefer_delivery_over_performance` to `false` and `revenue_type` has not been set to `cost_plus_margin`. Set this to your desired minimum margin (e.g., `10` for 10%). This may cause your delivery and performance to be deprioritized.<br>**Default:** `null` |
| `goal_threshold` | decimal | The performance goal threshold determines bidding, inventory discovery, and the bid/no bid check on optimized line items. A value is required here when you are optimizing to a CTR or CPC goal, or a CPA goal for only post-click conversions.<br> - If you are optimizing to a CTR, enter the desired clickthrough rate (a value between 0 and 1).<br>If you are optimizing to a CPC goal, enter your CPC goal.<br> - If you are optimizing to a CPA goal for only post-click conversions, enter your CPC goal (**not** your CPA goal), and set the `post_click_goal_task` and `post_click_goal_threshold` fields in the `goal_pixels` array of objects.<br><br>**Note:**<br> - If you are optimizing to a CPA goal with both post-click and post-view conversions, see [Goal Pixels](#goal-pixels) below for required settings.<br>**Default:** `null` |
| `goal_target` | decimal | The performance goal target is a required value when you are optimizing to a CTR, CPC goal, CPA goal (for only post-click conversions), or Viewable CPM goal.<br> - If you are optimizing to a CTR, enter the desired clickthrough rate (a value between `0` and `1`).<br>- If you are optimizing to a CPC goal, enter your CPC goal.<br>- If you are optimizing to a CPA goal for only post-click conversions, enter your CPC goal (**not** your CPA goal), and set the `post_click_goal_target` and `post_click_goal_threshold` fields in the `goal_pixels` array of objects.<br>- If you are optimizing to a Viewable CPM, set this field to `null`. |
| `campaign_group_valuation_strategy` | enum | Determines whether a line item that has a CPA goal for both post-click and post-view conversions is optimized for retargeting or prospecting.<br> - Set to `"retargeting"` for a retargeting line item (a line item that aims to drive users who have already shown interest in the brand further down a conversion funnel). The line item profile must target at least one segment that is not in the data marketplace. Use the [Profile Service](profile-service.md) to set up segment targeting.<br>- Set to `"prospecting"` for a prospecting line item (a line item that aims to drive new users into a conversion funnel). |
| `min_avg_cpm` | double | The value below which the average CPM may not fall. If the `max_avg_cpm` field is also set, `min_avg_cpm` serves as a lower bound of a range. You must set this field if you set `revenue_type` to `"vcpm"` (Dynamic CPM) or `"cost_plus_margin"`. If you set `revenue_type` to `"cpm"`, you must set this field to `null`. |
| `max_avg_cpm` | double | The value above which the average CPM may not rise. If the `min_avg_cpm` field is also set, `max_avg_cpm` serves as a upper bound of a range. You must set this field if you set `revenue_type` to `"vcpm"` or `"cost_plus_margin"` If you set `revenue_type` to `"cpm"`, you must set this field to `null`.<br><br>If you have disabled optimization for Cost Plus (via the `goal_type` field), you must set a flat CPM for Cost Plus. Use this field to set the flat CPM value. |
| `min_margin_cpm` | double | Margin Value when Margin Type is CPM. <br><br>**Note:** The `min_margin_cpm` and `min_margin_pct` fields cannot both be set at the same time. If one is set, the other must be `null`. Xandr validates customer entitlements when clients use these fields.<br>**Default:** `null` |
| `min_margin_pct` | double | Margin Value when Margin Type is Percentage. <br><br>**Note:** The `min_margin_cpm` and `min_margin_pct` fields cannot both be set at the same time. If one is set, the other must be `null`. Xandr validates customer entitlements when clients use these fields.<br>**Default:** `null` |

### Auction event

The following fields are contained within the `auction_event` object.

> [!NOTE]
> Do not supply values for the fields within this object that end in `_code` or `_id`. Only supply values for the fields in the `auction_event` object that end in **`_type`** . The object will return the fields ending in `_code` and `_id`, but they will be ignored on `POST` and `PUT` calls.

| Field | Type | Description |
|:---|:---|:---|
| `revenue_auction_event_type` | string | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br> - `"impression"`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin.<br> - `"view"`: Use this value when your Revenue Type is Viewable CPM. Only measured viewable impressions will be counted, according to the Xandr viewability measurement, using the IAB definition.<br>- `"click"`: Use this value when your Revenue Type is CPC.<br>- `"video"`: Use this value when your Revenue Type is CPCV. |
| `revenue_auction_event_type_code` | string | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br>- `"impression"`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin.<br>- `"view_display_50pv1s_an"`: Use this value when your Revenue Type is Viewable CPM.<br>- `"click"`: Use this value when your Revenue Type is CPC.<br>- `"video_completion"`: Use this value when your Revenue Type is CPCV. |
| `revenue_auction_type_id` | int | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br>- `1`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin.<br>- `2`: Use this value when your Revenue Type is Viewable CPM.<br>- `3`: Use this value when your Revenue Type is CPC.<br> - `10`: Use this value when your Revenue Type is CPCV. |
| `kpi_auction_event_type` | string | This field is used in conjunction with the settings of the `goal_type` field. Options are:<br> - `"impression"`: Use this value when you are optmizing optimizing to CPC, CPA, CTR, or not using optimization.<br> - `"view"`: Use this value when you are optimizing to a Viewable CPM.<br>- `"click"`: Use this value when your Revenue Type is CPC.<br>- `"video"`: Use this value when you are optimizing to CPCV or VCR. |
| `kpi_auction_event_type_code` | string | This field is used in conjunction with the settings of the goal_type field. Options are:<br> - `"impression"`: Use this value when you are optmizing optimizing to CPC, CPA, CTR, or not using optimization.<br>- `"view_display_50pv1s_an"`: Use this value when you are optimizing to a Viewable CPM.<br>- `"video_completion"`: Use this value when you are optimizing to CPCV or VCR. |
| `kpi_auction_type_id` | int | This field is used in conjunction with the settings of the goal_type field. Options are:<br>- `1`: Use this value when you are optimizing to CPC, CPA , CTR, or not using optimization.<br>- `2`: Use this value when you are optimizing to a Viewable CPM.<br>- `10`: Use this value when your Revenue Type is CPCV or VCR. |
| `kpi_value` | double | This field is used in conjunction with the settings of the `goal_type` field. Set this to one of the following:<br>- `null`: If you are optimizing to CPC, CPA, CTR, or not using optimization.<br>- `your goal`: If you are optimizing to Viewable CPM goal (e.g., 5)., CPCV or VCR. VCR goals must be between `0` and `1`. |
| `kpi_value_type` | string | This field is used in conjunction with the settings of the `kpi_code` field. Set this to one of the following:<br>- `none`: If you are optimizing to CPC, CPA, CTR, or not using optimization.<br>- `goal_value`: If you are optimizing to a cost-based goal not covered above (CPCV).<br>- `rate_threshold`: If you are optimizing to a rate-based goal not covered above (VCR). |
| `payment_auction_event_type` | string | This field is only relevant if you have either set `inventory_type` to `"real_time"` (RTB) or set the rtb field in the `supply_strategies` object to `true`. Options are:<br>- `"impression"`: If you want to pay per impression.<br> - `"view"`: If you want to pay per view. This option is only allowed when you have set your `revenue_type` field to use either Viewable CPM or Cost Plus (and disabled optimization).<br>- `"click"`: Use this value when your Revenue Type is CPC.<br>- `"video"`: If you want to pay per video complete. |
| `payment_auction_event_type_code` | string | This field is only relevant if you have either set `inventory_type` to `"real_time"` (RTB) or set the rtb field in the `supply_strategies` object to `true`. Options are:<br>- `"impression"`: If you want to pay per impression.<br>- `"view_display_50pv1s_an"`: If you want to pay per view. This option is only allowed when you have set your `revenue_type` field to use either Viewable CPM or Cost Plus (and disabled optimization).<br>- `"video_completion"`: If you want to pay per video complete. |
| `payment_auction_type_id` | int | This field is only relevant if you have either set `inventory_type` to `"real_time"` (RTB) or set the rtb field in the `supply_strategies` object to `true`. Options are:<br>- `1`: If you want to pay per impression.<br>- `2`: If you want to pay per view. This option is only allowed when you have set your `revenue_type` field to use either Viewable CPM or Cost Plus (and disabled optimization).<br>- `10`: If you want to pay per video complete. |

### Budget scheduling settings

The following fields are contained within the `budget_scheduling_settings` object.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `underspend_catchup_type` | enum | Dictates how Xandr's system deals with an underdelivered daily budget. Use the `"evenly"` value if you'd like the unspent portions of your budget to be spent evenly throughout the rest of flight, or `"ASAP"` if you'd like the unspent budget to be spent as soon as possible.<br>Possible values: `"evenly"` or `"ASAP"`. |

### Demographic measuring

The `in_demo_measurement` object enables demographic measuring and its relevant specifications for your line item. The `in_demo_measurement` object is a part of the Nielsen Digital Ad Ratings (DAR) feature, which costs $0.25 CPM to use.

> [!NOTE]
> To utilize demographic measuring for connected TV (CTV), your line item must have a targeting configuration that exclusively targets within the United States.

#### An example of the `in_demo_measurement` object within a JSON response

```
"in_demo_measurement": {
    "campaign_group_id": 12795878,
    "provider": "nielsen-dar",
    "status": "active",
    "pixel": null,
    "attributes": [{
            "key": "on_target_goal_pct",
            "value": "50"
        },
        {
            "key": "target_gender",
            "value": "all"
        },
        {
            "key": "target_age_lower",
            "value": "13"
        },
        {
            "key": "target_age_upper",
            "value": "99"
        }
    ]
},
...
```

| Field | Type (Length) | Description |
|:---|:---|:---|
| `campaign_group_id` | int | This field is used to associate the `in_demo_measurement` object with this line item.<br>This field's value is your line item's ID.<br>**Read Only.** |
| `provider` | string | This field indicates which third-party provider is providing the demographic measuring service.<br>Currently, the only possible value for this field is `"nielsen-dar"`.<br>**Required.** |
| `status` | boolean | This field indicates whether or not the selected `provider` has acknowledged and begun demographic measuring for your line item. To activate demographic measurement, set this field to `"active"`. It can take up to 24 hours for a third-party measurement provider to begin tracking your line item's impressions, during which time this field's value is set to `"active-pending"`.<br>Possible values:<br> - `"active"`: Measurement has been activated for this line item, and Xandr has received an acknowledgment from a third-party measurement provider's API. Impressions are being measured.<br>- `"active-pending"`: Measurement has been activated for this line item, but impressions aren't being measured as the line item awaits confirmation from a third-party measurement provider’s API.<br>- `"inactive"`: Measurement isn't currently enabled for this line item.<br>- `"inactive-pending"`: This value is similar to `"inactive"`, but it indicates that your selected third-party measurement provider's API hasn't yet processed your line item's deactivation request. Once the third-party measurement provider has acknowledged your line item's measurement deactivation, this value changes to `"inactive"`.<br>**Required.** |
| `pixel` | array of objects | The default value for this field is `null`.<br>**Read Only.** |
| `attributes` | array of objects | The `attributes` array of objects is comprised of four [key-value objects](#attributes-objects) containing values to specify what demography your line item is measuring its targeting performance against.<br>For more information on the `attributes` array of key-value objects, see the [Demographic Attributes](#demographic-attributes) table below.<br>**Required.** |

#### `attributes` objects

```
"attributes":[
{
"key":"on_target_goal_pct",
"value":"50"
},
{
"key":"target_gender",
"value":"all"
},
{
"key":"target_age_lower",
"value":"13"
},
{
"key":"target_age_upper",
"value":"99"
}
]
```

### Demographic attributes

| Key | Type (Length) | Description |
|:---|:---|:---|
| `on_target_goal_pct` | double | Indicates how often you'd like your line item to deliver to your specified demography (such specification is done by inserting values for the keys below). This reference goal percentage is used in reporting and doesn't affect line item performance.<br>Possible values: `1` to `100`. |
| `target_gender` | string | Specifies the gender of the demography that you're trying to target.<br>Possible values: `"all"`, `"male"`, or `"female"`. |
| `target_age_lower` | int | Specifies the age threshold of the demographic age range that you're trying to target.<br>Possible values: `13`, `18`, `21`, `25`, `30`, `35`, `40`, `45`, `50`, `55`, `60`, or `65`. |
| `target_age_upper` | int | Specifies the age limit for the demographic age range that you're trying to target.<br>Possible values: `17`, `20`, `24`, `29`, `34`, `39`, `44`, `49`, `54`, `59`, `64`, or `99` (which represents ages `65+`). |

### Offline attribution

The `offline_attribution` object enables offline sales attribution for your line item. Offline sales attribution is a **Beta** feature provided by Nielsen Catalina Solutions (NCS), so you'll need to gain **Beta** testing access to this feature prior to using it. To gain access, contact your Xandr account representative.

> [!NOTE]
> To utilize offline sales attribution, your line item must have a targeting configuration that exclusively targets within the United States.

#### An example of the `offline_attribution` object within a JSON `PUT` request

```
$ cat line-item.json

{
    "line-item": {
        "id": 1,
        ...
        "offline_attribution": {
            "product_group_id": 123,
            "report_level_type": "line_item",
            "frequency_type": "weekly",
            "lookback_type": "flight_lifetime"
        }
    }
}

$ curl -b cookies -c cookies -X PUT -d @line-item.json "https://api.appnexus.com/line-item?id=ID_INTEGER&advertiser_id=ID_INTEGER"
```

#### An example of the `offline_attribution` object within a JSON response

```
{
    "line-item": {
        "id": 1,
        ...
        "offline_attribution": {
            "product_group_id": 123,
            "product_group": {
                "provider_member_name": "ncs",
                "category_name": "CATEGORY NAME",
                "brand_name": "BRAND NAME",
                "product_high_name": "PRODUCT HIGH NAME",
                "product_low_name": "PRODUCT LOW NAME",
            }
            "report_level_type": "line_item",
            "frequency_type": "weekly",
            "lookback_type": "flight_lifetime"
        }
    }
}
...
```

#### An example of the `offline_attribution` object being deleted within a JSON `PUT` request

```
$ cat line-item.json

{
    "line-item": {
        "id": 1,
        ...
        "offline_attribution": null
    }
}

$ curl -b cookies -c cookies -X PUT -d @line-item.json "https://api.appnexus.com/line-item?id=ID_INTEGER&advertiser_id=ID_INTEGER"
```

| Field | Type | Description |
|:---|:---|:---|
| `product_group_id` | int | The product group entry to report on. You can find a product group ID by using the [Offline Attribution Product Group Service](offline-attribution-product-group-service.md).<br>**Required.** |
| `offline_attribution_product_group` | object | An object that returns information on the product group you're tracking against (based on your `product_group_id` selection) such as its<br>- `provider_member_name`<br>- `category_name`<br>- `brand_name`<br>- `product_high_name`<br>- `product_low_name`<br><br>**Read Only.** |
| `report_level_type` | string | What you want to show sales attribution data for in your generated reports.<br>Potential values:<br>- `"line_item"`<br>- `"split"`<br><br>**Required.** |
| `frequency_type` | string | Pertains to when you'll start receiving offline sales attribution data reports for your line item and how often new reports will be made.<br>Potential values:<br>- `"weekly"`<br>- `"per_flight"`<br><br>**Required.** |
| `lookback_type` | string | Pertains to how much line item data is shown in each generated report (this field is also based on your `frequency_type` selection).<br>Potential values:<br>- `"flight_lifetime"`<br>- `"last_week"`<br><br>**Required.** |

### Creatives

Each object in the `creatives` array includes the following fields. To obtain information for `"id"` or `"code"` fields you can use the [Creative Service](creative-service.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `is_expired` | boolean | If `true`, the creative is expired. If `false`, the creative is active.<br>**Read Only.** |
| `is_prohibited` | boolean | If `true`, the creative falls into a prohibited category on the Xandr platform.<br>**Read Only.** |
| `width` | int | The width of the creative.<br>**Read Only.** |
| `audit_status` | enum | The audit status of the creative. <br>Possible values: `"no_audit"`, `"pending"`, `"rejected"`, `"audited"`, or `"unauditable"`.<br>**Read Only.** |
| `name` | string | The name of the creative.<br>**Read Only.** |
| `pop_window_maximize` | boolean | If `true`, the publisher's tag will maximize the window. Only relevant for creatives with format `"url-html"` and `"url-js"`. If `pop_window_maximize` is set to `true`, then neither `height` nor `width` should be set on the creative.<br>**Read Only.** |
| `height` | int | The height of the creative.<br>**Read Only.** |
| `state` | enum | The state of the creative. <br>Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `format` | enum | The format of the creative file.<br>Possible values: `"url-html"`, `"url-js"`, `"flash"`, `"image"`, `"raw-js"`, `"raw-html"`, `"iframe-html"`, or `"text"`.<br>**Read Only.** |
| `is_self_audited` | boolean | If `true`, the creative is self-audited.<br>**Read Only.** |
| `id` | int | The ID of the creative. Either `id` or `code` is required when updating creative association. |
| `code` | string | The custom code for the creative. Either `id` or `code` is required when updating creative association. |
| `weight` | int | A user-supplied weight that determines the creative rotation strategy for same-sized creatives managed at the line item level. To use this field, the value of `creative_distribution_type` must be `"weighted"`. <br>Allowed value: An integer greater than `0` and less than or equal to `1000`. |
| `ad_type` | string | The creative ad type. <br>Possible values: `"banner"`, `"video"`, `"native"`, `"audio"`.<br><br>**Note:** All creatives associated to a line item must have the same ad type, which should match the `ad_types` selected for the line item.<br>**Read Only.** |
| `all_budget_intervals` | boolean | Indicates whether the creative will serve during all budget intervals, including all future budget intervals. <br>Possible values are:<br>- `True` (the default)<br>- `False`<br><br>If `true`, `custom_date_ranges` in the `creatives` array and `creatives` in the `budget_intervals` array must be set to `null`. Conversely, if you want to use custom date ranges and/or creatives, `all_budget_intervals` must be set to `false`. |
| `custom_date_ranges` | array of objects | The date ranges setting the periods when the creative will serve.<br><br>If specified:<br>`all_budget_intervals` must be set to `false`.<br>For more information, see [Custom Date Ranges](#custom-date-ranges) below. |

### Custom date ranges

The `custom_date_ranges` array sets the date ranges during which a creative will serve.

Dates must be in the format `YYYY-MM-DD hh:mm:ss`.

The date ranges must all meet the following specifications:

- They cannot include any dates before the start or after the end of any budget intervals defined for this line item.
- Date ranges must be at least an hour long.
- End dates cannot be later than `2038-01-19 00:00:00`.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `start_date` | timestamp | The start date of the custom date range. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be hh:00:00). |
| `end_date` | timestamp | The end date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be set to hh:59:59). |

#### Schedule a creative to serve during a custom budget interval

```
$cat line-item-with-custom-budget-intervals
{
    line_item: {
        budget_intervals: [
            {
                start_date: 1/1/2020,
                end_date: 2/1/2020,
                lifetime_budget: 1000,
                id: 7777,                                  
                creatives: [12345]                          
            },
            {
                start_date: 2/1/2020,
                end_date: 3/1/2020,
                lifetime_budget: 2000,
                id: 8888,                                  
                creatives: null
            }
        ],
        creatives: [
            {
                id: 12345,
                weight: 1,
                all_budget_intervals: false,                
                custom_date_ranges: [
                    {                                      
                        start_date: 2/5/2020 00:00:00,      
                        end_date: 2/10/2020 00:00:00                     
                    }
                ]
            },
            {
                id: 56789,
                weight: 2,
                all_budget_intervals: true,                 
                custom_date_ranges: null                                                   
            }
        ],
        creative_distribution_type: weighted
    }
}
```

### Budget intervals

Budget intervals on an augmented line item must fall within the budget intervals defined on the line item's parent insertion order(s). Budget intervals on line items should have budgets distinct from those of the parent insertion order(s). These function as line item-specific "sub-budgets" of the budget on the corresponding insertion order budget interval.

When creating a new augmented line item, ensure that the `start_date` and `end_date` of each of its `budget_intervals` array objects fall within one of the budget intervals defined on the parent insertion order (insertion orders are associated with line items via the `insertion_orders` array in the Line Item Service).

> [!NOTE]
> The `parent_interval_id` (in the `budget_intervals` array) has been deprecated and its value will be ignored.

Also consider the following when using the `budget_interval` array:

- Budget intervals on the same line item cannot overlap.
- Budget intervals on the line item can have unlimited lifetime budgets (i.e., if all budget fields are left set to `null`).
- Budget intervals cannot be used if budget fields on the top-most level of the `line_item` object (as described in the **General** section of this page) itself are set.
- If you are increasing the budget for the line item's budget interval, you must first increase the budget for the budget interval on the parent insertion order (otherwise you may not have sufficient budget). For more information, see [Insertion Order Service](insertion-order-service.md).
- For optimization to work best, your budget intervals should have a duration of at least 4 hours.

> [!NOTE]
>
> - If line item's parent insertion order's `budget_type` field is set to **`impression`** :
>   - The `lifetime_budget` and `daily_budget` fields in this array must be set to `null.`
>   - Use either the `lifetime_budget_imps` or `daily_budget_imps` field in this array to set your line item's budget.
>
> - If the line item's parent insertion order's `budget_type` field is set to **`revenue`** :
>   - The `lifetime_budget_imps` and `daily_budget_imps` fields in this array must be set to `null.`
>   - Use either the `lifetime_budget` or `daily_budget` field in this array to set your line item's budget.

Each object in the `budget_intervals` array contains the following fields.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the budget interval. |
| `start_date` | timestamp | The start date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be hh:00:00). |
| `end_date` | timestamp | The end date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be set to hh:59:59). For optimization to work best, your budget intervals should have a duration of at least 4 hours. If this field is set to `null`, then the line item's budget interval will run indefinitely. If you set this field to `'null'`:<br>- There may not be more than one object in the `budget_intervals` array (i.e., maximum of 1 budget interval).<br>- The `lifetime_pacing` field must set to `"false"`.<br>- The `"lifetime_budget"` must be set to `null` and the `"daily_budget"` field must be set to a non-null or non-0 value. |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). |
| `parent_interval_id` | int | **Deprecated.** The value of this field will be ignored. Instead, use the `start_date` and `end_date` fields of this array to define when the line item should run. |
| `lifetime_budget` | double | The lifetime budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object.<br><br>**Note:**<br>If you also set the `lifetime_budget_imps` field in this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_budget_imps` | double | The lifetime budget in impressions for the budget interval. <br><br>**Note:** If you add line items to this insertion order, any spend already associated with those line items before they are added to the insertion order is NOT counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted.<br><br>**Note:**<br>If you also set the `lifetime_budget` field in this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to pace the lifetime budget evenly over the budget interval. If `true`, you must set `lifetime_budget` or `lifetime_budget_imps`. |
| `daily_budget` | double | The daily budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object. <br><br>**Note:** If you add line items to this insertion order, any impressions associated to those line items when they are added to the insertion order are NOT counted under the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order are counted.<br><br>**Note:**<br>If you also set the `daily_budget_imps` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `daily_budget_imps` | double | The daily budget in impressions.<br><br>**Note:**<br>If the parent insertion order's `budget_type` field has been set to `"impression"` *and* the line items `revenue_type` field has been set to Viewable CPM, only the viewable impressions count against both line item and insertion order budgets.<br><br>If you also set the `daily_budget` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `enable_pacing` | boolean | If `true`, then spending will be paced over the course of the day. Only applicable if there is a `daily_budget`. |
| `creatives` | array | Specifies the creatives associated with this budget interval. In order to serve, creatives must also be specified in the line item `creatives` field and `all_budget_intervals` must be `false`. |

#### Delete a budget interval

> [!NOTE]
> You may remove budget intervals from an augmented line item. However, if you want to remove a budget interval from the parent insertion order, you must first remove any budget intervals (that fall within the parent insertion order's budget interval) from all augmented line items associated with the insertion order. Only then can you remove the budget interval from the insertion order. For more details, see [Insertion Order Service](insertion-order-service.md).

```
$ cat delete-budget-interval
{
  "line-item": {
    "budget_intervals": [
      {
        "id": 79970,
        "start_date": null,
        "end_date": null
      }
    ]
  }
}
```

#### Create a subflight

```
$ cat create-subflight

{
  "line-item": {
    ...,
    "budget_intervals": [
      {
        "id": 342856,
        "lifetime_pacing_percent": 150,
        "lifetime_budget": 10000,
        "lifetime_budget_imps": null,
        "start_date": "2022-04-01 00:00:00",
        "end_date": "2022-04-30 11:59:59",
        ...,
        "subflights": [
          {
            "id": 1, // ID generated on LI creation or update
            "name": "spend 200 every weekend for entire flight",
            "is_recurring": true,
            "use_flight_date_range": true,
            "recurring_day_of_week": [0,1,6],
            "start_date": null,
            "end_date": null,
            "daily_budget": 80,
            "daily_budget_imps": null,
            "subflight_pacing_percent": null,
          }
        ]
      }
    ],
    ...
  }
}
```

#### Delete a subflight

```
$ cat delete-subflight

{
  "line-item": {
    ...,
    "budget_intervals": [
      {
        "id": 342856,
        "subflights": [
          {
            "id": 1,
            "use_flight_date_range": false,
            "start_date": null,
            "end_date": null,
          }
        ]
      }
    ],
    ...
  }
}
```

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The subflight ID generated upon creating a new subflight.<br>**Read Only.** |
| `name` | string | The name given to the subflight.<br>**Required.** |
| `is_recurring` | boolean | Determines if the subflight is to be recurring. Having a recurring subflight means that you can select certain days of the week for which your subflight will take effect, whereas a standard subflight operates constantly under its start and end dates.<br>**Possible Values:**<br>- `true`: Recurring subflight.<br>- `false`: **(default value)** Standard subflight.<br>**Required.** |
| `recurring_day_of_week` | array of integers | Determines which days of the week your recurring subflight will take effect. Select either a single day or up to six consecutive days.<br>**Possible Values:**<br> - `0` (Sunday)<br> - `1` (Monday)<br> - `2` (Tuesday)<br> - `3` (Wednesday)<br> - `4` (Thursday)<br> - `5` (Friday)<br> - `6` (Saturday)<br><br>**Saturday-Monday Example:** `"recurring_day_of_week"`: `[0, 1, 6]`.<br><br>**Required if** `is_recurring` **equals** `true`. |
| `use_flight_date_range` | boolean | Determines whether the subflight uses its parent flight’s date range or its own date range, as determined by the subflight’s `start_date` and `end_date` selections.<br>**Possible Values:**<br> - `true`: The subflight will use its parent flight’s date range.<br>- `false`: The subflight will use its own start and end date.<br><br>**Note:**<br>If you set `is_recurring` to `false`, then you must also set `use_flight_date_range` to `false`.<br>**Required.** |
| `start_date` | date (yyyy-mm-dd) | The subflight’s start date (relative to your line item’s designated time zone). Your start date selection must match or start later than the start date selected for the subflight’s budget interval.<br><br>**Note:**<br>If `use_flight_date_range` is set to `true`, this field's value must be set to `null`.<br><br>**Required if** `is_recurring` **equals** `false`. |
| `end_date` | date (yyyy-mm-dd) | The subflight’s end date (relative to your line item’s designated time zone). Your end date selection must match or end earlier than the end date selected for the subflight’s budget interval.<br><br>**Note:**<br>If `use_flight_date_range` is set to `true`, this field's value must be set to `null` .<br><br>**Required if** `is_recurring` **equals** `false`. |
| `daily_budget` | int | Determines how much money you want your subflight to be able to spend daily. To make a selection for this field, you must set the parent flight’s `lifetime_pacing_percent` field selection to `null`.<br><br>**Note:**<br>If your line item is underspending while utilizing subflights with daily budgets, underspend catch-up settings will take effect on the next non-subflight date.<br><br>**Required if** `daily_budget` **isn't provided for the parent flight.** |
| `daily_budget_imps` | double | The daily number of impressions that the subflight is allowed to win.<br><br>**Note:**<br>If your line item is underspending while utilizing subflights with daily budgets, underspend catch-up settings will take effect on the next non-subflight date.<br><br>**Required if**:<br>- **The parent flight's** `daily_budget` **equals** `true` **and the subflight's** `daily_budget` **equals** `null`.<br>- **The parent flight's** `lifetime_pacing_percent` **equals** `null`. |
| `subflight_pacing_percent` | double | Determines how evenly the subflight's budget is distributed between its start and end date.<br><br>If set to `100`, the subflight's budget pacing is unaltered and distributed over every applicable day for the subflight, with roughly similar budget amounts being spent daily. If set higher than `100`, the subflight spends more per day at the beginning of its date range and less at the end. The reverse occurs if the pacing is lower than `100`.<br>**Possible Values:** `50`-`150`<br><br>**Required if** `daily_budget` **isn't provided.** |

### Goal pixels

The `goal_pixels` array of objects is used when working with `goal_type` `"cpa"` and contains information about performance goal targets and thresholds. Each object in the `goal_pixels` array of objects includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the conversion pixel. |
| `state` | enum | The state of the pixel. Possible values: `"active"` or `"inactive"`. |
| `post_click_goal` | double | **Deprecated.** Use `post_click_goal_target` and `post_click_goal_threshold` instead. |
| `post_view_goal` | double | **Deprecated.** Use `post_view_goal_target` and `post_view_goal_threshold` instead. |
| `trigger_type` | enum | The type of event required for an attributed conversion. Possible values: `"view"`, `"click"`, or `"hybrid"`.<br>**Read Only.** |
| `post_click_goal_target` | double | The advertiser goal value for post-click conversions for the pixel. If you want to set a CPA goal and optimize to only post-click conversions, set this field to your CPA goal value. |
| `post_view_goal_target` | double | The advertiser goal value for post-view conversions for the pixel (comparable to `goal_value` for `goal_type` `"cpc"`). If you want to set a CPA goal and optimize only to post-view conversions, ensure this field is set to `null`. |
| `post_click_goal_threshold` | double | The advertiser goal threshold for post-click conversions for the pixel. This determines the bid/no bid cutoff on optimized line items. If you want to set a CPA goal and optimize to both post-click and post-view conversions, this field must contain the same value as `post_view_goal_threshold`. |
| `post_view_goal_threshold` | double | The advertiser goal threshold for post-view conversions for the pixel. This determines the bid/no bid cutoff on optimized line items. If you want to set a CPA goal and optimize to both post-click and post-view conversions, this field must contain the same value as `post_click_goal_threshold`. |

### Stats

> [!NOTE]
> The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

### First run/last run

To include the `first_run` and `last_run` fields in a `GET` response, pass `flight_info=true` in the query string. You can also filter for line items based on when they first and last served, as follows:

#### Retrieve only line items that have never served

Pass `never_run=true` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&never_run=true'
```

> [!NOTE]
> You can use `never_run=true` in combination with other filters, but note that it will always be an OR relationship. For example, if you pass both `never_run=true` and `min_first_run=2012-01-01 00:00:00` in the query string, you will be looking for line items that have never served OR line items that first served on or after 2012-01-01.

#### Retrieve only line items that first served on or after a specific date

Pass `min_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00'
```

#### Retrieve only line items that first served on or before a specific date

Pass `max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&max_first_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that first served within a specific date range

Pass `min_first_run=YYYY-MM-DD HH:MM:SS&max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00&max_first_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that last served on or after a specific date

Pass `min_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00'
```

#### Retrieve only line items that last served on or before a specific date

Pass `max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&max_last_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that last served within a specific date range

Pass `min_last_run=YYYY-MM-DD HH:MM:SS&max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00&max_last_run=2012-08-01 00:00:00'
```

Fields of the type date can be filtered by `nmin` and `nmax` as well. The `nmin` filter lets you find dates that are either `null` or after the specified date, and the `nmax` filter lets you find dates that are either `null` or before the specified date.

### Alerts

This field notifies you of conditions that are preventing the line item from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional.

To retrieve line items based on pauses, you must pass certain query string parameters in the `GET` request. See below for use cases with query string parameters and examples.

> [!NOTE]
> You can use these query string parameters both when retrieving all line items or specific line items, but the examples below only cover retrieving all line items, as that is where this feature offers the most value.

#### Retrieve all line items and show alerts

Pass `show_alerts=true` in the query string. This parameter will add the `alerts` object to every line item in the response, whether or not the line item has pauses.

> [!NOTE]
> For each of the use cases below, you must pass `show_alerts=true` if you want the `alerts` object to show up in the response.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?show_alerts=true'

{
    "response": {
        "status": "OK",
        "line-items": [

            {
                "id": 45047,
                "code": null,
                "name": "Line Item 1",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-04-01 00:00:00",
                "end_date": "2012-05-01 00:00:00",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight end date is in the past."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 45048,
                "code": null,
                "name": "Line Item 2",
                "advertiser_id": 35081,
                "state": "inactive",
                "start_date": "2012-05-21 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 46308,
                "code": null,
                "name": "Test Line Item",
                "advertiser_id": 45278,
                "state": "inactive",
                "start_date": "2012-06-06 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only line items that have at least one pause

Pass `show_alerts=true&pauses=true` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?show_alerts=true&pauses=true'

{
    "response": {
        "status": "OK",
        "line-items": [
            {
                "id": 45047,
                "code": null,
                "name": "Line Item 1",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-04-01 00:00:00",
                "end_date": "2012-05-01 00:00:00",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight end date is in the past."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 45048,
                "code": null,
                "name": "Line Item 2",
                "advertiser_id": 35081,
                "state": "inactive",
                "start_date": "2012-05-21 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 46308,
                "code": null,
                "name": "Line Item 6",
                "advertiser_id": 45278,
                "state": "inactive",
                "start_date": "2012-06-06 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only line items that have no pauses

Pass `show_alerts=true&pauses=false` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?show_alerts=true&pauses=false'

{
    "response": {
        "status": "OK",
        "line-items": [
            {
                "id": 45054,
                "code": null,
                "name": "Line Item 7",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-04-01 00:00:00",
                "end_date": "2012-05-01 00:00:00",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 45057,
                "code": null,
                "name": "Line Item 9",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-05-21 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 46345,
                "code": null,
                "name": "Line Item 12",
                "advertiser_id": 45278,
                "state": "active",
                "start_date": "2012-06-06 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only line items that have a specific pause

Pass `show_alerts=true&pauses=PAUSE_ID` in the query string. For pause IDs, see the [Pauses](#pauses) table below.

In this example, we use pause ID 2 to retrieve all line items with flight start dates that are in the future.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?show_alerts=true&pauses=2'

{
    "response": {
        "status": "OK",
        "line-items": [
            {
                "id": 45047,
                "code": null,
                "name": "Line Item 5",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-11-01 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 2,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 45048,
                "code": null,
                "name": "Line Item 7",
                "advertiser_id": 35081,
                "state": "active",
                "start_date": "2012-10-15 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 2,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },

            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only line items that have two or more specific pauses

Pass `show_alerts=true&pauses=SUM_OF_PAUSE_IDS` in the query string. For pause IDs, see the [Pauses](#pauses) table below.

In this example, we add together pause ID `1` and pause ID `2` to retrieve all line items that are set to inactive and have a flight state date in the future.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?show_alerts=true&pauses=3'

{
    "response": {
        "status": "OK",
        "line-items": [
            {
                "id": 45047,
                "code": null,
                "name": "Line Item 3",
                "advertiser_id": 35081,
                "state": "inactive",
                "start_date": "2012-11-01 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 2,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },
            {
                "id": 45048,
                "code": null,
                "name": "Line Item 7",
                "advertiser_id": 35081,
                "state": "inactive",
                "start_date": "2012-10-15 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 2,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": null,
                    "pauses_last_checked": "2012-07-27 19:01:07"
                }
            },

            ...
        ],
        ...
        }
    }
}
```

### Pauses

| ID | Description |
|:---|:---|
| `1` | State is set to inactive. |
| `2` | Flight start is in the future. |
| `4` | Flight end is in the past. |

## Examples

### Update a line item to use a CPC performance goal

In this example, we'll update a line item to use a CPC performance goal. We're setting a cost-per-click goal threshold of $3.

```
$ cat line-item
{
    "line-item": {
    "name": "Weekday French Speakers Q3 2012",
    "state": "inactive",
    "comments": "The name says it all -- that's who we're trying to advertise to",
    "daily_budget": null,
    "revenue_type": "cpm",
    "goal_type": "cpc",
    "valuation": {
        "goal_target":3,
        "goal_threshold":3
    }
    "lifetime_budget": null,
    "end_date": null,
    "enable_pacing": null,
    "allow_safety_pacing": null,
    "publishers_allowed": "all"
    }
}
```

```
curl -b cookies -c cookies -X PUT -d @line-item "https://api.appnexus.com/line-item?id=152083&advertiser_id=51"
```

### Update a line item to use both a CPC and CPA performance goal

In this example, we'll update a line item to use both a CPC and CPA performance goal. We're setting the CPC goal of $5 and the CPA goal to $10.

```
$ cat line-item
{
    "line-item": {
    "name": "Weekday French Speakers Q3 2012",
    "state": "inactive",
    "comments": "The name says it all -- that's who we're trying to advertise to",
    "daily_budget": null,
    "revenue_type": "cpm",
    "goal_type": "cpa",
    "pixels": [
        {
        "id": "123456"
        }
    ],
    "goal_pixels":[
        {
        "id":"123456",
        "post_click_goal_threshold":10,
        "post_click_goal_target":10
        }
    ],
    “valuation”: {
        “goal_target”: 5,
        “goal_threshold”: 5
        }
    }
}
```

```
curl -b cookies -X PUT -d @line-item "https://api.appnexus.com/line-item?id=152083&advertiser_id=51"
```

### View a line item

To view a specific line item, we must pass in the line item and advertiser IDs via the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?id=4979347&advertiser_id=1887392'
{
    "response": {
        "count": 1,
        "dbg_info": {
            "output_term": "line-item",
            "version": "1.18.227",
            "warnings": []
        },
        "line-item": {
            "ad_types": [
                "banner"
            ],
            "advertiser": {
                "id": 1887392,
                "name": "ALI Closed Beta Demo Advertiser"
            },
            "advertiser_id": 1887392,
            "allow_safety_pacing": null,
            "auction_event": null,
            "bid_object_type": "creative",
            "broker_fees": null,
            "budget_intervals": [
                {
                    "code": null,
                    "enable_pacing": true,
                    "end_date": "2017-12-02 23:59:59",
                    "id": 2509919,
                    "lifetime_budget": 1,
                    "lifetime_budget_imps": null,
                    "lifetime_pacing": true,
                    "lifetime_pacing_pct": 100,
                    "object_id": 4979347,
                    "object_type": "campaign_group",
                    "parent_interval_id": null,
                    "start_date": "2017-11-30 00:00:00",
                    "timezone": "US/Eastern"
                }
            ],
            "budget_set_per_flight": true,
            "campaigns": null,
            "click_url": null,
            "clicktrackers": null,
            "code": null,
            "comments": null,
            "creative_distribution_type": null,
            "creatives": null,
            "currency": "USD",
            "custom_models": [
                {
                    "active": "1",
                    "id": 477441,
                    "name": "cadence 2017-11-07 18:03:37.738",
                    "type": "cadence"
                }
            ],
            "custom_optimization_note": null,
            "daily_budget": null,
            "daily_budget_imps": null,
            "deals": null,
            "delivery_goal": null,
            "discrepancy_pct": 0,
            "enable_pacing": null,
            "enable_v8": false,
            "end_date": null,
            "goal_pixels": [
                {
                    "id": 932952,
                    "name": "Test Pixel",
                    "post_click_goal": null,
                    "post_click_goal_confidence_threshold": null,
                    "post_click_goal_target": 10,
                    "post_click_goal_threshold": 10,
                    "post_click_model_id": null,
                    "post_view_goal": null,
                    "post_view_goal_confidence_threshold": null,
                    "post_view_goal_target": null,
                    "post_view_goal_threshold": null,
                    "post_view_model_id": null,
                    "state": "active",
                    "trigger_type": "hybrid"
                }
            ],
            "goal_type": "cpc",
            "goal_value": null,
            "id": 4979347,
            "imptrackers": null,
            "incrementality": null,
            "insertion_orders": [
                {
                    "advertiser_id": 1887392,
                    "budget_intervals": [
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": null,
                            "id": 2509856,
                            "lifetime_budget": 1,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 676605,
                            "object_type": "insertion_order",
                            "start_date": "2017-11-30 00:00:00",
                            "timezone": "US/Eastern"
                        }
                    ],
                    "code": null,
                    "currency": "USD",
                    "end_date": null,
                    "id": 676605,
                    "last_modified": "2017-12-01 02:44:34",
                    "name": "Swetha_Seamless_IO",
                    "start_date": null,
                    "state": "active",
                    "timezone": "US/Eastern"
                }
            ],
            "inventory_discovery": {
                "fail_criteria_amount": 9.486486,
                "fail_criteria_type": "booked_revenue",
                "use_ranked_discovery": true
            },
            "inventory_discovery_budget": null,
            "inventory_type": "real_time",
            "labels": null,
            "last_modified": "2017-12-02 05:30:29",
            "lifetime_budget": null,
            "lifetime_budget_imps": null,
            "lifetime_pacing": null,
            "lifetime_pacing_pct": null,
            "lifetime_pacing_span": null,
            "line_item_type": "standard_v2",
            "manage_creative": true,
            "member_id": 1370,
            "name": "Swetha_ALI_Basic_API1",
            "pixels": [
                {
                    "id": 932952,
                    "name": "Test Pixel",
                    "post_click_revenue": null,
                    "post_view_revenue": null,
                    "state": "active",
                    "trigger_type": "hybrid"
                }
            ],
            "prefer_delivery_over_performance": false,
            "priority": "5",
            "profile_id": 96266622,
            "publishers_allowed": "all",
            "remaining_days": null,
            "require_cookie_for_tracking": true,
            "revenue_type": "vcpm",
            "revenue_value": null,
            "roadblock": null,
            "start_date": null,
            "state": "active",
            "timezone": "US/Eastern",
            "total_days": null,
            "valuation": {
                "bid_price_pacing_enabled": false,
                "bid_price_pacing_lever": 0,
                "goal_confidence_threshold": null,
                "goal_target": 5,
                "goal_threshold": 5,
                "max_avg_cpm": 3,
                "max_revenue_value": null,
                "min_avg_cpm": 2,
                "min_margin_pct": null,
                "min_revenue_value": null,
                "no_revenue_log": false
            }
        },
        "num_elements": 100,
        "start_element": 0,
        "status": "OK"
    }
}
```

### View all of an advertiser's line items

Unlike the examples above, this line item has a `goal_pixels` array of objects attached. Notice that even though this advertiser has only one line item, it's returned via the `line-items` JSON array.

```
$ curl -b cookies 'https://api.appnexus.com/line-item?advertiser_id=51'
{
    "response": {
        "count": 3,
        "line-items": [
            { ..."id": 4274691,...},
            { ..."id": 4983291,...},
            { ..."id": 4983258,...}
        ]
    }
}
```

### Create a line item with a CPM revenue type, optimized to a CPA goal (post-click and post-view conversions)

```
cat li_cpa.json

{
    "line-item": {
    "name": "LI CPA Test",
    "state": "inactive",
    "daily_budget": null,
    "revenue_type": "cpm",
    "goal_type": "cpa",
    "goal_pixels": [
        {
            "id": 987654321,
            "name": "Confirmation Page",
            "post_click_goal": null,
            "post_click_goal_confidence_threshold": null,
            "post_click_goal_target": 1,
            "post_click_goal_threshold": 1,
            "post_click_model_id": null,
            "post_view_goal": null,
            "post_view_goal_confidence_threshold": null,
            "post_view_goal_target": 1,
            "post_view_goal_threshold": 1,
            "post_view_model_id": null,
            "state": "active",
            "trigger_type": "hybrid"
                }
            ], 
    "valuation": {
        "bid_price_pacing_enabled": false,
        "bid_price_pacing_lever": 0,
        "campaign_group_valuation_strategy": "retargeting",
        "goal_confidence_threshold": null,
        "goal_target": null,
        "goal_threshold": null,
        "max_avg_cpm": null,
        "max_revenue_value": null,
        "min_avg_cpm": null,
        "min_margin_pct": null,
        "min_revenue_value": null,
        "no_revenue_log": false
            },
}

$curl -b cookies -X POST -d @li_cpa.json 'https://api.appnexus.com/line-item?advertiser_id=12345'
{
    "response": {
        "count": 1,
        "dbg_info": {
            "output_term": "line-item",
            "version": "1.18.1023",
            "warnings": []
        },
        "line-item": {
            "ad_types": [
                "banner"
            ],
            "advertiser": {
                "id": 12345,
                "name": "Console Challenge (Please Do Not Modify)"
            },
            "advertiser_id": 12345,
            "allow_safety_pacing": null,
            "archived_on": null,
            "auction_event": {
                "kpi_auction_event_type": "impression",
                "kpi_auction_event_type_code": "impression",
                "kpi_auction_type_id": 1,
                "kpi_value": null,
                "payment_auction_event_type": "impression",
                "payment_auction_event_type_code": "impression",
                "payment_auction_type_id": 1,
                "revenue_auction_event_type": "impression",
                "revenue_auction_event_type_code": "impression",
                "revenue_auction_type_id": 1
            },
            "bid_object_type": "creative",
            "broker_fees": null,
            "budget_intervals": [
                {
                    "code": null,
                    "enable_pacing": true,
                    "end_date": "2019-02-11 23:59:59",
                    "id": 3886503,
                    "lifetime_budget": 0.01,
                    "lifetime_budget_imps": null,
                    "lifetime_pacing": true,
                    "lifetime_pacing_pct": 100,
                    "object_id": 7358523,
                    "object_type": "campaign_group",
                    "parent_interval_id": null,
                    "start_date": "2019-02-10 00:00:00",
                    "timezone": "US/Eastern"
                }
            ],
            "budget_set_per_flight": false,
            "campaigns": null,
            "click_url": null,
            "clicktrackers": null,
            "code": null,
            "comments": null,
            "creative_distribution_type": "ctr-optimized",
            "creatives": null,
            "currency": "USD",
            "custom_models": [
                {
                    "active": "1",
                    "experiment": "control",
                    "id": 222333,
                    "name": "Test 001",
                    "origin": "optimization",
                    "type": "conv_imp"
                },
                {
                    "active": "1",
                    "experiment": "control",
                    "id": 222334,
                    "name": "Test 002",
                    "origin": "optimization",
                    "type": "cadence"
                },
                {
                    "active": "1",
                    "experiment": "control",
                    "id": 222335,
                    "name": "Budget Splitter - 7358523 - Mon Feb 11 2019 04:08:49 GMT+0000",
                    "origin": "splitters",
                    "type": "budget_splitter"
                }
            ],
            "custom_optimization_note": null,
            "daily_budget": null,
            "daily_budget_imps": null,
            "deals": null,
            "delivery_goal": null,
            "discrepancy_pct": 0,
            "enable_pacing": null,
            "enable_v8": false,
            "end_date": null,
            "flat_fee": null,
            "flat_fee_type": null,
            "goal_pixels": [
                {
                    "id": 987654321,
                    "name": "Confirmation Page",
                    "post_click_goal": null,
                    "post_click_goal_confidence_threshold": null,
                    "post_click_goal_target": 1,
                    "post_click_goal_threshold": 1,
                    "post_click_model_id": null,
                    "post_view_goal": null,
                    "post_view_goal_confidence_threshold": null,
                    "post_view_goal_target": 1,
                    "post_view_goal_threshold": 1,
                    "post_view_model_id": null,
                    "state": "active",
                    "trigger_type": "hybrid"
                }
            ],
            "goal_type": "cpa",
            "goal_value": null,
            "id": 87654321,
            "imptrackers": null,
            "incrementality": null,
            "insertion_orders": [
                {
                    "advertiser_id": 12345,
                    "budget_intervals": [
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2018-05-31 23:59:59",
                            "id": 2957582,
                            "lifetime_budget": 100,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2018-05-23 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2018-09-24 23:59:59",
                            "id": 3331427,
                            "lifetime_budget": 100,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2018-09-23 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2018-11-30 23:59:59",
                            "id": 3494586,
                            "lifetime_budget": 600,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2018-10-31 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2018-12-12 23:59:59",
                            "id": 3636004,
                            "lifetime_budget": 300,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2018-12-07 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2019-01-14 23:59:59",
                            "id": 3746556,
                            "lifetime_budget": 400,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2019-01-07 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2019-01-22 23:59:59",
                            "id": 3773032,
                            "lifetime_budget": 0.01,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2019-01-15 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2019-02-06 23:59:59",
                            "id": 3857762,
                            "lifetime_budget": 0.01,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2019-02-04 00:00:00",
                            "timezone": "US/Eastern"
                        },
                        {
                            "code": null,
                            "daily_budget": null,
                            "daily_budget_imps": null,
                            "enable_pacing": false,
                            "end_date": "2019-02-28 23:59:59",
                            "id": 3886493,
                            "lifetime_budget": 600,
                            "lifetime_budget_imps": null,
                            "lifetime_pacing": false,
                            "object_id": 811332,
                            "object_type": "insertion_order",
                            "start_date": "2019-02-10 00:00:00",
                            "timezone": "US/Eastern"
                        }
                    ],
                    "code": null,
                    "currency": "USD",
                    "end_date": null,
                    "id": 811332,
                    "last_modified": "2019-02-25 15:36:24",
                    "name": "Natasha Test IO",
                    "start_date": null,
                    "state": "active",
                    "timezone": "US/Eastern"
                }
            ],
            "inventory_discovery": null,
            "inventory_type": "both",
            "is_archived": false,
            "labels": null,
            "last_modified": "2019-03-01 21:12:45",
            "lifetime_budget": null,
            "lifetime_budget_imps": null,
            "lifetime_pacing": null,
            "lifetime_pacing_pct": null,
            "lifetime_pacing_span": null,
            "line_item_type": "standard_v2",
            "manage_creative": true,
            "member_id": 1370,
            "name": "Copy test2_01_17",
            "pixels": [
                {
                    "id": 1017110,
                    "name": "Confirmation Page",
                    "post_click_revenue": null,
                    "post_view_revenue": null,
                    "state": "active",
                    "trigger_type": "hybrid"
                }
            ],
            "prefer_delivery_over_performance": false,
            "priority": "5",
            "profile_id": 109625231,
            "publishers_allowed": "all",
            "remaining_days": null,
            "require_cookie_for_tracking": true,
            "revenue_type": "cpm",
            "revenue_value": 1,
            "roadblock": null,
            "start_date": null,
            "state": "inactive",
            "supply_strategies": {
                "deals": false,
                "managed": false,
                "rtb": true
            },
            "timezone": "US/Eastern",
            "total_days": null,
            "user_info": {
                "creator_id": 17707,
                "owner_id": 17707
            },
            "valuation": {
                "bid_price_pacing_enabled": false,
                "bid_price_pacing_lever": 0,
                "campaign_group_valuation_strategy": "retargeting",
                "goal_confidence_threshold": null,
                "goal_target": null,
                "goal_threshold": null,
                "max_avg_cpm": null,
                "max_revenue_value": null,
                "min_avg_cpm": null,
                "min_margin_pct": null,
                "min_revenue_value": null,
                "no_revenue_log": false
            },
            "viewability_vendor": "appnexus"
        },
        "num_elements": 100,
        "start_element": 0,
        "status": "OK"
    }
}
```

### Create a line item with a revenue type of Dynamic CPM and optimized to a CPC goal

In this example, we set the CPC goal to $5 and minimum average CPM to $2 and maximum average CPM to $3.

```
{code}$ cat line_item_dcp_cpc
{
  "line-item": {
    "ad_types": [
      "banner"
     ],
    "advertiser": {
      "id": 1887392,
      "name": "ALI Closed Beta Demo Advertiser"
     },
    "currency": "USD",
    "insertion_orders": [{
      "advertiser_id": 1887392,
      "budget_intervals": [{
            "code": null,
            "daily_budget": null,
            "daily_budget_imps": null,
            "enable_pacing": false,
            "end_date": null,
            "id": 2509856,
            "lifetime_budget": 1,
            "lifetime_budget_imps": null,
            "lifetime_pacing": false,
            "object_id": 676605,
            "object_type": "insertion_order",
            "start_date": "2017-11-30 00:00:00",
            "timezone": "US/Eastern"
        }],
        "code": null,
        "currency": "USD",
        "end_date": null,
        "id": 676605,
        "last_modified": "2017-12-01 02:44:34",
        "name": "Swetha_Seamless_IO",
        "start_date": null,
        "state": "active",
        "timezone": "US/Eastern"
    }],
    "advertiser_id": 1887392,
    "budget_intervals": [{
        "code": null,
        "enable_pacing": true,
        "end_date": "2017-12-02 23:59:59",
        "lifetime_budget": 1,
        "lifetime_budget_imps": null,
        "lifetime_pacing": true,
        "lifetime_pacing_pct": 100,
        "parent_interval_id": null,
        "start_date": "2017-11-30 00:00:00",
        "timezone": "US/Eastern"
    }],
        "goal_pixels": null,
        "goal_type": "cpc",
        "goal_value": null,
        "inventory_type": "real_time",
        "line_item_type": "standard_v2",
        "manage_creative": true,
        "name": "Swetha_ALI_Basic_API1",
        "profile_id": 96266482,
        "revenue_type": "vcpm",
        "revenue_value": null,
        "state": "active",
        "valuation": {
            "goal_target": 5,
            "goal_threshold": 5,
            "min_avg_cpm": 2,
            "max_avg_cpm": 3
        }
    }
}
{code}

{code}
curl -b cookies -X POST -d  @line_item_dcp_cpc.json  "https://api.appnexus.com/line-item?&advertiser_id=1887392"
{code}
```

### Create a line item with a revenue type of Viewable CPM and optimized to both a CPC and CPA goal

In this example, we create a line item with a revenue type of Viewable CPM, a CPC goal of $5 and CPA goal of $10.

```
{code}$ cat line_item_dcp_vcpm_cpaopt
{
    "line-item": {
        "ad_types": [
            "banner"
        ],
        "advertiser": {
            "id": 1887392,
            "name": "ALI Closed Beta Demo Advertiser"
        },
        "currency": "USD",
        "insertion_orders": [{
            "advertiser_id": 1887392,
            "budget_intervals": [{
                "code": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "enable_pacing": false,
                "end_date": null,
                "id": 2509856,
                "lifetime_budget": 1,
                "lifetime_budget_imps": null,
                "lifetime_pacing": false,
                "object_id": 676605,
                "object_type": "insertion_order",
                "start_date": "2017-11-30 00:00:00",
                "timezone": "US/Eastern"
            }],
            "code": null,
            "currency": "USD",
            "end_date": null,
            "id": 676605,
            "last_modified": "2017-12-01 02:44:34",
            "name": "Swetha_Seamless_IO",
            "start_date": null,
            "state": "active",
            "timezone": "US/Eastern"
        }],

        "advertiser_id": 1887392,
        "budget_intervals": [{
            "code": null,
            "enable_pacing": true,
            "end_date": "2017-12-02 23:59:59",
            "lifetime_budget": 1,
            "lifetime_budget_imps": null,
            "lifetime_pacing": true,
            "lifetime_pacing_pct": 100,
            "parent_interval_id": null,
            "start_date": "2017-11-30 00:00:00",
            "timezone": "US/Eastern"
        }],
        "goal_type": "cpa",
        "goal_value": null,
        "inventory_type": "real_time",
        "line_item_type": "standard_v2",
        "manage_creative": true,
        "name": "Swetha_ALI_VCPM_CPA",
        "profile_id": 96293804,
        "revenue_type": "cpm",
        "revenue_value": 3,
        "state": "active",
        "goal_pixels": [{
            "id": 932952,
            "post_click_goal_target": 10,
            "post_click_goal_threshold": 10
        }],
        "pixels": [{
            "id": 932952
        }],

        "valuation": {
            "goal_target": 5,
            "goal_threshold": 5
        },
        "auction_event": {
            "revenue_auction_event_type": "view",
            "revenue_auction_event_type_code": "view_display_50pv1s_an",
            "revenue_auction_type_id": 2}
    }
}
{code}

{code}
curl -b cookies -X POST -d @line_item_dcp_vcpm_cpaopt.json “https://api.appnexus.com/line-item?&advertiser_id=1887392”
{code}
```

### Create a line item with a CPM revenue type, optimized to a VCR goal

In this example, we set the VCR goal to 50% and the CPM revenue value to $3.

> [!NOTE]
> Managed supply strategy must be set to `false` to apply a VCR goal to the line item. VCR optimization is not supported for line items targeting managed inventory.

```
$ cat line_item_vcr 
{
 "line-item": {
 
     "ad_types": [
         "video"
     ],
     "advertiser": {
         "id": 4127136,
         "name": "VCR Test Advertiser"
     },
     "advertiser_id": 4127136,
     "inventory_type": "both",
     "name": "Test VCR LI",
     "state": "active",
     "currency": "USD",
     "timezone": "US/Eastern",
     "revenue_type": "cpm",
     "revenue_value": 3,
     "supply_strategies": {
         "managed": false,
         "rtb": true,
         "deals": false,
         "programmatic_guaranteed": false
     },
     "goal_type": "none",
     "budget_intervals": [
         {
             "id": 12024043,
             "object_id": 14286184,
             "object_type": "campaign_group",
             "start_date": "2021-03-19 00:00:00",
             "end_date": "2021-04-30 23:59:59",
             "timezone": "US/Eastern",
             "code": null,
             "parent_interval_id": null,
             "creatives": null,
             "subflights": null,
             "lifetime_budget": 2,
             "lifetime_budget_imps": null,
             "lifetime_pacing": true,
             "enable_pacing": true,
             "lifetime_pacing_pct": 100,
             "daily_budget_imps_opt": null,
             "daily_budget_opt": null
         }
     ],
     "insertion_orders": [
         {
             "id": 3205367,
             "state": "inactive"
             "name": "VCR Test IO",
             "advertiser_id": 4127136,
             "currency": "USD",
             "budget_intervals": [
                 {
                     "id": 6461220,
                     "object_id": 3205367,
                     "object_type": "insertion_order",
                     "start_date": "2019-11-30 00:00:00",
                     "end_date": "2019-12-31 23:59:59",
                     "timezone": "US/Eastern",
                     "code": null,
                     "lifetime_budget": 1,
                     "lifetime_budget_imps": null,
                     "lifetime_pacing": false,
                     "enable_pacing": false,
                     "daily_budget_imps": null,
                     "daily_budget": null,
                     "daily_budget_imps_opt": null,
                     "daily_budget_opt": null
                 }
             ],
         }
     ],
     "auction_event": {
         "payment_auction_event_type_code": "impression",
         "payment_auction_event_type": "impression",
         "payment_auction_type_id": 1,
         "revenue_auction_event_type_code": "impression",
         "revenue_auction_event_type": "impression",
         "revenue_auction_type_id": 1,
         "kpi_auction_event_type_code": "video_completion",
         "kpi_auction_event_type": "video",
         "kpi_auction_type_id": 10,
         "kpi_value_type": "rate_threshold",
         "kpi_value": 0.5
     },
     "valuation": {
         "min_margin_pct": null,
         "min_margin_cpm": null,
         "max_avg_cpm": null,
         "min_avg_cpm": null,
         "min_revenue_value": null,
         "max_revenue_value": null,
         "goal_target": null,
         "goal_threshold": null,
         "no_revenue_log": false,
         "bid_price_pacing_enabled": false,
         "bid_price_pacing_lever": 0,
         "campaign_group_valuation_strategy": null,
         "goal_confidence_threshold": null
     }
  } 
} 
```

### Update a line item to optimize to a Viewable CPM goal

In this example, we are updating a line item to optimize to is a Viewable CPM goal of $5.

```
{code}$ cat line_item_vcpmopt.json
{
    "line-item": {
        "goal_type": "none",
        "goal_value": null,
        "name": "ALI_VCPMOpt",
        "state": "active",
        "goal_pixels": null,
        "auction_event": {
            "kpi_auction_event_type": "view",
            "kpi_auction_event_type_code": "view_display_50pv1s_an",
            "kpi_auction_type_id": 2,
            "kpi_value": 5
        }
    }
}
{code}

{code}
curl -b cookies -X PUT -d @line_item_vcpmopt.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

### Update a line item to use a revenue type of Viewable CPM

In this example, we are updating a line item to use a Revenue Type of VCPM and setting the value to $3.

```
{code}$ cat lineitem_vcpm.json
{
    "line-item": {
        "goal_type": "none",
        "goal_value": null,
        "inventory_type": "real_time",
        "line_item_type": "standard_v2",
        "revenue_type": "cpm",
        "revenue_value": 3,
        "state": "active",
        "auction_event": {               
            "revenue_auction_event_type": "view",
            "revenue_auction_event_type_code": "view_display_50pv1s_an",
            "revenue_auction_type_id": 2}
    }
}
{code}

{code}
curl -b cookies -X PUT -d @lineitem_vcpm.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

### Update a line item to use a revenue type of CPC

In this example, we are updating a line item to use a Revenue Type of CPC and setting the revenue value to $3.

```
{code}$ cat line_item_cpc.json
{
    "line-item": {
        "inventory_type": "real_time",
        "line_item_type": "standard_v2",
        "revenue_type": "cpm",
        "revenue_value": 3,
        "state": "active",
        "auction_event": {
        "revenue_auction_event_type": "click",
        "revenue_auction_event_type_code": "click",
        "revenue_auction_type_id": 3
        }
    }
}
{code}
{code}
curl -b cookies -X PUT -d @line_item_cpc.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

### Update a line item to use a revenue type of Cost Plus Margin (paying a flat CPM) and disable optimization

In this example, we are updating a line item to use a Revenue Type of Cost Plus Margin with a margin of 20% and with optimization disabled. The CPM is a flat CPM of 11.

```
{code}$ cat line_item_costplus_base.json
{
    "line-item": {
        "goal_type": "none",
        "goal_value": null,
        "inventory_type": "real_time",
        "line_item_type": "standard_v2",
        "revenue_type": "cost_plus_margin",
        "revenue_value": 0.20,
        "state": "active",
        "goal_pixels": null,
        "valuation":{"max_avg_cpm": 11}
    }
}
{code}

{code}
curl -b cookies -X PUT -d @line_item_costplus_base.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

### Update a line item to disable optimization

In this example, we are updating a line item to disable optimiztion.

```
{code}$ cat line_item_no_opt.json
{
    "line-item": {
        "auction_event": {
        "kpi_auction_event_type": "impression",
        "kpi_auction_event_type_code": "impression",
        "kpi_auction_type_id": 1,
        "kpi_value": null,
        "payment_auction_event_type": "impression",
        "payment_auction_event_type_code": "impression",
        "payment_auction_type_id": 1,
        "revenue_auction_event_type": "impression",
        "revenue_auction_event_type_code": "impression",
        "revenue_auction_type_id": 1
        },
        "goal_pixels": null,
        "goal_type": "none",
        "goal_value": null
    }
}
{code}

{code}
$ curl -b cookies -X PUT -d @line_item_no_opt.json "https://api.appnexus.com/line-item?&id=152083&advertiser_id=1887392"
{code}
```

### Create a Programmatic Guaranteed buying line item

Scenario: You have negotiated a Programmatic Guaranteed deal (PG deal) with a seller and would like to target this deal with a Programmatic Guaranteed buying line item (PG buying line item).

1. Create a PG deal profile and note the ID for this profile (see **Target a Programmatic Guaranteed deal** example in [Profile Service](profile-service.md)).

1. Create a PG buying line item JSON (you'll need an existing insertion order ID and profile ID).

    ``` 
    $ cat pg_buying_line_item
    {
      "line-item": {
        "insertion_orders": [
          {
            "id": 1234
          }
        ],
        "name": "My PG Buying Line Item",
        "state": "active",
        "ad_types": [
          "banner"
        ],
        "profile_id": 123456,
        "currency": "USD",
        "supply_strategies": {
          "rtb": false,
          "managed": false,
          "deals": false,
          "programmatic_guaranteed": true
        },
        "revenue_value": 0.0,
        "revenue_type": "cost_plus_margin",
        "creatives": [],
        "require_cookie_for_tracking": false,
        "line_item_type": "standard_v2",
        "manage_creative": true
      }
    }
    ```

1. Make a `POST` request to the **`https://api.appnexus.com/line-item`** endpoint using this PG buying line item JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @pg_buying_line_item 'https://api.appnexus.com/line-item?advertiser_id=123'
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 8757356,
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 8757356,
                "code": null,
                "name": "My PG Buying Line Item",
                "advertiser_id": 123,
                "state": "active",
                "start_date": null,
                "end_date": null,
                "timezone": "CET",
                "discrepancy_pct": 0,
                "publishers_allowed": "all",
                "revenue_value": 0,
                "revenue_type": "cost_plus_margin",
                "goal_type": "none",
                "goal_value": null,
                "last_modified": "2019-08-07 19:49:45",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": false,
                "profile_id": 123456,
                "member_id": 958,
                "flat_fee_type": null,
                "comments": null,
                "remaining_days": null,
                "total_days": null,
                "manage_creative": true,
                "budget_set_per_flight": true,
                "creative_distribution_type": null,
                "line_item_type": "standard_v2",
                "bid_object_type": "creative",
                "prefer_delivery_over_performance": false,
                "priority": "5",
                "enable_v8": false,
                "viewability_vendor": null,
                "is_archived": false,
                "archived_on": null,
                "delivery_model_type": "standard",
                "advertiser": {
                    "id": 123,
                    "name": "My Advertiser"
                },
                "flat_fee": null,
                "supply_strategies": {
                    "managed": false,
                    "rtb": false,
                    "deals": false,
                    "programmatic_guaranteed": true
                },
                "deals": null,
                "delivery_goal": null,
                "labels": null,
                "broker_fees": null,
                "pixels": null,
                "insertion_orders": [
                    {
                        "id": 1234,
                        "state": "active",
                        "code": null,
                        "name": "Test IO",
                        "advertiser_id": 123,
                        "start_date": null,
                        "end_date": null,
                        "timezone": "CET",
                        "last_modified": "2018-03-06 21:16:47",
                        "currency": "USD",
                        "budget_intervals": [
                            {
                                "id": 2436841,
                                "object_id": 1234,
                                "object_type": "insertion_order",
                                "start_date": "2017-11-08 00:00:00",
                                "end_date": "2017-11-13 23:59:59",
                                "timezone": "CET",
                                "code": null,
                                "lifetime_budget": 10,
                                "lifetime_budget_imps": null,
                                "lifetime_pacing": false,
                                "enable_pacing": false,
                                "daily_budget_imps": null,
                                "daily_budget": null
                            }
                        ]
                    }
                ],
                "goal_pixels": null,
                "imptrackers": null,
                "clicktrackers": null,
                "campaigns": null,
                "valuation": null,
                "creatives": null,
                "budget_intervals": null,
                "custom_models": null,
                "inventory_discovery": null,
                "incrementality": null,
                "auction_event": null,
                "custom_optimization_note": null,
                "roadblock": null,
                "ad_types": null,
                "user_info": null,
                "partner_fees": null,
                "product": null,
                "in_demo_measurement": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "enable_pacing": null,
                "allow_safety_pacing": null,
                "lifetime_pacing": null,
                "lifetime_pacing_span": null,
                "lifetime_pacing_pct": null,
                "inventory_type": "both"
            },
            "dbg_info": {
                "warnings": [],
                "version": "1.18.1247",
                "output_term": "line-item"
            }
        }
    }
    ```

### Delete a line item

```
curl -b cookies -X DELETE "https://api.appnexus.com/line-item?id=5851054&advertiser_id=5413231"
```

```
{"response":
    {
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "dbg_info":
            {
                "warnings":[],
                "version":"1.0.190",
                "output_term":"not_found"}
            }
    }
}
```

### Update a line item to optimize for CPCV

In this example, we are updating a line item to optimize to CPCV $0.08.

```
{code}$ cat line_item_CPCV.json
{
    "line-item": {
        "goal_type": "none",
        "goal_value": null,
        "name": "ALI_CPCV",
        "state": "active",
        "goal_pixels": null,
        "auction_event": {
                "payment_auction_event_type_code": "impression",
                "payment_auction_event_type": "impression",
                "payment_auction_type_id": 1,
                "revenue_auction_event_type_code": "impression",
                "revenue_auction_event_type": "impression",
                "revenue_auction_type_id": 1,
                "kpi_auction_event_type_code": "video_completion",
                "kpi_auction_event_type": "video",
                "kpi_auction_type_id": 10,
                "kpi_value_type": "goal_value",
                "kpi_value": 0.08
            }
    }
}
{code}
{code}
curl -b cookies -X PUT -d @line_item_CPCV.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

### A line item that is not optimized for CPCV

In this example, we have a line item that is not optimized for CPCV.

```
{code}$ cat line_item_CPCV.json
{
    "line-item": {
        "goal_type": "none",
        "goal_value": null,
        "name": "ALI_CPCV",
        "state": "active",
        "goal_pixels": null,
        "auction_event": { 
                "kpi_auction_event_type": "impression", 
                "kpi_auction_event_type_code": "impression", 
                "kpi_auction_type_id": 1, 
                "kpi_value": null, 
                "kpi_value_type": "none", 
                "payment_auction_event_type": "impression",
                "payment_auction_event_type_code": "impression", 
                "payment_auction_type_id": 1, 
                "revenue_auction_event_type": "impression",
                "revenue_auction_event_type_code": 
                "impression", "revenue_auction_type_id": 1 }
    }
}
{code}

{code}
curl -b cookies -X PUT -d @line_item_CPCV.json "https://api.appnexus.com/line-item?id=152083&advertiser_id=1887392"
{code}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Conversion Pixel Service](conversion-pixel-service.md)
- [Insertion Order Service](insertion-order-service.md)
