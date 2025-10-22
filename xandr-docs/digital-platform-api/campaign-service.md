---
title: Campaign Service
description: In this article, learn about the Campaign service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Campaign service

A campaign is a way to organize a set of targeting parameters within our platform in combination with the [Profile Service](profile-service.md). The campaign object includes parameters such as flight dates and associated creatives whereas profiles target user and inventory parameters such as geography, segment, frequency, domain, and category.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | - [https://api.appnexus.com/campaign?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/campaign?advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/campaign?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/campaign?advertiser_code=ADVERTISER_CODE)<br>(campaign JSON) | Add a new campaign. |
| `PUT` |  - [https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/campaign?code=CAMPAIGN_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/campaign?code=CAMPAIGN_CODE&advertiser_code=ADVERTISER_CODE)<br>(campaign JSON) | Modify an existing campaign. |
| `GET` |  - [https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/campaign?code=CAMPAIGN_CODE&advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/campaign?code=CAMPAIGN_CODE&advertiser_code=ADVERTISER_CODE) | View a specific campaign for one of your advertisers. |
| `GET` | - [https://api.appnexus.com/campaign?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/campaign?advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/campaign?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/campaign?advertiser_id=ADVERTISER_ID<br>https://api.appnexus.com/campaign?advertiser_code=ADVERTISER_CODE) | View all of the campaigns for one of your advertisers. |
| `GET` | [https://api.appnexus.com/campaign?id=1,2,3](https://api.appnexus.com/campaign?id=1,2,3) | View multiple campaigns by ID using a comma-separated list.<br><br>**Note:** **Helpful Filters**<br> - You can filter for campaigns based on when they first and last served. This is particularly useful when you are approaching your [object limit](object-limit-service.md) and need to identify campaigns that can be deleted from the system. For more details, see [First Run/Last Run](#first-runlast-run).<br> - You can filter for campaigns that are not serving due to various conditions. For more details, see [Alerts](#alerts). |
| `GET` | [https://api.appnexus.com/campaign?search=SEARCH_TERM](https://api.appnexus.com/campaign?search=SEARCH_TERM) | Search for campaigns with IDs or names containing certain characters. |
| `DELETE` | [https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/campaign?id=CAMPAIGN_ID&advertiser_id=ADVERTISER_ID) | Delete a campaign.<br><br>**Caution:**<br>Deletion is permanent and cannot be reverted. Although deleted campaigns continue to be available in reporting, you will no longer have visibility into their specific settings (e.g., cost budget and targeting). |
| `GET` | [https://api.appnexus.com/campaign/meta](https://api.appnexus.com/campaign/meta) | Find out which fields you can filter and sort by. |

## JSON fields

### General

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the campaign.<br>**Required On:** `PUT`, in query string. |
| `State` | enum | The state of the campaign. Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `parent_inactive` | boolean | If `true`, the campaign is inactive due to the parent line item being inactive, and the campaign's `state` is overridden (i.e., if `"parent_inactive": "true"` and `"state": "active"`, then the campaign is inactive).<br><br>**Note:**<br>To return this field, the `advertiser_id` must be included in the query string.<br>**Default:** `false`<br>**Read Only.** |
| `code` | string (100) | A custom code for the campaign. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No 2 objects at the same level (e.g., line items or campaigns) can use the same code per advertiser. For example, 2 lines items cannot both use code "XYZ", but a single line item and its child campaign can. |
| `name` | string (255) | The name of the campaign.<br>**Required On:** `POST` |
| `short_name` | string (50) | The name used by the Imp Bus. |
| `advertiser_id` | int | The ID of the advertiser to which the campaign belongs.<br>**Required On:** `POST`/`PUT`, in query string. |
| `profile_id` | int | You may associate an optional `profile_id` with this campaign. A profile is a generic set of rules for targeting inventory. For details, see the [Profile Service](profile-service.md). |
| `line_item_id` | int | The ID of the line item to which the campaign is associated.<br><br>**Caution:**<br>No more than 500 campaigns can be associated to a single line item.<br><br>**Required On:** `POST` |
| `start_date` | timestamp | The date and time when the campaign should start serving. Null corresponds to "immediately". This value reflects the Advertiser's time zone.<br>**Default:** `null` |
| `end_date` | timestamp | The date and time when the campaign should stop serving. Null corresponds to "indefinitely". This value reflects the Advertiser's time zone.<br>**Default:** `null` |
| `creatives` | array | The list of creative IDs or codes associated to the campaign. Update only requires id or code to be passed in but `GET` request will include more creative fields for convenience. <br>For more information, see [Creatives](#creatives) and the [example](#creatives-example) below. |
| `creative_groups` | array of IDs | You may wish to bucket a group of creatives and then add them to a campaign all at once. Create groups through the [Line Item Service](line-item-service.md). |
| `timezone` | enum | The timezone of the campaign. For details and accepted values, see [API Timezones](api-timezones.md). If no timezone is set, this will default to the advertiser's timezone, which defaults to the member's timezone, which defaults to EST5EDT. Campaign daily budgets are reset at midnight in the timezone of the campaign, so this field determines that time.<br><br>**Note:**<br>Any `PUT` calls to the `advertiser` service which include `set_child_timezone=true` in the query string will cause any timezone settings on the lower level objects (e.g., insertion orders, line items, campaigns) to be overridden with the latest timezone value for that advertiser.<br><br>**Default:** The advertiser's timezone. |
| `last_modified` | timestamp | The time of last modification to this campaign. |
| `supply_type` | string | The types of supply targeted by this campaign, as defined by the `supply_type_targets` field in the associated [profile](profile-service.md). This string can contain one or more of the following values, separated by commas: web, mobile_web, and mobile_app.<br>**Read Only.** |
| `supply_type_action` | enum | Whether the types of supply are "included" or "excluded" from targeting, as defined by the `supply_type_action` field in the associated [profile](profile-service.md).<br>**Read Only.** |
| `inventory_type` | enum | The type of inventory targeted by this campaign. <br>Possible values: `"real_time"`, `"direct"`, or `"both"`. `"Real-time"` includes all third-party inventory not managed by your network that has been enabled for reselling including external supply partners such as Microsoft Advertising Exchange and Google Ad Manager. `"Direct"` includes only inventory managed by your network.<br><br>**Default:** `"real_time"` |
| `roadblock_creatives` | boolean | Only serve this campaign if all creatives attached to it, are able to serve on one page load.<br><br>**Note:**<br>Roadblocking is only enabled for direct inventory. If you attempt to set `roadblock_creatives` to `true` for an `inventory_type` other than `direct`, the API will return an error. |
| `roadblock_type` | enum | There are several types of roadblocks available. Allowed values are `"no_roadblock"`, `"normal_roadblock"` (where the number of creatives is greater than or equal to the number of placements), `"partial_roadblock"` (where the number of creatives is less than or equal to the number of placements), and `"exact_roadblock"` (where the number of creatives is equal to the number of available placements).<br><br>**Default:** `"no_roadblock"` |
| `stats` | object | The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `all_stats` | array | The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `comments` | string | Comments about the campaign. |
| `labels` | array of objects | The optional labels applied to the campaign. One label is currently available: "Test/Control". For more details, see [Labels](#labels) below.<br><br>**Tip:**<br>You can report on campaign labels with the [Network Analytics](network-analytics.md), [Network Advertiser Analytics](network-advertiser-analytics.md), and [Advertiser Analytics](advertiser-analytics.md) reports. For example, if you use the "Test/Control" label to specify the user group you are targeting (as defined by the user_group_targets field in the associated [profile](profile-service.md)), you could run the Network Analytics report filtered by "user_group_for_campaign" to focus on the campaigns that target a particular user group, or grouped by "user_group_for_campaign" to rank the performance of your user groups. |
| `broker_fees` | array | The fees that the network must pay to brokers when serving an ad. These fees are in addition to the cost of the inventory and are typically for data, ad serving, or creative hosting. They can either be a percentage of the media cost or a flat CPM. For more details, see [Broker Fees](#broker-fees) below. |
| `click_url` | string (1000) | The (optional) landing page URL for non-3rd party image and flash creatives. |
| `valuation` | object | An object containing several fields relating to performance goals and minimum margin. For more details, see [Valuation](#valuation) below. |
| `remaining_days` | int | The number of days between today and the `end_date` for the campaign. <br><br>**Note:** This will be null if the `start_date` is in the future or if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `total_days` | int | The number of days between the `start_date` and `end_date` for the campaign. <br><br>**Note:** This will be null if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `first_run` | timestamp | The date and time when the campaign first served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a GET response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they first served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `last_run` | timestamp | The date and time when the campaign last served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a GET response, pass `flight_info=true` in the query string. For details about how to filter line items based on when they last served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `alerts` | object | The conditions that are preventing the campaign from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional. For example, "State is set to inactive" is considered a pause, whereas "No creatives are associated with this campaign" is considered a warning. To retrieve campaigns based on pauses and/or warnings, you must pass certain query string parameters in the GET request. For more details, including a complete list of possible pauses and warnings, see [Alerts](#alerts) below.<br>**Read Only.** |
| `creative_distribution_type` | enum | When multiple creatives of the same size are trafficked via a line item, this field's setting is used to determine the creative rotation strategy that will be used. Note that creatives must be managed on the campaign in order to use this field. Allowed values:<br> - **even:** The default. Use our standard creative optimization algorithm, where each creative's valuation is computed independently, and the best-valued creative is chosen to serve.<br> - **weighted:** Creative rotation is based on a user-supplied weight.<br> - **ctr-optimized:** The creative with the highest CTR delivers the most.<br>**Default:** `"even"` |
| `is_archived` | boolean | **Read-only.** Indicates whether the campaign has been automatically archived due to not being used. Once set to `true`, the value can't be changed and the only calls that can be made on the campaign object are `GET` and `DELETE`.<br><br>**Note:**<br>If a campaign is automatically archived, its profile will also be archived. If the campaign's parent line item is automatically archived, all campaigns (as well as their profiles) under that line item will also be archived. Once archived, the only calls that may be made on these objects are `GET` and `DELETE`. In addition, once archived, the campaign may not be associated with any line items.<br><br>**Default:** `false` |
| `archived_on` | timestamp | **Read-only.** The date and time on which the campaign was archived (i.e., when the `is_archived` field was set to `true`).<br><br>**Default:** `null` |

#### `creatives` example

```
[{"id": 233,"state":"active","code":"abc","name":"test","width":200,"height":200,
"audit_status":"pending","is_expired":true,
"is_prohibited":false,"is_self_audited:true,
"format":"image","pop_window_maximize":false}]
```

### Pricing/budgeting

| Field | Type | Description |
|:---|:---|:---|
| `lifetime_budget` | double | The lifetime budget in dollars (media cost). Null corresponds to "unlimited".<br><br>**Caution:**<br>If `lifetime_budget` is set to `null` (unlimited), and the line item and insertion order lifetime budgets are also set to `null`, severe overspend can occur.<br>**Default:** `null` |
| `lifetime_budget_imps` | int | The lifetime budget in impressions. Null corresponds to "unlimited".<br>**Default:** `null` |
| `daily_budget` | double | The daily budget in dollars (media cost). Null corresponds to "unlimited".<br>**Default:** `null` |
| `daily_budget_imps` | int | The daily budget in impressions. Null corresponds to "unlimited".<br>**Default:** `null` |
| `learn_budget` | double | The lifetime dollar (media cost) budget allocated to learning. Null corresponds to "unlimited".<br>**Default:** `null` |
| `learn_budget_imps` | int | The lifetime impression budget allocated to learning. Null corresponds to "unlimited".<br>**Default:** `null` |
| `learn_budget_daily_cap` | double | The maximum number of dollars (media cost) that can be allocated to learning per day. Null corresponds to "unlimited".<br>**Default:** `null` |
| `learn_budget_daily_imps` | int | The maximum number of impressions that can be allocated to learning per day. Null corresponds to "unlimited".<br>**Default:** `null` |
| `enable_pacing` | boolean | If `true`, the campaign's daily budgeted spend is spread out evenly throughout each day. This is only applicable if `daily_budget` is set. For more details about even daily pacing, see "Daily Pacing" in the UI documentation.<br>**Default:** `false` |
| `lifetime_pacing` | boolean | If `true`, the campaign will attempt to spend its overall lifetime budget evenly over the campaign flight dates. If true, you cannot set a `daily_budget`, you cannot set `enable_pacing` to false, and you must first establish a `lifetime_budget`, a `start_date`, and an `end_date` for the campaign.<br>**Default:** `false` |
| `lifetime_pacing_span` | int | In the event of an underspend event, this indicates the number of days across which the underspent amount will be distributed. The default value of `null` indicates a value of three (3) days.<br>**Default:** `null` |
| `priority` | int | For a campaign targeting direct inventory (`inventory_type` is `"direct"`), since you have already paid for inventory, there is no need to input a buying strategy. However, you can set the campaign's priority to weight the campaign against other direct campaigns within your account. The campaign with the highest priority will always win, even if a lower priority campaign bids more. For more information about managing priority, see "Bidding Priority" in the UI documentation.<br>**Default:** `5` |
| `cadence_modifier_enabled` | boolean | If `true`, bids will be adjusted upward and downward based on the frequency and recency of the user. Typically, bids are increased for low frequency-recency impressions and decreased for high frequency-recency users. This feature is based on the idea that the effectiveness of an ad differs when a user hasn't seen the ad before, hasn't seen it many times, or hasn't seen it recently. For more details, see "Cadence Modifier and the Chaos Factor" in the UI documentation.<br>**Default:** `false` |
| `expected_pacing` | double | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `total_pacing` | double | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_dollars` | enum | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `has_pacing_imps` | enum | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `imps_pacing_percent` | int | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |
| `media_cost_pacing_percent` | int | **Deprecated.**<br>**Note:**<br>The `stats` object and Quickstats have been deprecated (as of October 17, 2016). |

### Bidding strategies

| Field | Type | Description |
|:---|:---|:---|
| `cpm_bid_type` | enum | Possible values:<br> - `"base"`: Bid a fixed amount.<br> - `"average"`: Bid Estimated Average Price (EAP), an estimate of the price that is likely to win about 50% of the impressions from our platform sellers based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.) conduct a secondary auction, bidding EAP does not necessarily ensure winning half of off-platform impressions.<br> - `"clearing"`: Bid Estimated Clear Price (ECP), an estimate of the price that is likely to win most impressions from our platform sellers based on historical bids and their success or failure. Since off-platform sellers (e.g., Google Ad Manager, Rubicon, etc.) conduct a secondary auction, bidding ECP does not necessarily ensure winning off-platform impressions.<br> - `"predicted"`: Vary bids based on the likelihood of a click or conversion for each piece of inventory. For predicting CPC, use `cpc_goal`. For predicting CPA, see [Pixels](#pixels) below.<br> - `"margin"`: Bid a % margin of the revenue that the advertiser pays you. See `bid_margin`.<br> - `"custom_model"`: Calculate your bid price based on a custom predictive model. You set which model to use in the `bid_model` object. For more details, see [Custom Models](../data-science-toolkit/custom-models.md).<br><br>**Note:** You can set `cpm_bid_type` to `"custom_model"` only when `inventory_type` is `"rtb"`.<br><br> - `"none"`: None is available only if you pay on a per-click or per-conversion basis, and it will result in not being able to bid CPM.<br>**Required On:** `POST`, unless `inventory_type` is set to `"direct"`. |
| `base_bid` | double | A CPM bid. May be modified by the `cadence_modifer`.<br>**Required On:** `POST`, if `cpm_bid_type` is `"base"`. |
| `min_bid` | double | Set a minimum bid that will apply to variable pricing models (See `cpm_bid_type`). |
| `max_bid` | double | Set a maximum bid that will apply to variable pricing models (See `cpm_bid_type`). |
| `bid_margin` | double | The percent margin of the revenue that the advertiser pays you. For example, if your booked revenue is $1 CPM, and you set a bidding strategy margin of 25%, your campaign will bid $0.75. If your booked revenue type is a CPA or CPC goal, it will apply your desired margin and optimize to that predicted goal.<br>**Required On:** `POST`, if `cpm_bid_type` is `"margin"`. |
| `cpc_goal` | double | You may wish to vary bids based on the likelihood of some conversion event, either a click or an acquisition, for that particular inventory, in order to attain a specific cost per click or cost per acquisition. In this case, our platform's algorithm determines a bid based on past conversion rates and based on how much you value a conversion, whether you define it as a click or an acquisition (registration, purchase, etc.).<br>**Required On:** `POST`, if `cpm_bid_type` is `"predicted"` and the `roi_click_goal` and `roi_view_goal` are not set in the `pixels` array. |
| `max_learn_bid` | double | When using the `cpm_bid_type` `"predicted"`, the optimization engine submits "learn" bids to learn about new inventory. If necessary, enter the max CPM dollar amount for these bids.<br><br>**Note:**<br>When you set both `max_learn_bid` for learn bids and `max_bid` for non-learn bids, the lower of the two will be used for learn.<br>**Default:** `null` |
| `pixels` | array | If using a CPA Bidding Strategy, the pixel array is used to associate conversion pixels with the campaign and set CPA goals and payout values for the pixels. For more details, see [Pixels](#pixels) below. |
| `bid_model` | object | If using a custom predictive model to determine bid prices, this object is used to associate your custom model with the campaign. For more details, see [Bid Model](#bid-model) below.<br>**Default:** `null`<br>**Required On:** `POST`, if `cpm_bid_type` is `"custom_model"`. |

### Optimization levers

These optional fields give advanced users extra control over optimizing their campaigns. For detailed information on these fields, see "Optimization Levers" in the UI documentation.

> [!TIP]
> If you would like access to optimization levers, a Xandr admin must set the `expose_optimization_levers` field to `true` for your [member](member-service.md). For more details, contact your account representative.

| Field | Type | Description |
|:---|:---|:---|
| `ecp_learn_divisor` | string | **Deprecated.** This feature is not supported in version 7 of the Optimization engine. For newer ways to adjust learn bids, see `learn_override_type`.<br>**Default:** `null (3)` |
| `projected_learn_events` | int | **Deprecated.** This feature has been incorporated into the learn algorithm for version 7 of the Optimization engine.<br>**Default:** `null (3)` |
| `learn_threshold` | int | The number of successful events (clicks or conversions) required before moving from the learn stage to the optimized stage. Possible values: 1 - 100.<br>**Default:** `null (3)` |
| `max_learn_bid` | double | When using the `cpm_bid_type` "predicted", the optimization engine submits "learn" bids to learn about new inventory. If necessary, enter the max CPM dollar amount for these bids. <br><br>**Note:** When you set both `max_learn_bid` for learn bids and `max_bid` for non-learn bids, the lower of the two will be used for learn.<br><br>**Default:** `null` |
| `cadence_type` | enum | The level at which the cadence modifier is applied. Possible values: `"advertiser"` or `"creative"`.<br>**Default:** `"advertiser"` |
| `defer_to_li_prediction` | boolean | If true, this campaign will temporarily change the level at which it learns while maintaining a specified profit margin percentage. See "Optimization Levers" in the UI documentation for more details.<br>**Default:** `false` |
| `optimization_lookback` | array of objects | Optimization is based on the last 30 days of data, evenly weighted. You can use this field to give more weight to certain days within that window. <br>Possible values for `"day"`: 0 - 29. <br>Possible values for `"bias_percent"`: 0 - 100. <br>For more details, see [example](#optimization_lookback-example) below. |
| `optimization_version` | string | Indicates the version of optimization currently in use.<br>**Default:** `v7`<br>**Read Only.** |
| `learn_override_type` | enum | If you want to override our algorithm's learn bid, this is the type of bid to submit instead. Possible values:<br> - `"base_cpm_bid"`: A flat CPM bid. You specify the CPM value in the `base_cpm_bid_value` field.<br> - `"venue_avg_cpm_bid"`: The average bid for each venue.<br>**Default:** `null` |
| `base_cpm_bid_value` | double | The CPM value to use for learn bids, when `learn_override_type` is `"cpm_learn_bid"`. This value cannot be greater than 10.0.<br>**Default:** `null`<br>**Required On:** `POST`/`PUT`, if `learn_override_type` is `"base_cpm_bid"`. |
| `bid_multiplier` | double | The value by which to multiply the learn bid. This can be used for our algorithm's default learn bid or an override learn bid when `learn_override_type` is `"venue_average_cpm_bid"`. This value cannot be greater than `10.0`.<br>**Default:** `1.0` |
| `impression_limit` | int | For a specific venue, the number of impressions after which to stop overriding our algorithm's learn bid. This value must be greater than 0.<br>**Default:** `40000` |
| `campaign_modifiers` | array of objects | An array of objects containing the segment modifier-related settings associated with this campaign (format shown below). For more information, see "Segment Modifier" in the UI documentation.<br><br>**Note:**<br>You cannot set both `campaign_modifier` and `bid_modifier_model` in a single campaign.<br>For more details, see [example](#campaign_modifiers-example) below. |
| `bid_modifier_model` | object | The custom predictive model to apply multipliers to the campaign's optimization-derived CPM bid. This type of model is used in conjunction with our optimization-based buying strategy (when `cpm_bid_type` is `"predicted"` or `"margin"`).<br>For more details, see [Bid Modifier Model](#bid-modifier-model) below.<br><br>**Note:**<br>You can set `bid_modifier_model` only when `inventory_type` is `"rtb"`. Also, you cannot set both `bid_modifier_model` and `campaign_modifier` in a single campaign.<br>**Default:** `null` |

#### `optimization_lookback` example

```
"optimization_lookback":[
{
"day":8,
"bias_percent":10
},
{
"day":12,
"bias_percent":11
}
],
```

#### `campaign_modifiers` example

```
{
"campaign":
{
"id":123,
"name":"ModifiedCampaign",
"campaign_modifiers":[
{
"type":"segment_modifier_id",
"value":456
},
{
"type":"segment_price_id",
"value":789
},
{
"type":"segment_modifier_weight",
"value":1200
}
]
}
}
```

### Broker fees

When a network uses a broker to serve an impression, it pays a fee to the broker for that service. This value varies between different networks, different brokers, and different campaigns. Therefore, the network must specify how much it will pay each broker it uses. This can also be done at the Line Item level ([Line Item Service](line-item-service.md)) or at the Insertion Order level ([Insertion Order Service](insertion-order-service.md)).

To create or edit brokers, refer to the [Broker Service](broker-service.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `broker_id` | int | The ID of the broker. |
| `broker_name` | string | The name of the broker.<br>**Read Only.** |
| `payment_type` | enum | Type of payment to the broker. <br>Possible values: `"cpm"` or `"revshare"`. |
| `value` | double | The value of the payment, based on the payment type. |
| `description` | string (255) | The free-form description of the broker fee entry. |

#### Add a broker fee

```
$ cat add-broker-fees.json
{
    "campaign":
        {
    "broker_fees":[
        {
                "broker_id": 145,
                "broker_name": "Test 3",
                "payment_type": "cpm",
                "value": "1.00",
                "description": "JMS fee"
            }]
    }
}

$ curl -b cookies -c cookies -X PUT -d @add-broker-fees.json 'https://api.appnexus.com/campaign?id=376737&advertiser_id=35081'

{
    "response":{
         "status":"OK",
         "id":"376737",
         "count":1,
         "start_element":0,
         "num_elements":100,
        }
}
```

#### Modify a broker fee

```
$ cat modify-broker-fee.json
{
"campaign" :
{ "broker_fees": [
    {
        "broker_id": 145,
        "payment_type": "cpm",
        "value": "3.00",
        "description": "New JMS fee"
        }]
    }
}

$ curl -b cookies -c cookies -X PUT -d @modify-broker-fee.json 'https://api.appnexus.com/campaign?id=376737&advertiser_id=35081'

{
    "response":{
        "status":"OK",
        "id":"376737",
        "count":1,
        "start_element":0,
        "num_elements":100,
        
```

### Creatives

Each object in the `creatives` array includes the following fields. To obtain information for `"id"` or `"code"` fields, you can use the [Creative Service](creative-service.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative. Either `"id"` or `"code"` is required when updating creative association.<br>**Required On:** `PUT` |
| `code` | string | The custom code for the creative. Either `"id"` or `"code"` is required when updating creative association.<br>**Required On:** `PUT` |
| `name` | string | The name of the creative.<br>**Read Only.** |
| `width` | int | The width of the creative.<br>**Read Only.** |
| `height` | int | The height of the creative.<br>**Read Only.** |
| `state` | enum | The state of the creative. <br>Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `audit_status` | enum | The audit status of the creative. <br>Possible values: `"no_audit"`, `"pending"`, `"rejected"`, `"audited"`, or `"unauditable"`.<br>**Read Only.** |
| `is_expired` | boolean | Whether the creative is expired. If `false`, the creative is active.<br>**Read Only.** |
| `is_prohibited` | boolean | Whether the creative falls into a prohibited category on our platform. |
| `is_self_audited` | boolean | Whether the creative is self-audited. If `true`, then yes. <br>**Read Only.** |
| `format` | enum | The format of the creative file. <br>Possible values: `"url-html"`, `"url-js"`, `"flash"`, `"image"`, `"raw-js"`, `"raw-html"`, `"iframe-html"`, or `"text"`.<br>**Read Only.** |
| `weight` | int | A user-supplied weight that determines the creative rotation strategy for same-sized creatives managed at the campaign level. To use this field, the value of `creative_distribution_type` must be `"weighted"`. <br>Allowed value: An integer greater than `0` and less than or equal to `1000`. |
| `pop_window_maximize` | boolean | If `true`, the publisher's tag will maximize the window. Only relevant for creatives with format `"url-html"` and `"url-js"`. If `pop_window_maximize` is set to `true`, then neither `"height"` nor `"width"` should be set on the creative.<br>**Read Only.** |

### Valuation

The `valuation` object contains the following fields related to minimum margin. For more information on minimum margin, see "Using Minimum Margin to Balance Margin and Delivery" in the UI documentation.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `min_margin_rtb_pct` | decimal | The minimum margin PCT on RTB inventory. Overrides what is set in the line item.<br>**Default:** `null` |
| `eap_multiplier` | decimal | The EAP multiplier value. Can only be used on inventory types "real_time" or "both".<br>**Default:** `1.000000` |

### Stats

> [!CAUTION]
> The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

### Labels

Each object in the `labels` array includes the following fields.

> [!NOTE]
> You can use the read-only [Label Service](label-service.md) to view all possible labels for campaigns, advertisers, insertion orders, line items, and publishers. This service also allows you to view the labels that have already been applied to your objects.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the label. Possible value: 9 (Test/Control). |
| `name` | enum | The name of the label. This field is read-only. Possible value: "Test/Control". |
| `value` | string (100) | The value assigned to the label. This could be the name of the `user_group_target` in the associated [profile](profile-service.md). |

### Pixels

> [!NOTE]
> Before you can associate a pixel to a campaign, the pixel must already be attached to the parent line item. Also, if `cpc_bid_type` is `"predicted"` and `cpc_goal` is not set, you must provide a value for either `roi_click_goal` or `roi_view_goal`.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the conversion pixel. |
| `state` | enum | The state of the conversion pixel. Possible values: `"active"` or `"inactive"`. |
| `name` | string | **Read-only.** The name of the conversion pixel. |
| `roi_click_goal` | double | If paying on a per-impression (CPM) basis and optimizing to a predicted CPA goal, set this field to the click goal. |
| `roi_view_goal` | double | If paying on a per-impression (CPM) basis and optimizing to a predicted CPA goal, set this field to the view goal. |
| `click_payout` | double | If paying on per-conversion (CPA) basis, set this field to the amount to pay the publisher per click. |
| `view_payout` | double | If paying on a per-conversion (CPA) basis, set this field to the amount to pay the publisher per view. |

### Bid model

The `bid_model` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the custom model. Only custom models with `model_output` set to `"Bid"` are allowed. Use the [Custom Model Service](../data-science-toolkit/custom-model-service.md) to retrieve these IDs. |
| `name` | string | The name of the custom model.<br>**Read Only.** |
| `active` | Boolean | The status of the model. Possible values: `1` (true) or `0` (false).<br>**Read Only.** |

### Bid modifier model

The `bid_modifier_model` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the custom model. Only customs models with `model_output` set to `"bid_modifier"` are allowed. Use the [Custom Model Service](../data-science-toolkit/custom-model-service.md) to retrieve these IDs. |
| `name` | string | The name of the custom model.<br>**Read Only.** |
| `active` | Boolean | The status of the model. Possible values: `1` (true) or `0` (false).<br>**Read Only.** |

### First run/last run

To include the `first_run` and `last_run` fields in a `GET` response, pass `flight_info=true` in the query string. You can also filter for campaigns based on when they first and last served, as follows:

#### Retrieve only campaigns that have never served

Pass `never_run=true` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&never_run=true'
```

> [!NOTE]
> You can use `never_run=true` in combination with other filters, but be aware that it will always be an OR relationship. For example, if you pass both `never_run=true` and `min_first_run=2012-01-01 00:00:00` in the query string, you will be looking for campaigns that have never served OR line items that first served on or after 2012-01-01.

#### Retrieve only campaigns that first served on or after a specific date

Pass `min_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&min_first_run=2012-01-01+00:00:00'
```

#### Retrieve only campaigns that first served on or before a specific date

Pass `max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&max_first_run=2012-08-01+00:00:00'
```

#### Retrieve only campaigns that first served within a specific date range

Pass `min_first_run=YYYY-MM-DD HH:MM:SS&max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&min_first_run=2012-01-01+00:00:00&max_first_run=2012-08-01+00:00:00'
```

#### Retrieve only campaigns that last served on or after a specific date

Pass `min_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&min_last_run=2012-01-01+00:00:00'
```

#### Retrieve only campaigns that last served on or before a specific date

Pass `max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&max_last_run=2012-08-01+00:00:00'
```

#### Retrieve only campaigns that last served within a specific date range

Pass `min_last_run=YYYY-MM-DD HH:MM:SS&max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/campaign?advertiser_id=100&flight_info=true&min_last_run=2012-01-01+00:00:00&max_last_run=2012-08-01+00:00:00'
```

### Alerts

This field notifies you of conditions that are preventing the campaign from serving. There are two types of alerts: pauses and warnings. Pauses are considered intentional and user-driven, whereas warnings are considered unintentional. For example, "State is set to inactive" is considered a pause, whereas "No creatives are associated with this campaign" is considered a warning.

To retrieve campaigns based on pauses and/or warnings, you must pass certain query string parameters in the `GET` request. See below for use cases with query string parameters and examples. Note that you can use these query string parameters both when retrieving all campaigns or specific campaigns, but the examples below only cover retrieving all campaigns, as that is where this feature offers the most value.

#### Retrieve all campaigns and show alerts

Pass `show_alerts=true` in the query string. This parameter will add the `alerts` object to every campaign in the response, whether or not the campaign has pauses or warnings.

> [!NOTE]
> For each of the use cases below, you must pass `show_alerts=true` if you want the `alerts` object to show up in the response.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 2,
                            "message": "Parent line item is inactive."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58991,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58992,
                "state": "inactive",
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
                            "message": "Parent line item is inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have at least one pause

Pass `show_alerts=true&pauses=true` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=true'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 8,
                            "message": "Flight end is in the past."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "inactive",
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
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have no pauses

Pass `show_alerts=true&pauses=false` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=false'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58991,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58992,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 2,
                            "message": "All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited)."
                        }
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have a specific pause

Pass `show_alerts=true&pauses=PAUSE_ID` in the query string. For pause IDs, see the [Pauses](#pauses) table below.

In this example, we use pause ID 4 to retrieve all campaigns with flight start dates that are in the future.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=4'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 66493,
                "state": "inactive",
                "start_date": "2012-10-01 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 15:01:02"
                }
            },
            {
                "id": 66510,
                "state": "active",
                "start_date": "2012-9-01 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 2,
                            "message": "Parent line item is inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 15:01:02"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have two or more specific pauses

Pass `show_alerts=true&pauses=SUM_OF_PAUSE_IDS` in the query string. For pause IDs, see the [Pauses](#pauses) table below.

In this example, we add together pause ID 1 and pause ID 2 to retrieve all campaigns that are set to inactive and whose line items are also set to inactive.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=3'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 66493,
                "state": "inactive",
                "start_date": "2012-10-01 00:00:00",
                "end_date": null,
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 2,
                            "message": "Parent line item is inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 15:01:02"
                }
            },
            {
                "id": 66510,
                "state": "inactive",
                "start_date": "2012-9-01 00:00:00",
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
                            "message": "Parent line item is inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 15:01:02"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have at least one warning

Pass `show_alerts=true&warnings=true` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&warnings=true'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 2,
                            "message": "All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited)."
                        },
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have no warnings

Pass `show_alerts=true&warnings=false` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&warnings=false'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
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
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58991,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58992,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have a specific warning

Pass `show_alerts=true&warnings=WARNING_ID` in the query string. For warning IDs, see the [Warnings](#warnings) table below.

In this example, we use warning ID 1 to retrieve all campaigns that have no associated creatives.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&warnings=1'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have at least one pause AND at least one warning

Pass `show_alerts=true&pauses=true&warnings=true` in the query string.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=true&warnings=true'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 2,
                            "message": "Parent line item is inactive."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 58993,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 2,
                            "message": "All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited)."
                        }

                    ],
                    "pauses": [
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have a specific pause AND a specific warning

Pass `show_alerts=true&pauses=PAUSE_ID&warnings=WARNING_ID` in the query string. For pause and warning IDs, see the [Pauses](#pauses) and [Warnings](#warnings) tables below.

In this example, we retrieve all campaigns that have a flight start date in the future (pause ID 4) AND that do not have any associated creatives (warning ID 1).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=4&warnings=1'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58990,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        },
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

#### Retrieve only campaigns that have pauses OR warnings

You can combine the parameters described above with `alert_boolean_op=or`to retrieve campaigns that have certain pauses OR certain warnings. See the [examples](#examples) below. For pause and warning IDs, see [Pauses](#pauses) and [Warnings](#warnings) tables below.

> [!NOTE]
> The `alert_boolean_op=or`parameter can be used only to retrieve campaigns with pauses OR warnings. It cannot be used to look for OR relationships between pauses (i.e., pause 1 OR pause 2) or between warnings (i.e., warning 1 OR warning 2).

In this example, we retrieve all campaigns that are set to inactive (pause ID 1) OR that do not have any eligible creatives (warning ID 2).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=1&warnings=2&alert_boolean_op=or'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58934,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 2,
                            "message": "All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited)."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "inactive",
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
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

In this example, we retrieve all campaigns that are set to inactive (pause ID 1) OR that have no warnings.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=1&warnings=false&alert_boolean_op=or'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58934,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "inactive",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [
                        {
                            "id": 1,
                            "message": "State is set to inactive."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

In this example, we retrieve all campaigns that have no pauses OR that have no warnings.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=false&warnings=false&alert_boolean_op=or'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58934,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [

                    ],
                    "pauses": [
                        {
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            ...
        ],
        ...
        }
    }
}
```

In this example, we retrieve all campaigns that are set to inactive (pause ID 1) AND whose parent line item is set to inactive (pause ID 4) OR that have no associated creatives (warning ID 1).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?show_alerts=true&pauses=5&warnings=1&alert_boolean_op=or'

{
    "response": {
        "status": "OK",
        "campaigns": [
            {
                "id": 58934,
                "state": "inactive",
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
                            "id": 4,
                            "message": "Flight start is in the future."
                        }
                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
                }
            },
            {
                "id": 81287,
                "state": "active",
                ...
                "alerts": {
                    "warnings": [
                        {
                            "id": 1,
                            "message": "No creatives are associated with this campaign."
                        }
                    ],
                    "pauses": [

                    ],
                    "warnings_last_checked": "2012-07-27 14:40:36",
                    "pauses_last_checked": "2012-08-08 13:01:03"
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
|---|---|
| 1 | State is set to inactive. |
| 2 | Parent line item is inactive. |
| 4 | Flight start is in the future. |
| 8 | Flight end is in the past. |

### Warnings

| ID | Description |
|---|---|
| 1 | No creatives are associated with this campaign. |
| 2 | All creatives associated to this campaign are either ineligible to serve (inactive, expired, prohibited) or can serve only on direct inventory and on supply partners who trust your network's self-classification (unaudited). |

## Examples

### View campaign 17607 for advertiser 9

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/campaign?id=17607&advertiser_id=11'

{
    "response": {
        "status": "OK",
        "campaign": {
            "id": 167051,
            "state": "inactive",
            "code": null,
            "advertiser_id": 11,
            "line_item_id": 69405,
            "creative_id": 851325,
            "pixel_id": 16688,
            "short_name": null,
            "name": "My example campaign",
            "profile_id": 752909,
            "start_date": "2011-10-31 00:00:00",
            "end_date": null,
            "timezone": "EST5EDT",
            "priority": 5,
            "cadence_modifier_enabled": true,
            "cpc_goal": null,
            "cpm_bid_type": "predicted",
            "base_bid": null,
            "min_bid": null,
            "max_bid": null,
            "bid_margin": 0,
            "roadblock_creatives": false,
            "roadblock_type": "no_roadblock",
            "inventory_type": "real_time",
            "last_modified": "2014-05-28 16:06:01",
            "max_learn_bid": null,
            "cadence_type": "creative",
            "click_url": null,
            "require_cookie_for_tracking": true,
            "allow_unverified_ecp": false,
            "defer_to_li_prediction": false,
            "ecp_learn_divisor": "3.000000",
            "projected_learn_events": "3",
            "learn_threshold": 3,
            "cpc_payout": null,
            "comments": null,
            "optimization_version": "v7",
            "learn_override_type": null,
            "base_cpm_bid_value": null,
            "impression_limit": 40000,
            "bid_multiplier": 1,
            "remaining_days": null,
            "total_days": null,
            "supply_type_action": "include",
            "supply_type": "mobile_web, web",
            "creatives": [
                {
                    "id": 445832,
                    "code": null,
                    "name": "Donate car.png",
                    "width": "300",
                    "height": "250",
                    "state": "inactive",
                    "audit_status": "no_audit",
                    "is_expired": true,
                    "is_prohibited": false,
                    "is_self_audited": true,
                    "format": "image",
                    "pop_window_maximize": null
                }
            ],
            "pixels": [
                {
                    "id": 16688,
                    "roi_click_goal": 5,
                    "roi_view_goal": 5,
                    "click_payout": null,
                    "view_payout": null,
                    "code": null,
                    "name": "123",
                    "state": "active",
                    "trigger_type": "hybrid"
                }
            ],
            "optimization_lookback": [
                {
                    "day": "0",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "1",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "2",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "3",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "4",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "5",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "6",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "7",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "8",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "9",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "10",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "11",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "12",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "13",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "14",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "15",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "16",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "17",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "18",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "19",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "20",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "21",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "22",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "23",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "24",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "25",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "26",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "27",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "28",
                    "bias_percent": "50.000000"
                },
                {
                    "day": "29",
                    "bias_percent": "50.000000"
                }
            ],
            "campaign_modifiers": null,
            "labels": [
                {
                    "id": "9",
                    "name": "Test/Control",
                    "value": "Test pattern - Group 1"
                }
            ],
            "broker_fees": null,
            "valuation": null,
            "lifetime_budget": 16000,
            "lifetime_budget_imps": null,
            "daily_budget": 500,
            "daily_budget_imps": null,
            "enable_pacing": true,
            "allow_safety_pacing": true,
            "lifetime_pacing": false,
            "lifetime_pacing_span": null
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
}
```

### Create a direct campaign

This code represents the minimum information required to create an inactive campaign for direct inventory with no creatives and no targeting.

```
$ cat create-campaign.json

{
    "campaign": {
    "state": "inactive",
    "name": "Rich's cool campaign",
    "advertiser_id": 11,
    "line_item_id": 47726,
    "inventory_type": "direct"
    }
}
```

```
$ curl -b cookies 'https://api.appnexus.com/campaign?advertiser_id=11'
{
  "response": {
    "status": "OK",
    "id": 11,
    "dbg_info": {
      ...
    }
  }
}
        
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
