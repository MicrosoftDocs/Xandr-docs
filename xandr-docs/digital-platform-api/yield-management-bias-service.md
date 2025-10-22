---
title: Yield Management Bias Service
description: Explore the Yield Management Bias service to create and update biases within an existing Yield Management Profile.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Yield Management Bias service

The Yield Management Bias Service is used to create and update biases within an existing [Yield Management Profile](yield-management-profile-service.md). Biases are a way of modifying bids from certain buyers or groups of buyers so that they appear higher or lower than they actually are for the purposes of running an auction.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | - [https://api.appnexus.com/ym-bias?ym_profile_id=YM_PROFILE_ID](https://api.appnexus.com/ym-bias?ym_profile_id=YM_PROFILE_ID)<br>- [https://api.appnexus.com/ym-bias?ym_profile_code=YM_PROFILE_CODE](https://api.appnexus.com/ym-bias?ym_profile_code=YM_PROFILE_CODE)<br>(ym-bias JSON) | Add a bias. |
| `PUT` | - [https://api.appnexus.com/ym-bias?id=YM_BIAS_ID](https://api.appnexus.com/ym-bias?id=YM_BIAS_ID)<br>- [https://api.appnexus.com/ym-bias?code=YM_BIAS_CODE](https://api.appnexus.com/ym-bias?code=YM_BIAS_CODE)<br>(ym-bias JSON) | Modify an existing bias. |
| `GET` | - [https://api.appnexus.com/ym-bias?ym_profile_id=YM_PROFILE_ID](https://api.appnexus.com/ym-bias?ym_profile_id=YM_PROFILE_ID)<br>- [https://api.appnexus.com/ym-bias?ym_profile_code=YM_PROFILE_CODE](https://api.appnexus.com/ym-bias?ym_profile_code=YM_PROFILE_CODE) | View all biases associated with a particular [Yield Management Profile](yield-management-profile-service.md). |
| `GET` | - [https://api.appnexus.com/ym-bias?id=YM_BIAS_ID](https://api.appnexus.com/ym-bias?id=YM_BIAS_ID)<br>- [https://api.appnexus.com/ym-bias?code=YM_BIAS_CODE](https://api.appnexus.com/ym-bias?code=YM_BIAS_CODE) | View a specific bias. |
| `GET` | [https://api.appnexus.com/ym-bias?id=1,2,3](https://api.appnexus.com/ym-bias?id=1,2,3) | View multiple biases by ID using a comma-separated list. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for a yield management bias.<br>**Default:** Auto-incremented Number (i.e. 123).<br>**Required On:** `PUT` |
| `code` | string | A optional custom code used to reference a yield management bias.<br>**Default:** `NULL` |
| `name` | string | A name used to describe a yield management bias.<br>**Default:** `None`<br>**Required On:** `POST` |
| `description` | string | An optional description how the yield management bias is being used.<br>**Default:** `NULL` |
| `ym_profile_id` | int | The ID of the yield management profile that the yield management bias is associated with. For details, see the [Yield Management Profile Service](yield-management-profile-service.md).<br><br>**Note:** This ID cannot be changed once it is set.<br><br>**Default:** `NULL`<br>**Required On:** `POST` |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a bias. A profile is a generic set of rules for targeting inventory, and certain biases may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md).<br>**Default:** `NULL` |
| `priority` | int | The priority field (optional) is used to create a hierarchy of how the bias should to be applied. Value may be between `1`-`10` where priority `10` is treated as the highest priority value.<br>**Default:** `5` |
| `members` | array of objects | This is an array specifying the member(s) the yield management bias should be applied to. For details, see the [Members Array](#members-array) below.<br>**Default:** `NULL` |
| `buyer_groups` | array of objects | This is an array specifying the buyer group(s) the yield management bias should be applied to. For details, see the [Buyer Groups Array](#buyer-groups-array) below.<br>**Default:** `NULL` |

### Members array

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the buyer member (as found in the [Platform Member Service](platform-member-service.md)) for which the bias should be applied.<br>**Default:** `None`<br>**Required On:** `POST`, `PUT` |
| `name` | array | This is the name of the buyer member.<br>**Default:** N/A |
| `type` | enum<br>(`'percent'`,`'cpm'`) | This determines which value to use for the bias, represented as a percentage or a flat CPM.<br>**Default:** `"percent"`<br>**Required On:** `POST`, `PUT` |
| `bias_pct` | double | This is the % amount the buyer member should be adjusted by. If `bias_pct = 5`, then the net bid will be increased 5%.<br>**Default:** `0.00`<br>**Required On:** `POST`, `PUT` (if `type` is `'percent'`). |
| `bias_cpm` | double | This is the CPM increase/decrease the buyer member should be adjusted by.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` (if `type` is `'cpm'`). |

### Buyer groups array

| Parameter | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the buyer group for which the bias should be applied.<br>**Default:** `None`<br>**Required On:** `POST`, `PUT` |
| `name` | array | This is the name of the buyer group.<br>**Default:** N/A |
| `type` | enum<br>(`'percent'`,`'cpm'`) | This determines which value to use for the bias, represented as a percentage or a flat CPM.<br>**Default:** `"percent"`<br>**Required On:** `POST`, `PUT` |
| `bias_pct` | double | This is the % amount the buyer member should be adjusted by. If `bias_pct = 5`, then the net bid will be increased 5%.<br>**Default:** `0.00`<br>**Required On:** `POST`, `PUT` (if `type` is `'percent'`). |
| `bias_cpm` | double | This is the CPM increase/decrease the buyer member should be adjusted by.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` (if `type` is `'cpm'`). |

## Examples

### View a specific bias

```
$ curl -b cookies -c cookies  "https://api.appnexus.com/ym-bias?id=1234"
{
    "ym-bias": {
        "member_id": 3,
        "id": 124,
        "name": "Canada Bias",
        "description": "This rule will used to set the bias for a set of demand attributes across Canadian inventory.",
        "profile_id": 1241,
        "priority": 5,
        "ym_profile_id": 1234
        "members": [
                    {
                        "id": 100,
                        "name": "eBay",
                        "type": "percent",
                        "bias_pct": 10
                    },
                    {
                        "id": 256,
                        "name": "MiG",
                        "type": "cpm",
                        "bias_cpm": -0.25
                    }
                ],
        "buyer_groups": [
                    {
                        "id": 120,
                        "name": "Third Party Ad Networks",
                        "type": "percent",
                        "bias_pct": -5
                    },
                    {
                        "id": 153,
                        "name": "Value Ad Networks",
                        "type": "cpm",
                        "bias_cpm": 0.50
                    }
                ]
    }
}
```

### View all biases associated with a given [Yield Management Profile](yield-management-profile-service.md)

> [!NOTE]
> The first bias in the array below is not associated with `{{members}}` or `{{buyer_groups}}`, but with a `{{profile_id}}` (for details, see [JSON fields](#json-fields) above).

```
$ curl -b cookies "https://api.appnexus.com/ym-bias?ym_profile_id=123"
{
 "response": {
  "status": "OK",
  "ym-biases": [
   {
    "priority": 10,
    "member_id": 999,
    "members": null,
    "name": "Low Frequency Bias",
    "last_modified": "2011-02-22 19:26:32",
    "code": null,
    "id": 4,
    "description": null,
    "profile_id": 456,
    "ym_profile_id": 123,
    "buyer_groups": null
   },
   {
    "priority": 5,
    "member_id": 999,
    "members": [
               {
        "id": 890,
        "name": "The one I'm biased slightly against",
        "type": "percent",
        "bias_pct": -5
           }
    ],
    "name": "A secret bias only I can see",
    "last_modified": "2011-07-05 23:32:46",
    "code": null,
    "id": 1575,
    "description": null,
    "profile_id": null,
    "ym_profile_id": 123,
    "buyer_groups": null
   }
  ],
  "start_element": null,
  "count": 2,
  "num_elements": null
 }
}
```
