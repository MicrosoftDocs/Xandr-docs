---
title: Line Item Service
description: Explore the Line Item service, their JSON fields, REST API, and functions with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Line Item Service

> [!NOTE]
> This page describes the Line Item Service for standard (legacy) line items. If you use Augmented Line Items, see [Line Item Service - ALI](line-item-service---ali.md) instead.

The line items under an insertion order represent the agreed upon strategies you will be executing for the advertiser. After setting up a line item and optionally (depending on whether the advertiser uses insertion orders) associating it to one or more insertion orders, you can create campaigns to specify how to spend the money to fulfill your agreement. Line items are where you will record "booked revenue" using the `revenue_type` and `revenue_value` fields, which describe the revenue type (CPM, CPA, etc.) and amount that you will be paid by your advertisers.

> [!NOTE]
> Insertion orders will eventually be mandatory. Therefore, as a best practice, Xandr encourages you to begin using insertion orders as part of your API implementation.

Xandr suggests associating your line items with insertion orders to preserve historical pacing and performance data across line items under a single insertion order, and to streamline your setup for long-standing advertiser relationships by adding budget intervals to an insertion order. Line items can be associated to one or more insertion orders, but only to those of the same type (an insertion order that uses budget intervals or one that does not). Each line item is associated with one or more child campaigns; bidding strategies and inventory targeting are then set at the campaign level.

> [!NOTE]
> **Seamless line items**
>
> There are two types of line items: seamless and non-seamless (legacy). The main difference between seamless and non-seamless line items is that seamless line items use the `budget_intervals` array and non-seamless line items do not. In terms of setup, the main differences are:
>
> - To create an **seamless** line item, you must:
>   - Associate the line item to each insertion order by specifying the IDs of the parent seamless insertion orders in the `insertion_orders` array. Each object in the array should have an `id` field whose value corresponds to one of the parent seamless insertion orders. This associates the line item with each of those insertion orders. You may not associate seamless line items with non-seamless insertion orders.
>   - Use the `parent_interval_id` field in the `budget_intervals` array to specify each budget interval defined on all insertion orders associated with the line item. This will determine when the line item runs.
>   - Leave the `start_date` and `end_date` fields (and any budget or pacing related fields) on the top-level line item object level set to `null`.
>   - Only associate seamless line items with seamless insertion orders.
>
> You should also use the budget and pacing related fields in the `budget_intervals` array to specify the budget available to the line item during each budget interval and how the spending of that budget should be paced.
>
> - To create a **non-seamless** line item, you must:
>   - Use the budget and pacing related fields and the `start_date` and `end_date` fields on the main line item object to specify the dates during which the insertion order should run, what budget is available to it during those dates and how the spending of the budget should be paced.
>   - Leave all fields in the `budget_intervals` field (and any fields in its array) set to `null`. You may not associate non-seamless line items with seamless insertion orders.
>   - Only associate non-seamless line items with non-seamless insertion orders.
>
> Seamless line items are the preferred model. You should use the seamless line item workflow when creating new line items. You cannot convert a non-seamless line item to seamless or link non-seamless line items to seamless insertion orders (or seamless lines items to non-seamless insertion orders).
>
> In the UI, API `budget_intervals` are referred to as "Billing Periods".
>
> **About Performance Goals**
>
> Performance goals are also set on the line item. They are used to track and measure campaign performance when an advertiser has articulated performance goals and when the `revenue_type` and the `goal_type` are not measured the same way. For example, a `revenue_type` of `"cpm"` might be matched with a `goal_type` of `"ctr"` because the advertiser wants to measure goal achievement in terms of the click-through rate but pay in CPM.
>
> To set performance goals for line items with `goal_type` `"cpa"`, use the `goal_pixels` array. This array contains information about performance goal targets and thresholds. To set performance goals for line items with the `goal_type` `"cpc"` or `"ctr"`, use the `valuation` object. This object contains the performance goal threshold, which determines the bid/no bid cutoff on optimized campaigns, and the performance goal target, which represents the desired clicks or click-through rate.
>
> To learn more about performance goals, see [Understanding Performance Goals](../monetize/understanding-performance-goals.md) in the UI documentation.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>(line item JSON) | Add a new line item. |
| `PUT` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE)<br>(line item JSON) | Modify an existing line item. |
| `GET` | - [https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE) | View all of an advertiser's line items. |
| `GET` | [https://api.appnexus.com/line-item?id=1,2,3](https://api.appnexus.com/line-item?id=1,2,3) | View multiple line items by ID using a comma-separated list. |
| `DELETE` | [https://api.appnexus.com/line-item?id=1](https://api.appnexus.com/line-item?id=1) | Delete a specific line item identifying by its ID.<br><br>**Warning:**<br>Deletion is Recursive and Permanent.<br>Deleting a line item will also delete all of its associated budget intervals and splits. The deletions are permanent and cannot be reverted.<br><br>**Note:**<br>**Helpful Query String Filters**<br> - You can filter for line items based on when they first and last served. This is particularly useful when you are approaching your [object limit](object-limit-service.md) and need to identify line items that can be deleted from the system. For more details, see [First Run and Last Run](#first-run-and-last-run) below.<br> - You can filter for line that are not serving due to various conditions. For more details, see [Alerts](#alerts) below. |
| `GET` | [https://api.appnexus.com/line-item?search=SEARCH_TERM](https://api.appnexus.com/line-item?search=SEARCH_TERM) | Search for line items with IDs or names containing certain characters. |
| `DELETE` | - [https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/line-item?code=LINE-ITEM_CODE&advertiser_code=ADVERTISER_CODE) | Delete a line item.<br><br>**Warning:**<br>Deletion is Recursive and Permanent<br>Deleting a line item will also delete all of its child campaigns, impression trackers and clicktrackers. The deletions are permanent and cannot be reverted. Although deleted objects continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., revenue budget and tracking for line items, cost budget and targeting for campaigns). |
| `GET` | [https://api.appnexus.com/line-item/meta](https://api.appnexus.com/line-item/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item.<br>**Required On:** `PUT`, in query string |
| `code` | string (100) | A custom code for the line item. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No 2 objects at the same level (e.g., line items or campaigns) can use the same code per advertiser. For example, 2 lines items cannot both use code "XYZ", but a single line item and its child campaign can.<br>**Default:** `null` |
| `name` | string (255) | The name of the line item.<br>**Required On:** `POST` |
| `advertiser_id` | int | The ID of the advertiser to which the line item belongs. |
| `state` | enum | The state of the line item. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `line_item_type` | enum | The type of line item. Possible values are:<br> - `"standard_v1"`: Standard line item (non-ALI).<br> - `"standard_v2"`: Augmented line item (ALI).<br>**Note:** If you are creating an ALI, see this version of the [Line Item service documentation](line-item-service---ali.md) as different field settings are required.<br> - `"guaranteed_delivery"`: Guaranteed line item (GDLI).<br>**Default:** `"standard_v1"` |
| `start_date` | timestamp | The date and time when the non-seamless line item should start serving. This value reflects the Advertiser's time zone.<br><br>**Important:** If you are creating a seamless line item, do not set this field.<br><br>**Default:** `null` (immediately) |
| `end_date` | timestamp | The date and time when the non-seamless line item should stop serving. This value reflects the Advertiser's time zone.<br><br>**Important:**<br>If you are creating a seamless line item, do not set this field.<br><br>**Default:** `null` (indefinitely)<br><br>**Important:** Dates are inclusive; for example, an `end_date` of May 4th means the campaign runs until 23:59:59 on May 4th. |
| `timezone` | enum | The timezone by which budget and spend are counted. For details and accepted values, see [API Timezones](api-timezones.md).<br><br>**Note:**<br>Any `PUT` calls to the `advertiser` service which include `set_child_timezone=true` in the query string will cause any timezone settings on the lower level objects (e.g., insertion orders, line items, campaigns) to be overridden with the latest timezone value for that advertiser.<br><br>**Default:** "`EST5EDT"` or the advertiser's timezone. |
| `discrepancy_pct` | double | **Deprecated.** |
| `publishers_allowed` | string | Specifies the type of inventory to bid on with this line item. Possible values: `real_time` or `direct`. Real-time campaigns may target inventory that is exposed for RTB by other Xandr members or by our inventory supply partners. Direct campaigns may only target publisher inventory within your network. |
| `revenue_value` | double | The amount paid to the network by the advertiser.<br><br>**Note:**<br>This field must be set under certain conditions, but may not be set in others. In addition to the `POST`/`PUT` requirements listed in the **Required On** column, note the following:<br> - The field **may** be populated when `revenue_type` is `cpm`, `cpc`, `cpa`, `cost_plus_margin`, `cost_plus_cpm`, `est_cpm`. However, if the `revenue_type` is `"cpa"` this field will be ignored because revenue is tracked via `post_view_revenue` or `post_click_revenue` on the pixel.<br>- The field **may not** be populated when `revenue_type` is `"none"` or `"vcpm"`.<br><br>**Required On:**<br>`POST`/`PUT`, if `revenue_type` is `"cpc"`.<br>`POST`/`PUT`, if `revenue_type` is `"flat_fee"`.<br><br>**Note:** If `"flat_fee_type"` is `"daily"` this is the value paid out per day. If `"flat_fee_type"` is `"one_time"` this is the value paid out on the final allocation date. |
| `revenue_type` | enum | The way the advertiser has agreed to pay you. Possible values are listed below.<br><br>**Note:** If `post_view_revenue` or `post_click_revenue` is set for any pixel in the `pixels` array, `revenue_type` must be `"cpa"`.<br><br> The `revenue_type` cannot be set to a value that is incompatible with any of the line item's child campaigns.<br> - `"none"`: Do not track revenue for the line item.<br> - `"cpm"`: A flat payment per 1000 impressions.<br> - `"cpc"`: A flat payment per click.<br>- `"cpa"`: A flat payment per conversion.<br>- `"cost_plus_cpm"`: Media cost (what you spend on inventory) plus an extra CPM.<br>- `"cost_plus_margin"`: Media cost (what you spend on inventory) plus a percentage of what you spend.<br>- `"flat_fee"`: A flat payment that the advertiser will pay you on a specified allocation date. That date can be daily or at the end of the flight. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable. Note that the flat fee will not be booked on the allocation date unless the line item has served at least 1 impression. If you define a `revenue_type` of `flat_fee` you must specify a value for `flat_fee_type`.<br> - `"vcpm"`: (Publisher Ad Server only) A flat payment per 1000 viewable impressions. For more information about viewability, see [Introduction to Viewability](../invest/introduction-to-viewability.md).<br>- `"est_cpm"`: The estimated flat payment per 1000 impressions.<br><br>**Default:** `"none"` |
| `goal_type` | enum | For line items that make use of performance goals, the way that the advertiser would like to measure campaign optimization. <br>Possible values: `"none"`, `"cpc"`, `"cpa"`, or `"ctr"`.<br><br>**Default:** `"none"` |
| `goal_value` | double | **Deprecated.** Use `valuation` object instead. For details, see [Valuation](#valuation) below. |
| `last_modified` | timestamp | The time of last modification to this line item.<br>**Read Only.** |
| `click_url` | string (1000) | The click URL to apply at the line item level. |
| `currency` | string (3) | The currency used for this line item. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Note:** Once the line item has been created, the currency cannot be changed.<br> As a best practice, align currency to the billing currency in order to achieve the best possible local currency experience.<br><br>**Default:** Default currency of the advertiser. |
| `require_cookie_for_tracking` | boolean | Indicates whether you want to serve only to users who use cookies, in order to do conversion tracking (because Xandr conversion attribution is cookie-based). `true` indicates you will not serve to non-cookie users, because they have no potential for conversion attribution. `false` indicates you will serve to non-cookie users and accept no conversion attribution for those users. This flag is only enforced when a conversion pixel has been applied, so setting `true` will not require cookies for a line item that has no conversion pixels. |
| `profile_id` | int | You may associate an optional `profile_id` with this line item. A profile is a generic set of rules for targeting inventory. For details, see the [Profile Service](profile-service.md). |
| `member_id` | int | ID of the line item's owning member. |
| `comments` | string | Comments about the line item. |
| `remaining_days` | int | **Read-only.** The number of days between today and the `end_date` for the line item. <br><br>**Note:** This will be `null` if the `start_date` is in the future or if either the `start_date` or `end_date` is not set. |
| `total_days` | int | The number of days between the `start_date` and `end_date` for the line item. Note that this will be null if either the `start_date` or `end_date` is not set.<br>**Read-only.** |
| `manage_creative` | boolean | If `true`, creatives are managed at the line item level. If `false`, creatives are managed at the campaign level.<br>**Default:** `false` |
| `advertiser` | object | An object describing the advertiser with which this line item is associated. For details, see [Advertiser](#advertiser) below.<br>**Read-only.** |
| `flat_fee` | object | A flat payment that the advertiser will pay you on a specified allocation date. That allocation date can be daily or at the end of the flight. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable. Note that the flat fee will not be booked on the allocation date unless the line item has served at least 1 impression. For more information, see [Flat Fee](#flat-fee) below.<br>**Required On:** `POST`/`PUT`, if `revenue_type` is `"flat_fee"`. |
| `flat_fee_type` | string | Flat fees can be paid out daily or on the flight end date. Available values are:<br> - `one_time`: The fee will be paid on the final allocation date. The associated `revenue_value` is the value to be paid on that date. The flight cannot be longer than one month.<br>- `daily`: The fee will be paid daily. The associated `revenue_value` is the daily fee, *not* the fee for the entire flight.<br>**Default:** `one_time`<br>**Required On:** `POST`/`PUT`, if `revenue_type` is `"flat_fee"`. |
| `labels` | array | The optional labels applied to the line item. Currently, four labels are available: `"Trafficker"`, `"Sales Rep"`, and `"Campaign Type"`. For more details, see [Labels](#labels) below.<br><br>**Note:**<br>You can report on line item labels with the [Network Analytics](network-analytics.md) and [Network Advertiser Analytics](network-advertiser-analytics.md) reports. For example, if you use the `"Trafficker`" label to specify the name of the trafficker responsible for each line item, you could run the Network Analytics report filtered by `"trafficker_for_line_item"` to focus on the line items that a particular trafficker is responsible for, or grouped by `"trafficker_for_line_item"` to rank the performance of your traffickers. |
| `broker_fees` | array | The commissions that the network must pass to brokers when serving an ad. These commissions are deducted from the booked revenue (the amount the network receives from the advertiser) and are typically for brokering a relationship with the advertiser. They can either be a percentage of the revenue or a flat CPM. For more details, see [Broker Fees](#broker-fees) below.<br><br>**Note:**<br>Broker fees at the line item level override broker fees at the insertion order level. |
| `pixels` | array of objects | The conversion pixels being used for CPA revenue type. Both post-click and post-view revenue may be specified. You may only attach 20 pixels to a line item. If you need to attach more, speak with your Xandr Implementation Consultant or Support. <br>For more details, see [Pixels](#pixels) and the example below for a sample of the format.<br>**Default:** `null` |
| `insertion_orders` | array of objects | Objects containing metadata for the insertion orders this line item is associated with. For more information, see [Insertion Orders](#insertion-orders) below.<br><br>**Note:**<br>Once a line item is associated with a seamless insertion order, it cannot be associated to a non-seamless insertion order. Only seamless insertion orders may be associated with seamless line items. Only non-seamless insertions orders may be associat4ed with non-seamless line items. |
| `goal_pixels` | array | For a line item with the `goal_type` `"cpa"`, the pixels used for conversion tracking, as well as the post-view and post-click revenue. For more details, see [Goal Pixels](#goal-pixels) and the example below for a sample of the format. |
| `imptrackers` | array of objects | The third-party impression trackers associated with the line item. For more details, see [Impression Tracker Service](impression-tracker-service.md).<br>**Read Only.** |
| `clicktrackers` | array of objects | The third-party click trackers associated with the line item. For more details, see [Click Tracker Service](click-tracker-service.md).<br>**Read Only.** |
| `campaigns` | array of objects | The campaigns that are associated with the line item. For more details, see [Campaigns](#campaigns) below.<br><br>**Note:**<br>To associate a campaign to a line item, use the `line_item_id` field in the [Campaign Service](campaign-service.md). Note that no more than 500 campaigns can be associated to a single line item.<br>**Read Only.** |
| `valuation` | object | For a line item with the `goal_type` `"cpc"` or `"ctr"`, the performance goal threshold, which determines the bid/no bid cutoff on optimized campaigns, and the performance goal target, which represents the desired clicks or click-through rate. For more details, see [Valuation](#valuation) below. |
| `creatives` | array of objects | The creatives that are associated with the line item. For more details, see [Creatives](#creatives) below. |
| `budget_intervals` | array of objects | **Note:**<br>This array is only relevant to and required for seamless line items (if the line item is non-seamless, leave this field set to `null`).<br><br>Budget intervals enable multiple date intervals to be attached to a line item, each with corresponding budget values. For more details, see [Budget Intervals](#budget-intervals) below.<br><br>**Note:**<br>If you use `budget_intervals`, the following fields should not be used on the `line-item` object:<br> - `lifetime_pacing`<br>- `lifetime_budget`<br> - `lifetime_budget_imps`<br> - `enable_pacing`<br> - `lifetime_pacing_span`<br> - `allow_safety_pacing`<br> - `daily_budget`<br> - `daily_budget_imps`<br> - `lifetime_pacing_pct` |
| `roadblock` | object | The roadblock settings for the line item. For details, see [Roadblock](#roadblock) below. |
| `lifetime_budget` | double | The lifetime budget in revenue. The revenue currency is defined by the `currency` field. If you don't want to allocate line item budget to this `budget_interval`, set this field to `0`.<br><br>**Note:** Only applicable to non-seamless line items.<br><br>If you also set the `lifetime_budget_imps` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields.<br><br>**Default:** `null` (unlimited) |
| `lifetime_budget_imps` | int | The lifetime budget in impressions.<br>`lifetime_budget_imps` functions as a lifetime `"catch-all"` or `"cap"` for a line item's total impression budget. A line item won't exceeded the number of impressions set for this field, and if the number of delivered impressions is greater than the mount set for this field, the line item will stop bidding.<br>If you don't want to allocate line item budget to this `budget_interval`, set this field to `0`.<br><br>**Note:** Only applicable to non-seamless line items.<br>If you also set the `lifetime_budget` field, whichever budget is exhausted first will cause spending to stop. The best practice is to only set one of these fields.<br><br>**Default:** `null` (unlimited) |
| `daily_budget` | double | The daily budget in revenue. The revenue currency is defined by the `currency` field.<br><br>**Note:** Only applicable to non-seamless line items.<br><br>If you also set the `daily_budget_imps` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields.<br>**Default:** `null` (unlimited) |
| `daily_budget_imps` | int | The daily budget in impressions.<br><br>**Note:** Only applicable to non-seamless line items.<br>If you also set the `lifetime_budget` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields.<br><br>**Default:** `null` (unlimited) |
| `enable_pacing` | boolean | If `true`, the daily budgeted spend is spread out evenly throughout a day. Only applicable if there is a daily budget. That's why it defaults to `true` if daily budget is set, otherwise it defaults to `null`.<br><br>**Note:** Only applicable to non-seamless line items.<br>**Default:** `null` |
| `allow_safety_pacing` | boolean | If `true`, spend per minute is limited to a maximum of 1% of the lifetime budget and 5% of the daily budget.<br><br>**Note:** Only applicable to non-seamless line items. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to spend its overall lifetime budget evenly over the line item flight dates. If `true`, you cannot set a `daily_budget`, you cannot set `enable_pacing` to `false`, and you must first establish a `lifetime_budget`, a `start_date`, and an `end_date` for the line item.<br><br>**Note:** Only applicable to non-seamless line items.<br><br>**Default:** `null` |
| `lifetime_pacing_span` | int | In the event of an underspend event, this indicates the number of days across which the underspent amount will be distributed.<br><br>**Note:** Only applicable to non-seamless line items.<br><br>**Default:** `null` (3 days) |
| `lifetime_pacing_pct` | double | A double integer between-- and including-- 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between 50 and 150 on the following scale:<br> - `50`: Pace behind schedule<br> - `100`: Pace evenly<br>- `150`: Pace ahead of schedule<br><br>**Note:**<br>**Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.<br><br> Only applicable to non-seamless line items.<br><br>**Default:** `100` |
| `payout_margin` | double | The payout margin on performance offer line items. |
| `insertion_order_id` | int | The ID of the current active insertion order (when applicable). Must append `include_insertion_order_id=true` to return this field in a `GET` call. For details, see the [Insertion Order Service](insertion-order-service.md).<br><br>**Note:** Only seamless insertion orders may be associated with seamless line items. Only non-seamless insertions orders may be associated with non-seamless line items. |
| `stats` | object | The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `all_stats` | array | To show Rapid Reports for all available intervals (today, yesterday, the last 7 days, life time), pass `all_status=true` in the query string of a `GET` request.<br>**Read Only.** |
| `object_stats` | object | The number of total, active, and inactive campaigns under the line item.<br>**Read Only.** |
| `first_run` | timestamp | The date and time when the line item had its first impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they first served, see [First Run and Last Run](#first-run-and-last-run) below.<br>**Read Only.** |
| `last_run` | timestamp | The date and time when the line item had its last impression, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they last served, see [First Run and Last Run](#first-run-and-last-run) below.<br>**Read Only.** |
| `expected_pacing` | double | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `total_pacing` | double | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_dollars` | enum | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_imps` | enum | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `imps_pacing_percent` | int | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `rev_pacing_percent` | int | **Deprecated.**<br>**Attention:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `alerts` | object | The conditions that are preventing the line item from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional. Note that, at this time, there are no warnings for line items. To retrieve line items based on pauses, you must pass certain query string parameters in the `GET` request. For more details, including a complete list of possible pauses, see [Alerts](#alerts) below.<br>**Read Only.** |
| `creative_distribution_type` | enum | When multiple creatives of the same size are trafficked via a line item, this field's setting is used to determine the creative rotation strategy that will be used. Note that creatives must be managed on the line item in order to use this field. Allowed values:<br> - `even`: The default. Use the standard Xandr creative optimization algorithm, where each creative's valuation is computed independently, and the best-valued creative is chosen to serve.<br> - `weighted`: Creative rotation is based on a user-supplied weight.<br> - `ctr-optimized`: The creative with the highest CTR delivers the most.<br>**Default:** `"even"` |
| `is_archived` | boolean | Indicates whether the line item has been automatically archived due to not being used. Once set to `true`, the value can't be changed and the only calls that can be made on the line item object are `GET` and `DELETE`.<br><br>**Note:**<br>If a line item is automatically archived, its profile as well as all of its campaigns (and their profiles) will also be archived and the only calls that may be made on those objects are `GET` and `DELETE`. In addition, once archived, the line item may not be associated with any insertion orders.<br><br>**Default:** `false`<br>**Read Only.** |
| `archived_on` | timestamp | The date and time on which the line item was archived (i.e., when the `is_archived` field was set to `true`).<br>**Default:** `null`<br>**Read Only.** |
| `priority` | int | For Direct Buying Strategy, the priority for campaigns that buy your own managed inventory. Priority must be set on the campaign object.<br>**Default:** `5` |

### Advertiser

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for this advertiser. |
| `name` | string | The name of the advertiser associated with the unique ID above. |

### Labels

You can use the read-only [Label Service](label-service.md) to view all possible labels for line items, advertisers, insertion orders, campaigns, and publishers. This service also allows you to view the labels that have already been applied to your objects.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the label. Possible values: `7`, `8`, `11`. |
| `name` | enum | The name of the label. Possible values: `"Trafficker"`, `"Sales Rep"`, or `"Campaign Type"`.<br>**Read Only.** |
| `value` | string (100) | The value assigned to the label. For example, for the `"Sales Rep"` label, this could be a name such as `"Michael Sellers"`. |

### Broker fees

When a network uses a broker to serve an impression, it pays a fee to the broker for that service. This value varies between different networks, different brokers, and different campaigns. Therefore, the network must specify how much it will pay each broker it uses. This can also be done at the Campaign level ([Campaign Service](campaign-service.md)) or at the insertion order level ([Insertion Order Service](insertion-order-service.md)).

To create or edit brokers, refer to the [Broker Service](broker-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `broker_id` | int | The ID of the broker. |
| `broker_name` | string | The name of the broker.<br>**Read Only.** |
| `payment_type` | enum | The type of payment to the broker. <br>Possible values: `"cpm"` or `"revshare"`.<br><br>**Note:** The `payment_type` can only be set to `"cpm"` if the `revenue_type` is set to `"cpm"`. Where `revenue_type` is set to `"cpa"` or `"cpc"`, `payment_type` must be set to `"revshare"`. |
| `value` | double | The value of the payment, based on the payment type. |
| `description` | string (255) | The free-form description of the broker fee entry. |

#### Create a Broker fee

```
$ cat add-LI-broker-fees.json
{
    "line-item":
        {
    "broker_fees":[
        {
            "broker_id": 145,
                "payment_type": "cpm",
                "value": "1.00",
                "description": "Smart JMS fee"
            }]
    }
}

$ curl -b cookies -c cookies -X PUT -d @add-LI-broker-fees.json 'https://api.appnexus.com/line-item?id=152083&advertiser_id=11'

{
    "response":{
        "status":"OK",
        "id":"152083",
        "count":1,
        "start_element":0,
        "num_elements":100,

        }
}
```

#### Modify a Broker fee

```
$ cat modify-LI-broker-fee.json
{
"line-item" :
{ "broker_fees": [
    {
    "broker_id": 145,
        "payment_type": "cpm",
    "value": "2.00",
        "description": "Extra JMS fee"
        }]
    }
}

$ curl -b cookies -c cookies -X PUT -d @modify-broker-fee.json $ curl -b cookies -c cookies -X PUT -d @modify-LI-broker-fee.json 'https://api.appnexus.com/line-item?id=152083&advertiser_id=11' | json-pp

{
    "response":{
        "status":"OK",
        "id":"152083",
        "count":1,
        "start_element":0,
        "num_elements":100,
     }
}
```

### Pixels

Each object in the `pixels` array includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the conversion pixel. |
| `state` | enum | The state of the pixel. Possible values: `"active"` or `"inactive"`. |
| `post_click_revenue` | double | The post click revenue value for the pixel. |
| `post_view_revenue` | double | The post view revenue value for the pixel. |
| `name` | string | The name of the conversion pixel.<br>**Read Only.** |
| `trigger_type` | enum | The type of event required for an attributed conversion. Possible values: `"view"`, `"click"`, or `"hybrid"`.<br>**Read Only.** |

### Insertion orders

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of the insertion order.<br><br>**Note:**<br>Once a line item is associated with a seamless insertion order, it cannot be associated with a non-seamless insertion order. Only seamless insertion orders may be associated with seamless line items. Only non-seamless insertions orders may be associated with non-seamless line items. |
| `state` | enum | The state of this insertion order: `"active"` or `"inactive"`. |
| `code` | string | An optional custom code used to identify this insertion order. |
| `name` | string | The name of this insertion order. |
| `advertiser_id` | int | The unique identifier of the advertiser associated with this insertion order. |
| `start_date` | date | The start date for this insertion order. |
| `end_date` | date | The end date for this insertion order. |
| `timezone` | enum | The timezone that this insertion order is associated with. For a list of allowed values, see [API Timezones](api-timezones.md). The default value is `"EST5EDT"` or the advertiser's timezone. |
| `last_modified` | date | The date at which this insertion order object was last updated. |
| `currency` | enum | The currency type associated with this insertion order. For a list of supported currencies, see [Currency Service](currency-service.md). |
| `budget_intervals` | array of objects | The metadata for the budget intervals from the associated insertion order. Budget intervals enable multiple date intervals to be attached to an insertion order, each with corresponding budget values. For more information, see [Insertion Order Service](insertion-order-service.md). |

### Campaigns

Each object in the `campaigns` array includes the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the campaign.<br>**Read Only.** |
| `name` | string | The name of the campaign.<br>**Read Only.** |
| `state` | enum | The state of the campaign. Possible values: `"active"`, `"inactive"`, or `"parent_inactive"`.<br>**Read Only.** |
| `inventory_type` | enum | The type of inventory targeted by this campaign. Possible values: `"real_time"`, `"direct"`, or `"both"`. `"Real-time"` includes all third-party inventory not managed by your network that has been enabled for reselling including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager. `"Direct"` includes only inventory managed by your network.<br>**Read Only.** |
| `cpm_bid_type` | enum | The bidding strategy for buying third-party inventory on a per-impression basis. Possible values: `"base"`, `"average"`, `"clearing"`, `"predicted"`, or `"margin"`. Average is equivalent to Estimated Average Price (EAP); clearing is equivalent to Estimated Clear Price (ECP); predicted means you set a CPC goal or CPA goal.<br>**Read Only.** |
| `priority` | int | For Direct Buying Strategy, the priority for campaigns that buy your own managed inventory.<br>**Default:** `5`. |
| `start_date` | date | The date the campaign starts. |
| `end_date` | date | The date the campaign ends. |
| `creative_count` | int | The number of creatives associated with the campaign. |
| `profile_id` | int | The ID of the profile associated with the campaign. |

### Valuation

The valuation object is used to set performance goals for line items with the `goal_type` `"cpc"` or `"ctr"`. It contains the performance goal threshold, which determines the bid/no bid cutoff on optimized campaigns, and the performance goal target, which represents the desired clicks or click-through rate.

The `valuation` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `min_margin_pct` | decimal | For line items with `revenue_type` `"cpm"`, `"cpa"`, or `"cpc"` the minimum margin PCT.<br>**Default:** `null` |
| `goal_threshold` | decimal | For line items with the `goal_type` `"cpc"` or `"ctr"`, the performance goal threshold, which determines the bid/no bid cutoff on optimized campaigns.<br>**Default:** `null` |
| `goal_target` | decimal | For line items with the `goal_type` `"cpc"` or `"ctr"`, the performance goal target, representing the desired clicks or click-through rate.<br>**Default:** `null` |
| `performance_mkt_managed` | boolean | If `true`, the line item is a performance marketplace line item that buys on managed inventory. This field is applicable only when `revenue_type` is `"cpc"` or `"cpa"`.<br>**Default:** `false` |
| `campaign_group_valuation_strategy` | enum | **Note:**<br>**Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change. <br><br>For line items with `revenue_type` `“cpm”`, `“cpc”`, or `“cpa”`, determines which performance goal optimization strategy will be applied. Possible values are:<br> - `“prospecting”`: To use Xandr's standard optimization.<br> - `"retargeting"`: To optimize to a user retargeting segment. If you select this setting, you must also associate a user retargeting segment with the line item. To create user segments, see the [Segment service](segment-service.md). To associate user retargeting segments with the line item, see [Profile Service](profile-service.md).<br><br>**Default:** `null` |

### Creatives

Each object in the `creatives` array includes the following fields. To obtain information for `"id"` or `"code"` fields you can use the [Creative Service](creative-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `is_expired` | boolean | If `true`, the creative is expired. If `false`, the creative is active.<br>**Read Only.** |
| `is_prohibited` | oolean | If `true`, the creative falls into a prohibited category on the Xandr platform.<br>**Read Only.** |
| `width` | int | The width of the creative.<br>**Read Only.** |
| `audit_status` | enum | The audit status of the creative. Possible values: `"no_audit"`, `"pending"`, `"rejected"`, `"audited"`, or `"unauditable"`.<br>**Read Only.** |
| `name` | string | **Read-only.** The name of the creative. |
| `pop_window_maximize` | boolean | If `true`, the publisher's tag will maximize the window. Only relevant for creatives with format `"url-html"` and `"url-js"`. If `pop_window_maximize` is set to `true`, then neither `height` nor `width` should be set on the creative.<br>**Read Only.** |
| `height` | int | The height of the creative.<br>**Read Only.** |
| `state` | enum | The state of the creative. Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `format` | enum | The format of the creative file. Possible values: `"url-html"`, `"url-js"`, `"flash"`, `"image"`, `"raw-js"`, `"raw-html"`, `"iframe-html"`, or `"text"`.<br>**Read Only.** |
| `is_self_audited` | boolean | If `true`, the creative is self-audited.<br>**Read Only.** |
| `id` | int | The ID of the creative. Either `id` or `code` is required when updating creative association. |
| `weight` | int(10) | A user-supplied weight that determines the creative rotation strategy for same-sized creatives managed at the line item level. To use this field, the value of `creative_distribution_type` must be `"weighted"`. Allowed value: an integer greater than `0` and less than or equal to `1000`. |
| `code` | string | The custom code for the creative. Either `id` or `code` is required when updating creative association. |

### Budget intervals

> [!NOTE]
> This array is only used for seamless line items.

Budget intervals on seamless line items must be copies of the budget intervals defined on their parent insertion orders. Budget intervals on the line item will automatically have the same `start_date` and `end_date` as their corresponding insertion order budget intervals but should have distinct budgets. These function as line item-specific "sub-budgets" of the budget on the corresponding insertion order budget interval.

Line item budget intervals are created (and linked to their insertion order budget intervals) by the `parent_interval_id` field. When creating a new seamless line item, you must populate the `budget_intervals` array with references to all budget intervals on all insertion orders you are associating with that line item (insertion orders are associated with line items via the `insertion_orders` array in the Line Item Service). This is done by adding objects to the array that contain a single field, `parent_interval_id`, whose value is an insertion order budget interval the line item should inherit. See *Add a seamless line item with budget intervals* in the **[Examples](#examples)** section below.

Also consider the following when using the `budget_interval` array:

- Date ranges (e.g., `start_date`, `end_date`) of different budget intervals on the same line item cannot overlap.
- Budget intervals on the line item can have unlimited lifetime budgets (i.e., if those budget fields are left set to `null`).
- Budget intervals cannot be used if budget fields on the top-most level of the `insertion_order` object itself are set.
- Edits made to insertion order-level budget intervals are propagated to corresponding line item-level budget intervals (e.g., deleting a budget interval on the insertion order will also delete that budget interval on all line items that use it).
- If you are increasing the budget for the line item's budget interval, you must first increase the budget for the budget interval on the parent insertion order (otherwise you may not have sufficient budget). For more information, see [Insertion Order Service](insertion-order-service.md).

Each object in the `budget_intervals` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item budget interval. |
| `start_date` | timestamp | The start date of the budget interval, which is inherited from the insertion order. Format is `YYYY-MM-DD hh:mm:ss`. |
| `end_date` | timestamp | The end date of the budget interval, which is inherited from the insertion order. Format must be `YYYY-MM-DD hh:mm:ss` (hh:mm:ss must be set to 23:59:59).<br><br>**Note:** If the `end_date` of the parent insertion order's budget interval has been set to `null` (e.g, no end date), then the `end_date` on the line item must be set to a non-null value. |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). The default value is `"EST5EDT"` or the advertiser's timezone.<br><br>**Note:**<br>Any `PUT` calls to the `advertiser` service which include `set_child_timezone=true` in the query string will cause any timezone settings on the lower level objects (e.g., insertion orders, line items, campaigns) to be overridden with the latest timezone value for that advertiser. |
| `parent_interval_id` | int | The ID of the parent insertion order's budget interval. This is the `id` field in the `budget_intervals` array on the insertion order. Required in order for the line item's budget interval to inherit the values of the `start_date` and `end_date` fields in the insertion order's budget interval. |
| `lifetime_budget` | double | The lifetime budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object. Set this field to `0` if you don't want the line item to spend during this budget interval.<br>This field defaults to `null` (unlimited).<br><br>**Note:**<br>If you also set the `lifetime_budget_imps` field in this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_budget_imps` | int | The lifetime budget in impressions for the budget interval. <br><br>**Note:** If you add line items to this insertion order, any spend already associated with those line items before they are added to the insertion order is NOT counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted. Set this field to `0` if you don't want the line item to spend during this budget interval.<br><br>This field defaults to `null` (unlimited).<br><br>**Note:**<br>If you also set the `lifetime_budget` field in this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_pacing` | boolean | If `true`, the line item will attempt to pace the lifetime budget evenly over the budget interval. If `true` , you must set `lifetime_budget` or `lifetime_budget_imps`. |
| `daily_budget` | double | The daily budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object. <br><br>**Note:** If you add line items to this insertion order, any impressions associated to those line items when they are added to the insertion order are NOT counted under the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order are counted.<br><br>This field defaults to `null` (unlimited).<br><br>**Note:**<br>If you also set the `daily_budget_imps` field in this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `daily_budget_imps` | int | The daily budget in impressions.<br>This field defaults to `null` (unlimited).<br><br>**Note:**<br>If you also set the `daily_budget` field, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `enable_pacing` | boolean | If `true`, then spending will be paced over the course of the day. Only applicable if there is a `daily_budget`. |

### Goal pixels

The `goal_pixels` array is used when working with `goal_type` `"cpa"` and contains information about performance goal targets and thresholds.

Each object in the `goal_pixels` array includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the conversion pixel. |
| `state` | enum | The state of the pixel. Possible values: `"active"` or `"inactive"`. |
| `post_click_goal` | double | **Deprecated.** Use `post_click_goal_target` and `post_click_goal_threshold` instead. |
| `post_view_goal` | double | **Deprecated.** Use `post_view_goal_target` and `post_view_goal_threshold` instead. |
| `trigger_type` | enum | The type of event required for an attributed conversion. Possible values: `"view"`, `"click"`, or `"hybrid"`.<br>**Read Only.** |
| `post_click_goal_target` | double | The post-click advertiser goal value for the pixel. |
| `post_view_goal_target` | double | The post-view advertiser goal value for the pixel. (Comparable to `goal_value` for `goal_type` `"cpc"` and `"ctr"`.) |
| `post_click_goal_threshold` | double | The post-click advertiser goal threshold for the pixel, which determines the bid/no bid cutoff on optimized campaigns. Cannot be enabled without a target set. (Comparable to `goal_threshold` in the valuation object for `goal_type` `"cpc"` and `"ctr"`.) |
| `post_view_goal_threshold` | double | The post-view advertiser goal threshold for the pixel, which determines the bid/no bid cutoff on optimized campaigns. Cannot be enabled without a target set. (Comparable to `goal_threshold` in the valuation object for `goal_type` `"cpc"` and `"ctr"`.) |

### Delivery goal

This section applies only to Publisher Ad Server clients.

| Field | Type | Description |
|:---|:---|:---|
| `delivery_goal` | array of objects | **For Guaranteed Delivery line items only.** For Guaranteed Delivery line items, the most important performance indicator is that the line item delivers its budget in full and evenly across its flight dates. To achieve these ends, these line items have an associated `delivery_goal`. These line items will deliver their impression or percentage goals evenly across their flight dates. This array specifies exactly what the line item's goals are.<br>For more information about Guaranteed Delivery line items, see [Guaranteed Delivery](../monetize/guaranteed-delivery.md).<br>**Default:** `null` |

> [!NOTE]
> The `delivery_goal` array contains information about the delivery goal attached to this line item. Guaranteed Delivery line items will attempt to deliver against impression or percentage goals.
>
> In order for Guaranteed Delivery line items to serve, there are a number of different validations that have to be performed. The validations change depending on the type of delivery goal; they are described below.
>
> To see how to create a Guaranteed Delivery line item and its associated campaign (in a way that passes the validations described in this section), see the *Create a guaranteed delivery line item* example.
>
> | Field | Type | Description |
> |:---|:---|:---|
> | `id` | int | The unique, automatically generated ID of this delivery goal. |
> | `type` | string | The type of delivery goal. Allowed values:<br> - `"impressions"`: Guaranteed Delivery line items with impression goals will attempt to serve the specified number of impressions evenly across their flight dates. If the delivery goal `type` is `"impressions"`, budget must be set at the line item level.<br> - `"percentage"`: Currently, the percentage goal is only available for "exclusive" Guaranteed line items. <br>**Note:** If the delivery goal `type` is `"percentage"`, the line item cannot have a budget. |
> | `disallow_non_guaranteed` | boolean | When `true`, this line item will always serve over non-guaranteed line items participating in the same (managed) auction. |
> | `percentage` | int | If the type of delivery goal is `"percentage"`, this is the actual percentage at which the Guaranteed Delivery line item will serve. Allowed values are integers 0 <= n <= 100. If the delivery goal's `type` is `"impressions"`, this field must be `null`. |
> | `reserved` | boolean | **This is a required field.** When `true`, this line item has inventory "reserved" for it; in other words, the line item is set to purchase a guaranteed number or percentage of impressions on a seller's inventory during its flight. <br><br>**Note:** You will not be able to set a guaranteed line item's `state` to `"active"` unless this field is set to `true`. |
> | `guaranteed_delivery_version` | int | This temporary flag denotes the version of the Guaranteed Delivery pacing algorithm being used. It can be set at either the member or line item level. The flag will be removed when the new version (2) of the algorithm is released platform-wide. Allowed values:<br>- `1`<br>- `2`<br>**Default:** `null` |
>
> **Validations on Guaranteed Delivery line items**
>
> In order for a Guaranteed Delivery line item to serve, you must create the line item and associate it with one or more campaigns. The campaigns are not created automatically when you set up the Guaranteed Delivery line item.
>
> Further validations on Guaranteed Delivery line items include:
>
> - The line item must have a valid `start_date` and `end_date`.
> - `lifetime_pacing` must be set to `true`.
> - `enable_pacing` must be set to `false`.
> - `manage_creative` must be set to `true`.
> - `allow_safety_pacing` must be set to `false`.
> - The associated campaign's `inventory_type` must be `"direct"`.
> - If the delivery goal type is `"impressions"`, the budget must be set at the line item level.
> - If the delivery goal type is `"impressions"`, the `lifetime_budget` and `daily_budget` fields must **not** be set.
> - If the delivery goal type is `"impressions"`, then `lifetime_budget_imps` must be set.
> - If the delivery goal type is `"percentage"`, the line item cannot have a budget associated with it.
> - The line item's `revenue_type` must be one of:
>   - `"cpm"`
>   - `"flat_fee"`
> - The line item's `publishers_allowed` must be set to `"direct"`.
> - If you associate only one campaign with a line item, that campaign's `start_date` and `end_date` must be set to `null`.

### Stats

The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

### First run and last run

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

Fields of the type date can be filtered by `nmin` and `nmax` as well. The `nmin` filter lets you find dates that are either null or after the specified date, and the `nmax` filter lets you find dates that are either null or before the specified date.

### Alerts

This field notifies you of conditions that are preventing the line item from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional.

> [!NOTE]
> At this time, there are no warnings for line items.

To retrieve line items based on pauses, you must pass certain query string parameters in the `GET` request. See below for use cases with query string parameters and examples. Note that you can use these query string parameters both when retrieving all line items or specific line items, but the examples below only cover retrieving all line items, as that is where this feature offers the most value.

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
                        },
                        {
                            "id": 128,
                            "message": "All campaigns under this line item are inactive."
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
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=false'

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

In this example, we use pause ID `2` to retrieve all line items with flight start dates that are in the future.

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
| `128` | All campaigns under this line item are inactive. |

### Flat fee

The `flat_fee` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `flat_fee_status` | enum | The status of the flat fee disbursement. Possible values: `"pending"`, `"processing"`, `"allocated"`, or `"error"`.<br>**Read Only.** |
| `flat_fee_allocation_date` | timestamp | The date when the flat fee revenue is scheduled to be allocated to publishers. <br>**Example:** `"2012-06-08 00:00:00"`. This value will be `null` if the `flat_fee_type` is daily. |
| `flat_fee_adjustment_id` | int | The ID for any adjustments required to this flat fee. |

### Roadblock

Roadblocks can be set at only one level, either line item or campaign. If a roadblock has been set on a campaign, it can't be set on the parent line item. Roadblocks can be applied only for managed inventory and can't be enabled when you're working with third-party inventory.

| Field | Type | Description |
|:---|:---|:---|
| `type` | enum | The type of roadblock. Possible values include:<br>- `no_roadblock`: There is no roadblocking set at the line item level.<br>- `normal_roadblock`: The line item serves if the number of creatives is greater than or equal to the number of ad slots available.<br> - `partial_roadblock`: The line item serves when at least one creative of each size fits an eligible ad slot.<br> - `exact_roadblock`: The line item serves when the number of creatives is equal to the number of ad slots available. |
| `master_width` | int | The width of the master creative. Set this value only when using page-level roadblocking. For standard roadblocking, omit this field or set the value to `0`. (Do not set the value to `null`.) |
| `master_height` | int | The height of the master creative. Set this value only when using page-level roadblocking. For standard roadblocking, omit this field or set the value to `0`. (Do not set the value to `null`.) |

The master creative is the creative with a size matching the `master_height` and `master_width` specified in the roadblock object. If more than one creative matches that size, the system will choose one as the master.

The master creative is used for page-level roadblocking, where one impression is recorded for the full set of creatives delivered for the roadblock. That recorded impression is based on the master creative. This means that if the master creative doesn't serve, no impression will be recorded. If you want to use creative-level roadblocking, where each creative delivered is counted as an impression, leave the `master_width` and `master_height` values blank.

## Examples

### Add a seamless line item with budget intervals

In this example, we'll create a new inactive seamless line item, `"Lauren's Line Item"`, that uses budget intervals. We have already created an insertion order `(238174)` with billing periods to which we want to associate the new line item. The budget intervals of the line item will be associated with those of the insertion order through the `parent_interval_id` field in the `budget_intervals` array on the line item.

```
$ cat line-item
{
    "line-item": {
        "name": "Lauren's Line Item",
        "state": "inactive",
        "insertion_orders": [
            {
                "id": 238174
            }
        ],
        "budget_intervals": [
            {
                "parent_interval_id": 1377
            },
            {
                "parent_interval_id": 1378
            }
        ]
    }
}
```

```
$ curl -b cookies -X POST -d @line-item.json "https://api.appnexus.com/line-item?&advertiser_id=599314"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 2304063,
    "start_element": 0,
    "num_elements": 100,
    "line-item": {
      "id": 2304063,
      "code": null,
      "name": "Lauren's Line Item",
      "advertiser_id": 599314,
      "state": "inactive",
      "start_date": null,
      "end_date": null,
      "timezone": "EST5EDT",
      "discrepancy_pct": 0,
      "publishers_allowed": "all",
      "revenue_value": 0,
      "revenue_type": "cpm",
      "goal_type": "none",
      "goal_value": null,
      "last_modified": "2015-09-02 14:17:50",
      "click_url": null,
      "currency": "USD",
      "require_cookie_for_tracking": true,
      "profile_id": null,
      "member_id": 958,
      "comments": null,
      "remaining_days": null,
      "total_days": null,
      "manage_creative": false,
      "advertiser": {
        "id": 599314,
        "name": "Cindy's Adv"
      },
      "flat_fee": null,
      "delivery_goal": null,
      "labels": null,
      "broker_fees": null,
      "pixels": null,
      "insertion_orders": [
        {
          "id": 238174,
          "state": "inactive",
          "code": null,
          "name": "LH Test IO",
          "advertiser_id": 599314,
          "start_date": null,
          "end_date": null,
          "timezone": "EST5EDT",
          "last_modified": "2015-09-02 13:56:56",
          "currency": "USD",
          "budget_intervals": [
            {
              "id": 1377,
              "object_id": 238174,
              "object_type": "insertion_order",
              "start_date": "2015-09-02 00:00:00",
              "end_date": "2015-09-10 00:00:00",
              "timezone": "EST5EDT",
              "lifetime_budget": 1000,
              "lifetime_budget_imps": null,
              "lifetime_pacing": false,
              "enable_pacing": false,
              "daily_budget_imps": null,
              "daily_budget": null
            },
            {
              "id": 1378,
              "object_id": 238174,
              "object_type": "insertion_order",
              "start_date": "2015-09-10 00:00:00",
              "end_date": "2015-09-18 00:00:00",
              "timezone": "EST5EDT",
              "lifetime_budget": 1000,
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
      "valuation": {
        "performance_mkt_managed": false,
      },
      "creatives": null,
      "budget_intervals": [
        {
          "id": 1379,
          "object_id": 2304063,
          "object_type": "campaign_group",
          "start_date": "2015-09-02 00:00:00",
          "end_date": "2015-09-10 00:00:00",
          "timezone": "EST5EDT",
          "parent_interval_id": 1377,
          "budget_allocation": null
        },
        {
          "id": 1380,
          "object_id": 2304063,
          "object_type": "campaign_group",
          "start_date": "2015-09-10 00:00:00",
          "end_date": "2015-09-18 00:00:00",
          "timezone": "EST5EDT",
          "parent_interval_id": 1378,
          "budget_allocation": null
        }
      ],
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "enable_pacing": null,
      "allow_safety_pacing": null,
      "lifetime_pacing": null,
      "lifetime_pacing_span": null,
      "lifetime_pacing_pct": null,
      "payout_margin": null
    }
  }
}
```

### Add a non-seamless line item

In this example, we'll create a new line item and associate a conversion pixel with our new line item.

> [!NOTE]
> We are not linking any campaigns to this line item yet; therefore `campaigns` is set to `null`.

```
$ cat line-item
{
    "line-item": {
    "name": "Weekday French Speakers Q3 2012",
    "state": "inactive",
    "comments": "The name says it all -- that's who we're trying to advertise to",
    "daily_budget": null,
    "revenue_type": "cpa",
    "code": "wfspq312",
    "pixels": [
        {
        "id": "123456",
        "state": "inactive",
        "post_view_revenue": null,
        "post_click_revenue": "30.000000"
        }
    ],
    "start_date": "2011-11-04 00:00:00",
    "lifetime_budget": null,
    "end_date": null,
    "enable_pacing": null,
    "allow_safety_pacing": null,
    "publishers_allowed": "all",
    "campaigns": null
    }
}
```

```
curl -b cookies -c cookies -X POST -d @line-item "https://api.appnexus.com/line-item?advertiser_id=51"
```

### Add a line item with a CPC performance goal

In this example, we'll create a line item with a CPC performance goal. We're setting a cost-per-click goal threshold of $2.34 and a target (for reporting purposes) of $2.00.

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
        "goal_target":2.00,
        "goal_threshold":2.34
    }
    "lifetime_budget": null,
    "end_date": null,
    "enable_pacing": null,
    "allow_safety_pacing": null,
    "publishers_allowed": "all",
    "campaigns": null
    }
}
```

```
curl -b cookies -c cookies -X POST -d @line-item "https://api.appnexus.com/line-item?advertiser_id=51"
```

### Add a line item with a CPA performance goal

In this example, we'll create a line item with a CPA performance goal. We're setting a CPA goal threshold of $4.56 and a target (for reporting purposes) of $4.00.

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
        "id": "123456",
        "state": "inactive",
        "post_view_revenue": null,
        "post_click_revenue": "30.000000"
        }
    ],
    "goal_pixels":[
        {
        "id":"123456",
        "post_view_goal_threshold":4.56,
        "post_view_goal_target":4.00
        }
    ].
    "lifetime_budget": null,
    "end_date": null,
    "enable_pacing": null,
    "allow_safety_pacing": null,
    "publishers_allowed": "all",
    "campaigns": null
    }
}
```

```
curl -b cookies -c cookies -X POST -d @line-item "https://api.appnexus.com/line-item?advertiser_id=51"
```

### Add a performance offer line item

In this example, we'll create a performance offer line item that buys both managed and cross-net inventory on a CPC basis.

```
$ cat line-item
{
    "line-item": {
        "name": "US CA",
        "state": "inactive",
        "daily_budget": null,
        "revenue_type": "cpc",
        "revenue_value": "5.00",
        "goal_type": "none",
        "valuation": {
            "performance_mkt_managed": true,
        },
        "lifetime_budget": null,
        "end_date": null,
        "enable_pacing": null,
        "allow_safety_pacing": null,
        "publishers_allowed": "all",
        "campaigns": null,
        "manage_creative": true,
        "payout_margin": 0.2
    }
}
```

```
curl -b cookies -c cookies -X POST -d @line-item "https://api.appnexus.com/line-item?advertiser_id=51"
```

### View a line item

To view a specific line item, we must pass in the line item and advertiser IDs via the query string. This line item has a conversion pixel already set up.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?id=164532&advertiser_id=52049'

{
    "response": {
    "status": "OK",
    "line-item": {
        "id": 164532,
        "code": "wfspq312",
        "name": "Weekday French Speakers Q3 2012",
        "advertiser_id": 52049,
        "state": "inactive",
        "start_date": "2011-11-04 00:00:00",
        "end_date": null,
        "timezone": "EST5EDT",
        "discrepancy_pct": 0,
        "lifetime_budget": null,
        "lifetime_budget_imps": null,
        "daily_budget": null,
        "daily_budget_imps": null,
        "enable_pacing": null,
        "allow_safety_pacing": null,
        "publishers_allowed": "all",
        "revenue_value": 0,
        "revenue_type": "cpa",
        "pixels": [
        {
            "id": "39688",
            "state": "inactive",
            "post_view_revenue": null,
            "post_click_revenue": "30.000000"
        }
        ],
        "campaigns": null,
        "insertion_orders": null,
        "goal_type": "none",
        "goal_value": null,
        "goal_pixels": null,
        "last_modified": "2012-06-19 20:29:38",
        "all_stats": null,
        "click_url": null,
        "currency": "USD",
        "require_cookie_for_tracking": true,
        "labels": null,
        "advertiser": {
        "id": 52049,
        "name": "Cody's Great Advertiser"
        },
        "broker_fees": null,
        "profile_id": null,
        "member_id": 1282,
        "flat_fee": null,
        "imptrackers": null,
        "clicktrackers": null,
        "comments": "The name says it all -- that's who we're trying to advertise to",
        "is_malicious": false,
        "remaining_days": null,
        "total_days": 60
    },
    "count": 1,
    "start_element": null,
    "num_elements": null
    }
}
```

### View all of an advertiser's line items

Unlike the examples above, this line item has two campaigns attached, as well as a `goal_pixels` array. Notice that even though this advertiser has only one line item, it's returned via the `line-items` JSON array.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/line-item?advertiser_id=51'

{
   "response":{
      "status":"OK",
      "line-items":[
         {
            "id":2,
            "code":null,
            "name":"Default Line Item",
            "advertiser_id":51,
            "state":"active",
            "start_date":null,
            "end_date":null,
            "timezone":"EST5EDT",
            "lifetime_budget":null,
            "lifetime_budget_imps":null,
            "daily_budget":null,
            "daily_budget_imps":null,
            "enable_pacing":false,
            "publishers_allowed":"all",
            "lifetime_spend":null,
            "lifetime_imps":null,
            "daily_spend":null,
            "daily_imps":null,
            "revenue_value":null,
            "revenue_type":null,
            "pixels":[
               {
                  "id":"934",
                  "state":"active",
                  "post_view_revenue":null,
                  "post_click_revenue":null
               }
            ],
            "campaigns":[
               {
                  "id":"21999",
                  "name":"My second campaign",
                  "state":"inactive"
               },
               {
                  "id":"21180",
                  "name":"My first campaign",
                  "state":"active"
               }
            ],
            "goal_type":"cpa",
            "goal_value":null,
            "goal_pixels":[
               {
                  "id":934,
                  "state":"active",
                  "post_view_goal":1,
                  "post_click_goal":2
               }
            ],
            "labels" [
               {
                  "value: "First Contact",
                  "id": 7,
                  "name": "Trafficker"
               },
               {
                  "value: "Second Contact",
                  "id": 8,
                  "name": "Sales Rep"
               },
            "last_modified":"2010-06-09 19:32:56",
            "comments": null
            "is_malicious": false,
            "remaining_days": null,
            "total_days": 30
         }
      ],
      "count":1,
      "start_element":null,
      "num_elements":null
   }
}
```

### Modify a budget interval on a seamless line item

> [!NOTE]
> Do not modify the values of the `start_date` or `end_date` fields within the budget interval on the line item. The line item inherits its budget interval dates from the parent insertion order.

```
$ cat modify-budget-interval
{
    "line-item": {
        "budget_intervals": [
            {
                "parent_interval_id": 197186,
                "id": 219368,
                "lifetime_budget": 100
            },
            {
                "parent_interval_id": 197187,
                "id": 219369,
                "lifetime_budget": 100
            }
        ]
    }
}
curl -b cookies -X PUT -d @modify-budget-interval "https://api.appnexus.com/line-item?advertiser_id=608591&id=3319754"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": "3319754",
    "start_element": 0,
    "num_elements": 100,
    "line-item": {
      "id": 3319754,
      "code": null,
      "name": "Seamless Line Item Test",
      "advertiser_id": 608591,
      "state": "active",
      "start_date": null,
      "end_date": null,
      "timezone": "EST5EDT",
      "discrepancy_pct": 0,
      "publishers_allowed": "all",
      "revenue_value": 0,
      "revenue_type": "cpm",
      "goal_type": "none",
      "goal_value": null,
      "last_modified": "2016-09-01 17:44:32",
      "click_url": null,
      "currency": "USD",
      "require_cookie_for_tracking": true,
      "profile_id": null,
      "member_id": 958,
      "comments": null,
      "remaining_days": null,
      "total_days": null,
      "manage_creative": false,
      "creative_distribution_type": null,
      "line_item_type": "standard_v1",
      "prefer_delivery_over_performance": false,
      "advertiser": {
        "id": 608591,
        "name": "Don Test Advertiser"
      },
      "flat_fee": null,
      "delivery_goal": null,
      "labels": null,
      "broker_fees": null,
      "pixels": null,
      "insertion_orders": [
        {
          "id": 379643,
          "state": "inactive",
          "code": null,
          "name": "Seamless Insertion Order Test",
          "advertiser_id": 608591,
          "start_date": null,
          "end_date": null,
          "timezone": "EST5EDT",
          "last_modified": "2016-08-30 15:23:07",
          "currency": "USD",
          "budget_intervals": [
            {
              "id": 197186,
              "object_id": 379643,
              "object_type": "insertion_order",
              "start_date": "2016-09-01 00:00:00",
              "end_date": "2016-09-30 00:00:00",
              "timezone": "EST5EDT",
              "lifetime_budget": null,
              "lifetime_budget_imps": null,
              "daily_budget_imps": null,
              "daily_budget": null,
              "enable_pacing": false,
              "lifetime_pacing": false,
              "lifetime_pacing_pct": null
            },
            {
              "id": 197187,
              "object_id": 379643,
              "object_type": "insertion_order",
              "start_date": "2016-10-01 00:00:00",
              "end_date": "2016-10-31 00:00:00",
              "timezone": "EST5EDT",
              "lifetime_budget": null,
              "lifetime_budget_imps": null,
              "daily_budget_imps": null,
              "daily_budget": null,
              "enable_pacing": false,
              "lifetime_pacing": false,
              "lifetime_pacing_pct": null
            }
          ]
        }
      ],
      "goal_pixels": null,
      "imptrackers": null,
      "clicktrackers": null,
      "campaigns": null,
      "valuation": {
        "min_margin_pct": null,
        "max_avg_cpm": null,
        "min_avg_cpm": null,
        "goal_target": null,
        "goal_threshold": null,
        "no_revenue_log": false,
        "performance_mkt_managed": false,
        "bid_price_pacing_enabled": false,
        "bid_price_pacing_lever": 0,
        "goal_confidence_threshold": null
      },
      "creatives": null,
      "budget_intervals": [
        {
          "id": 219368,
          "object_id": 3319754,
          "object_type": "campaign_group",
          "start_date": "2016-09-01 00:00:00",
          "end_date": "2016-09-30 00:00:00",
          "timezone": "EST5EDT",
          "parent_interval_id": 197186,
          "lifetime_budget": 100,
          "lifetime_budget_imps": null,
          "lifetime_pacing": false,
          "enable_pacing": true,
          "daily_budget_imps": null,
          "daily_budget": null
        },
        {
          "id": 219369,
          "object_id": 3319754,
          "object_type": "campaign_group",
          "start_date": "2016-10-01 00:00:00",
          "end_date": "2016-10-31 00:00:00",
          "timezone": "EST5EDT",
          "parent_interval_id": 197187,
          "lifetime_budget": 100,
          "lifetime_budget_imps": null,
          "lifetime_pacing": false,
          "enable_pacing": true,
          "daily_budget_imps": null,
          "daily_budget": null
        }
      ],
      "expected_value_model": null,
      "custom_models": null,
      "inventory_discovery": null,
      "inventory_discovery_budget": null,
      "incrementality": null,
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "enable_pacing": null,
      "allow_safety_pacing": null,
      "lifetime_pacing": null,
      "lifetime_pacing_span": null,
      "lifetime_pacing_pct": null,
      "payout_margin": null
    },
    "dbg_info": {
      ...
    }
  }
}
```

> [!NOTE]
> This section applies only to Publisher Ad Server clients. Create a guaranteed delivery line item.
>
> Creating a Guaranteed Delivery line item requires that your line item/campaign combo meets all of the validations described in the [Delivery Goal](#delivery-goal) section above. Note that you will also need to associate the line item with a targeting [profile](profile-service.md).
>
> In this example we'll create a line item, and then a campaign associated with that line item.
>
> Always create the Line Item first. In order to avoid a race condition in the API, create your line item first, then the associated campaign.
>
> ```
> $ cat guaranteed-delivery-line-item.json
>      
> {
>     "line-item": {
>         "name": "Rich's Second Guaranteed Line Item - Impressions Delivery Goal",
>         "state": "inactive",
>         "lifetime_budget_imps": 10000,
>         "lifetime_pacing": true,
>         "enable_pacing": false,
>         "manage_creative": true,
>         "allow_safety_pacing": false,
>         "delivery_goal": {
>             "type": "impressions",
>             "disallow_non_guaranteed": true
>         },
>         "daily_budget": null,
>         "revenue_type": "cpm",
>         "start_date": "2015-05-15 00:00:00",
>         "end_date": "2015-05-20 00:00:00",
>         "lifetime_budget": null,
>         "publishers_allowed": "direct",
>         "campaigns": null
>     }
> }
> 
> $ curl -b cookies -X POST -d @guaranteed-delivery-line-item.json 'https://api.appnexus.com/line-item?advertiser_id=561703'
> ```
>
> Now that we have a Guaranteed Delivery line item, we need to create the associated campaign:
>
> ```
> $ cat campaign.json
> 
> 
> {
>     "campaign": {
>          "state": "inactive",
>          "name": "Rich's Guaranteed Campaign",
>          "advertiser_id": 41884,
>          "line_item_id": 232854,
>          "inventory_type": "direct"
>     }
> }
> 
> $ curl -b cookies -X POST -d @campaign.json 'https://api.appnexus.com/campaign?advertiser_id=561703'
> ```
>
> Keep in mind that if you associate only one campaign with a line item, the `start_date` and `end_date` for the campaign must both be set to `null`.

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

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
- [Campaign Service](campaign-service.md)
- [Conversion Pixel Service](conversion-pixel-service.md)
- [Insertion Order Service](insertion-order-service.md)
