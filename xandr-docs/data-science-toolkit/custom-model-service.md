---
title: Data Science Toolkit - Custom Model Service
description: Learn how the Custom Model service lets you add and maintain custom predictive models (decision trees) for use in campaigns.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---


# Data Science Toolkit - Custom model service

The Custom Model service lets you add and maintain custom predictive models (decision trees) for use in campaigns. For background information, see [Custom Models](custom-models.md).

> [!TIP]
> Before adding a custom model, use the [Custom Model Parser Service](custom-model-parser-service.md) to check the validity and size of your decision tree.

## REST API

**Add a new custom model:**

``` 
POST https://api.appnexus.com/custom-model  
(new_model JSON)
```

**Modify a custom model:**

``` 
PUT https://api.appnexus.com/custom-model?id=ID
(model_update JSON)
```

**View all custom models:**

``` 
GET https://api.appnexus.com/custom-model
```

**View a specific custom model:**

``` 
GET https://api.appnexus.com/custom-model?id=ID
```

**Delete a custom model:**

``` 
DELETE https://api.appnexus.com/custom-model?id=ID
```

> [!NOTE]
> You cannot delete a custom model that is used by one or more campaigns.

**Find out which fields you can filter and sort by:**

``` 
GET https://api.appnexus.com/custom-model/meta
```

## JSON fields

| Field | Type (Length) | Description |
|--|--|--|
| `active` | Boolean | If `true`, the custom model is active and available for use in campaigns.<br>**Default**: `true` |
| `advertiser_id` | int | The ID of the advertiser to which the custom model belongs.<br>**Required on**: `POST` |
| `code` | string | A custom code that is used as an external ID or as a look-up value for an object. This value must be unique within your member. |
| `custom_model_structure` | enum | The structure of the custom model. Currently, the only allowed structure is `"decision_tree"`.<br>**Required on**: `POST` |
| `id` | int | The ID of the custom model.<br>**Default**: Auto-generated number<br>**Required On**: `PUT/ DELETE`, in query string |
| `last_modified` | date | **Read-only**. The date and time when the custom model was last modified. |
| `member_id` | int | **Read-only**. The ID of the member to which the custom model belongs.<br>**Default**: Member's ID |
| `model_output` | enum | The type of custom model. Possible values:<br>- `"bid"`: The Bid Price model outputs a CPM bid. This type of model serves as a campaign's third-party buying strategy in place of standard CPM strategies. To use this type of model in a [campaign](../digital-platform-api/campaign-service.md), set `cpm_bid_type` to `"custom_model"` and then specify the custom model ID in the `bid_model` object.<br>- `"bid_modifier"`: The Bid Modifier model applies a multiplier to a campaign's optimization-derived CPM bid. This type of model is used in conjunction with a Xandr optimization-based buying strategy (when `cpm_bid_type` is `"predicted"` or `"margin"`). To use this type of model in a [campaign](../digital-platform-api/campaign-service.md), specify the custom model ID in the `bid_modifier_model` object.<br>**Required on**: `POST` |
| `model_text` | string | The logic of the model, expressed as a decision tree. You must write your decision tree in our Bonsai Language and then include a base64-encoded version here.<br>**Default**: `null`<br>**Note**:<br>- Size limit: Your tree must be smaller than 3 MB, or 3,145,728 bytes. If it is larger than that, you will not be able to add your tree.<br>- GET queries: In a GET query, the `model_text` will ONLY be returned if you provide a model ID in the query string. It will not be returned for unfiltered queries.<br>- Check the Validity and Size of Your Tree.<br>- Before adding a custom model, use the [Custom Model Parser Service](custom-model-parser-service.md) to check the validity and size of your decision tree. See that service for details about validation and error messages. |
| `name` | string (191) | The name of the custom model. This must be unique and must be no more than 191 characters.<br>**Required On**: `POST` |
| `original_text` | string | **Read-only**. The decision tree in plain text. We provide this in the response so that you can retrieve and review your tree's original format whenever necessary to iterate on tree design. Note that tabs are replaced with `\t` and new lines are replaced with `\n`.<br>**Default**: `null`<br>**Note**: In a GET query, the `original_text` will ONLY be returned if you identify a specific model ID in the query string. It will not be returned for unfiltered queries. |

## Examples

**View all custom models**

``` 
$ curl -b cookies -c cookies 'https://api.appnexus.com/custom-model'
 
{
    "response": {
        "status": "OK",
        "count": 10,
        "start_element": 0,
        "num_elements": 100,
        "custom_models": [
            {
                "id": 327,
                "name": "Bid by Region/Hour of Day",
                                "code": "code1_abc12345",
                "member_id": 958,
                "advertiser_id": 39776,
                "custom_model_structure": "decision_tree",
                "model_output": "bid",
                "active": true,
                "last_modified": "2015-09-22 19:52:57"
            },
            {
                "id": 329,
                "name": "Bid by Device Type/Hour of Day",
                                "code": "code2_abc12345",
                "member_id": 958,
                "advertiser_id": 39776,
                "custom_model_structure": "decision_tree",
                "model_output": "bid",
                "active": true,
                "last_modified": "2015-09-22 20:52:53"
            },
            ...  
        ]
    }
}
```

**View a specific custom model**

``` 
$ curl -b cookies -c cookies 'https://api.appnexus.com/custom-model?id=327'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "custom_model": {
            "id": 327,
            "name": "Bid by Region/Hour of Day",
                        "code": "code1_abc12345",
            "member_id": 1234,
            "advertiser_id": 39776,
            "custom_model_structure": "decision_tree",
            "model_output": "bid",
            "model_text": "aWYgZXZlcnkgcmVnaW9uID0gIlVTOkNBIiwgdXNlcl9ob3VyIHJhbmdlICgxMiwxNCk6CgkxLjUKZWxpZiBldmVyeSByZWdpb24gPSAiVVM6TlkiLCB1c2VyX2hvdXIgcmFuZ2UgKDEsMyk6CgkwLjEKZWxzZToKCTAuNQ==",
            "original_text": "if every region = \"US:CA\", user_hour range (12,14):\n\t1.5\nelif every region = \"US:NY\", user_hour range (1,3):\n\t0.1\nelse:\n\t0.5",
            "active": true,
            "last_modified": "2015-09-22 19:52:57"
        }
    }
}
```

**Add a custom model**

``` 
$ curl -b cookies -c cookies -X POST -d @custom_model.json 'https://api.appnexus.com/custom-model?member_id=1234'
$ cat custom_model.json
 
{
    "custom_model": {
        "name": "Bid by Device Type/Hour of Day", 
        "advertiser_id": 39776,
        "custom_model_structure": "decision_tree",
        "model_output": "bid",
                "model_text": "aWYgZXZlcnkgZGV2aWNlX3R5cGUgPSAiT3RoZXJzIChpbmNsdWRpbmcgUEMpIiwgdXNlcl9ob3VyIHJhbmdlICg5LDE4KToKCTEuNQplbGlmIGV2ZXJ5IGRldmljZV90eXBlIGluICgiVGFibGV0IiwgIlBob25lIiksIHVzZXJfaG91ciBpbiAoNSw2LDcsOCwxOSwyMCwyMSwyMik6CgkyCmVsc2U6CgkwLjU="
    }
}
 
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
            "name": "Bid by Device Type/Hour of Day",
                        "code": null,
            "member_id": 1234,
            "advertiser_id": 39776,
            "custom_model_structure": "decision_tree",
            "model_output": "bid",
            "model_text": "aWYgZXZlcnkgZGV2aWNlX3R5cGUgPSAiT3RoZXJzIChpbmNsdWRpbmcgUEMpIiwgdXNlcl9ob3VyIHJhbmdlICg5LDE4KToKCTEuNQplbGlmIGV2ZXJ5IGRldmljZV90eXBlIGluICgiVGFibGV0IiwgIlBob25lIiksIHVzZXJfaG91ciBpbiAoNSw2LDcsOCwxOSwyMCwyMSwyMik6CgkyCmVsc2U6CgkwLjU=",
            "original_text": "if every device_type = \"Others (including PC)\", user_hour range (9,18):\n\t1.5\nelif every device_type in (\"Tablet\", \"Phone\"), user_hour in (5,6,7,8,19,20,21,22):\n\t2\nelse:\n\t0.5",
            "active": true,
            "last_modified": "2015-09-22 20:52:53"
        }
    }
}
 
```

**Modify a custom model**

``` 
$ cat custom_model_update.json 
 
{
    "custom_model": {
        "model_text": "aWYgc2VnbWVudCAxMjM0Og0KwqDCoMKgwqBpZi..."    
    }
}
 
$ curl -b cookies -c cookies -X PUT -d @custom_model_update.json 'https://api.appnexus.com/custom-model?id=3'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "custom_model": {
            "id": 3,
            "name": "User Hour Model",
                        "code": null,
            "member_id": 1234,
            "advertiser_id": 83736,
            "custom_model_structure": "decision_tree",
            "model_output": "bid",
            "model_text": "aWYgc2VnbWVudCAxMjM0Og0KwqDCoMKgwqBpZi...",
            "original_text": "if every region = \"US:CA\", user_hour range (12,16):\n\t1.5\nelif every region = \"US:NY\", user_hour range (1,5):\n\t0.1\nelse:\n\t0.5",
            "active": true
        }
    }
}
```

**Delete a custom model**

``` 
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/custom-model?id=3'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```

## Related topics

- [Custom Model Parser Service](custom-model-parser-service.md)
- [The Bonsai Language](the-bonsai-language.md)
