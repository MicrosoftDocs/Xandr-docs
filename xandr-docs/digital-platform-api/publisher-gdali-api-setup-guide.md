---
title: Publisher GDALI API Setup Guide
description: Use our API setup guide to learn the process of creating and configuring a Guaranteed Delivery Augmented Line Item (GDALI).
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Publisher GDALI API setup guide

Setting up an API implementation of a Guaranteed Delivery Augmented Line Item (GDALI) can seem complicated because it requires configuring a number of different properties on different API objects. This guide will explain the process of creating and configuring a typical GDALI using our API.

## Overview

A GDALI provides you with a workflow specifically designed to deliver:

- Budget in full across its flight dates.
- Budget evenly across its flight dates.
- Guaranteed goals while still (optionally) competing in the auction with other demand such as RTB.

Setting up a GDALI typically involves making requests to the following API service endpoints to access or create the corresponding buy-side objects:

| API Endpoint | API Object | Detailed Reference |
|:---|:---|:---|
| [https://api.appnexus.com/insertion-order](https://api.appnexus.com/insertion-order) | insertion-order | [Insertion Order Service](insertion-order-service.md) |
| [https://api.appnexus.com/profile](https://api.appnexus.com/profile) | profile | [Profile Service](profile-service.md) |
| [https://api.appnexus.com/line-item](https://api.appnexus.com/line-item) | line-item (ALI) | [Line Item - ALI Service](line-item-service---gdali.md) |

This guide uses `cURL` examples for all requests. You can use other API request tools (e.g., [Postman](https://www.getpostman.com/)), but you’ll then need to adjust the examples accordingly.

## Prerequisites

Before beginning this setup, be sure to read [API Getting Started](api-getting-started.md). It provides information on testing environments, usage constraints, API semantics (running commands, filtering, sorting, etc.), and best practices.

This guide assumes you have created or can access the following API objects required to create any GDALI:

- `advertiser`: For more information, see [Advertiser Service](advertiser-service.md).
- `insertion-order`: (Instructions for creating a seamless insertion order included below for convenience) For more information, see [Insertion Order Service](insertion-order-service.md).

    > [!NOTE]
    > GDALIs can only be associated with seamless insertion orders; legacy/non-seamless insertion orders are not supported.

## Order of operations

Xandr API objects often have dependencies on other objects and there is an order you must follow in creating or accessing objects when you create a GDALI. For example, to create a GDALI, you must provide the IDs of the following objects: `advertiser`, `insertion-order`, and (optionally) `profile`. To obtain the IDs for these objects, you'll need to either create them or already have access to them. The steps in this guide follow the typical order of operations required to create a GDALI.

## Best practices

For a general list of best practices to follow when working with the API, see [API Best Practices](api-best-practices.md). The following are some best practices that are specific to a GDALI setup:

- **Set the `state` field of the GDALI to** `"inactive"` until the line item is fully configured and ready for testing.
- **Note the ID of any objects you create**. The IDs of objects you create are returned in the response body of requests. You'll often need these IDs later so copying them when they're returned can reduce the number of additional GET requests you have to make to obtain them.

## Setup procedure

The following steps will guide you through the process of setting up a GDALI with typical configurations:

- [Step 1 - Obtain an authorization token](#step-1-obtain-an-authorization-token)
- [Step 2 - Create a seamless insertion order](#step-2-create-a-seamless-insertion-order) (if an appropriate one is not available under the advertiser)
- [Step 3 - Create a profile](#step-3-create-a-profile)
- [Step 4 - Create a GDALI](#step-4-create-a-gdali)

### Step 1: Obtain an authorization token

First, you’ll need to obtain an authorization token. You must then include this authorization token in all subsequent requests. For more information, see [Authentication Service](authentication-service.md). To obtain an authorization token, do the following:

1. Create a JSON file containing your username and password.

    ```
    {
        "auth": {
            "username" : "USERNAME",
            "password" : "PASSWORD"
        }
    }
    ```

1. Make a `POST` request to the `/auth` endpoint with this JSON file in the request body. For more information, see [Authentication Service](authentication-service.md). In the `cURL` request below, the authorization token returned is stored in the “`cookies`” file.

    ```
    curl -c cookies -X POST -d @authentication.json 'https://api.appnexus.com/auth'
    ```

1. Check the response body of your request (see **Example response** below). If your request was successful, you’ll get a "`status`" of “`OK`” and the "`token`" field will be populated with the authentication token value.

    **Example response**

    ```
    {
       "response" : {
          "token" : "authn:225692:2d787d1838283:lax1",
          "status" : "OK"      
       }
    }
    ```

### Step 2: Create a seamless insertion order

Next, create a seamless insertion order. Be sure to note the ID for this insertion order for later use. For more information, see [Insertion Order Service](insertion-order-service.md).

1. Create a publisher insertion order JSON:

    ```
    $ cat seamless_io_gdali
    {
    "insertion-order": {
        "name": "Test-Seamless-IO-GDALI",
        "advertiser_id": "3872575",
        "timezone": "UTC",
        "budget_type": "impression",
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

1. Make a `POST` request to the [https://api.appnexus.com/insertion-order](https://api.appnexus.com/insertion-order) endpoint with this publisher insertion order JSON and an appropriate `advertiser_id`.

    ```
    curl -b cookies -X POST -d @seamless_io_gdali.json 'https://api.appnexus.com/insertion-order?advertiser_id=3872575'
    ```

1. Check the response body of your request (see **Example response** below). If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

    **Example response**

    ```
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

1. Note the insertion order ID in the response body so you can use it when you create the GDALI in [Step 4 - Create a GDALI](#step-4-create-a-gdali).

> [!NOTE]
> For an insertion order to be associated with a guaranteed delivery augmented line item (GDALI), the insertion order must:
>
> - Be a [Seamless Insertion Order](insertion-order-service.md) (legacy insertion orders are not compatible).  
> - Have `budget_type` set to `"flexible"` or `"impression"`.
> - Not contain more than one `budget_intervals` array.
> - Have unlimited budget (set via the `budget_intervals` array).
>
> Insertion orders not matching the above may only be associated to non-guaranteed line items. Note the above settings are also required for programmatic guaranteed line items (PGLI). An insertion order with the above settings may also be associated to non-guaranteed line items.
>
> Associating a `profile_id` (e.g., frequency capping or setting additional targeting) on the insertion order object may result in unexpected forecasting or delivery for PGLIs and GDALIs. It is recommended not to use `profile_id` for insertion orders intended for the use with GDALIs.

#### JSON fields for publisher insertion order

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The name of the insertion order. (Maximum of 255 characters.) |
| `state` | enum | The state of the insertion order. Possible values: `"active"` or `"inactive"`. |
| `currency` | string | The currency assigned to the insertion order. For a full list of available currencies, use the read-only [Currency Service](currency-service.md). <br><br>**Note:** Once the insertion order has been created, the currency cannot be changed. |
| `budget_type` | enum | The budget type of the insertion order. For GDALI, the value must be set to `"flexible"` or `"impression"`. |
| `budget_intervals` | array | Budget intervals enable date intervals to be attached to an insertion order.<br><br>**Note:**<br>- The insertion order must not contain more than one `budget_intervals` array.<br>- The insertion order must have unlimited budget (all budget fields in the `budget_intervals` array must be omitted or set to `null`). |
| `budget_intervals.start_date` | timestamp<br>(obj in array) | The start date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` <br><br>**Note:** `hh:mm:ss` must be set to `00`. Typically this would be the current date. |
| `budget_intervals.end_date` | timestamp<br>(obj in array) | The end date of the budget interval. This value is optional. |
| `budget_intervals.timezone` | string<br>(obj in array) | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). The default value is `"EST5EDT"` or the advertiser's timezone. |
| `profile_id` | int | A profile is a generic set of rules for targeting inventory.<br><br>**Warning:** Associating a profile_id (e.g., frequency capping or setting additional targeting) on the insertion order object may result in unexpected forecasting or delivery for programmatic guaranteed (PGLI) and guaranteed delivery (GDALI) line items. It is recommended not to use profile_id for insertion orders intended for use with GDALIs. |

### Step 3: Create a profile

Next, create a GDALI profile for targeting. This step is optional, but leaving the `"profile_id"` as `null` will result in "run of network" targeting, which could have implications on forecasting and reservations. Be sure to note the ID for this profile for later use.

1. Create a GDALI profile JSON that includes `300x250` size targets, as well as placement targeting:

    ```
    $ cat gdali_profile
    {
            "profile": {
                    "advertiser_id": 3872575,
                    "placement_targets": [{
                                    "id": 1357911,
                                    "action": "include"
                            },
                            {
                                    "id": 246810,
                                    "action": "include"
                            }
                    ],
                    "size_targets": [{
                            "width": 300,
                            "height": 250
                    }]
            }
    }
    ```

1. Make a `POST` request to the [https://api.appnexus.com/profile](https://api.appnexus.com/profile) endpoint with this GDALI profile JSON and an appropriate `advertiser_id`.

    ```
    curl -b cookies -c cookies -X POST -d @gdali_profile 'https://api.appnexus.com/profile?advertiser_id=3872575'
    ```

1. Check the response body of your request (see **Example response** below). If your request was successful, you’ll get a "`status`" of  “`OK`” and you’ll see the updates you made.

    **Example response**

    ```
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 123353104,
            "start_element": 0,
            "num_elements": 100,
            "profile": {
                "id": 123397648,
                "code": null,
                "description": null,
                "country_action": "exclude",
                "region_action": "exclude",
                "city_action": "exclude",
                "browser_action": "exclude",
                "use_inventory_attribute_targets": false,
                "last_modified": "2020-10-02 12:09:22",
                "daypart_timezone": null,
                "dma_action": "exclude",
                "domain_action": "exclude",
                "domain_list_action": "exclude",
                "inventory_action": "exclude",
                "language_action": "exclude",
                "segment_boolean_operator": "and",
                "min_session_imps": null,
                "session_freq_type": "platform",
                "carrier_action": "exclude",
                "supply_type_action": "exclude",
                "device_type_action": "exclude",
                "screen_size_action": "exclude",
                "device_model_action": "exclude",
                "location_target_radius": null,
                "location_target_latitude": null,
                "location_target_longitude": null,
                "querystring_action": "exclude",
                "querystring_boolean_operator": "and",
                "is_expired": false,
                "non_audited_url_action": "include",
                "daypart_bitmap": null,
                "is_archived": false,
                "archived_on": null,
                "advertiser_id": 3872575,
                "publisher_id": null,
                "max_session_imps": null,
                "max_day_imps": null,
                "max_lifetime_imps": null,
                "max_page_imps": null,
                "min_minutes_per_imp": null,
                "venue_action": "exclude",
                "operating_system_action": "exclude",
                "require_cookie_for_freq_cap": true,
                "trust": "seller",
                "allow_unaudited": false,
                "is_template": false,
                "created_on": "2020-10-02 12:09:22",
                "operating_system_family_action": "exclude",
                "use_operating_system_extended_targeting": true,
                "mobile_app_instance_action_include": false,
                "mobile_app_instance_list_action_include": false,
                "inventory_prefer_direct": false,
                "deal_action_include": true,
                "exclude_unknown_seller_member_group": false,
                "ad_slot_position_action_include": false,
                "ad_slot_intro_bumper_action_include": true,
                "ad_slot_outro_bumper_action_include": true,
                "graph_id": null,
                "media_subtype_action_include": false,
                "ads_txt_authorized_only": false,
                "require_transparency_and_consent_framework_string": false,
                "postal_code_action_include": true,
                "inventory_url_allowlist_settings": {
                    "apply_to_rtb": true,
                    "apply_to_managed": true
                },
                "user_group_targets": null,
                "country_targets": null,
                "region_targets": null,
                "city_targets": null,
                "inventory_attribute_targets": null,
                "placement_type_targets": null,
                "age_targets": null,
                "daypart_targets": null,
                "browser_targets": null,
                "dma_targets": null,
                "domain_targets": null,
                "domain_list_targets": null,
                "language_targets": null,
                "size_targets": [
                    {
                        "width": 300,
                        "height": 250
                    }
                ],
                "zip_targets": null,
                "member_targets": null,
                "video_targets": {
                    "allow_unknown_playback_method": false,
                    "allow_unknown_context": false,
                    "allow_unknown_player_size": false
                },
                "engagement_rate_targets": null,
                "segment_group_targets": null,
                "carrier_targets": null,
                "supply_type_targets": null,
                "device_type_targets": null,
                "screen_size_targets": null,
                "device_model_targets": null,
                "querystring_targets": null,
                "gender_targets": null,
                "intended_audience_targets": null,
                "inventory_network_resold_targets": null,
                "operating_system_targets": null,
                "operating_system_family_targets": null,
                "position_targets": null,
                "site_targets": null,
                "venue_targets": null,
                "operating_system_extended_targets": null,
                "postal_code_targets": null,
                "postal_code_list_targets": null,
                "seller_member_group_targets": null,
                "cross_device": null,
                "key_value_targets": null,
                "media_subtype_targets": null,
                "content_category_targets": null,
                "deal_targets": null,
                "placement_targets": [
                    {
                        "id": 1357911,
                        "action": "include",
                        "name": "Placement 1 Name",
                        "deleted": false,
                        "site_id": 123456,
                        "site_name": "Site 1 Name",
                        "publisher_id": 1234567,
                        "publisher_name": "Publisher 1 Name"
                    },
                    {
                        "id": 246810,
                        "action": "include",
                        "name": "Placement 2 Name",
                        "deleted": false,
                        "site_id": 123456,
                        "site_name": "Site 1 Name",
                        "publisher_id": 1234567,
                        "publisher_name": "Publisher 1 Name"
                    }
                ],
                "platform_content_category_targets": null,
                "platform_placement_targets": null,
                "platform_publisher_targets": null,
                "publisher_targets": null,
                "ip_range_list_targets": null,
                "mobile_app_instance_targets": null,
                "mobile_app_instance_list_targets": null,
                "ad_slot_position_targets": null,
                "inventory_url_list_targets": null,
                "deal_list_targets": null,
                "max_hour_imps": null,
                "max_week_imps": null,
                "max_month_imps": null
            },
            "dbg_info": {
                "warnings": [
                ],
                "version": "1.0.56",
                "output_term": "profile"
            }
        }
    }
    ```

1. Note the profile ID in the response body so you can use it when you create the GDALI in [Step 4 - Create a GDALI](#step-4-create-a-gdali).

#### JSON fields for GDALI profile

For a full list of fields and more information, see [Profile Service](profile-service.md).  

| Field | Type | Description |
|:---|:---|:---|
| `placement_targets` | array of objects | The placement IDs to be either excluded or included in the profile. |
| `size_targets` | array of objects | List of eligible sizes to be included in the profile. |

### Step 4: Create a GDALI

Finally, you'll need to create the GDALI. In the example below, we will be defining a GDALI with impression delivery goal booking revenue on a CPM basis.

1. Create a GDALI JSON (you'll need an existing advertiser ID and insertion order ID from [Step 2 - Create a seamless insertion order](#step-2-create-a-seamless-insertion-order)).

    ```
    $ cat gdali_imp_cpm
    {
    "line-item": {
        "name": "Test-GDALI",
        "advertiser_id": "3872575",
        "insertion_orders": [{"id": 4971824}],
        "line_item_subtype": "gd_buying_imp",
        "state": "inactive",
        "priority": 14,
        "profile_id": 123397648,
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

1. Make a `POST` request to the [https://api.appnexus.com/line-item](https://api.appnexus.com/line-item) endpoint using this GDALI JSON and an appropriate `advertiser_id`.

    ```
    curl -b cookies -X POST -d @gdali_imp_cpm 'https://api.appnexus.com/line-item?advertiser_id=3872575'
    ```

1. Check the response body of your request (see **Example response** below). If your request was successful, you’ll get a "`status`" of “`OK`” and you’ll see the updates you made.

    **Example response**

    ```
    {
        "response": {
            "status": "OK",
            "count": 1,
            "id": 12977272,
            "start_element": 0,
            "num_elements": 100,
            "line-item": {
                "id": 12977272,
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
                "last_modified": "2020-10-05 18:36:18",
                "click_url": null,
                "currency": "USD",
                "require_cookie_for_tracking": true,
                "profile_id": 123397648,
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
                    "id": 2247829,
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
                        "id": 10015349,
                        "object_id": 12977272,
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

1. Note the line item ID in the response body so you can identify this GDALI later to change its `state` (`active` or `inactive`) or modify it.
  
#### JSON fields for GDALI line item

For more information, see [Line Item Service - GDALI](line-item-service---gdali.md).

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Name of the GDALI. |
| `state` | enum | State of the line item. Possible values: `"active"` or `"inactive"`. |
| `line_item_subtype` | enum | The line item subtype. For GDALIs, the value for this field must be one of the following:<br>- `"gd_buying_imp"`: Guaranteed delivery line item with impression delivery goal. Eligible only for transacting on managed supply.<br>- `"gd_buying_exclusive"`: Guaranteed delivery line item with exclusive delivery goal (also referred to as "share of voice" or "SOV"). Eligible only for transacting on managed supply.<br>For more information, see [Line Item Service - GDALI](line-item-service---gdali.md).<br><br>**Note:** The `line_item_subtype` field (and associated fields/arrays) cannot be changed after the line item is created. |
| `budget_scheduling_settings.underspend_catchup_type` | enum<br>(prop in obj) | The `underspend_catchup_type` field dictates how Xandr's system deals with an underdelivered daily budget. Use the `"evenly"` value if you'd like the unspent portions of your budget to be spent evenly throughout the rest of flight, or `"ASAP"` if you'd like the unspent budget to be spent as soon as possible.<br>Possible values: `"evenly"` or `"ASAP"` (default). |
| `priority` | int | The line item's priority is used to weight the line item against other direct line items within your account.<br><br>**Note:** The Microsoft Monetize UI sets the default value for guaranteed delivery line item with impression delivery goal to 14, and 19 for `exclusive`. The default value for all line items created via the API is 5. |
| `ad_types` | array of strings | The type of creative used for this line item. <br>Possible values: <br>- `"banner"`<br>- `"video"`  (includes audio types as well)<br>- `"native"`<br><br>One or more values are supported. This value determines how auction items are tracked for the line item's buying strategy, paying strategy, forecasting, creative association, and targeting options.<br><br>**Note:** All creatives associated to a line item must have the same ad type, which should match the `ad_types` selected here. |
| `timezone` | enum | The timezone by which budget and spend are counted. For details and accepted values, see [API Timezones](api-timezones.md). |
| `currency` | string (3) | The currency used for this line item. For a list of supported currencies, see the [Currency Service](currency-service.md).<br><br>**Note:** Once the line item has been created, the currency cannot be changed. |
| `revenue_type` | enum | The way the advertiser has agreed to pay you (also called Booked Revenue). Possible values are:<br>- `"cpm"`: Select this value if you are being paid flat payment for 1000 impressions (CPM).<br>&nbsp; - For Viewable CPM, set `revenue_type` to `"cpm"`, the `revenue_value` field to the Viewable CPM value, the `revenue_auction_event_type` field to `"view"`  the `revenue_auction_event_type_code` field to `"view_display_50pv1s_an"` and `"revenue_auction_type_id"` to `2`. Only measured viewable impressions will be counted, according to the Xandr viewability measurement, using the IAB definition.<br>- `"flat_fee"`: A flat payment that the advertiser will pay you on a specified allocation date. That date can be daily or at the end of the flight. If you pay managed publishers a percentage of your revenue, their share will be paid out on the allocation date, after which the line item will no longer be editable.<br><br>**Note:** The flat fee will not be booked on the allocation date unless the line item has served at least one impression. If you define a `revenue_type` of `flat_fee` you must specify a value for `flat_fee_type`. |
| `flat_fee_type` | array | Flat fees can be paid out daily or on the flight end date. Available values are:<br>- `one_time`: The fee will be paid on the final allocation date. The associated `revenue_value` is the value to be paid on that date. The flight cannot be longer than one month.<br>- `daily`: The fee will be paid daily. The associated `revenue_value` is the daily fee, not the fee for the entire flight. |
| `revenue_value` | double | The amount paid to the network by the advertiser.<br><br>**Note:** Depending on what you set the `revenue_type` field to, this field must be set to the actual value of that revenue type (e.g. `flat_fee` or `cpm`). |
| `budget_intervals` | array | Budget intervals enable date intervals and budgets to be attached to a line items.<br><br>**Note:** The GDALI must not contain more than one `budget_intervals` array. |
| `budget_intervals.timezone` | string<br>(obj in array) | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). The default value is `"EST5EDT"` or the advertiser's timezone. |
| `budget_intervals.start_date` | timestamp<br>(obj in array) | The start date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` <br>**Note:** `hh:mm:ss` must be set to `00`. Typically, this would be the current date. |
| `budget_intervals.end_date` | timestamp<br>(obj in array) | The end date of the budget interval. Format must be `YYYY-MM-DD hh:mm:ss` (`hh:mm:ss` should be set to `hh:59:59`). Must not be `null` for GDALIs. For delivery to work best, your budget intervals should have a duration of at least 4 hours. |
| `budget_intervals.lifetime_budget_imps` | double (obj in array) | The lifetime budget in impressions for the budget interval.<br><br>**Note:** When a line item is enabled for roadblocks, only master creative imps will count against `lifetime_budget_imps`. |
| `budget_intervals.lifetime_pacing` | boolean (obj in array) | If `true`, the line item will attempt to pace the lifetime budget evenly over the budget interval. GDALIs must be defined as `true`. |
| `budget_intervals.lifetime_pacing_pct` | double (obj in array) | A double integer between (and including) 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between (and including) 50 and 150 on the following scale:<br>- `50`: Pace behind schedule.<br>- `100`: Pace evenly.<br>- `150`: Pace ahead of schedule.<br><br>**Note:** It's recommended to set this field to `105`. By default, the value will be set to `100`. |
| `delivery_goals` | array | The `delivery_goals` array contains information about the delivery goal attached to the GDALI. GDALIs will attempt to deliver against impression or percentage goals. |
| `delivery_goals.type` | string (obj in array) | The type of delivery goal. Allowed values are:<br>- `"impressions"`: GDALIs with impression goals will attempt to serve the specified number of impressions evenly across their flight dates. If the delivery goal `type` is `"impressions"`, lifetime budget must be set at the line item level.<br>- `"percentage"`: Currently, the percentage goal is only available for "exclusive" GDALIs. <br><br>**Note:** If the delivery goal `type` is `"percentage"`, the line item cannot have a budget. |
| `delivery_goals.percentage` | int (obj in array) | If the type of delivery goal is `"percentage"`, this is the actual percentage at which the GDALI will serve. Allowed values are integers 0 <= n <= 100. If the delivery goal `type` is `"impressions"`, this field must be `null`. |
| `delivery_goals.disallow_non_guaranteed` | boolean (obj in array) | When `true`, this line item will always serve over non-guaranteed line items participating in the same (managed) auction.<br><br>**Note:** Setting `disallow_non_guaranteed` to `true` may impact competition in the auction, which could impact yield. |
| `delivery_goals.reserved` | boolean (obj in array) | When `true`, this line item has inventory "reserved" for it; in other words, the line item is set to purchase a guaranteed number or percentage of impressions on a seller's inventory during its flight. Note that you will not be able to set a GDALI's `state` to `"active"` unless this field is set to `true`. |
| `roadblock` | object | The `roadblock` object contains information to enable the delivery of two or more creatives to the page in unison. Roadblocks can be applied only for managed inventory and can't be enabled when you're working with third-party inventory. |
| `roadblock.type` | enum | The type of roadblock. For GDALIs, this value must be either:<br>- `null`: (default) There is no roadblocking set at the line item level.<br>- `partial_roadblock`: Enables roadblocking on the line item. The line item serves when at least one creative of each size fits an eligible ad slot. |
| `roadblock.master_width` | int | The width of the master creative. This value is required when roadblock type equals `partial_roadblock`. |
| `roadblock.master_height` | int | The height of the master creative. This value is required when roadblock type equals `partial_roadblock`. |
| `profile_id` | int | You may associate an optional `profile_id` with this line item. A profile is a generic set of rules for targeting inventory. For details, see the [Profile Service](profile-service.md). |

## Related topics

- [API Getting Started](api-getting-started.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
