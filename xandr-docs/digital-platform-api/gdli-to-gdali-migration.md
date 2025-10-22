---
title: GDLI to GDALI Migration
description: This article explains the differences between the legacy GDLI and the new GDALI, and provides links to the resources needed to migrate to GDALIs.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# GDLI to GDALI migration

## Overview

Xandr offers Guaranteed Delivery Augmented Line Item (GDALI) that is based on our Augmented Line Item (ALI) and associated with the Seamless Insertion Order. The GDALI offers similar features to the legacy Guaranteed Delivery Line Item (GDALI), but by consolidating onto the ALI framework, we will be able to simplify the API, provide Ad Ops with a more intuitive workflow and user experience, and improve on the feature set available to guaranteed delivery line items.  

This document explains the differences between the legacy GDLI and the current GDALI and provide links to the resources you'll need to migrate to using GDALIs.

## What changed?

The GDALI uses the same insertion order and line item service endpoints as the legacy GDLI. But we've updated and added new fields and logic to both the insertion order and line item objects to enable the GDALI features.

## Insertion order changes

> [!NOTE]
> For an insertion order to be associated with a guaranteed delivery augmented line item (GDALI), the insertion order must:
>
> - Be a [Seamless Insertion Order](./insertion-order-service.md) (legacy insertion orders are not compatible).
> - Have `budget_type` set to `"flexible"` or `"impression"`.
> - Not contain more than one budget_intervals array.
> - Have unlimited budget (set via the `budget_intervals` array).
>
> Insertion orders not matching the above may only be associated to non-guaranteed line items. Note the above settings are also required for programmatic guaranteed line items (PGLI). An insertion order with the above settings may also be associated to non-guaranteed line items.
>
> Associating a profile_id (e.g., frequency capping or setting additional targeting) on the insertion order object may result in unexpected forecasting or delivery for PGLIs and GDALIs. It is recommended not to use `profile_id` for insertion orders intended for the use with GDALIs.

| Feature | Legacy Setting | New Setting |
|:---|:---|:---|
| Budget Type | Budget type was specified on the insertion order object but was not required. See [Example for Budget Type - Legacy setting](#example-for-budget-type---legacy-setting) below.| Budget type is specified on the insertion order object and must be set to `"flexible"` or `"impression"` for the insertion order to be compatible with GDALI and PG line items. See [Example for Budget Type - New setting](#example-for-budget-type---new-setting) below |
| Flight Dates and Budgeting | Flight dates and budgets were specified on the insertion order object. See [Example for flight dates and budgeting - Legacy setting](#example-for-flight-dates-and-budgeting---legacy-setting)  | Flight dates and budgets are specified within the `budget_intervals` property on the insertion order object. <br><br>**Note**: <br> - The insertion order must not contain more than one `budget_intervals` array.<br> - GDALI and PG line items require an "unlimited" budget set on the insertion order. Budget fields may be omitted or set to `null`.<br> - The `allow_safety_pacing` field is no longer used. See [Example for flight dates and budgeting - New setting](#example-for-flight-dates-and-budgeting---new-setting).|
| `Profile` | Profile was not supported on legacy insertion orders. | Use of the `profile_id` on the insertion order is not recommended, as use may result in unexpected forecasting results or delivery. |

### Example for budget type - Legacy setting

```
{
...,
"budget_type": null
}
```

### Example for budget type - New setting

```
{
...,
"budget_type": "impression"
}
```

### Example for flight dates and budgeting - Legacy setting

```
{
...,
"start_date": "2020-10-01 00:00:00",
"end_date": null,
"timezone": "UTC",
"lifetime_pacing": null,
"lifetime_budget": null,
"lifetime_budget_imps": null,
"enable_pacing": null,
"lifetime_pacing_span": null,
"allow_safety_pacing": null,
"daily_budget": null,
"daily_budget_imps": null,
"lifetime_pacing_pct": null,
...
}
```

### Example for flight dates and budgeting - New setting

```
{
...,
"budget_intervals": [
{
"start_date": "2020-10-01 00:00:00",
"end_date": null,
"timezone": "UTC",
"lifetime_budget": null,
"lifetime_budget_imps": null,
"daily_budget_imps": null,
"daily_budget": null,
"enable_pacing": false,
"lifetime_pacing": false,
"lifetime_pacing_pct": null
...
}
]
}
```

### Examples

> [!TIP]
> See [Publisher GDALI API Setup Guide](./publisher-gdali-api-setup-guide.md) for a step-by-step API guide for creating a GDALI.

#### Example legacy IO for GDLI API setup

1. Create Legacy IO JSON (you'll need an existing advertiser ID).

    ```
    $ cat legacy_io_gdli
    {
    "insertion-order": {
        "name": "Test-Legacy-IO-GDLI",
        "advertiser_id": "3872575",
        "timezone": "UTC",
        "start_date": "2020-10-01 00:00:00",
        "currency": "USD"
      }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/insertion-order` endpoint using this JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @legacy_io_gdli.json 'https://api.appnexus.com/insertion-order?advertiser_id=3872575'
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 4969719,
            "start_element": 0,
            "num_elements": 100,
            "insertion-order": {
                "id": 4969719,
                "name": "Test-Legacy-IO-GDLI",
                "code": null,
                "state": "active",
                "advertiser_id": 3872575,
                "profile_id": null,
                "member_id": 958,
                "start_date": "2020-10-01 00:00:00",
                "end_date": null,
                "remaining_days": null,
                "total_days": null,
                "last_modified": "2020-10-01 03:28:27",
                "timezone": "UTC",
                "currency": "USD",
                "comments": null,
                "budget_type": null,
                "billing_code": null,
                "viewability_standard_provider": null,
                "is_running_political_ads": false,
                "line_items": null,
                "labels": null,
                "broker_fees": null,
                "budget_intervals": null,
                "tpas_details": null,
                "political_content": null,
                "lifetime_pacing": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "enable_pacing": null,
                "lifetime_pacing_span": null,
                "allow_safety_pacing": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "lifetime_pacing_pct": null
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "insertion-order"
            }
        }
    }
    ```

#### Example seamless IO for GDALI API setup

1. Create Seamless IO JSON (you'll need an existing advertiser ID).

    ```
    $ cat seamless_io_gdali
    {
    "insertion-order": {
        "name": "Test-Seamless-IO-GDALI",
        "advertiser_id": "3872575",
        "timezone": "UTC",
        "budget_type": "impression"
        "budget_intervals": [
          {
            "start_date": "2020-10-01 00:00:00",
            "timezone": "UTC"
          }
        ],
        "currency": "USD"
      }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/insertion-order` endpoint using this JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @seamless_io_gdali.json 'https://api.appnexus.com/insertion-order?advertiser_id=3872575'
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 4971824,
            "start_element": 0,
            "num_elements": 100,
            "insertion-order": {
                "id": 4971824,
                "name": "Test-Seamless-IO-GDALI",
                "code": null,
                "state": "active",
                "advertiser_id": 3872575,
                "profile_id": null,
                "member_id": 958,
                "start_date": null,
                "end_date": null,
                "remaining_days": null,
                "total_days": null,
                "last_modified": "2020-10-01 11:17:21",
                "timezone": "UTC",
                "currency": "USD",
                "comments": null,
                "budget_type": "impression",
                "billing_code": null,
                "viewability_standard_provider": "iab",
                "is_running_political_ads": false,
                "line_items": null,
                "labels": null,
                "broker_fees": null,
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
                "tpas_details": null,
                "political_content": null,
                "lifetime_pacing": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "enable_pacing": null,
                "lifetime_pacing_span": null,
                "allow_safety_pacing": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "lifetime_pacing_pct": null
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "insertion-order"
            }
        }
    }
    ```

## Line item changes

| Feature | Legacy GDLI | GDALI |
|:---|:---|:---|
| Line Item Subtype | This is a new field to the line item service. | Line item subtype should be specified as `gd_buying_imp` for impression guaranteed line items, and `gd_buying_exclusive` for exclusive (also known as share of voice/SOV) guaranteed line items.<br><br>By defining `line_item_subtype`, the user may omit the following fields/arrays in the request payload:<br> - `line_item_type`<br> - `bid_object_type`<br>- `delivery_model_type`<br> - `supply_strategies`<br>If the user provides conflicting `line_item_subtype` and fields/arrays outlined above, we'll prefer the line_item_subtype and ignore other fields on the call.<br><br>**Note**: The `line_item_subtype` field cannot be changed after the line item is created.<br><br>More details on the `line_item_subtype` field can be found in [Line Item Service - GDALI](./line-item-service---gdali.md). See [Example for Line Item Subtype - GDALI](#example-for-line_item_subtype---gdali) |
| Line Item Type | Line Item Type was specified as guaranteed_delivery. See [Example for line item type - Legacy GDLI](#example-for-line_item_type---legacy-gdli)  | **Tip**: When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `line_item_type` field may be omitted and will default to `"standard_v2"`. |
| Bid Object Type | Bid object type was specified on the line item object but was not required. See [Example for bid object type - Legacy GDLI](#example-for-bid_object_type---legacy-gdli)  | **Tip**: When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `bid_object_type` field may be omitted and will default to `"creative"`. |
| Delivery Model Type | Delivery model type was specified on the line item object but was not required. See [Example for delivery model type - Legacy GDLI](#example-for-delivery_model_type---legacy-gdli) | **Tip**: When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `delivery_model_type` field may be omitted. |
| Supply Strategies | Supply Strategies were previously specified using the `inventory_type` field within a campaign object with a value of `real_time`, `direct`, or `both`. See [Example for supply strategies - Legacy GDLI](#example-for-supply_strategies---legacy-gdli) | **Tip**: When `"line_item_subtype"` is set to `gd_buying_imp` or `gd_buying_exclusive`, the `supply_strategies` field may be omitted.<br>Guaranteed delivery line items will always be set to `"managed": true` and all other strategies will be set to `false`.<br><br>See the "Supply Strategies" section in [Line Item Service - GDALI](./line-item-service---gdali.md) for more information. |
| Flight Dates and Budgeting | Flight dates and budget details were specified on the line item object. See [Example for flight dates and budgeting - Legacy GDLI](#example-for-flight-dates-and-budgeting---legacy-gdli) | Flight dates and budget details are specified within the `budget_intervals` property on the `line item` object.<br><br>**Note**: <br> - A guaranteed delivery line item must not contain more than one  `budget_intervals` array.<br><br> - Impression line items ( `"line_item_subtype": "gd_buying_imp"`)  require a value be set for `lifetime_budget_imps`, as well as `lifetime_pacing` set to `true`. All revenue budget fields must be set to `null`. Setting `daily_budget_imps` in addition to `lifetime_budget_imps` may impact delivery.<br><br> - Exclusive line items (`"line_item_subtype": "gd_buying_exclusive"`) must omit all budget fields, or set them to `null`. See [Example for exclusive line items - GDALI](#example-for-exclusive-line-items---gdali)|
| Creative Scheduling | Required campaign shells to target specific creatives to deliver on specific dates within the line item's flight. | Creatives now support defining custom date ranges at which they will serve, see "Custom Date Ranges" in [Line Item Service - GDALI](./line-item-service---gdali.md) for details. |
| Priority | Priority was previously specified within a campaign object. The default value is 5. See [Example for priority - Legacy GDLI](#example-for-priority---legacy-gdli) | Priority is specified on the line item object. The Monetize UI sets the default value for impression guaranteed line items to 14, and 19 for exclusive. The default value for all line items created via the API is 5. See [Example for priority - GDALI](#example-for-priority---gdali) |
| Ad Types | Ad types were specified on the line item object but was not required. See [Example for ad types - Legacy GDLI](#example-for-ad_types---legacy-gdli) | One or more ad types are required (accepted inputs are banner, video (includes audio) and native). Among others, this field will be used for forecasting. See [Example for ad types - GDALI](#example-for-ad_types---gdali) |
| Revenue Type | Viewable CPM was defined as a revenue type. See [Example for revenue type - Legacy GDLI](#example-for-revenue_type---legacy-gdli) | Acceptable values include: `"cpm"` and `"flat_fee"`. See **Auction Event** (in this table) for information on Viewable CPM. |
| Auction Event | Auction event was specified on the line item object but was not required. See [Example for auction event - Legacy GDLI](#example-for-auction_event---legacy-gdli) | The `Auction Event` object should be used to define a non-impression based transaction, such as booking revenue on a Viewable CPM basis. See [Line Item Service - GDALI](./line-item-service---gdali.md) for details. [For example, the following configuration would enable a $4 Viewable CPM](#example-for-auction_event---gdali). |
| Roadblocks | Roadblock could be defined on the campaign or line item object. | Roadblock is specified on the line item object.<br><br>**Warning**: Only page-level partial roadblocks are supported by GDALI. The `master_width` and `master_height` fields must be defined for roadblock line items. See [Example for roadblock - GDALI](#example-for-roadblock---gdali) |
| Campaigns | Required defining a campaign object and associating to the line item in order for the line to deliver. | GDALI no longer supports campaign objects; this step is no longer required. |
| Splits | Splits were not supported on legacy GDLIs. | The [Splits Service](./splits-service.md) can be utilized for use cases such as targeting creatives to a subset of inventory. |
| Broker Fees | The `broker_fees` array was used to define [Broker Fees](./broker-service.md). | GDALI does not support broker fees or [Partner Fees](./partner-fee-service.md). |
| Alerts | The alerts object returned the conditions that are preventing the line item from serving. | GDALI does not support alerts. |
| Underspend Catch Up | "Underspend catch up" was not supported in legacy GDLIs | GDALI supports "underspend catch up." For more information, see the "Budget Scheduling Settings" section of [Line Item Service - GDALI](./line-item-service---gdali.md). |

### Example for `line_item_subtype` - GDALI

```
{
...,
"line_item_subtype": "gd_buying_imp"
}
```

### Example for `line_item_type` - Legacy GDLI

```
{
...,
"line_item_type": "guaranteed_delivery"
}
```

### Example for `bid_object_type` - Legacy GDLI

```
{
...,
"bid_object_type": null
}
```

### Example for `delivery_model_type` - Legacy GDLI

```
{
...,
"delivery_model_type": null
}
```

### Example for `supply_strategies` - Legacy GDLI

```
{
...,
"campaigns": [
{
...,
"inventory_type": "direct"
}
]
}
```

### Example for flight dates and budgeting - Legacy GDLI

```
{
...,
"start_date": "2020-10-01 00:00:00",
"end_date": "2020-10-31 23:59:59",
"timezone": "UTC",
"lifetime_pacing": true,
"lifetime_budget": null,
"lifetime_budget_imps": 10000,
"enable_pacing": null,
"lifetime_pacing_span": null,
"allow_safety_pacing": null,
"daily_budget": null,
"daily_budget_imps": null,
"lifetime_pacing_pct": 105
...
}
```

### Example for exclusive line items - GDALI

```
{
...,
"budget_intervals": [
{
"start_date": "2020-10-01 00:00:00",
"end_date": "2020-10-31 23:59:59",
"timezone": "UTC",
"lifetime_budget": null,
"lifetime_budget_imps": 10000,
"daily_budget_imps": null,
"daily_budget": null,
"enable_pacing": true,
"lifetime_pacing": true,
"lifetime_pacing_pct": 105
}
]
}
```

### Example for `priority` - Legacy GDLI

```
{
...,
"campaigns": [
{
...,
"priority": 14
}
]
}
```

### Example for `priority` - GDALI

```
{
...,
"priority": 14
}
```

### Example for `ad_types` - Legacy GDLI

```
{
...,
"ad_types": null
}
```

### Example for `ad_types` - GDALI

```
{
...,
"ad_types": [
"banner"
]
}
```

### Example for `revenue_type` - Legacy GDLI

```
{
...,
"revenue_type": "vcpm"
}
```

### Example for `auction_event` - Legacy GDLI

```
{
...,
"auction_event": null
}
```

### Example for `auction_event` - GDALI

```
{
"line-item": {
...
"revenue_type": "cpm",
"revenue_value": 4
...
"auction_event": {
"revenue_auction_event_type": "view",
"revenue_auction_event_type_code": "view_display_50pv1s_an",
"revenue_auction_type_id": 2
}
...
}
}
```
### Example for `roadblock` - GDALI

```
{
...,
"roadblock": {
"type": "partial_roadblock",
"master_width": 728,
"master_height": 90
}
}
```

### Examples

#### Example legacy GDLI API setup

1. Create legacy GDLI JSON (you'll need an existing insertion order ID and advertiser ID).

    ```
    $ cat legacy_gd_imp_cpm
    {
    "line-item": {
        "name": "Test-Legacy-GDLI",
        "advertiser_id": "3872575",
        "insertion_orders": [{"id": 4969719}],
        "line_item_type": "guaranteed_delivery",
        "publishers_allowed": "direct",
        "state": "inactive",
        "start_date": "2020-10-01 00:00:00",
        "end_date": "2020-10-31 00:00:00",
        "timezone": "UTC",
        "lifetime_budget_imps": 150000,
        "lifetime_pacing": true,
        "lifetime_pacing_pct": 105,
        "allow_safety_pacing": false,
        "enable_pacing": false,
        "currency": "USD",
        "revenue_type": "cpm",
        "revenue_value": 1,
        "manage_creative": true,
        "delivery_goal": {
          "type": "impressions",
          "disallow_non_guaranteed": false,
          "reserved": true
        }
      }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/line-item` endpoint using this JSON and the appropriate `advertiser_id`.

    ```
    $ curl -b cookies -X POST -d @legacy_gd_imp_cpm.json 'https://api.appnexus.com/line-item?advertiser_id=3872575'
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 12950674,
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 12950674,
                "code": null,
                "name": "Test-Legacy-GDLI",
                "advertiser_id": 3872575,
                "state": "inactive",
                "start_date": "2020-10-01 00:00:00",
                "end_date": "2020-10-31 00:00:00",
                "timezone": "UTC",
                "discrepancy_pct": 0,
                "publishers_allowed": "direct",
                "revenue_value": 1,
                "revenue_type": "cpm",
                "goal_type": "none",
                "goal_value": null,
                "last_modified": "2020-10-02 10:50:23",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": true,
                "profile_id": null,
                "member_id": 958,
                "flat_fee_type": null,
                "comments": null,
                "remaining_days": 29,
                "total_days": 30,
                "manage_creative": true,
                "budget_set_per_flight": true,
                "creative_distribution_type": null,
                "line_item_type": "guaranteed_delivery",
                "bid_object_type": "creative",
                "prefer_delivery_over_performance": false,
                "priority": null,
                "enable_v8": false,
                "viewability_vendor": null,
                "is_archived": false,
                "archived_on": null,
                "delivery_model_type": "standard",
                "waive_deductions_when_disallowed": false,
                "line_item_subtype": null,
                "advertiser": {
                    "id": 3872575,
                    "name": "Adrian Custom Format Testing"
                },
                "flat_fee": null,
                "deals": null,
                "delivery_goal": {
                    "id": 2245570,
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
                        "id": 4969719,
                        "state": "active",
                        "code": null,
                        "name": "Test-Legacy-IO-GDLI",
                        "advertiser_id": 3872575,
                        "start_date": "2020-10-01 00:00:00",
                        "end_date": null,
                        "timezone": "UTC",
                        "last_modified": "2020-10-02 03:28:27",
                        "currency": "USD",
                        "budget_intervals": null,
                        "political_content": null
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
                "budget_scheduling_settings": null,
                "ad_types": null,
                "user_info": null,
                "partner_fees": null,
                "product": null,
                "in_demo_measurement": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": 150000,
                "daily_budget": null,
                "daily_budget_imps": 5240,
                "enable_pacing": false,
                "allow_safety_pacing": false,
                "lifetime_pacing": true,
                "lifetime_pacing_span": null,
                "lifetime_pacing_pct": 105
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

1. Create campaign JSON (you'll need an existing line item ID and advertiser ID).

    ```
    $ cat legacy_campaign
    {
    "campaign": {
        "name": "Test-Legacy-Campaign",
        "advertiser_id": "3872575",
        "line_item_id": 12950674,
        "state": "active",
        "priority": 14,
        "inventory_type": "direct"
      }
    }
    ```

1. Make a `POST` request to the `https://api.appnexus.com/campaign` endpoint using this JSON and the appropriate `advertiser_id` and `line_item_id`.

    ```
    $ curl -b cookies -X POST -d @legacy_campaign.json 'https://api.appnexus.com/campaign?advertiser_id=3872575&line_item_id=12950674'
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 46327974,
            "start_element": 0,
            "num_elements": 100,
            "campaign": {
                "id": 46327974,
                "state": "active",
                "parent_inactive": true,
                "code": null,
                "advertiser_id": 3872575,
                "line_item_id": 12950674,
                "creative_id": null,
                "pixel_id": null,
                "short_name": null,
                "name": "Test-Legacy-Campaign",
                "profile_id": null,
                "start_date": null,
                "end_date": null,
                "timezone": "UTC",
                "priority": 14,
                "cadence_modifier_enabled": false,
                "cpc_goal": null,
                "cpm_bid_type": "margin",
                "base_bid": null,
                "min_bid": null,
                "max_bid": null,
                "bid_margin": 0,
                "roadblock_creatives": false,
                "roadblock_type": "no_roadblock",
                "inventory_type": "direct",
                "last_modified": "2020-10-02 10:55:04",
                "max_learn_bid": null,
                "cadence_type": "advertiser",
                "member_id": 958,
                "click_url": null,
                "require_cookie_for_tracking": true,
                "allow_unverified_ecp": false,
                "defer_to_li_prediction": false,
                "ecp_learn_divisor": null,
                "projected_learn_events": null,
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
                "campaign_type": "default",
                "creative_distribution_type": null,
                "allocation_pct": null,
                "allocation_strategy": "unconstrained",
                "is_archived": false,
                "archived_on": null,
                "supply_type_action": null,
                "supply_type": null,
                "creatives": null,
                "pixels": null,
                "optimization_lookback": null,
                "campaign_modifiers": null,
                "labels": null,
                "broker_fees": null,
                "valuation": null,
                "bid_model": null,
                "bid_modifier_model": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "daily_budget": null,
                "daily_budget_imps": null,
                "enable_pacing": null,
                "allow_safety_pacing": null,
                "lifetime_pacing": null,
                "lifetime_pacing_span": null,
                "lifetime_pacing_pct": null
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "campaign"
            }
        }
    }
    ```

#### Example GDALI API setup

Further examples can be found on [Line Item Service - GDALI](./line-item-service---gdali.md).

1. Create GDALI JSON (you'll need an existing insertion order ID and advertiser ID).

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

1. Make a `POST` request to the `https://api.appnexus.com/line-item` endpoint using this JSON and the appropriate `advertiser_id`.

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
                "version": "x1.0.56",
                "output_term": "line-item"
            }
        }
    }
    ```

## GDALI documentation

Publishers should refer to the following new API documents to learn more about GDALIs:

- [Insertion Order Service](./insertion-order-service.md): A reference for creating and configuring a seamless insertion order required for a GDALI along with other publisher order management workflows.
- [Line Item Service - GDALI](./line-item-service---gdali.md): A reference for creating and configuring a GDALI.
- [Publisher GDALI API Setup Guide](./publisher-gdali-api-setup-guide.md): A step-by-step API guide for creating a GDALI.
