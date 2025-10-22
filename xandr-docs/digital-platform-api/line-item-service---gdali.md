---
title: Line Item Service - GDALI
description: Explore the Line Item Service for a Guaranteed Delivery Augmented Line Item (GDALI), which defines your financial relationship with an advertiser.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Line Item service - GDALI

> [!NOTE]
> This page describes the Line Item Service for a Guaranteed Delivery Augmented Line Item (GDALI). While a GDALI uses the same line item service and endpoint as other types of line items (for example, [Line Item Service - ALI](line-item-service---ali.md)), there are a number of required fields that have to be configured properly to get the expected GDALI behavior.
>
> To create a GDALI, you must set the `line_item_subtype` field to "`gd_buying_imp"` or `"gd_buying_exclusive"`, and associate the line item with a seamless insertion order via the `insertion_orders` array. For more information, see [Insertion Order Service](insertion-order-service.md).

A line item defines your financial relationship with an advertiser, including budget, revenue type, and inventory targeting.

A GDALI is typically used for direct-sold business when an arrangement has been secured from a buyer with a committed impression volume, and is designed to:

- Deliver budget in full across its flight dates.
- Deliver budget evenly across its flight dates.
- Optionally compete in the auction with other demand, such as RTB/Open Exchange, while guaranteeing the original delivery goal.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>(line item JSON) | Add a new GDALI. |
| `PUT` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE)<br>(line item JSON) | Modify an existing GDALI. |
| `GET` | - [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE) | View all of an advertiser's line items. |
| `GET` | [https://api.appnexus.com/line-item?id=1,2,3](https://api.appnexus.com/line-item?id=1,2,3) | View multiple line items by ID using a comma-separated list.<br><br>**Tip:** <br>**Helpful Query String Filters:**<br>You can filter for line items based on when they first and last served. This is particularly useful when you are approaching your [object limit](object-limit-service.md) and need to identify line items that can be deleted from the system. For more details, see [First Run and Last Run](#first-run-and-last-run) below. |
| `GET` | [https://api.appnexus.com/line-item?search=SEARCH_TERM](https://api.appnexus.com/line-item?search=SEARCH_TERM) | Search for line items with IDs or names containing certain characters. |
| `DELETE` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE) | Delete a line item.<br><br>**Warning:** Deleting a line item will also delete all of its impression trackers and clicktrackers. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., revenue budget, tracking, cost budget, and targeting). |

## JSON fields

> [!NOTE]
> **Migration Notes** in the table are provided for users who are migrating from legacy line items to GDALIs.
>
> - NO CHANGE indicates a field that remains the same between legacy line items and GDALIs.
> - ACTION REQUIRED indicates a field that is new for GDALIs and requires configuration.
> - UNSUPPORTED indicates a field that is not used for GDALIs and should not be used.

### General

| Field | Type (Length) | Description |
|---|---|---|
| `id` | int | The ID of the line item.<br>**Required On:** `PUT`, in query string.<br>Migration Notes: NO CHANGE |
| `code` | string (100) | A custom code for the line item. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No two objects at the same level (e.g., insertion orders or line items) can use the same code per advertiser. For example, two line items cannot both use code "XYZ", but a single insertion order and its child line item can.<br>**Default:** `null`<br>Migration Notes: NO CHANGE |
| `name` | string (255) | The name of the line item.<br>**Required On:** `POST`<br>Migration Notes: NO CHANGE |
| `advertiser_id` | int | The ID of the advertiser to which the line item belongs.<br>Migration Notes: NO CHANGE |
| `state` | enum | The state of the line item. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"`<br>Migration Notes: NO CHANGE |
| `line_item_type` | enum | **Note:** When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `line_item_type` field may be omitted and will default to `"standard_v2"`.<br>The type of line item.<br>**Default:** `"standard_v2"`<br>Migration Notes: ACTION REQUIRED<br>When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `line_item_type` field may be omitted and will default to `"standard_v2"`. |
| `line_item_subtype` | enum | The line item subtype. For GDALIs, the value for this field must be one of the following:<br>- `"gd_buying_imp"`: Guaranteed delivery line item with impression delivery goal. Eligible only for transacting on managed supply.<br>- `"gd_buying_exclusive"`: Guaranteed delivery line item with exclusive delivery goal (also referred to as "share of voice" or "SOV"). Eligible only for transacting on managed supply.<br><br>**Note:**<br>- This field is only applicable for augmented line items (i.e., `"line_item_type"` = `"standard_v2"`). Any other value will not display or accept a `line_item_subtype`.<br>- By defining `line_item_subtype`, the user may omit the following fields/arrays in the request payload:<br>&nbsp; - `line_item_type`<br>&nbsp; - `bid_object_type`<br>&nbsp; - `delivery_model_type`<br>&nbsp; - `supply_strategies`<br>- If the user provides conflicting `line_item_subtype` and fields/arrays outlined above, we'll prefer the `line_item_subtype` and ignore other fields on the call.<br>- The `line_item_subtype` field (and associated fields/arrays listed above) cannot be changed after the line item is created.<br><br>**Required On:** `POST`<br>Migration Notes: ACTION REQUIRED<br>By defining `line_item_subtype`, the user may omit the following fields/arrays in the request payload:<br>- `line_item_type`<br>- `bid_object_type`<br>- `delivery_model_type`<br>- `supply_strategies`<br>If the user provides conflicting `line_item_subtype` and fields/arrays outlined above, we will prefer the `line_item_subtype` and ignore other fields on the call.<br>The `line_item_subtype` field (and associated fields/arrays listed above) cannot be changed after the line item is created. |
| `start_date` | timestamp | Do not use this field. Instead, use the `start_date` and `end_date` fields within the `budget_intervals` array to designate when the line item should run.<br>**Default:** `null` (immediately)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `end_date` | timestamp | Do not use this field. Instead, use the `start_date` and `end_date` fields within the `budget_intervals` array to designate when the line item should run.<br>**Default:** `null` (indefinitely)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `timezone` | enum | The timezone by which budget and spend are counted. For details and accepted values, see [API Timezones](api-timezones.md).<br><br>**Note:** For ALIs, be sure to use this field (and not the one in the `budget_intervals` array) to set the line item's time zone.<br><br>**Default:** "UTC" or advertiser's timezone<br>Migration Notes: NO CHANGE<br>For ALIs, be sure to use this field (and not the one in the `budget_intervals` array) to set the line item's time zone. |
| `ad_types` | array of strings | The type of creative used for this line item. Possible values:<br>- `"banner"`<br>- `"video"` (includes audio types as well)<br>- `"native"`<br><br>One or more values are supported. This value determines how auction items are tracked for the line item's buying strategy, paying strategy, forecasting, creative association, and targeting options.<br><br>**Note:** All creatives associated to a line item must have the same ad type, which should match the `ad_types` selected here.<br><br>**Default:** `"banner"`<br>**Required On:** `POST`/`PUT`<br>Migration Notes: ACTION REQUIRED<br>`"ad_types": [ "banner" ]` |
| `discrepancy_pct` | double | **Deprecated.**<br>Migration Notes: **UNSUPPORTED** |
| `publishers_allowed` | string | **Deprecated.** Use the values of the `supply_strategies` array to set the supply types (e.g., RTB/Open Exchange, Deals, Managed).<br>Migration Notes: **UNSUPPORTED** |
| `revenue_value` | double | The amount paid to the network by the advertiser.<br><br>**Note:** Depending on what you set the `revenue_type` field to, this field must be set to the actual value of that revenue type (e.g. `flat_fee`, `cpm`, or the desired viewable CPM).<br><br>**Required On:** `POST`/`PUT`<br>Migration Notes: NO CHANGE |
| `revenue_type` | enum | The way the advertiser has agreed to pay you (also called Booked Revenue). Possible values are listed below.<br>- `"cpm"`: Select this value if you are being paid flat payment for 1000 impressions (CPM)<br>&nbsp; - For Viewable CPM, set `revenue_type` to `"cpm"`, the `revenue_value` field to the Viewable CPM value, the `revenue_auction_event_type` field to `"view"` the `revenue_auction_event_type_code` field to `"view_display_50pv1s_an"` and `"revenue_auction_type_id"` to `2`. Only measured viewable impressions will be counted, according to the Xandr viewability measurement, using the IAB definition.<br>- `"flat_fee"`: A flat payment that the advertiser will pay you on a specified allocation date. That date can be daily or at the end of the flight. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable.<br><br>**Note:** The flat fee will not be booked on the allocation date unless the line item has served at least 1 impression. If you define a `revenue_type` of `flat_fee` you must specify a value for `flat_fee_type`.<br>**Required On:** `POST`<br>Migration Notes: ACTION REQUIRED<br>Viewable CPM revenue type has a new API configuration. For details, see [Auction Event](#auction-event) below. |
| `goal_type` | enum | Not currently supported for guaranteed delivery line items.<br>**Default:** `"none"`<br>Migration Notes: UNSUPPORTED |
| `goal_value` | double | **Deprecated.** Use `valuation` object instead.<br>Migration Notes: UNSUPPORTED |
| `last_modified` | timestamp | **Read-only.** The time of last modification to this line item.<br>Migration Notes: NO CHANGE |
| `click_url` | string (1000) | The click URL to apply at the line item level.<br>Migration Notes: NO CHANGE |
| `currency` | string (3) | The currency used for this line item. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Warning:** Once the line item has been created, the currency cannot be changed.<br><br>**Tip:** As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience.<br><br>**Default:** Default currency of the advertiser<br>Migration Notes: NO CHANGE |
| `require_cookie_for_tracking` | boolean | Indicates whether you want to serve only to users who use cookies, in order to do conversion tracking (because Xandr conversion attribution is cookie-based) and frequency capping.<br><br>**Note:** This flag is only enforced when a conversion pixel and/or frequency/recency cap has been applied, so setting `true` will not require cookies for a line item that has no conversion pixels and/or frequency capping.<br>- `true` indicates you will not serve to non-cookie users.<br>- `false` indicates you will serve to non-cookie users and accept no conversion attribution or frequency/recency capping for those users.<br><br>**Default:** `true`<br>Migration Notes: NO CHANGE |
| `profile_id` | int | You may associate an optional `profile_id` with this line item. A profile is a generic set of rules for targeting inventory. For details, see the [Profile Service](profile-service.md).<br>Migration Notes: NO CHANGE |
| `member_id` | int | ID of the member that owns the line item.<br>Migration Notes: NO CHANGE |
| `comments` | string | Comments about the line item.<br>Migration Notes: NO CHANGE |
| `remaining_days` | int | Not currently supported for guaranteed delivery line items.<br>Migration Notes: UNSUPPORTED |
| `total_days` | int | Not currently supported for guaranteed delivery line items.<br>Migration Notes: UNSUPPORTED |
| `manage_creative` | boolean | Must be set to `true` (creatives are managed at the line item level).<br>**Default:** `true`<br>Migration Notes: ACTION REQUIRED<br>`"manage_creative": true` |
| `advertiser` | object | **Read-only.** An object describing the advertiser with which this line item is associated. For details, see [Advertiser](#advertiser) below.<br>Migration Notes: NO CHANGE |
| `labels` | array | The optional labels applied to the line item. Currently, the labels available are: `"Trafficker"` and `"Sales Rep"`. For details, see [Labels](#labels) below.<br><br>**Note:** You can report on line item labels with the [Network Analytics](network-analytics.md) and [Network Advertiser Analytics](network-advertiser-analytics.md) reports. For example, if you use the `"Trafficker"` label to specify the name of the trafficker responsible for each line item, you could run the Network Analytics report filtered by `"trafficker_for_line_item"` to focus on the line items that a particular trafficker is responsible for, or grouped by `"trafficker_for_line_item"` to rank the performance of your traffickers. <br><br>Migration Notes: NO CHANGE |
| `broker_fees` | array | **Deprecated.** Broker fees are only eligible with legacy Insertion Order, Line Item, and Campaign objects.<br>Migration Notes: UNSUPPORTED<br>GDALIs do not support Broker Fees. |
| `pixels` | array of objects | The conversion pixels used to track CPA revenue. Both post-click and post-view revenue may be specified. You may only attach 20 pixels to a line item. If you need to attach more, speak with your Xandr Implementation Consultant or Support. For more details, see [Pixels](#pixels) and the example below for a sample of the format.<br>**Default:** `null`<br>Migration Notes: NO CHANGE |
| `insertion_orders` | array of objects | Objects containing metadata for the insertion orders this line item is associated with. For more information, see [Insertion Orders](#insertion-orders) below.<br>Migration Notes: NO CHANGE |
| `goal_pixels` | array of objects | Do not use this field.<br>Migration Notes: UNSUPPORTED |
| `imptrackers` | array of objects | **Read-only.** The third-party impression trackers associated with the line item. For more details, see [Impression Tracker Service](impression-tracker-service.md).<br>Migration Notes: NO CHANGE |
| `clicktrackers` | array of objects | **Read-only.** The third-party click trackers associated with the line item. For more details, see [Click Tracker Service](click-tracker-service.md).<br>Migration Notes: NO CHANGE |
| `valuation` | object | Not currently supported for guaranteed delivery line items.<br>Migration Notes: UNSUPPORTED |
| `creatives` | array of objects | The creatives that are associated with the line item. For more details, see [Creatives](#creatives) below.<br>Migration Notes: NO CHANGE |
| `budget_scheduling_settings` | object | The `budget_scheduling_settings` is a parent object that defines budget and scheduling settings. The `underspend_catchup_type` field is currently the only existing field of this object. For more details, see [Budget Scheduling Settings](#budget-schedule-setting) below. |
| `budget_intervals` | array of objects | Use this array for defining budget and flight dates. For more details, see [Budget Intervals](#budget-intervals) below.<br><br>**Warning:** GDALIs only support a single budget interval.<br>If you use `budget_intervals`, the following fields should not be used on the line-item object:<br> - `lifetime_pacing`<br> - `lifetime_budget`<br> - `lifetime_budget_imps`<br> - `enable_pacing`<br> - `lifetime_pacing_span`<br> - `allow_safety_pacing`<br> - `daily_budget`<br> - `daily_budget_imps`<br> - `lifetime_pacing_pct`<br><br>Migration Notes: ACTION REQUIRED<br>This array replaces budgeting and flight dates from legacy line items. Use this array for defining budget and flight dates.<br><br>**Warning:** GDALIs only support a single budget interval.<br><br>See [array of objects](#budget_intervals-objects). |
| `lifetime_budget` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `lifetime_budget_imps` | int | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `daily_budget` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `daily_budget_imps` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null` (unlimited)<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `enable_pacing` | boolean | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null`<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `allow_safety_pacing` | boolean | **Deprecated.** This field may not be set.<br>Migration Notes: UNSUPPORTED |
| `lifetime_pacing` | boolean | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** `null`<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `lifetime_pacing_span` | int | **Deprecated.** This field may not be set.<br>**Default:** `null` (3 days)<br>Migration Notes: UNSUPPORTED |
| `lifetime_pacing_pct` | double | Do not use this field. Instead, use the budget fields within the `budget_intervals` array.<br>**Default:** 100<br>Migration Notes: UNSUPPORTED<br>See the `budget_intervals` array. |
| `payout_margin` | double | The payout margin on performance offer line items.<br>Migration Notes: UNSUPPORTED |
| `insertion_order_id` | int | The ID of the current active insertion order (when applicable). Must append `include_insertion_order_id=true` to return this field in a `GET` call. For details, see the [Insertion Order Service](insertion-order-service.md).<br>Migration Notes: NO CHANGE |
| `stats` | object | **Deprecated.** The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.<br>Migration Notes: UNSUPPORTED |
| `all_stats` | array | **Read-only.** To show Rapid Reports for all available intervals (today, yesterday, the last 7 days, life time), pass `all_status=true` in the query string of a `GET` request.<br>Migration Notes: NO CHANGE |
| `first_run` | timestamp | **Read-only.** The date and time when the line item had its first impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they first served, see [First Run and Last Run](#first-run-and-last-run) below.<br>Migration Notes: NO CHANGE |
| `last_run` | timestamp | **Read-only.** The date and time when the line item had its last impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they last served, see [First Run and Last Run](#first-run-and-last-run) below.<br>Migration Notes: NO CHANGE |
| `expected_pacing` | double | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).Migration Notes: UNSUPPORTED |
| `total_pacing` | double | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).<br>Migration Notes: UNSUPPORTED |
| `has_pacing_dollars` | enum | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).<br>Migration Notes: UNSUPPORTED |
| `has_pacing_imps` | enum | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).<br>Migration Notes: UNSUPPORTED |
| `imps_pacing_percent` | int | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).<br>Migration Notes: UNSUPPORTED |
| `rev_pacing_percent` | int | **Deprecated.**<br><br>**Caution:** The `stats` object and Quickstats have been deprecated (as of October 17, 2016).<br>Migration Notes: UNSUPPORTED |
| `alerts` | object | Not currently supported for guaranteed delivery line items.<br>Migration Notes: UNSUPPORTED |
| `inventory_type` | enum | **Deprecated.** Use the values of the `supply_strategies` array to set the supply types (e.g., RTB/Open Exchange, Deals, Managed).<br>Migration Notes: UNSUPPORTED<br>Use the values of the `supply_strategies` array to set the supply types (e.g., RTB/Open Exchange, Deals, Managed). |
| `supply_strategies` | array of objects | **Note:** When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `supply_strategies` field may be omitted.<br>Guaranteed delivery line items will always be set to `"managed"`: `true` and all other strategies will be set to `false`. <br><br>An array containing several boolean fields used to designate which inventory supply sources you would like to target. The values of this object's boolean fields supersede the setting of the `inventory_type` field and once set will cause the `inventory_type` field to be permanently locked and ignored. Values in this object include:<br>- `"managed"`: boolean<br>- `"rtb"`: boolean<br>- `"deals"`: boolean<br>- `"programmatic_guaranteed"`: boolean<br><br>For more details, see [Supply Strategies](#supply-strategies) below.<br>Migration Notes: ACTION REQUIRED<br>When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `supply_strategies` field may be omitted.<br>Guaranteed delivery line items will always be set to `"managed"`: `true` and all other strategies will be set to `false`.<br>The `supply_strategies` array replaces the `inventory_type` field previously defined on the legacy campaign. |
| `creative_distribution_type` | enum | When multiple creatives of the same size are trafficked via a line item, this field's setting is used to determine the creative rotation strategy that will be used. Allowed values:<br>- `even`: Even rotation is handled automatically by our system. Also select this if you want creative rotation to be handled at the splits level.<br>- `weighted`: Creative rotation is based on a user-supplied weight.<br>- `ctr-optimized`: The creative in the size bucket with the highest CTR delivers the most. The default.<br>**Default:** `"even"`<br>Migration Notes: NO CHANGE |
| `prefer_delivery_over_performance` | boolean | Not currently supported for guaranteed delivery line items.<br>**Default:** `false`<br>Migration Notes: UNSUPPORTED |
| `viewability_vendor` | string | This field determines what provider measures the viewability of the ad unit. The only value that is currently valid is `"appnexus"`.<br>**Default:** `"appnexus"`<br>Migration Notes: ACTION REQUIRED<br>This field defaults to `appnexus`; `appnexus` is the only value that is currently valid. |
| `is_archived` | boolean | **Read-only.** Indicates whether the line item has been automatically archived due to not being used. Once set to `true`, the value can't be changed and the only calls that can be made on the line item object are `GET` and `DELETE`.<br><br>**Note:** ALIs and GDALIs do not support this feature.<br>If a line item is automatically archived, its profile will also be archived and the only calls that may be made on either of those objects are `GET` and `DELETE`. In addition, once archived, the line item may not be associated with any insertion orders.<br><br>**Default:** `false`<br>Migration Notes: UNSUPPORTED<br>Auto-archival is not currently supported by augmented line items. |
| `archived_on` | timestamp | **Read-only.** The date and time on which the line item was archived (i.e., when the `is_archived` field was set to `true`).<br><br>**Note:** ALIs and GDALIs do not support this feature.<br>**Default:** `null`<br>Migration Notes: UNSUPPORTED |
| `partner_fees` | array | Currently unsupported by guaranteed delivery line items. For details, see [Partner Fee Service](partner-fee-service.md).<br>Migration Notes: UNSUPPORTED<br>GDALIs do not support Partner Fees. |
| `delivery_goal` | array | For guaranteed delivery line items, the most important performance indicator is that the line item delivers its budget in full and evenly across its flight dates. To achieve these ends, these line items have an associated `delivery_goal`. These line items will deliver their impression or percentage goals evenly across their flight dates. This array specifies exactly what the line item's goals are.<br>For more details, see [Delivery Goal](#delivery-goal) below.<br>**Default:** `null`<br>Migration Notes: NO CHANGE |
| `priority` | int | For a line item targeting managed inventory (`supply_strategies` `managed` is `true`), since you have already paid for inventory, there is no need to input a buying strategy. However, you can set the line item's priority to weight the line item against other direct line items within your account.<br>**Default:** `5`<br>Migration Notes: Priority was previously specified within a campaign object; GDALIs define the priority on the line item object.<br><br>**Note:** The Microsoft Monetize UI sets the default value for impression `guaranteed` lines to 14, and 19 for `exclusive`. The default value for all line items created via the API is `5`. |
| `auction_event` | object | An object describing the auction event at which the line item should record. GDALI's only support impression-based auction events.<br>For details, see [Auction Event](#auction-event) below.<br><br>**Note:** Omitting the `auction_event` object (or setting to null) will automatically set this object to it default impression-based value.<br>**Default:** `null`<br>Migration Notes: ACTION REQUIRED<br>Omitting the `auction_event` object (or setting to `null`) will automatically set this object to it default impression-based value. |
| `bid_object_type` | enum | **Note:** When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `bid_object_type` field may be omitted and will default to `"creative"`.<br><br>The bid object type of the line item (e.g. `"creative"` or `"deal"`).<br>Migration Notes: ACTION REQUIRED<br>When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `bid_object_type` field may be omitted and will default to `"creative"`. |
| `custom_models` |  | Currently unsupported by guaranteed delivery line items. For details, see the [Splits Service](splits-service.md) on how to associate splits to GDALIs for creative targeting use cases.<br>Migration Notes: UNSUPPORTED |
| `deals` |  | Currently unsupported by guaranteed delivery line items. For details, see [Deal Line Item API Setup Guide](deal-line-item-api-setup-guide.md).<br>Migration Notes: UNSUPPORTED |
| `delivery_model_type` |  | **Caution:** When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `delivery_model_type` field may be omitted.<br>The type of delivery model (e.g. `"guaranteed"` or `"exclusive"`).<br>Migration Notes: ACTION REQUIRED<br>When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `delivery_model_type` field may be omitted. |
| `flat_fee` | object | A flat payment that the advertiser will pay you on a specified allocation date. That allocation date can be daily or at the end of the flight. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable.<br><br>**Note:** The flat fee will not be booked on the allocation date unless the line item has served at least one impression. For more information, see [Flat Fee](#flat-fee) below.<br><br>**Required On:** `POST`/`PUT`, if `revenue_type` is `"flat_fee"`.<br>Migration Notes: NO CHANGE |
| `flat_fee_type` | string | Flat fees can be paid out daily or on the flight end date. Available values are:<br>- `one_time`: The fee will be paid on the final allocation date. The associated `revenue_value` is the value to be paid on that date. The flight cannot be longer than one month.<br>- `daily`: The fee will be paid daily. The associated `revenue_value` is the daily fee, *not* the fee for the entire flight.<br>**Default:** `one_time`<br>**Required On:** `POST`/`PUT` if `revenue_type` is `"flat_fee"`.<br>Migration Notes: NO CHANGE |
| `roadblock` | object | The roadblock settings for the line item. For details, see [Roadblock](#roadblock) below.<br>Migration Notes: NO CHANGE<br><br>**Warning:** Only page-level "partial" roadblocks are supported by GDALI. |

#### `budget_intervals` objects

```
"budget_intervals": [
{
"start_date": "2020-02-03 00:00:00",
"end_date": "2020-02-29 23:59:59",
"lifetime_budget": null,
"lifetime_budget_imps": 1000000,
"daily_budget_imps": null,
"daily_budget": null,
"enable_pacing": false,
"lifetime_pacing": false,
"lifetime_pacing_pct": null
}
]
```
> [!NOTE] 
> The start_date and end_date of each of its budget_intervals array objects fall within the budget intervals defined on the parent Insertion order.  Only a single budget interval can be associated to guaranteed line items

| Field | Type (Length) | Description |
|---|---|---|
| `id` | int | The ID of the budget interval |
| `start_date` | timestamp | The start date of the budget interval. Format must be YYYY-MM-DD hh:mm:ss (hh:mm:ss should be hh:00:00). |
| `end_date` | timestamp | The end date of the budget interval. Format must be YYYY-MM-DD hh:mm:ss (hh:mm:ss should be set to hh:59:59). |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). The default value is "EST5EDT" or the advertiser's timezone. |
| `lifetime_budget_imps` | double | The lifetime budget in impressions for the budget interval. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to pace the lifetime budget evenly over the budget interval. GDALIs must be defined as `true`. |
| `lifetime_pacing_pct` | double | A double integer between (and including) 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between (and including) 50 and 150 on the following scale: <br> - 50: Pace behind schedule. <br> - 100: Pace evenly. <br>- 150: Pace ahead of schedule. <br> **NOTE:** It's recommended to set this field to 105. By default, the value will be set to 100. |
| `enable_forecast_pacing`| boolean | If true, daily budget will be calculated based on forecasted capacity for the line item. When false, daily budget will be evenly distributed across each day of the flight. <br> **NOTE:**  `lifetime_pacing_pct` will be applied regardless of whether `enable_forecast_pacing` is enabled or disabled. |

### Supply strategies

The `supply_strategies` object is used to designate which supply source you wish to target when buying inventory.

> [!NOTE]
> When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `supply_strategies` field may be omitted.
> [!CAUTION]
> The values of this object's boolean fields supersede the setting of the `inventory_type` field. Once any of these fields are set to `true` on an ALI, the `inventory_type` field will be ignored and unsettable for that line item. If you attempt to make a `PUT` call on the value of the `inventory_type` field after one or more of these fields have been set to `true`, the following error message will be generated: `"inventory_type cannot be updated once supply_strategies has been set"`.

| Field | Type | Description |
|:---|:---|:---|
| `managed` | boolean | Designates whether you wish to target managed inventory. This only includes inventory managed by your network. |
| `rtb` | boolean | Designates whether you wish to target inventory on the Open Exchange. This includes all third-party inventory not managed by your network that has been enabled for reselling (including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager). |
| `deals` | boolean | Designates whether you wish to target deal inventory. This includes any deals which you are are eligible to bid on. |
| `programmatic_guaranteed` | boolean | Designates whether you wish to target a programmatic guaranteed deal with this line item. If this is set to `true`, then the `rtb`, `managed`, and `deals` fields must be set to `false`. |

#### Target managed inventory

```
$ cat LI-supply-strategies.json

{
    "line-item": {
      ...
      "supply_strategies": {
          "managed": true,
          "rtb": false,
          "deals": false,
          "programmatic_guaranteed": false
      }
      ...
    }
}
```

### Delivery goal

The `delivery_goal` array contains information about the delivery goal attached to the GDALI. GDALIs will attempt to deliver against impression or percentage goals.

In order for GDALIs to serve, there are a number of different validations that have to be performed. The validations change depending on the type of delivery goal (see `type` field below).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique, automatically generated ID of this delivery goal. |
| `type` | string | The type of delivery goal. Allowed values:<br> - `"impressions"`: GDALIs with impression goals will attempt to serve the specified number of impressions evenly across their flight dates. If the delivery goal `type` is `"impressions"`, lifetime budget must be set at the line item level.<br>- `"percentage"`: Currently, the percentage goal is only available for `"exclusive"` GDALIs.<br><br>**Note:** If the delivery goal `type` is `"percentage"`, the line item cannot have a budget. |
| `disallow_non_guaranteed` | boolean | When `true`, this line item will always serve over non-guaranteed line items participating in the same (managed) auction.<br><br>**Note:** For exclusive delivery type, we recommend setting this field to `true` to ensure delivery. For impression guaranteed line items, setting this field to `true` may impact competition in the auction, which could impact yield. |
| `percentage` | int | If the type of delivery goal is `"percentage"`, this is the actual percentage at which the GDALI will serve. Allowed values are integers 0 <= n <= 100. If the delivery goal's `type` is `"impressions"`, this field must be `null`. |
| `reserved` | boolean | **This is a required field.** When `true`, this line item has inventory `"reserved"` for it; in other words, the line item is set to purchase a guaranteed number or percentage of impressions on a seller's inventory during its flight.<br><br>**Note:** You will not be able to set a GDALI's `state` to `"active"` unless this field is set to `true`. |
| `guaranteed_delivery_version` | int | **Deprecated.** This field is no longer in use. |

#### Apply a delivery goal to an exclusive guaranteed line item

```
$ cat LI-exclusive-delivery.json

{
    "line-item": {
      ...
      "line_item_subtype": "gd_buying_exclusive",
      ...
      "delivery_goal": {
          "type": "percentage",
          "percentage": 100,
          "disallow_non_guaranteed": true,
          "reserved": true
      }
      ...
    }
}
```

#### Apply a delivery goal to an impression guaranteed line item

```
$ cat LI-imp-delivery.json

{
    "line-item": {
      ...
      "line_item_subtype": "gd_buying_imp",
      ...
      "delivery_goal": {
          "type": "impressions",
          "disallow_non_guaranteed": false,
          "reserved": true
      }
      ...
    }
}
```

### Flat fee

The `flat_fee` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `lat_fee_status` | enum | **Read-only.** The status of the flat fee disbursement. Possible values: `"pending"`, `"processing"`, `"allocated"`, or `"error"`. |
| `flat_fee_allocation_date` | timestamp | The date when the flat fee revenue is scheduled to be allocated to publishers. <br>**Example:** `"2019-06-08 00:00:00"`.<br>This value will be `null` if the `flat_fee_type` is `daily`. |
| `flat_fee_adjustment_id` | int | **Read-only.** The ID for any adjustments required to this flat fee. |

#### Apply a daily $100 flat fee to a line item

```
$ cat LI-daily-flat-fee.json

{
    "line-item": {
      ...
      "revenue_value": 100,
      "revenue_type": "flat_fee",
      “flat_fee_type”: “daily”,
      ...
    }
}
```

#### Apply a one-time flat fee to a line item

```
$ cat LI-one-time-flat-fee.json

{
    "line-item": {
      ...
      "revenue_value": 10,
      "revenue_type": "flat_fee",
      "flat_fee_type": "one_time",
      ...
      "flat_fee": {
          " flat_fee_allocation_date": "2020-12-01 00:00:00"
      }
      ...
    }
}
```

### Budget schedule setting

The `budget_scheduling_settings` contains the following field.

| Field | Type | Description |
|:---|:---|:---|
| `underspend_catchup_type` | enum | Dictates how Xandr's system deals with an underdelivered daily budget. Use the `"evenly"` value if you'd like the unspent portions of your budget to be spent evenly throughout the rest of flight, or `"ASAP"` if you'd like the unspent budget to be spent as soon as possible.<br>Possible values: `"evenly"` or `"ASAP"` (default). |

### Roadblock

The `roadblock` object contains information to enable the delivery of two or more creatives to the page in unison. Roadblocks can be applied only for managed inventory and can't be enabled when you're working with third-party inventory.

GDALIs support "page-level" roadblocks, where one impression is recorded for the full set of creatives delivered for the roadblock. Impressions are recorded based on delivery of the master creative; if the master creative doesn't serve, no impression will be recorded. Budgets are based on master impressions delivered, exclusive of companion delivery.

> [!NOTE]
> The `master_width` and `master_height` fields must be defined for roadblock line items. The master creative is the creative with a size matching the `master_height` and `master_width` specified in the `roadblock` object. If more than one creative matches that size, the system will choose one as the master.
>
> Video roadblock line items are identified by the slot position and not the ad size `master_width` and `master_height` of the master creative. This is because the ad size is set to 1x1 for all videos.
>
> To serve a roadblock, one creative for each size must be eligible to serve on the page. All creatives will serve if ad slots are available. If more than one creative per size exists, creatives will rotate through a single ad slot. There can be more ad slots available than there are creatives to fill them.

For more on roadblocking, see [Target Your Inventory with Roadblocking](../monetize/target-your-inventory-with-roadblocking.md).

| Field | Type | Description |
|:---|:---|:---|
| `type` | enum | The type of roadblock. For GDALIs, this value must be either:<br>- `null`: (default) There is no roadblocking set at the line item level.<br>- `partial_roadblock`: Enables roadblocking on the line item. The line item serves when at least one creative of each size fits an eligible ad slot. |
| `master_width` | int | The width of the master creative. This value is required when roadblock type equals `partial_roadblock`. **Note**: For all video ad types, the width must be set to `1`. |
| `master_height` | int | The height of the master creative. This value is required when roadblock type equals `partial_roadblock`. **Note**: For all video ad types, the height must be set to `1`. |
|`slot_type` |string|The slot position of the master creative. Possible values are: `"AD_POD_FIRST"` (First Slot), `"AD_POD_LAST"` (Last Slot), `"INTRO_BUMPER"`, `"OUTRO_BUMPER"`.|

#### Apply a partial roadblock to a line item

```
$ cat LI-roadblock.json

{
    "line-item": {
      ...
      "roadblock": {
          "type": "partial_roadblock",
          "master_width": 300,
          "master_height": 600
          "ad_types": "banner"
      }
      ...
    }
}
```

#### Apply a partial roadblock to a line item with video ad type

```
$ cat LI-roadblock.json

{
    "line-item": {
      ...
      "roadblock": {
          "type": "partial_roadblock",
          "master_width": 1,
          "master_height": 1,
          "ad_types": "video",
          "slot_type": "AD_POD_FIRST"
      }
      ...
    }
}
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
| `id` | int | The ID of the label. Possible values: `7`, `8`, `11`. |
| `name` | enum | **Read-only.** The name of the label. <br>Possible values: `"Trafficker"` or `"Sales Rep"`. |
| `value` | string (100) | The value assigned to the label. For example, for the `"Sales Rep"` label, this could be a name such as `"Michael Sellers"`. |

#### Apply a trafficker label to a line item

```
$ cat LI-trafficker.json
 
{
    "line-item": {
      ...
      "labels": {
          "id": 7,
          “value”: “Michael Sellers”
      }
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
| `name` | string | **Read-only.** The name of the conversion pixel. |
| `trigger_type` | enum | **Read-only.** The type of event required for an attributed conversion. <br>Possible values: `"view"`, `"click"`, or `"hybrid"`. |

### Insertion orders

> [!NOTE]
> **Insertion Orders for Guaranteed Delivery Augmented Line Items (GDALI)**
>
> For an insertion order to be associated with a Guaranteed Delivery Augmented Line Item (GDALI), the insertion order must:
>
> - Be a [Seamless Insertion Order](insertion-order-service.md) (legacy insertion orders are not compatible).
> - Have `budget_type` set to `impression`.
> - Not contain more than one `budget_intervals` array.
> - Have unlimited budget (set via the `budget_intervals` array).
>
> Insertion orders not matching the above may only be associated to non-guaranteed line items.
>
> The above criteria is also required for programmatic guaranteed line items (PGLI). An insertion order with the above settings may also be associated to non-guaranteed line items.
>
> Associating a `profile_id` (e.g., frequency capping or setting additional targeting) on the insertion order object may result in unexpected forecasting or delivery for PGLIs and GDALIs. It is recommended not to use `profile_id` for insertion orders intended for the use with GDALIs.
>
> | Field | Type | Description |
> |:---|:---|:---|
> | `id` | int | The unique ID of the insertion order. |
> | `state` | enum | The state of this insertion order: `"active"` or `"inactive"`. |
> | `code` | string | An optional custom code used to identify this insertion order. |
> | `name` | string | The name of this insertion order. |
> | `advertiser_id` | int | The unique identifier of the advertiser associated with this insertion order. |
> | `budget_type` | enum | The budget type of the insertion order. |
> | `timezone` | enum | The timezone that this insertion order is associated with. For a list of allowed values, see [API Timezones](api-timezones.md). |
> | `last_modified` | date | The date at which this insertion order object was last updated. |
> | `currency` | enum | The currency type associated with this insertion order. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Note:** For best results, set the currency on the parent insertion order. For more information, see [Insertion Order Service](insertion-order-service.md). |
> | `budget_intervals` | array of objects | The metadata for the budget intervals from the associated insertion order. Budget intervals enable multiple date intervals to be attached to an insertion order, each with corresponding budget values. For more information, see [Insertion Order Service](insertion-order-service.md). |

### Auction event

The following fields are contained within the `auction_event` object.

> [!NOTE]
>
> - Guaranteed delivery line items only support impression and view-based auction events.
> - Omitting the `auction_event` object (or setting to `null`) results in the line item tracking revenue/payment based on impression events.
> - Do not supply values for the fields within this object that end in `_code` or `_id`. Only supply values for the fields in the `auction_event` object that end in `_type`. The object will return the fields ending in `_code` and `_id`, but they will be ignored on `POST` and `PUT` calls.
>
> For Viewable CPM, set:
>
> - `revenue_auction_event_type` field to `"view"`- Use this value when your Revenue Type is Viewable CPM. Only measured viewable impressions will be counted, according to the Xandr viewability measurement, using the IAB definition.
> - `revenue_auction_event_type_code` field to `"view_display_50pv1s_an"` - Use this value when your Revenue Type is Viewable CPM.
> - `revenue_auction_type_id` to `2` - Use this value when your Revenue Type is Viewable CPM.

| Field | Type | Description |
|:---|:---|:---|
| `revenue_auction_event_type` | string | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br>`"impression"`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin. |
| `revenue_auction_event_type_code` | string | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br>`"impression"`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin. |
| `revenue_auction_type_id` | int | This field is used in conjunction with the settings of the `revenue_type` field. Options are:<br>`1`: Use this value when your Revenue Type is CPM, Dynamic CPM or Cost Plus Margin. |
| `kpi_auction_event_type` | string | Not currently supported by GDALIs. |
| `kpi_auction_event_type_code` | string | Not currently supported by GDALIs. |
| `kpi_auction_type_id` | int | Not currently supported by GDALIs. |
| `kpi_value` | double | Not currently supported by GDALIs. |
| `payment_auction_event_type` | string | Not currently supported by GDALIs. |
| `payment_auction_event_type_code` | string | Not currently supported by GDALIs. |
| `payment_auction_type_id` | int | Not currently supported by GDALIs. |

#### Set $4 Viewable CPM revenue to a line item

```
$ cat LI-viewable-cpm.json
 
{
    "line-item": {
      ...
      “revenue_type”: “cpm”,
      “revenue_value”: 4
      ...
      "auction_event": {
          "revenue_auction_event_type": “view”,
          "revenue_auction_event_type_code": “view_display_50pv1s_an”,
          "revenue_auction_type_id": 2
      }
      ...
    }
}
```

### Creatives

Each object in the `creatives` array includes the following fields. To obtain information for `"id"` or `"code"` fields you can use the [Creative Service](creative-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `is_expired` | boolean | **Read-only.** If `true`, the creative is expired. If `false`, the creative is active. |
| `is_prohibited` | boolean | **Read-only.** If `true`, the creative falls into a prohibited category on the Xandr platform. |
| `width` | int | **Read-only.** The width of the creative. |
| `audit_status` | enum | **Read-only.** The audit status of the creative. Possible values: `"no_audit"`, `"pending"`, `"rejected"`, `"audited"`, or `"unauditable"`. |
| `name` | string | **Read-only.** The name of the creative. |
| `pop_window_maximize` | boolean | **Read-only.** If `true`, the publisher's tag will maximize the window. Only relevant for creatives with format `"url-html"` and `"url-js"`. If `pop_window_maximize` is set to `true`, then neither `height` nor `width` should be set on the creative. |
| `height` | int | **Read-only.** The height of the creative. |
| `state` | enum | **Read-only.** The state of the creative. <br>Possible values: `"active"` or `"inactive"`. |
| `format` | enum | **Read-only.** The format of the creative file. <br>Possible values: `"url-html"`, `"url-js"`, `"flash"`, `"image"`, `"raw-js"`, `"raw-html"`, `"iframe-html"`, or `"text"`. |
| `is_self_audited` | boolean | **Read-only.** If `true`, the creative is self-audited. |
| `id` | int | The ID of the creative. Either `id` or `code` is required when updating creative association. |
| `code` | string | The custom code for the creative. Either `id` or `code` is required when updating creative association. |
| `weight` | int | A user-supplied weight that determines the creative rotation strategy for same-sized creatives managed at the line item level. To use this field, the value of `creative_distribution_type` must be `"weighted"`. <br>Allowed value: An integer greater than `0` and less than or equal to `1000`. |
| `ad_type` | string | **Read-only.** The creative ad type. <br>Possible values: `"banner"`, `"video"`, and `"native"`.<br><br>**Note:** All creatives associated to a line item must have the same ad type, which should match the `ad_types` selected for the line item. |
| `all_budget_intervals` | boolean | Indicates whether the creative will serve during all budget intervals, including all future budget intervals. <br>Possible values are:<br>- `True` (the default)<br>- `False`<br>If `true`, `custom_date_ranges` in the `creatives` array and `creatives` in the `budget_intervals` array must be set to `null`. Conversely, if you want to use custom date ranges and/or creatives, `all_budget_intervals` must be set to `false`. |
| `custom_date_ranges` | array of objects | The date ranges setting the periods when the creative will serve.<br>If specified:<br>- `all_budget_intervals` must be set to `false`<br>- You must also specify the creative IDs in the `creatives` field of the `budget_intervals` array.<br>For more information, see [Custom Date Ranges](#custom-date-ranges) below. |

### Custom date ranges

The `custom_date_ranges` array sets the date ranges during which a creative will serve.

Dates must be in the format `YYYY-MM-DD hh:mm:ss`.

The date ranges must all meet the following specifications:

- They cannot include any dates before the start or after the end of any budget intervals defined for this line item.
- Both start and end dates are required.
- Date ranges must be at least an hour long.
- End dates cannot be later than `2038-01-19 00:00:00`.

| Field | Type | Description |
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
                start_date: 2/1/2020,
                end_date: 3/1/2020,
                lifetime_budget: 2000,
                id: 8888,                                  
                creatives: null
            }
        ],
        creatives: [
            {
                id: 56789,
                weight: 1,
                all_budget_intervals: true,                 
                custom_date_ranges: null                                                   
            },
            {
                id: 12345,
                weight: 2,
                all_budget_intervals: false,                
                custom_date_ranges: [
                    {                                      
                        start_date: 2/5/2020 00:00:00,      
                        end_date: 2/10/2020 00:00:00                     
                    }
                ]
            }
        ],
        creative_distribution_type: weighted
    }
}
```

### Budget intervals

When creating a new guaranteed delivery line item, ensure that the `start_date` and `end_date` of each of its `budget_intervals` array objects fall within one of the budget intervals defined on the parent insertion order (insertion orders are associated with line items via the `insertion_orders` array in the Line Item Service).

> [!NOTE]
>
> - Although budgets of any size may be configured on the line item, setting a lifetime budget with an equivalent daily impression budget of 1,000 impressions or less may result in the line item spending its lifetime budget prior to its designated end date.
> - If the parent insertion order's `budget_type` field has been set to `"impression"` *and* the line item's `auction_event` field has been set to Viewable CPM, only the viewable impressions count against both line item and insertion order budgets.
> - The `parent_interval_id` (in the `budget_intervals` array) has been deprecated and its value will be ignored.

Also consider the following when using the `budget_intervals` array:

- A guaranteed delivery line item must not contain more than one `budget_intervals` array.
- Impression guaranteed line items ("`line_item_subtype`": "`gd_buying_imp`") require a value be set for `lifetime_budget_imps`, as well as `lifetime_pacing` set to `true`. All revenue budget fields must be set to `null`. Setting `daily_budget_imps` in addition to `lifetime_budget_imps` may impact delivery; best practice is to only set the `lifetime_budget_imps` field.
- Exclusive line items ("`line_item_subtype`": "`gd_buying_exclusive`") must omit all budget fields, or set to `null`.

Each object in the `budget_intervals` array contains the following fields.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the budget interval. |
| `start_date` | timestamp | The start date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be hh:00:00). |
| `end_date` | timestamp | The end date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss should be set to hh:59:59). Must not be `null` for guaranteed delivery line items. For delivery to work best, your budget intervals should have a duration of at least 4 hours. |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). |
| `parent_interval_id` | int | **Deprecated.** The value of this field will be ignored. Instead, use the `start_date` and `end_date` fields of this array to define when the line item should run. |
| `lifetime_budget` | double | The lifetime budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object.<br><br>**Note:** If you also set the `lifetime_budget_imps` field in this array, whichever budget is exhausted first will cause spending to stop. A GDALI should only have `lifetime_budget_imps` defined. |
| `lifetime_budget_imps` | double | The lifetime budget in impressions for the budget interval.<br><br>**Note:**<br>- If you add line items to this insertion order, any spend already associated with those line items before they are added to the insertion order is NOT counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted.<br>- If you also set the `lifetime_budget` field in this array, whichever budget is exhausted first will cause spending to stop. A GDALI should only have `lifetime_budget_imps` defined.<br>- When a line item is enabled for roadblocks, only master creative imps will count against `lifetime_budget_imps`. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to pace the lifetime budget evenly over the budget interval. If `true`, you must set `lifetime_budget` or `lifetime_budget_imps`. |
| `lifetime_pacing_pct` | double | A double integer between-- and including-- 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between 50 and 150 on the following scale:<br>- `50`: Pace behind schedule.<br>- `100`: Pace evenly.<br>- `150`: Pace ahead of schedule.<br><br>**Note:** It's recommended to set this field to `105`. By default, the value will be set to `100`. |
| `daily_budget` | double | The daily budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object.<br><br>**Note:**<br>- If you add line items to this insertion order, any impressions associated to those line items when they are added to the insertion order are NOT counted under the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order are counted.<br>- If you also set the `daily_budget_imps` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `daily_budget_imps` | double | The daily budget in impressions.<br><br>**Note:** If you also set the `daily_budget` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `enable_pacing` | boolean | If `true`, then spending will be paced over the course of the day. Only applicable if there is a `daily_budget`. |
| `creatives` | array | Specifies the creatives associated with this budget interval. In order to serve, creatives must also be specified in the line item `creatives` field and `all_budget_intervals` must be `false`. |

#### Apply budget interval to a line item

```
$ cat LI-budget-intervals.json
 
{
    "line-item": {
      ...
      "budget_intervals": {
          "start_date": “2020-08-01 00:00:00”,
          "end_date": “2020-08-31 23:59:59”,
          "timezone": "UTC",
          "lifetime_budget_imps": 150000,
          "lifetime_pacing": true
      }
      ...
    }
}
```

### Stats

> [!NOTE]
> The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

### First run and last run

To include the `first_run` and `last_run` fields in a `GET` response, pass `flight_info=true` in the query string. You can also filter for line items based on when they first and last served, as follows:

#### Retrieve only line items that have never served

Pass `{{never_run=true}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&never_run=true'
```

> [!NOTE]
> You can use `{{never_run=true}}` in combination with other filters, but note that it will always be an OR relationship. For example, if you pass both `{{never_run=true}}` and `{{min_first_run=2012-01-01 00:00:00}}` in the query string, you will be looking for line items that have never served OR line items that first served on or after 2012-01-01.

#### Retrieve only line items that first served on or after a specific date

Pass `{{min_first_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00'
```

#### Retrieve only line items that first served on or before a specific date

Pass `{{max_first_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&max_first_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that first served within a specific date range

Pass `{{min_first_run=YYYY-MM-DD HH:MM:SS&max_first_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00&max_first_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that last served on or after a specific date

Pass `{{min_last_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00'
```

#### Retrieve only line items that last served on or before a specific date

Pass `{{max_last_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&max_last_run=2012-08-01 00:00:00'
```

#### Retrieve only line items that last served within a specific date range

Pass `{{min_last_run=YYYY-MM-DD HH:MM:SS&max_last_run=YYYY-MM-DD HH:MM:SS}}` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00&max_last_run=2012-08-01 00:00:00'
```

Fields of the type date can be filtered by `nmin` and `nmax` as well. The `nmin` filter lets you find dates that are either null or after the specified date, and the `nmax` filter lets you find dates that are either null or before the specified date.

## Examples

### View a line item

To view a specific line item, we must pass in the line item and advertiser IDs via the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?id=12954413&advertiser_id=3872575'

{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "line-item": {
            "id": 12954413,
            "code": null,
            "name": "Test-GDALI",
            "advertiser_id": 3872575,
            "state": "inactive",
            "start_date": null,
            "end_date": null,
            "timezone": "UTC",
            "discrepancy_pct": 0,
            "publishers_allowed": "all",
            "revenue_value": 1,
            "revenue_type": "cpm",
            "goal_type": "none",
            "goal_value": null,
            "last_modified": "2020-10-05 00:05:36",
            "click_url": null,
            "currency": "USD",
            "require_cookie_for_tracking": true,
            "profile_id": null,
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
            "priority": 5,
            "enable_v8": true,
            "viewability_vendor": "appnexus",
            "is_archived": false,
            "archived_on": null,
            "delivery_model_type": "guaranteed",
            "waive_deductions_when_disallowed": false,
            "line_item_subtype": "gd_buying_imp",
            "advertiser": {
                "id": 3872575,
                "name": "GDALI Testing Advertiser"
            },
            "flat_fee": null,
            "supply_strategies": {
                "managed": true,
                "rtb": false,
                "deals": false,
                "programmatic_guaranteed": false
            },
            "deals": null,
            "delivery_goal": {
                "id": 2246279,
                "type": "impressions",
                "disallow_non_guaranteed": false,
                "percentage": null,
                "reserved": true,
                "guaranteed_delivery_version": null
            },
            "labels": null,
            "broker_fees": null,
            "pixels": null,
            "insertion_orders": [
                {
                    "id": 4971824,
                    "state": "active",
                    "code": null,
                    "name": "Test-Seamless-IO-GDALI",
                    "advertiser_id": 3872575,
                    "start_date": null,
                    "end_date": null,
                    "timezone": "UTC",
                    "last_modified": "2020-10-02 11:17:21",
                    "currency": "USD",
                    "budget_intervals": [
                        {
                            "id": 9974698,
                            "object_id": 4971824,
                            "object_type": "insertion_order",
                            "start_date": "2020-10-01 00:00:00",
                            "end_date": null,
                            "timezone": "UTC",
                            "code": null,
                            "lifetime_budget": null,
                            "lifetime_budget_imps": null,
                            "daily_budget_imps": null,
                            "daily_budget": null,
                            "enable_pacing": false,
                            "lifetime_pacing": false,
                            "lifetime_pacing_pct": null
                        }
                    ],
                    "political_content": null
                }
            ],
            "goal_pixels": null,
            "imptrackers": null,
            "clicktrackers": null,
            "campaigns": null,
            "valuation": null,
            "creatives": null,
            "budget_intervals": [
                {
                    "id": 9980002,
                    "object_id": 12954413,
                    "object_type": "campaign_group",
                    "start_date": "2020-10-01 00:00:00",
                    "end_date": "2020-10-31 23:59:59",
                    "timezone": "UTC",
                    "code": null,
                    "parent_interval_id": null,
                    "creatives": null,
                    "lifetime_budget": null,
                    "lifetime_budget_imps": 150000,
                    "lifetime_pacing": true,
                    "enable_pacing": true,
                    "lifetime_pacing_pct": 105
                }
            ],
            "custom_models": null,
            "inventory_discovery": null,
            "incrementality": null,
            "auction_event": null,
            "custom_optimization_note": null,
            "roadblock": null,
            "budget_scheduling_settings": null,
            "ad_types": [
                "banner"
            ],
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
            "inventory_type": "direct"
        },
        "count": 1,
        "dbg_info": {
            "warnings": [

            ],
            "version": "1.0.56",
            "output_term": "line-item"
        }
    }
}
```

### View all of an advertiser's line items

> [!NOTE]
> If an advertiser has only one line item, it will be returned via the `{{line-items}}` JSON array.

```
$ curl -b cookies 'https://api.appnexus.com/line-item?advertiser_id=3872575'
{
    "response": {
        "count": 3,
        "line-items": [
            { ..."id": 12954413,...},
            { ..."id": 4983291,...},
            { ..."id": 4983258,...}
        ]
    }
}
```

### Update a line item end date

In this example, we are updating the end date of a line item.

```
$ cat line_item_end_date_update.json

{
    "line-item": {
        "budget_intervals: [
            {
                "end_date": "2020-12-31 23:59:59"
            }
        ]
    }
}

curl -b cookies -X PUT -d @line_item_end_date_update.json "https://api.appnexus.com/line-item?id=12954413&advertiser_id=3872575"
```

### Update a line item reserve property to true

In this example, we are updating the reserve property of a line item to true. For more details, see [Delivery Goal](#delivery-goal).

```
$ cat line_item_reserve.json
{
    "line-item": {
        "delivery_goal: {
            "reserved": true
        }
    }
}

curl -b cookies -X PUT -d @line_item_reserve.json "https://api.appnexus.com/line-item?id=12954413&advertiser_id=3872575"
```

### Create a GDALI with impression delivery model and CPM revenue type

1. Create a GDALI JSON (you'll need an existing insertion order ID and advertiser ID).

    ```
    $ cat gd_imp_cpm
    
    {
    "line-item": {
        "name": "Test-GDALI",
        "advertiser_id": "3872575",
        "insertion_orders": [{"id": 4971824}],
        "line_item_subtype": "gd_buying_imp",
        "state": "inactive",
        "priority": 14,
        "ad_types": [
          "banner"
        ],
        "timezone": "UTC",
        "budget_intervals": [
          {
            "start_date": "2020-10-01 00:00:00",
            "end_date": "2020-10-31 23:59:59",
            "timezone": "UTC",
            "lifetime_budget_imps": 150000,
            "lifetime_pacing": true,
            "lifetime_pacing_pct": 105
          }
        ],
        "currency": "USD",
        "revenue_type": "cpm",
        "revenue_value": 1,
        "delivery_goal": {
          "type": "impressions",
          "disallow_non_guaranteed": false,
          "reserved": true
        }
      }
    }
    ```

1. Make a `POST` request to the **`https://api.appnexus.com/line-item`** endpoint using this GDALI JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @gd_imp_cpm.json 'https://api.appnexus.com/line-item?advertiser_id=3872575'
    
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 12954413,
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 12954413,
                "code": null,
                "name": "Test-GDALI",
                "advertiser_id": 3872575,
                "state": "inactive",
                "start_date": null,
                "end_date": null,
                "timezone": "UTC",
                "discrepancy_pct": 0,
                "publishers_allowed": "all",
                "revenue_value": 1,
                "revenue_type": "cpm",
                "goal_type": "none",
                "goal_value": null,
                "last_modified": "2020-10-01 17:31:15",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": true,
                "profile_id": null,
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
                "priority": 14,
                "enable_v8": true,
                "viewability_vendor": "appnexus",
                "is_archived": false,
                "archived_on": null,
                "delivery_model_type": "guaranteed",
                "waive_deductions_when_disallowed": false,
                "line_item_subtype": "gd_buying_imp",
                "advertiser": {
                    "id": 3872575,
                    "name": "GDALI Testing Advertiser"
                },
                "flat_fee": null,
                "supply_strategies": {
                    "managed": true,
                    "rtb": false,
                    "deals": false,
                    "programmatic_guaranteed": false
                },
                "deals": null,
                "delivery_goal": {
                    "id": 2246279,
                    "type": "impressions",
                    "disallow_non_guaranteed": false,
                    "percentage": null,
                    "reserved": true,
                    "guaranteed_delivery_version": null
                },
                "labels": null,
                "broker_fees": null,
                "pixels": null,
                "insertion_orders": [
                    {
                        "id": 4971824,
                        "state": "active",
                        "code": null,
                        "name": "Test-Seamless-IO-GDALI",
                        "advertiser_id": 3872575,
                        "start_date": null,
                        "end_date": null,
                        "timezone": "UTC",
                        "last_modified": "2020-10-02 11:17:21",
                        "currency": "USD",
                        "budget_intervals": [
                            {
                                "id": 9974698,
                                "object_id": 4971824,
                                "object_type": "insertion_order",
                                "start_date": "2020-10-01 00:00:00",
                                "end_date": null,
                                "timezone": "UTC",
                                "code": null,
                                "lifetime_budget": null,
                                "lifetime_budget_imps": null,
                                "daily_budget_imps": null,
                                "daily_budget": null,
                                "enable_pacing": false,
                                "lifetime_pacing": false,
                                "lifetime_pacing_pct": null
                            }
                        ],
                        "political_content": null
                    }
                ],
                "goal_pixels": null,
                "imptrackers": null,
                "clicktrackers": null,
                "campaigns": null,
                "valuation": null,
                "creatives": null,
                "budget_intervals": [
                    {
                        "id": 9980002,
                        "object_id": 12954413,
                        "object_type": "campaign_group",
                        "start_date": "2020-10-01 00:00:00",
                        "end_date": "2020-10-31 23:59:59",
                        "timezone": "UTC",
                        "code": null,
                        "parent_interval_id": null,
                        "creatives": null,
                        "lifetime_budget": null,
                        "lifetime_budget_imps": 150000,
                        "lifetime_pacing": true,
                        "enable_pacing": true,
                        "lifetime_pacing_pct": 105
                    }
                ],
                "custom_models": null,
                "inventory_discovery": null,
                "incrementality": null,
                "auction_event": null,
                "custom_optimization_note": null,
                "roadblock": null,
                "budget_scheduling_settings": null,
                "ad_types": [
                    "banner"
                ],
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
                "inventory_type": "direct"
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "line-item"
            }
        }
    }
    ```

### Create a GDALI exclusive line item with daily flat fee revenue

1. Create a GDALI JSON (you'll need an existing insertion order ID and advertiser ID).

    ```
    $ cat gd_exclusive_flat
    
    {
    "line-item": {
        "name": "Test-flat fee-GDALI",
        "advertiser_id": "3872575",
        "insertion_orders": [{"id": 4971824}],
        "line_item_subtype": "gd_buying_exclusive",
        "state": "inactive",
        "priority": 14,
        "ad_types": [
          "banner"
        ],
        "timezone": "UTC",
        "budget_intervals": [
          {
            "start_date": "2020-10-01 00:00:00",
            "end_date": "2020-10-31 23:59:59",
            "timezone": "UTC"
          }
        ],
        "currency": "USD",
        "revenue_value": 100,
        "revenue_type": "flat_fee",
        “flat_fee_type”: “daily”,
        "delivery_goal": {
          "type": "percentage",
          "percentage": 100,
          "disallow_non_guaranteed": true,
          "reserved": true
        }
      }
    }
    ```

1. Make a `POST` request to the **`https://api.appnexus.com/line-item`** endpoint using this GDALI JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @gd_exclusive_flat.json 'https://api.appnexus.com/line-item?advertiser_id=3872575'
    
    {
        "response": {
            "status": "OK",
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 13024486,
                "code": null,
                "name": "Test-flat fee-GDALI",
                "advertiser_id": 3872575,
                "state": "inactive",
                "start_date": null,
                "end_date": null,
                "timezone": "UTC",
                "discrepancy_pct": 0,
                "publishers_allowed": "all",
                "revenue_value": 100,
                "revenue_type": "flat_fee",
                "goal_type": "none",
                "goal_value": null,
                "last_modified": "2020-10-01 17:10:31",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": true,
                "profile_id": null,
                "member_id": 958,
                "flat_fee_type": "daily",
                "comments": null,
                "remaining_days": null,
                "total_days": null,
                "manage_creative": true,
                "budget_set_per_flight": true,
                "creative_distribution_type": null,
                "line_item_type": "standard_v2",
                "bid_object_type": "creative",
                "prefer_delivery_over_performance": false,
                "priority": 14,
                "enable_v8": true,
                "viewability_vendor": "appnexus",
                "is_archived": false,
                "archived_on": null,
                "delivery_model_type": "exclusive",
                "waive_deductions_when_disallowed": false,
                "line_item_subtype": "gd_buying_exclusive",
                "advertiser": {
                    "id": 3872575,
                    "name": "GDALI Testing Advertiser"
                },
                "flat_fee": {
                    "flat_fee_status": "pending",
                    "flat_fee_allocation_date": null,
                    "flat_fee_adjustment_id": null
                },
                "supply_strategies": {
                    "managed": true,
                    "rtb": false,
                    "deals": false,
                    "programmatic_guaranteed": false
                },
                "deals": null,
                "delivery_goal": {
                    "id": 2253549,
                    "type": "percentage",
                    "disallow_non_guaranteed": true,
                    "percentage": 100,
                    "reserved": true,
                    "guaranteed_delivery_version": null
                },
                "labels": null,
                "broker_fees": null,
                "pixels": null,
                "insertion_orders": [
                    {
                        "id": 4971824,
                        "state": "active",
                        "code": null,
                        "name": "Test-Seamless-IO-GDALI",
                        "advertiser_id": 3872575,
                        "start_date": null,
                        "end_date": null,
                        "timezone": "UTC",
                        "last_modified": "2020-10-01 11:17:21",
                        "currency": "USD",
                        "budget_intervals": [
                            {
                                "id": 9974698,
                                "object_id": 4971824,
                                "object_type": "insertion_order",
                                "start_date": "2020-10-01 00:00:00",
                                "end_date": null,
                                "timezone": "UTC",
                                "code": null,
                                "lifetime_budget": null,
                                "lifetime_budget_imps": null,
                                "daily_budget_imps": null,
                                "daily_budget": null,
                                "enable_pacing": false,
                                "lifetime_pacing": false,
                                "lifetime_pacing_pct": null
                            }
                        ],
                        "political_content": null
                    }
                ],
                "goal_pixels": null,
                "imptrackers": null,
                "clicktrackers": null,
                "campaigns": null,
                "valuation": null,
                "creatives": null,
                "budget_intervals": [
                    {
                        "id": 10082806,
                        "object_id": 13024486,
                        "object_type": "campaign_group",
                        "start_date": "2020-10-01 00:00:00",
                        "end_date": "2020-10-31 23:59:59",
                        "timezone": "UTC",
                        "code": null,
                        "parent_interval_id": null,
                        "creatives": null,
                        "lifetime_budget": null,
                        "lifetime_budget_imps": null,
                        "daily_budget_imps": null,
                        "daily_budget": null,
                        "enable_pacing": false,
                        "lifetime_pacing": false,
                        "lifetime_pacing_pct": null
                    }
                ],
                "custom_models": null,
                "inventory_discovery": null,
                "incrementality": null,
                "auction_event": null,
                "custom_optimization_note": null,
                "roadblock": null,
                "budget_scheduling_settings": null,
                "ad_types": [
                    "banner"
                ],
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
                "inventory_type": "direct"
            },
            "count": 1,
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.68",
                "output_term": "line-item"
            }
        }
    }
    ```

### Create a GDALI roadblock line item

1. Create a GDALI JSON (you'll need an existing insertion order ID and advertiser ID).

    > [!NOTE]
    > The impression budget for GDALIs with roadblocks enabled represents *master* creative delivery only.

    ```
    $ cat gd_roadblock
    
    {
    "line-item": {
        "name": "Test-Roadblock-GDALI",
        "advertiser_id": "3872575",
        "insertion_orders": [{"id": 4971824}],
        "line_item_subtype": "gd_buying_imp",
        "state": "inactive",
        "priority": 14,
        "ad_types": [
          "banner"
        ],
        "timezone": "UTC",
        "budget_intervals": [
          {
            "start_date": "2020-10-01 00:00:00",
            "end_date": "2020-10-31 23:59:59",
            "timezone": "UTC",
            "lifetime_budget_imps": 150000,
            "lifetime_pacing": true,
            "lifetime_pacing_pct": 105
          }
        ],
        "currency": "USD",
        "revenue_type": "cpm",
        "revenue_value": 1,
        "roadblock": {
            "type": "partial_roadblock",
            "master_width": 300,
            "master_height": 600
        },
        "delivery_goal": {
          "type": "impressions",
          "disallow_non_guaranteed": false,
          "reserved": true
        }
      }
    }
    ```

1. Make a `POST` request to the **`https://api.appnexus.com/line-item`** endpoint using this GDALI JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @gd_roadblock.json 'https://api.appnexus.com/line-item?advertiser_id=3872575'
    
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 12971164,
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 12971164,
                "code": null,
                "name": "Test-Roadblock-GDALI",
                "advertiser_id": 3872575,
                "state": "inactive",
                "start_date": null,
                "end_date": null,
                "timezone": "UTC",
                "discrepancy_pct": 0,
                "publishers_allowed": "all",
                "revenue_value": 1,
                "revenue_type": "cpm",
                "goal_type": "none",
                "goal_value": null,
                "last_modified": "2020-10-05 15:04:17",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": true,
                "profile_id": null,
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
                "priority": 14,
                "enable_v8": true,
                "viewability_vendor": "appnexus",
                "is_archived": false,
                "archived_on": null,
                "delivery_model_type": "guaranteed",
                "waive_deductions_when_disallowed": false,
                "line_item_subtype": "gd_buying_imp",
                "advertiser": {
                    "id": 3872575,
                    "name": "GDALI Testing Advertiser"
                },
                "flat_fee": null,
                "supply_strategies": {
                    "managed": true,
                    "rtb": false,
                    "deals": false,
                    "programmatic_guaranteed": false
                },
                "deals": null,
                "delivery_goal": {
                    "id": 2247697,
                    "type": "impressions",
                    "disallow_non_guaranteed": false,
                    "percentage": null,
                    "reserved": true,
                    "guaranteed_delivery_version": null
                },
                "labels": null,
                "broker_fees": null,
                "pixels": null,
                "insertion_orders": [
                    {
                        "id": 4971824,
                        "state": "active",
                        "code": null,
                        "name": "Test-Seamless-IO-GDALI",
                        "advertiser_id": 3872575,
                        "start_date": null,
                        "end_date": null,
                        "timezone": "UTC",
                        "last_modified": "2020-10-02 11:17:21",
                        "currency": "USD",
                        "budget_intervals": [
                            {
                                "id": 9974698,
                                "object_id": 4971824,
                                "object_type": "insertion_order",
                                "start_date": "2020-10-01 00:00:00",
                                "end_date": null,
                                "timezone": "UTC",
                                "code": null,
                                "lifetime_budget": null,
                                "lifetime_budget_imps": null,
                                "daily_budget_imps": null,
                                "daily_budget": null,
                                "enable_pacing": false,
                                "lifetime_pacing": false,
                                "lifetime_pacing_pct": null
                            }
                        ],
                        "political_content": null
                    }
                ],
                "goal_pixels": null,
                "imptrackers": null,
                "clicktrackers": null,
                "campaigns": null,
                "valuation": null,
                "creatives": null,
                "budget_intervals": [
                    {
                        "id": 10008444,
                        "object_id": 12971164,
                        "object_type": "campaign_group",
                        "start_date": "2020-10-01 00:00:00",
                        "end_date": "2020-10-31 23:59:59",
                        "timezone": "UTC",
                        "code": null,
                        "parent_interval_id": null,
                        "creatives": null,
                        "lifetime_budget": null,
                        "lifetime_budget_imps": 150000,
                        "lifetime_pacing": true,
                        "enable_pacing": true,
                        "lifetime_pacing_pct": 105
                    }
                ],
                "custom_models": null,
                "inventory_discovery": null,
                "incrementality": null,
                "auction_event": null,
                "custom_optimization_note": null,
                "roadblock": {
                    "type": "partial_roadblock",
                    "master_width": 300,
                    "master_height": 600
                },
                "budget_scheduling_settings": null,
                "ad_types": [
                    "banner"
                ],
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
                "inventory_type": "direct"
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "line-item"
            }
        }
    }
    ```

## Related topics

- [Publisher GDALI API Setup](publisher-gdali-api-setup-guide.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Insertion Order Service](insertion-order-service.md)
