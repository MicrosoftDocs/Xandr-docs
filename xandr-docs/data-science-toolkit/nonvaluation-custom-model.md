---
title: Data Science Toolkit - Non-valuation Custom Model
description: Use non-valuation custom models to insert creative macros into impression tracking calls. Non-valuation custom models do not affect bid valuation. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---

# Data Science Toolkit - Non-valuation custom model

Non-valuation custom models do not affect bid valuation. They are used to insert custom creative macros into impression tracking calls, and will eventually be used for other functions, such as affecting Learn status.

A creative macro is a text placeholder that is replaced with some useful piece of impression-level information when a creative is served. Creative macros are used to transmit impression-level information to systems outside of Xandr, which you can then use for reporting, optimization, and many other purposes. For example, if you use third-party creative hosting, you could use a macro to populate a segment ID in your placement, which the creative server would then use to decide which creative to serve.

> [!NOTE]
> This functionality is only available for the [Augmented Line Item](../digital-platform-api/line-item-service---ali.md).

## Creative macro leaf syntax

In order for a macro to communicate with the ad server and pass what information should be populated, it must be preceded by a key. The syntax for creative macro leaves is:

```
leaf_name: "name"
creative_macros["MACRO1"]: "value1"
creative_macros["MACRO2"]: "value2
```

Since this is a non-valuation model, a value is not required. It is possible to have a leaf that consists simply of the `leaf_name`. See the [example](#example) below for more information.

> [!NOTE]
> **The restrictions are as follows:**
>
> - Macros are case-sensitive.
> - Keys and values can contain Unicode text that must not be bigger than 100 utf-8 encoded bytes in total.
> - The parser applies the NFC Unicode transformation and may change the Unicode codepoints and the resulting utf-8 encoded result. The best way to avoid unpredictable behavior is to always use NFC-normalized text both in the key and value.
> - There may be no more than two macros per leaf.
>
> Do not duplicate the names of existing [Xandr Creative Macros](../bidders/xandr-macros.md). This may cause unpredictable behavior.

## API workflow

### Step 1. Create an augmented line item

In this example, we create an augmented line item.

```
$cat ali
{
    "line-item": {
        "name": "ALI Custom Macro Test",
        "code": "ali-cm-test",
        "state": "inactive",
        "line_item_type": "standard_v2",
        "revenue_type": "cpm"
    }
}
$curl -b cookies -X POST -s -d @ali "https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID"
{
   "response" : {
      "num_elements" : 100,
      "count" : 1,
      "line-item" : {
         "lifetime_pacing" : null,
         "daily_budget_imps" : null,
         "total_days" : null,
         "budget_intervals" : null,
         "creative_distribution_type" : null,
         "remaining_days" : null,
         "line_item_type" : "standard_v2",
         "delivery_goal" : null,
         "goal_pixels" : null,
         "name" : "ALI Custom Macro Test",
         "revenue_value" : 0,
         "campaigns" : null,
         "discrepancy_pct" : 0,
         "code" : "ali-cm-test",
         "pixels" : null,
         "manage_creative" : false,
         "flat_fee" : null,
         "comments" : null,
         "inventory_discovery_budget" : null,
         "goal_value" : null,
         "require_cookie_for_tracking" : true,
         "insertion_orders" : null,
         "clicktrackers" : null,
         "enable_pacing" : null,
         "flat_fee_type" : null,
         "imptrackers" : null,
         "profile_id" : null,
         "broker_fees" : null,
         "inventory_type" : "both",
         "creatives" : null,
         "valuation" : {
            "bid_price_pacing_lever" : 0,
            "max_avg_cpm" : null,
            "goal_threshold" : null,
            "performance_mkt_managed" : false,
            "goal_target" : null,
            "goal_confidence_threshold" : null,
            "min_margin_pct" : null,
            "campaign_group_valuation_strategy" : null,
            "min_avg_cpm" : null,
            "bid_price_pacing_enabled" : false,
            "no_revenue_log" : false
         },
         "publishers_allowed" : "all",
         "lifetime_budget" : null,
         "custom_optimization_note" : null,
         "currency" : "USD",
         "daily_budget" : null,
         "auction_event" : null,
         "member_id" : 958,
         "priority" : "5",
         "advertiser_id" : 354236,
         "inventory_discovery" : null,
         "payout_margin" : null,
         "lifetime_pacing_pct" : null,
         "id" : 3925282,
         "state" : "inactive",
         "allow_safety_pacing" : null,
         "custom_models" : null,
         "timezone" : "EST5EDT",
         "end_date" : null,
         "incrementality" : null,
         "expected_value_model" : null,
         "goal_type" : "none",
         "start_date" : null,
         "last_modified" : "2017-03-20 16:00:21",
         "lifetime_budget_imps" : null,
         "click_url" : null,
         "revenue_type" : "cpm",
         "lifetime_pacing_span" : null,
         "prefer_delivery_over_performance" : false,
         "advertiser" : {
            "name" : "MCG Test Advertiser",
            "id" : 354236
         },
         "labels" : null
      },
      "status" : "OK",
      "start_element" : 0,
      "dbg_info" : {...},
      "id" : 3925282
   }
} 
```

For more information, see [ALI Workflow with Custom Models](./ali-workflow-with-custom-models.md).

### Step 2. Create a custom model tree

In this example, we create a custom model that will insert the creative macros.

```
$cat custom-macro-tree
if user_hour = 1:
    leaf_name: "cm_1"
    creative_macros["ProductViewed"]: "15436"
    creative_macros["LandingPage"]: "k2344"
else:
    leaf_name: "cm_2"
    creative_macros["TestMacro"]: "yourvaluegoeshere"
```

### Step 3. Upload custom model

In this example, we upload the custom model.

```
$ cat custom_model
 
{
    "custom_model": {
        "name": "Custom Macro Test Model", 
        "member_id": 958,
        "advertiser_id": ADVERTISER_ID,
                "custom_model_structure": "decision_tree",
        "model_output": "bid",
                "model_text": "aWYgdXNlcl9ob3VyID0gMToNCiAgICBsZWFmX25hbWU6ICJjbV8xIg0KICAgIGNyZWF0aXZlX21hY3Jvc1siUHJvZHVjdFZpZXdlZCJdOiAiMTU0MzYiDQogICAgY3JlYXRpdmVfbWFjcm9zWyJMYW5kaW5nUGFnZSJdOiAiazIzNDQiDQplbHNlOg0KICAgIGxlYWZfbmFtZTogImNtXzIiDQogICAgY3JlYXRpdmVfbWFjcm9zWyJUZXN0TWFjcm8iXTogInlvdXJ2YWx1ZWdvZXNoZXJlIiMgY3JhZnQgeW91ciB0cmVlIGhlcmUhDQoNCg0KDQoJCQk="            
        }
}
$ curl -b cookies -X POST -d @custom-model "https://api.appnexus.com/custom-model?advertiser_id=ADVERTISER_ID"
{
   "response" : {
      "id" : "82495",
      "num_elements" : 100,
      "start_element" : 0,
      "count" : 1,
      "custom_model" : {
         "code" : null,
         "name" : "Custom Macro Test Model",
         "model_text" : "<removed>",
         "model_output" : "bid",
         "active" : true,
         "last_modified" : "2017-03-20 15:57:03",
         "advertiser_id" : 354236,
         "member_id" : 958,
         "original_text" : "<removed>",
         "compiled_text" : "<removed>",
         "custom_model_structure" : "decision_tree",
         "id" : 82495
      },
      "dbg_info" : {... },
      "status" : "OK"
   }
} 
```

For more information, see [Custom Model Service](./custom-model-service.md).

### Step 4. Associate custom model with line item

In this example, we associate the custom model with the line item by setting the `type` field in the line item's `custom_models` array to 'nonvaluation'.

```
$cat update-ali
{
    "line-item": {
        "id": 11111,
        "custom_models": [
            {
                "id": 82495,
                "type": "nonvaluation"
            }            
        ]
    }
}
$curl -b cookies -X PUT -d '@update-ali' "https://api.appnexus.com/line-item?id=11111&advertiser_id=ADVERTISER_ID"
{
   "response" : {
      "start_element" : 0,
      "status" : "OK",
      "count" : 1,
      "num_elements" : 100,
      "line-item" : {
         "code" : "ali-cm-test",
         "inventory_discovery_budget" : null,
         "inventory_discovery" : null,
         "daily_budget_imps" : null,
         "clicktrackers" : null,
         "advertiser_id" : 354236,
         "id" : 3925282,
         "goal_type" : "none",
         "profile_id" : null,
         "prefer_delivery_over_performance" : false,
         "lifetime_pacing_pct" : null,
         "manage_creative" : false,
         "last_modified" : "2017-03-20 16:04:49",
         "payout_margin" : null,
         "flat_fee_type" : null,
         "daily_budget" : null,
         "click_model" : null,
         "lifetime_pacing" : null,
         "publishers_allowed" : "all",
         "insertion_orders" : null,
         "advertiser" : {
            "id" : 354236,
            "name" : "MCG Test Advertiser"
         },
         "enable_pacing" : null,
         "end_date" : null,
         "budget_intervals" : null,
         "click_url" : null,
         "priority" : "5",
         "pixels" : null,
         "valuation" : {
            "max_avg_cpm" : null,
            "min_margin_pct" : null,
            "goal_confidence_threshold" : null,
            "bid_price_pacing_enabled" : false,
            "goal_threshold" : null,
            "campaign_group_valuation_strategy" : null,
            "performance_mkt_managed" : false,
            "no_revenue_log" : false,
            "bid_price_pacing_lever" : 0,
            "goal_target" : null,
            "min_avg_cpm" : null
         },
         "member_id" : 958,
         "start_date" : null,
         "imptrackers" : null,
         "flat_fee" : null,
         "custom_models" : [
            {
               "active" : "1",
               "type" : "non_valuation",
               "name" : "Custom Macro Test Model",
               "id" : 82495
            }
         ],
         "delivery_goal" : null,
         "currency" : "USD",
         "expected_value_model" : null,
         "timezone" : "EST5EDT",
         "lifetime_pacing_span" : null,
         "campaigns" : null,
         "lifetime_budget" : null,
         "incrementality" : null,
         "custom_optimization_note" : null,
         "name" : "ALI Custom Macro Test",
         "creatives" : null,
         "comments" : null,
         "revenue_value" : 0,
         "inventory_type" : "both",
         "broker_fees" : null,
         "line_item_type" : "standard_v2",
         "require_cookie_for_tracking" : true,
         "lifetime_budget_imps" : null,
         "remaining_days" : null,
         "goal_pixels" : null,
         "state" : "inactive",
         "total_days" : null,
         "discrepancy_pct" : 0,
         "goal_value" : null,
         "labels" : null,
         "revenue_type" : "cpm",
         "allow_safety_pacing" : null,
         "auction_event" : null,
         "creative_distribution_type" : null
      },
      "dbg_info" : {...},
      "id" : "3925282"
   }
} 
```

## Example

Creative macro non-valuation custom model

```
#1. If the user hour is between 1am and 2am, insert the macro MyCustomMacro1 with a value of "testvalue1" and the macro MyCustomMacro2 with a value of "testvalue2".
#2. Otherwise, do nothing. (Since this is a non-valuation custom model, a value is not required for the second leaf.)
if user_hour = 1:
    leaf_name: "cm_1"
    creative_macros["MyCustomMacro1"]: "testvalue1"
    creative_macros["MyCustomMacro2"]: "testvalue2"
else:
    leaf_name: "cm_2" 
```

## Related topic
[Custom Models](./custom-models.md)
