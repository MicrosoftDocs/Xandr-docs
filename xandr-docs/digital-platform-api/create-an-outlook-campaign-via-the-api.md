---
title: Create an Outlook Campaign via the API
description: In this article, learn step-by-step instructions on how to create an Outlook campaign via the API.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Create an Outlook campaign via the API

This page shows you how to use the Campaign Service and the Profile Service to set up a campaign that targets Outlook.com inventory.

## Before you begin

Before careating an Outlook profile and campaign, you should add your Outlook creatives to Xandr. For instructions, see [Add a Microsoft Outlook Creative via the API](add-a-microsoft-outlook-creative-via-the-api.md).

## Step 1: Create a profile that targets Outlook.com inventory

To ensure that your campaign will reach Microsoft Outlook.com inventory, you should:

- Set `supply_type_targets` to `"web"` and `supply_type_action` to `"include"`.
- Set `domain_targets` to `"outlook.com"` and `domain_action` to `"include"`.

You can also add targeting based on frequency, geography, daypart, segment, and system. However, note that you cannot target Outlook.com users based on age, gender, tag position, or tag query strings.

```
$ cat outlook_profile.json
{
    "profile": {
        "supply_type_action": "include",
        "supply_type_targets": [
            "web"
        ],
        "domain_targets": [
            {
                "domain": "outlook.com"
            }
        ]
    }
}
$ curl -b cookies -c cookies -X POST -d @outlook_profile 'https://api.appnexus.com/profile?advertiser_id=41884'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "profile": {
            "id": 326106,
            "code": null,
            "description": null,
            "country_action": "exclude",
            "region_action": "exclude",
            "city_action": "exclude",
            "browser_action": "exclude",
            "use_inventory_attribute_targets": true,
            "last_modified": "2013-11-20 20:10:23",
            "daypart_timezone": null,
            "dma_action": "exclude",
            "domain_action": "include",
            "domain_list_action": "exclude",
            "inventory_action": "exclude",
            "language_action": "exclude",
            "segment_boolean_operator": "and",
            "min_session_imps": null,
            "session_freq_type": "platform",
            "carrier_action": "exclude",
            "supply_type_action": "include",
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
            "advertiser_id": 50544,
            "publisher_id": null,
            "max_session_imps": null,
            "max_day_imps": null,
            "max_lifetime_imps": null,
            "max_page_imps": null,
            "min_minutes_per_imp": null,
            "venue_action": "exclude",
            "operating_system_action": "exclude",
            "require_cookie_for_freq_cap": true,
            "trust": "xandr",
            "allow_unaudited": false,
            "is_template": false,
            "created_on": "2013-11-20 20:10:23",
            "operating_system_family_action": "exclude",
            "use_operating_system_extended_targeting": true,
            "user_group_targets": null,
            "country_targets": null,
            "region_targets": null,
            "city_targets": null,
            "inv_class_targets": null,
            "inventory_source_targets": null,
            "inventory_attribute_targets": null,
            "age_targets": null,
            "daypart_targets": null,
            "browser_targets": null,
            "browser_family_targets": null,
            "dma_targets": null,
            "domain_targets": [
                {
                    "profile_id": 326106,
                    "domain": "outlook.com"
                }
            ],
            "domain_list_targets": null,
            "language_targets": null,
            "size_targets": null,
            "postal_code_targets": null,
            "member_targets": null,
            "segment_group_targets": null,
            "carrier_targets": null,
            "supply_type_targets": [
                "web"
            ],
            "device_type_targets": null,
            "screen_size_targets": null,
            "device_model_targets": null,
            "querystring_targets": null,
            "gender_targets": null,
            "intended_audience_targets": [
                "general",
                "children",
                "young_adult"
            ],
            "inventory_group_targets": null,
            "inventory_network_resold_targets": null,
            "ip_targets": null,
            "operating_system_targets": null,
            "operating_system_family_targets": null,
            "position_targets": {
                "allow_unknown": true,
                "positions": null
            },
            "site_targets": null,
            "venue_targets": null,
            "operating_system_extended_targets": null,
            "content_category_targets": null,
            "deal_targets": null,
            "placement_targets": null,
            "platform_content_category_targets": null,
            "platform_placement_targets": null,
            "platform_publisher_targets": null,
            "publisher_targets": null,
            "segment_targets": null,
            "exelate_targets": null
        }
    }
    }
```

## Step 2: Create an Outlook campaign

Setting up an Outlook campaign is similar to setting up any other web campaign. You can set flight dates, budgeting, and buying strategy. To ensure that you reach Outlook.com inventory, however, be sure to pay particularly close attention to the following settings:

- Use the `profile_id` field to associate the campaign to the Outlook targeting profile you created in [Step 1](#step-1-create-a-profile-that-targets-outlookcom-inventory).
- Set `line_item_id` to the ID of the line item under which you want to create the Outlook campaign.
- Set `supply_type` to `"web"`.
- Since Microsoft is an external supply partner, set `inventory_type` to `"real_time"`.
- Use the `creatives` array to associate Outlook creatives to the campaign.

```
$ cat outlook_campaign.json
{
    "campaign": {
        "state": "inactive",
        "name": "Outlook.com campaign",
        "profile_id": 1997433,
        "line_item_id": 202232,
        "start_date": "2012-10-01 00:00:00",
        "end_date": "2012-10-31 23:59:59",
        "inventory_type": "real_time",
        "supply_type": "web",
        "creatives": [
            {
                "id": "3156586"
            },
            {
                "id": "3156587"
            }
        ]
    }
}
$ curl -b cookies -c cookies -X POST -d @outlook_campaign 'https://api.appnexus.com/campaign?advertiser_id=41884'
{
    "response": {
        "status": "OK",
        "campaign": {
            "id": 567735,
            "state": "inactive",
            "code": null,
            "advertiser_id": 41884,
            "short_name": null,
            "name": "Outlook.com campaign",
            "profile_id": 1997433,
            "line_item_id": 202232,
            "start_date": "2012-10-01 00:00:00",
            "end_date": "2012-10-31 23:59:59",
            "timezone": "CET",
            "lifetime_budget": null,
            "lifetime_budget_imps": null,
            "daily_budget": null,
            "daily_budget_imps": null,
            "enable_pacing": null,
            "allow_safety_pacing": null,
            "priority": 5,
            "cadence_modifier_enabled": false,
            "cpc_goal": null,
            "cpm_bid_type": "base",
            "base_bid": 0,
            "min_bid": null,
            "max_bid": null,
            "bid_margin": 0,
            "roadblock_creatives": false,
            "roadblock_type": "no_roadblock",
            "inventory_type": "real_time",
            "last_modified": "2012-09-10 15:35:16",
            "creatives": [
                {
                    "id": "3156586",
                    "mapping_state": "active",
                    "name": "Outlook creative 1.png",
                    "width": "100",
                    "height": "72",
                    "state": "active",
                    "audit_status": "pending",
                    "is_expired": false,
                    "is_prohibited": false,
                    "is_self_audited": false,
                    "format": "image",
                    "pop_window_maximize": null
                },
                {
                    "id": "3156587",
                    "mapping_state": "active",
                    "name": "Outlook creative 2.png",
                    "width": "100",
                    "height": "72",
                    "state": "active",
                    "audit_status": "pending",
                    "is_expired": false,
                    "is_prohibited": false,
                    "is_self_audited": false,
                    "format": "image",
                    "pop_window_maximize": null
                }
            ],
            "supply_type": "web",
            "pixels": null,
            "learn_threshold": "10",
            "confidence_threshold": 33,
            "projected_learn_events": "3",
            "ecp_learn_divisor": "3.000000",
            "cadence_type": "advertiser",
            "member_id": 882,
            "click_url": null,
            "require_cookie_for_tracking": true,
            "labels": null,
            "broker_fees": null,
            "allow_unverified_ecp": false,
            "defer_to_li_prediction": false,
            "optimization_lookback": null,
            "cpc_payout": null,
            "comments": null,
            "optimization_lever_mode": "manual",
            "optimization_version": "v6",
            "override_type": null,
            "override_value": null,
            "impression_limit": 40000,
            "bid_multiplier": 1,
            "remaining_days": null,
            "total_days": null
        },
        "count": 1,
        "start_element": 0,
        "num_elements": 100
    }
    }
```

## Related topics

- [Buying Microsoft Outlook.com Inventory](buying-microsoft-outlook-com-inventory.md)
- [Add a Microsoft Outlook Creative](add-a-microsoft-outlook-creative-via-the-api.md)
- [Check the Audit Status of an Outlook Creative](check-the-audit-status-of-an-outlook-creative-via-the-api.md)
