---
title: Data Science Toolkit - Creative Selection Custom Model
description: Explore the process of assigning creatives using a custom model, with syntax explanations, detailed API workflow instructions, and illustrative examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---

# Data Science Toolkit - Creative selection custom model

By default, Xandr randomly distributes the creatives associated with a line item. You can also assign creatives using a custom model. Any [Bonsai Language](the-bonsai-language.md) feature or logic can be used to determine which creative should be served.

> [!NOTE]
> This functionality is only available for the [Augmented Line Item](../digital-platform-api/line-item-service---ali.md).

## Weighting process

In each leaf, you list creative IDs and their weights. Weights may be integers between 0-1000. The allocation percentage of a creative is determined by dividing the creative's weight by the sum of the weight of all eligible creatives.
  
For example, a line item has three creatives, A, B, and C and they are weighted respectively 50, 30, and 20. They will serve on 50%, 30%, and 20% of all impressions if all creatives are eligible. If only creatives B and C are eligible, creative B will serve on 60% of impressions and creative C will serve on 40%.

> [!NOTE]
> It's a good idea to include only creatives that will be eligible in similar circumstances on the same leaf to make it easier for you to determine the effects of weighting and targeting. For example, you might want to include only creatives of the same size, or only creatives that are eligible for SSL, in a single leaf, ensuring that all creatives will be eligible for the same impressions.

Follow these guidelines for getting the best results when weighting your creatives:

- Creatives with a weight of zero (0) will not be served.
- If a leaf does not contain a creative list, creative selection will revert back to random selection of creatives associated with the line item.
- Models may not contain duplicate creative IDs.
- Creatives must be attached to the line item. Creatives that are attached to the line item but not included in a leaf are considered to have a weight of zero.

## Creative selection leaf syntax

The syntax for creative distribution leaves is:

```
leaf_name: "NAME"
creatives: {ID: WEIGHT, ID: WEIGHT, ID: WEIGHT} 
```

## API process overview

### Step 1: Create an augmented line item

In this example, we create an augmented line item.

```
$cat ali
{
    "line-item": {
        "name": "ALI Creative Selection Test",
        "code": "ali-cs-test",
        "state": "inactive",
        "line_item_type": "standard_v2",
        "revenue_type": "cpm"
    }
}
$curl -b cookies -X POST -s -d @ali "https://api.appnexus.com/line-item?advertiser_id=ADVERTISER_ID"   
{
   "response" : {
      "status" : "OK",
      "start_element" : 0,
      "line-item" : {
         "lifetime_pacing_span" : null,
         "prefer_delivery_over_performance" : false,
          ...
      "dbg_info" : {...},
      "num_elements" : 100
   }
}
```

For more information, see [ALI Workflow with Custom Models](ali-workflow-with-custom-models.md).

### Step 2: Attach creative IDs to augmented line item

In this example, we associate three creatives to our line item.

```
 $ cat line-item
{
    "line-item": 
                {
                "id": "11111",
                "manage_creative": true,
                "creatives": [
                        {"id": 12345},
                        {"id": 67890},
                        {"id": 12347}
                                        ] 
                }
}
$ curl -b cookies -X PUT -d @line-item 'https://api.appnexus.com/line-item?id=LINEITEM_ID&advertiser_id=ADVERTISER_ID&id=LINE_ITEM_ID'
{
   "response" : {
      "dbg_info" : {...},
      "line-item" : {
         "profile_id" : null,
         "enable_pacing" : null,
         "lifetime_pacing" : null,
         "revenue_value" : 0,
         "lifetime_budget_imps" : null,
         ...
         "creatives" : [
            {
               "code" : null,
               "height" : 600,
               "audit_status" : "no_audit",
               "weight" : null,
               "is_prohibited" : false,
               "is_self_audited" : true,
               "id" : 22367666,
               "format" : "image",
               "state" : "inactive",
               "pop_window_maximize" : null,
               "name" : "MCG Test Ad 120x600",
               "is_expired" : true,
               "width" : 120
            },
            {
               "pop_window_maximize" : null,
               "is_expired" : true,
               "name" : "MCG Test Ad 300x240",
               "width" : 300,
               "id" : 22367932,
               "format" : "image",
               "state" : "inactive",
               "is_self_audited" : true,
               "code" : null,
               "weight" : null,
               "height" : 240,
               "audit_status" : "no_audit",
               "is_prohibited" : false
            },
            {
               "state" : "inactive",
               "id" : 38520371,
               "format" : "image",
               "width" : 320,
               "pop_window_maximize" : null,
               "is_expired" : true,
               "name" : "480.png",
               "is_prohibited" : false,
               "code" : null,
               "audit_status" : "no_audit",
               "height" : 480,
               "weight" : null,
               "is_self_audited" : false
            }
         ] 
                ...    
   }
}
```

### Step 3: Create a custom model tree

In this example, we create a custom model that will weigh and select creatives.

```
$cat creative-tree
if user_hour = 1:
        leaf_name: "cs_1"
        creatives: {12345: 30, 67890: 20}
else:
        leaf_name: "cs_2"
        creatives: {12347: 1}
```

### Step 4: Upload custom model

In this example, we upload the custom model.

```
$ cat custom_model
 
{
    "custom_model": {
        "name": "Creative Selection Test Model", 
        "member_id": 958,
        "advertiser_id": ADVERTISER_ID,
                "custom_model_structure": "decision_tree",
        "model_output": "bid",
                "model_text": "aWYgdXNlcl9ob3VyID0gMToNCglsZWFmX25hbWU6ICJjc18xIg0KCWNyZWF0aXZlczogezEyMzQ1OiAzMCwgNjc4OTA6IDIwfQ0KZWxzZToNCglsZWFmX25hbWU6ICJjc18yIg0KCWNyZWF0aXZlczogezEyMzQ3OiAxfQ=="
                }
}
$ curl -b cookies -X POST -d @custom-model "https://api.appnexus.com/custom-model?advertiser_id=39776"   
{
   "response" : {
      "status" : "OK",
      "count" : 1,
      "start_element" : 0,
      "dbg_info" : {
        ...
      },
      "num_elements" : 100,
      "id" : "80324",
      "custom_model" : {
         "name" : "Creative Selection Test Model",
         "original_text" : "<removed>",
         "code" : null,
         "custom_model_structure" : "decision_tree",
         "compiled_text" : "<removed>",
         "model_output" : "bid",
         "id" : 33333,
         "last_modified" : "2017-03-17 17:29:22",
         "active" : true,
         "advertiser_id" : 354236,
         "model_text" : "<removed>"
      }
   }
}
```

For more information, see [Custom Model Service](custom-model-service.md).

### Step 5: Associate custom model with line item

In this example, we associate the custom model with the line item by setting the `type` field in the line item's `custom_models` array to '`creative_selection`'.

```
$cat update-ali
{
    "line-item": {
        "id": 11111,
        "custom_models": [
            {
                "id": 33333,
                "type": "creative_selection"
            }            
        ]
    }
}
$curl -b cookies -X PUT -d '@update-ali' "https://api.appnexus.com/line-item?id=11111&advertiser_id=ADVERTISER_ID"
{
   "response" : {
      "dbg_info" : {...},
      "num_elements" : 100,
      "id" : "3919914",
      "count" : 1,
      "line-item" : {
         "profile_id" : null,
         "imptrackers" : null,
         "flat_fee" : null,
         "inventory_discovery" : null,
         "broker_fees" : null,
         "state" : "inactive",
         "lifetime_budget_imps" : null,
         "prefer_delivery_over_performance" : false,
         "creatives" : [...],
                 ...
         "custom_models" : [
            {
               "type" : "creative_selection",
               "name" : "Creative Selection Test Model",
               "id" : 80324,
               "active" : "1"
            }
         ]
                ...
   }
} 
```

## Examples

### Creative distribution tree with different weights for creatives

```
if user_hour = 1:
        leaf_name: "cs_1"
        creatives: {64947527: 30, 64946991: 20, 65023365: 10}
else:
        leaf_name: "cs_2"
        creatives: {65946990: 1}
```

### Creative distribution tree with uniform random distribution

```
if user_hour = 1:
        leaf_name: "cs_1"
        creatives: {64947527: 1, 64946991: 1, 65023365: 1}
else:
        leaf_name: "cs_2"
        creatives: {65946990: 1}
```
