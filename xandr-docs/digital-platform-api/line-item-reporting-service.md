---
title: Line Item Reporting Service
description: Explore the Line Item Reporting service, their JSON fields, REST API, and functions with thorough example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Line Item Reporting service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.
>
> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.

Xandr admins can use this service to create the `standard_v2` line item.  

## REST API

| HTTP Methods | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://sor-api.adnxs.net/standard_v2`<br>(standard_v2 JSON) | Add a new Augmented Targeting line item and associated profile. |
| `PUT` | `https://sor-api.adnxs.net/standard_v2`<br>(standard_v2 JSON) | Modify an Augmented Targeting line item and associated profile. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `line_item` | array | See [Line Item Array](#line-item-array). |
| `campaigns` | array | See [Campaigns Array](#campaigns-array). |

### Line item array

The Line Item Array functions like the [Line Item Service](line-item-service.md).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the line item.<br>**Required On:** `PUT`, in query string. |
| `name` | string | The name of the line item.<br>**Required On:** `POST` |
| `line_item_type` | enum | For the Line Item Reporting Service to work correctly, select `standard_v2`.<br>**Default:** `standard_v1`<br>**Required On:** `POST` |
| `revenue_type` | enum | The way the advertiser has agreed to pay you. Possible values for `line_item_type` = `standard_v2` are listed below:<br> - `"cpm"`: A flat payment per 1000 impressions. Requires a `revenue_value`.<br> - `"vcpm"`: Expected value for each impression.<br>For a revenue type of `"cpm"` or `"vcpm"`, one of the following is required:<br> - `goal_type`:<br>&nbsp; - `cpa`: Use [Goal Pixels array](../digital-platform-api/line-item-service.md#goal-pixels). <br>&nbsp; - `cpc`: Use [Valuation array](#valuation-array).<br>Each can also include:<br> - `max_avg_cpm` in the [Valuation array](#valuation-array).<br>**Required On:** `POST` |
| `revenue_value` | double | The amount paid to the network by the advertiser.<br>**Required On:** `POST` |
| `budget_intervals` | array | See [Budget Intervals](./line-item-service.md#budget-intervals).<br><br>**Note:**<br> - Set `enable_pacing` to `true`.<br>AND<br> - Set `lifetime_budget` or `lifetime_budget_imp` and `lifetime_pacing`.<br>OR<br> - Set `lifetime_budget` or `lifetime_budget_imps` and `daily_budget` or `daily_budget_imps`.<br>**Required On:** `POST` |
| `creative` | array | The creatives that are associated with the line item. You must first add the creative through the [Creative Service](creative-service.md) if you don't already have a creative to use. See [Creative Array](#creative-array). |
| `profile` | array | See [Profile Service](profile-service.md). |

### Creative array

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative. Either `id` or `code` is required when updating creative association. |
| `code` | string | The custom code for the creative. Either `id` or `code` is required when updating creative association. |

### Valuation array

| Field | Type | Description |
|:---|:---|:---|
| `goal_threshold` | decimal | For line items with the `goal_type` `"cpc"`, the performance goal threshold, which determines the bid/no bid cutoff on optimized campaigns.<br>**Default:** `null` |
| `goal_target` | decimal | For line items with the `goal_type` `"cpc"`, the performance goal target, representing the desired clicks or click-through rate.<br>**Default:** `null` |
| `performance_mkt_managed` | boolean | **Default:** Set to `false`. |
| `min_margin_pct` | decimal | For line items with `revenue_type` `"cpm"`, `"cpa"`, or `"cpc"` the minimum margin PCT.<br>**Default:** `null` |
| `min_avg_cpm` | decimal | The line item revenue cannot fall below this minimum average eCPM.<br>**Default:** `null` |
| `max_avg_cpm` | decimal | The line item revenue cannot exceed this maximum average eCPM.<br>**Default:** `null` |

### Campaigns array

The following is the default campaign that you have to feed the Line Item Reporting Service when you create a new line item. You will always have to construct a campaign with the following fields and values, and the Line Item Reporting Service will create and associate the actual campaign for you. The Line Item Reporting Service expects the campaign in a list, even though you would only put one campaign.

| Field | Type | Value |
|:---|:---|:---|
| `name` | string | Line Item's name. |
| `state` | enum | Line Item's state. |
| `inventory_type` | enum | `"both"` |
| `cpm_bid_type` | enum | `"bpp"` |
| `require_cookie_for_tracking` | enum | `"false"` |

## Example

### Create a new Augmented Trading line item

```
$ cat standard_v2.json
{
  "standard_v2": {
    "line_item": {
      "line_item_type": "standard_v2",
      "payout_margin": null,
      "require_cookie_for_tracking": true,
      "name": "Tst",
      "code": null,
      "state": "active",
      "start_date": null,
      "end_date": null,
      "click_url": null,
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "lifetime_pacing": null,
      "enable_pacing": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "budget_intervals": [
        {
          "start_date": "2016-01-08 00:00:00",
          "end_date": "2016-01-09 00:00:00",
          "lifetime_budget": 1,
          "lifetime_budget_imps": null,
          "parent_interval_id": 7103,
          "lifetime_pacing": false,
          "enable_pacing": true,
          "daily_budget": 1,
          "daily_budget_imps": null
        }
      ],
      "insertion_orders": [
        {
          "id": 269592,
          "name": "First Test",
          "code": null,
          "state": "active",
          "advertiser_id": 764141,
          "start_date": null,
          "end_date": null,
          "remaining_days": null,
          "total_days": null,
          "last_modified": "2016-01-08 21:57:18",
          "timezone": "EST5EDT",
          "currency": "JPY",
          "comments": null,
          "billing_code": null,
          "line_items": [
            {
              "id": 2621282,
              "name": "First LI",
              "code": null,
              "state": "active",
              "start_date": null,
              "end_date": null,
              "timezone": "EST5EDT"
            },
            {
              "id": 2621320,
              "name": "TEst 2",
              "code": null,
              "state": "active",
              "start_date": null,
              "end_date": null,
              "timezone": "EST5EDT"
            },
            {
              "id": 2621351,
              "name": "Test",
              "code": null,
              "state": "active",
              "start_date": null,
              "end_date": null,
              "timezone": "EST5EDT"
            }
          ],
          "spend_protection_pixels": null,
          "labels": null,
          "broker_fees": null,
          "budget_intervals": [
            {
              "id": 7103,
              "object_id": 269592,
              "object_type": "insertion_order",
              "start_date": "2016-01-08 00:00:00",
              "end_date": "2016-01-09 00:00:00",
              "timezone": "EST5EDT",
              "lifetime_budget": 1,
              "lifetime_budget_imps": null,
              "lifetime_pacing": false,
              "enable_pacing": false,
              "daily_budget_imps": null,
              "daily_budget": null
            }
          ],
          "tpas_details": null,
          "lifetime_pacing": null,
          "lifetime_budget": null,
          "lifetime_budget_imps": null,
          "enable_pacing": null,
          "lifetime_pacing_span": null,
          "allow_safety_pacing": null,
          "daily_budget": null,
          "daily_budget_imps": null,
          "lifetime_pacing_pct": null
        }
      ],
      "currency": "JPY",
      "broker_fees": [],
      "manage_creative": true,
      "creative_distribution_type": "even",
      "creatives": [],
      "labels": [],
      "revenue_type": "vcpm",
      "revenue_value": null,
      "track_revenue": "track",
      "pixels": [],
      "valuation": {
        "goal_target": 1,
        "goal_threshold": 1,
        "performance_mkt_managed": false,
        "min_margin_pct": 1,
        "min_avg_cpm": 1,
        "max_avg_cpm": 1
      },
      "goal_type": "cpc",
      "goal_value": null,
      "goal_pixels": null,
      "comments": null,
      "profile": {
        "require_cookie_for_freq_cap": true,
        "max_day_imps": null,
        "max_lifetime_imps": null,
        "min_minutes_per_imp": null,
        "max_page_imps": null,
        "device_type_action": "exclude",
        "device_type_targets": null,
        "supply_type_action": "exclude",
        "supply_type_targets": null,
        "city_targets": null,
        "city_action": "exclude",
        "country_action": "exclude",
        "country_targets": null,
        "region_targets": null,
        "region_action": "exclude",
        "dma_targets": null,
        "dma_action": "exclude",
        "location_target_latitude": null,
        "location_target_longitude": null,
        "location_target_radius": null,
        "zip_targets": null,
        "postal_code_targets": null,
        "content_category_targets": null,
        "domain_action": "exclude",
        "domain_targets": null,
        "domain_list_action": "exclude",
        "domain_list_targets": null,
        "inventory_action": "exclude",
        "placement_targets": null,
        "publisher_targets": null,
        "site_targets": null,
        "mobile_app_instance_action_include": false,
        "mobile_app_instance_targets": null,
        "mobile_app_instance_list_action_include": false,
        "mobile_app_instance_list_targets": null,
        "member_targets": null,
        "platform_content_category_targets": null,
        "platform_placement_targets": null,
        "platform_publisher_targets": null,
        "segment_boolean_operator": "or",
        "segment_group_targets": [],
        "daypart_targets": null,
        "daypart_timezone": null,
        "querystring_action": "exclude",
        "querystring_boolean_operator": "and",
        "querystring_targets": null,
        "position_targets": {
          "allow_unknown": true,
          "positions": null
        },
        "gender_targets": null,
        "age_targets": null,
        "certified_supply": false,
        "allow_unaudited": false,
        "trust": "appnexus",
        "video_targets": {
          "contexts": null,
          "playback_methods": null,
          "player_sizes": null,
          "allow_unknown_playback_method": false,
          "allow_unknown_context": false,
          "allow_unknown_player_size": false
        },
        "inventory_attribute_targets": [
          {
            "id": "2"
          },
          {
            "id": "4"
          },
          {
            "id": "6"
          },
          {
            "id": "8"
          },
          {
            "id": "10"
          },
          {
            "id": "14"
          },
          {
            "id": "16"
          },
          {
            "id": "18"
          }
        ],
        "intended_audience_targets": [
          "general",
          "children",
          "young_adult"
        ],
        "use_inventory_attribute_targets": true,
        "use_operating_system_extended_targeting": true,
        "operating_system_extended_targets": null,
        "operating_system_family_action": "exclude",
        "operating_system_family_targets": null,
        "operating_system_action": "exclude",
        "operating_system_targets": null,
        "language_action": "exclude",
        "language_targets": null,
        "browser_action": "exclude",
        "browser_targets": null,
        "carrier_action": "exclude",
        "carrier_targets": null,
        "device_model_action": "exclude",
        "device_model_targets": null
      },
      "id": 0
    },
    "campaigns": [
      {
        "name": "Tst",
        "state": "active",
        "inventory_type": "both",
        "cpm_bid_type": "bpp",
        "require_cookie_for_tracking": false
      }
    ]
  }
}
 
$ curl -b cookies -c cookies -X POST -d @standard_v2.json "http://sor-api.adnxs.net/standard_v2"
```
