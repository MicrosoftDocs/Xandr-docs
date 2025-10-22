---
title: Data Science Toolkit - Create a Bonsai Decision Tree Custom Model
description: Learn how to create a Bonsai decision tree custom model and easily upload it to our platform using clear, step-by-step instructions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---

# Data Science Toolkit - Create a Bonsai decision tree custom model

The Digital Platform API empowers you to create your own custom predictive models (previously known as "the AppNexus Programmable Bidder") and upload them directly to our open platform. You can:

- Have your data scientists write predictive models in [Bonsai](the-bonsai-language.md), a high-level domain-specific language (DSL) that's very similar to the popular Python language.
- Validate and upload your models via our API and assign them to campaigns via our API or UI.
- Run your models on our bidders and benefit from our infrastructure's speed, scale, reliability, and lower costs.

This page helps you get started.

## Custom model types

Currently, it's possible to create two types of custom predictive models:

### Bid price

The Bid Price model uses a decision tree to determine a campaign's CPM bid. This type of model serves as a campaign's third-party buying strategy, in place of standard CPM strategies like "Bid a Base CPM" or "Optimize to a % Margin".

### Bid modifier

The Bid Modifier model uses a decision tree to adjust a campaign's optimization-derived CPM bid up or down. This type of model is used in conjunction with a buying strategy that uses Xandr's optimization, like "Optimize to a predicted CPA goal" or "Optimize to a predicted CPC goal".

> [!NOTE]
> The bids calculated by the model are always expressed in the currency set on the advertiser, even if you have specified a different currency for the campaign.

## Process overview

> [!NOTE]
> The Alpha workflow requires using the API. Alpha clients are expected to have completed our [API Onboarding Process](../digital-platform-api/api-onboarding-process.md) before getting started.

### Step 1: Identify your requirements

You will write your custom model as a decision tree, where branches of the tree express conditions that lead to specific outputs (bid prices in the case of a Bid Price Model and bid multipliers in the case of a Bid Modifier Model). The conditions can be based on a set of Bonsai features and feature values. Before writing your tree:

- Take a close look at the [Bonsai Features](bonsai-language-features.md) that are available.
- Sketch how you want to use tree features to determine outputs.
- Be sure to take advantage of reporting data in identifying the right features and values:
  - [Standard Reporting](../invest/reporting-guide.md)
  - [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md)

#### Example: Decision tree for bid pricing

:::image type="content" source="media/datascience-c.png" alt-text="Diagram of a decision tree for bid pricing.":::

> [!NOTE]
> Use custom models for pricing, not targeting.
>
> Use custom models to determine how to price impressions, not how to target them. For targeting impressions, you should continue to use the **Targeting** section of campaign setup in or the [Profile Service](../digital-platform-api/profile-service.md) for targeting via the API.

### Step 2: Create your decision tree

Once you know the features and steps you want to follow to price or modify bids for a campaign, write them as a decision tree in our [Bonsai Language](the-bonsai-language.md). Use the examples on that page as well as the simple example below to jumpstart your understanding of how to write your tree.

> [!NOTE]
> Use tabs for indentation, not spaces.
>
> In Bonsai, indentation is used to group expressions (similar to Python). Be sure to use **tabs** to indicate line indentation. Spaces are not currently supported.

#### Example: Bonsai tree for bid pricing

> [!NOTE]
> In the code example below, lines beginning with `#` are comments to help you understand the logic of this tree.

```
# This tree determines a bid price as follows:
# 1. If the user is in California, and the hour is between 12pm and 14pm there, bid $1.50.
# 2. If the user is in New York, and the hour is between 1am and 3am there, bid $0.10.
# 3. Otherwise, bid $0.50.
 
if every region = "US:CA", user_hour range (12,14):
        1.5
elif every region = "US:NY", user_hour range (1,3):
        0.1
else:
        0.5
```

### Step 3: Encode your decision tree

Base64-encode your decision tree.

#### Example: Base64-encoded

```
IyBUaGlzIHRyZWUgZGV0ZXJtaW5lcyBhIGJpZCBwcmljZSBhcyBmb2xsb3dzOgojIDEuIElmIHRoZSB1c2VyIGlzIGluIENhbGlmb3JuaWEsIGFuZCB0aGUgaG91ciBpcyBiZXR3ZWVuIDEycG0gYW5kIDE0cG0gdGhlcmUsIGJpZCAkMS41MC4KIyAyLiBJZiB0aGUgdXNlciBpcyBpbiBOZXcgWW9yaywgYW5kIHRoZSBob3VyIGlzIGJldHdlZW4gMWFtIGFuZCAzYW0gdGhlcmUsIGJpZCAkMC4xMC4KIyAzLiBPdGhlcndpc2UsIGJpZCAkMC41MC4KCmlmIGV2ZXJ5IHJlZ2lvbiA9ICJVUzpDQSIsIHVzZXJfaG91ciByYW5nZSAoMTIsMTQpOgoJMS41CmVsaWYgZXZlcnkgcmVnaW9uID0gIlVTOk5ZIiwgdXNlcl9ob3VyIHJhbmdlICgxLDMpOgoJMC4xCmVsc2U6CgkwLjU=
```

### Step 4: Check your decision tree for errors

Use the [Custom Model Parser Service](custom-model-parser-service.md) to check the validity of your decision tree.

- In the JSON request, put your base64-encoded tree in the `model_text` field as a string.
- If there are errors, use the `error` field in the response to help you identify and resolve Bonsai syntax or feature errors. For guidance, see [Error Messages](custom-model-parser-service.md#error-messages).
- If there are no errors, the `size` field in the response shows you the size of your tree in Lisp (the format we use to store trees). Make sure the `size` is less than 3MB, or 3,145,728 bytes.  

> [!NOTE]
> If the tree is larger than 3MB, you will not be able to add the tree.

#### Example: JSON file containing your base64-encoded tree

```
$ cat check_tree.json 
 
{
    "custom-model-parser": {
                "model_text": "IyBUaGlzIHRyZWUgZGV0ZXJtaW5lcyBhIGJpZCBwcmljZSBhcyBmb2xsb3dzOgojIDEuIElmIHRoZSB1c2VyIGlzIGluIENhbGlmb3JuaWEsIGFuZCB0aGUgaG91ciBpcyBiZXR3ZWVuIDEycG0gYW5kIDE0cG0gdGhlcmUsIGJpZCAkMS41MC4KIyAyLiBJZiB0aGUgdXNlciBpcyBpbiBOZXcgWW9yaywgYW5kIHRoZSBob3VyIGlzIGJldHdlZW4gMWFtIGFuZCAzYW0gdGhlcmUsIGJpZCAkMC4xMC4KIyAzLiBPdGhlcndpc2UsIGJpZCAkMC41MC4KCmlmIGV2ZXJ5IHJlZ2lvbiA9ICJVUzpDQSIsIHVzZXJfaG91ciByYW5nZSAoMTIsMTQpOgoJMS41CmVsaWYgZXZlcnkgcmVnaW9uID0gIlVTOk5ZIiwgdXNlcl9ob3VyIHJhbmdlICgxLDMpOgoJMC4xCmVsc2U6CgkwLjU="
    }
}
```

#### Example: `POST` to `custom-model-parser` service

```
$ curl -b cookies -c cookies -X POST -d @check_tree.json 'https://api.appnexus.com/custom-model-parser'
{
    "response": {
        "service": "custom-model-parser",
        "method": "post",
        "custom-model-parser": {
            "model_text": "(if (and (region = 3922) (user_hour range 12 14)) 1.5 (if (and (region = 3950) (user_hour range 1 3)) 0.1 0.5))",
            "size": 111
        },
        "dbg_info": {
            ...
        }
    }
}
```

### Step 5: Add your decision tree as a custom model

Once you've confirmed that your tree is valid, use the [Custom Model Service](custom-model-service.md) to upload your encoded decision tree. Be sure to:

- Set the correct custom model type in the `model_output` field:
  - For a Bid Price model, use `"bid"`.
  - For a Bid Modifier model, use `"bid_modifier"`.
- Put your base64-encoded tree in the `model_text` field as a string.
- Provide a unique `name`. This is required and will make it easier to select the correct model in.
- Provide the `advertiser_id` to which the custom model belongs. You will be able to use the model only in campaigns under this advertiser.

#### Example: JSON file defining your custom model

```
$ cat custom_model.json
 
{
    "custom_model": {
        "name": "Bid by Region/Hour of Day", 
        "member_id": 958,
        "advertiser_id": 39776,
        "custom_model_structure": "decision_tree",
        "model_output": "bid",
                "model_text": "aWYgZXZlcnkgZGV2aWNlX3R5cGUgPSAiT3RoZXJzIChpbmNsdWRpbmcgUEMpIiwgdXNlcl9ob3VyIHJhbmdlICg5LDE4KToKCTEuNQplbGlmIGV2ZXJ5IGRldmljZV90eXBlIGluICgiVGFibGV0IiwgIlBob25lIiksIHVzZXJfaG91ciBpbiAoNSw2LDcsOCwxOSwyMCwyMSwyMik6CgkyCmVsc2U6CgkwLjU="
    }
}
```

#### Example: `POST` to `custom-model` service

```
$ curl -b cookies -c cookies -X POST -d @custom_model.json 'https://api.appnexus.com/custom-model'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "329",
        "start_element": 0,
        "num_elements": 100,
        "custom_model": {
            "id": 329,
            "name": "Bid by Region/Hour of Day",
            "member_id": 958,
            "advertiser_id": 39776,
            "custom_model_structure": "decision_tree",
            "model_output": "bid",
            "model_text": "aWYgZXZlcnkgcmVnaW9uID0gIlVTOkNBIiwgdXNlcl9ob3VyIHJhbmdlICgxMiwxNCk6CgkxLjUKZWxpZiBldmVyeSByZWdpb24gPSAiVVM6TlkiLCB1c2VyX2hvdXIgcmFuZ2UgKDEsMyk6CgkwLjEKZWxzZToKCTAuNQ=",
            "original_text": "if every region = \"US:CA\", user_hour range (12,14):\n\t1.5\nelif every region = \"US:NY\", user_hour range (1,3):\n\t0.1\nelse:\n\t0.5",
            "active": true,
            "last_modified": "2015-09-22 20:52:53"
        },
        "dbg_info": {
            "instance": "64.bm-hbapi.prod.nym2",
            "s1ave_hit": true,
            "db": "10.3.129.206",
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [
            ],
            "time": 39.799213409424,
            "start_microtime": 1438028779.7596,
            "version": "1.15.572",
            "s1ave_lag": 0,
            "member_last_modified_age": 21425,
            "output_term": "custom_model"
        }
    }
}
```

### Step 6: Assign your custom model to a campaign

This step changes depending on the type of custom model you are using and whether you're using the API or UI to assign your model to a campaign. Expand the relevant option below for instructions.

#### Bid price model

Use the API

Use the [Campaign Service](../digital-platform-api/campaign-service.md) to assign your custom model to a campaign. Be sure to:

- Set `cpm_bid_type` to `"custom_model"`.
- Provide the `id` of your custom model in the `bid_model` object.
- Set `inventory_type` to `"real_time"`.

  **JSON file defining your campaign**

  ```
  $ cat campaign.json
   
  {
      "campaign": {
          "name": "Custom Model Campaign - Bid by Region/Hour of Day",
          "cpm_bid_type": "custom_model",
          "bid_model": {
              "id": 329
          }, 
          "line_item_id": 34287,
          "inventory_type": "real_time"
      }
  }
  ```

  **`POST` to campaign service**

  ```
  $ curl -b cookies -c cookies -X POST -d @campaign.json 'https://api.appnexus.com/campaign?advertiser_id=45278'
   
  {
      "response": {
          "status": "OK",
          "count": 1,
          "start_element": 0,
          "num_elements": 100,
          "campaign": {
              "id": 9061978,
              "state": "active",
              "parent_inactive": false,
              "code": null,
              "advertiser_id": 45278,
              "line_item_id": 34287,
              "creative_id": null,
              "pixel_id": null,
              "short_name": null,
              "name": "Custom Model Campaign - Bid Based on Region/Hour of Day",
              "profile_id": 31746900,
              "start_date": "2015-06-03 00:00:00",
              "end_date": null,
              "timezone": "EST5EDT",
              "priority": 5,
              "cadence_modifier_enabled": false,
              "cpc_goal": null,
              "cpm_bid_type": "custom_model",
              "base_bid": 0,
              "min_bid": null,
              "max_bid": null,
              "bid_margin": 0,
              "roadblock_creatives": false,
              "roadblock_type": "no_roadblock",
              "inventory_type": "real_time",
              "last_modified": "2015-06-03 16:25:15",
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
              "impression_limit": null,
              "bid_multiplier": null,
              "remaining_days": null,
              "total_days": null,
              "supply_type_action": "exclude",
              "supply_type": null,
              "creatives": null,
              "pixels": null,
              "optimization_lookback": null,
              "campaign_modifiers": null,
              "labels": null,
              "broker_fees": null,
              "valuation": null,
              "bid_model": {
                  "id": 329,
                  "name": "Bid Based on Region/Hour of Day",
                  "active": "1"
              },
              "lifetime_budget": null,
              "lifetime_budget_imps": null,
              "daily_budget": null,
              "daily_budget_imps": null,
              "enable_pacing": null,
              "allow_safety_pacing": null,
              "lifetime_pacing": null,
              "lifetime_pacing_span": null
          },
          "dbg_info": {
              "instance": "61.bm-hbapi.prod.nym2",
              "s1ave_hit": true,
              "db": "10.3.129.211",
              "awesomesauce_cache_used": false,
              "count_cache_used": false,
              "warnings": [
              ],
              "time": 48.674821853638,
              "start_microtime": 1436503279.2047,
              "version": "1.15.558",
              "s1ave_lag": 0,
              "member_last_modified_age": 1395,
              "output_term": "campaign"
          }
      }
  }
  ```

#### Bid modifier model

Use the API

Use the [Campaign Service](../digital-platform-api/campaign-service.md) to assign your custom model to a campaign. Be sure to:

- Set `cpm_bid_type` to an optimization-based buying strategy (`"predicted"` or `"margin"`) and any corresponding required fields.
  - In the JSON below, for example, we set `cpm_bid_type` to `"predicted"` and `cpc_click_goal` to `1.00` to optimize CPM bids to a predicted $1.00 CPC goal.
- In the `bid_modifier_model` object, provide the `id` of the custom model that will modify the campaign's CPM bids.
- Set `inventory_type` to `"real_time"`.

  **JSON file defining your campaign**

  ```
  $ cat campaign.json

  {
      "campaign": {
          "name": "Custom Model Campaign - Modify Bid Based on Region/Hour of Day",
          "cpm_bid_type": “predicted”,
          “cpc_goal”: 1.00,
          "bid_modifier_model": {
              "id": 148
          },
          "line_item_id": 34287,
          "inventory_type": "real_time"
      }
  }
  ```

  **`POST` to campaign service**

  ```
  $ curl -b cookies -c cookies -X POST -d @campaign.json 'https://api.appnexus.com/campaign?advertiser_id=45278'
   
  {
      "response": {
          "status": "OK",
          "count": 1,
          "id": 10101640,
          "start_element": 0,
          "num_elements": 100,
          "campaign": {
              "id": 10101640,
              "state": "inactive",
              "parent_inactive": false,
              "code": null,
              "advertiser_id": 45278,
              "line_item_id": 34287,
              "creative_id": null,
              "pixel_id": null,
              "short_name": null,
              "name": "Custom Model Campaign - Modify Bid Based on Region/Hour of Day",
              "profile_id": null,
              "start_date": null,
              "end_date": null,
              "timezone": "EST5EDT",
              "priority": 5,
              "cadence_modifier_enabled": true,
              "cpc_goal": 1,
              "cpm_bid_type": "predicted",
              "base_bid": null,
              "min_bid": null,
              "max_bid": null,
              "bid_margin": 0,
              "roadblock_creatives": false,
              "roadblock_type": "no_roadblock",
              "inventory_type": "real_time",
              "last_modified": "2015-08-10 20:59:49",
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
              "bid_modifier_model": {
                  "id": 148,
                  "name": "Modify Bid Based on Region/Hour of Day",
                  "active": "1"
              },
              "lifetime_budget": null,
              "lifetime_budget_imps": null,
              "daily_budget": null,
              "daily_budget_imps": null,
              "enable_pacing": null,
              "allow_safety_pacing": null,
              "lifetime_pacing": null,
              "lifetime_pacing_span": null
          },
          "dbg_info": {
              "instance": "64.bm-hbapi.prod.nym2",
              "s1ave_hit": false,
              "db": "master",
              "awesomesauce_cache_used": false,
              "count_cache_used": false,
              "warnings": [
              ],
              "time": 1010.1411342621,
              "start_microtime": 1439240389.0273,
              "version": "1.15.580",
              "s1ave_lag": 0,
              "member_last_modified_age": 1439240389,
              "output_term": "campaign"
          }
      }
  }
  ```

## Related topics

- [Bonsai Language Features](bonsai-language-features.md)
- [Custom Model Parser Service](custom-model-parser-service.md)
- [Custom Model Service](custom-model-service.md)
- [Campaign Service](../digital-platform-api/campaign-service.md)
