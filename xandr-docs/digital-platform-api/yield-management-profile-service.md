---
title: Yield Management Profile Service
description: Explore the Yield Management Profile service, to create and update profiles that define dynamic price floors, bid biases, and auction tiers for a publisher.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Yield Management Profile service

The Yield Management Profile Service is used to create and update yield management profiles which define dynamic [price floors](yield-management-floor-service.md), [bid biases](yield-management-bias-service.md), and [auction tiers](yield-management-auction-tier-service.md) for a publisher.

More concretely, the Yield Management Profile is a set of rules with the following properties and behaviors:

- The profile *targets*:
  - Some/all inventory
  - Some/all buyers

- The profile *specifies*:
  - 0 or more floor rules
  - 0 or more bias rules
  - 0 or more modifiers that will apply to those floors and biases
  - 0 or more auction tiers

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | - [https://api.appnexus.com/ym-profile?id=YMP_ID](https://api.appnexus.com/ym-profile?id=YMP_ID)<br>- [https://api.appnexus.com/ym-profile?id=YMP_CODE](https://api.appnexus.com/ym-profile?id=YMP_CODE) | View a specific profile. |
| `GET` | - [https://api.appnexus.com/ym-profile?publisher_id=PUBLISHER_ID](https://api.appnexus.com/ym-profile?publisher_id=PUBLISHER_ID)<br>- [https://api.appnexus.com/ym-profile?publisher_code=PUBLISHER_CODE](https://api.appnexus.com/ym-profile?publisher_code=PUBLISHER_CODE) | View all profiles associated with a particular publisher. |
| `GET` | [https://api.appnexus.com/ym-profile?id=1,2,3](https://api.appnexus.com/ym-profile?id=1,2,3) | View multiple profiles by ID using a comma-separated list. |
| `POST` | [https://api.appnexus.com/ym-profile](https://api.appnexus.com/ym-profile)<br>(ym-profile JSON) | Add a profile.<br><br>**Note:** After adding a profile, you can use the [Publisher Service](publisher-service.md) to assign the profile to a particular publisher. |
| `PUT` | - [https://api.appnexus.com/ym-profile?id=YMP_ID](https://api.appnexus.com/ym-profile?id=YMP_ID)<br>- [https://api.appnexus.com/ym-profile?id=YMP_CODE](https://api.appnexus.com/ym-profile?id=YMP_CODE)<br>(ym profile JSON) | Modify an existing profile. |
| `DELETE` | [https://api.appnexus.com/ym-profile?id=YMP_ID](https://api.appnexus.com/ym-profile?id=YMP_ID) | Delete an existing profile. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for a yield management profile.<br>**Default:** Auto-incremented Number (i.e. 123).<br>**Required On:** `PUT` |
| `code` | string | An optional custom code used to reference a yield management profile.<br>**Default:** `NULL` |
| `name` | string | A name used to describe a yield management profile.<br>**Default:** `None`<br>**Required On:** `POST` |
| `description` | string | An optional description of the yield management profile.<br>**Default:** `NULL` |
| `base_ym_bias_id` | int | The ID of the YM bias that should be applied if no other YM biases should be used. Typically, this YM bias has a priority 1 (lowest priority) and no profile.<br>**Default:** `NULL` |
| `base_ym_floor_id` | int | The ID of the YM floor that should be applied if no other YM floors should be used. Typically, this YM floor has a priority 1 (lowest priority) and no profile.<br>**Default:** `NULL` |
| `publisher_id` | int | **Read-only.** The ID of the publisher to which the yield management profile is associated. You use the [Publisher Service](publisher-service.md) to make the association between the yield management profile and the publisher. |
| `modifiers` | array | The modifiers applied to the technical attribute of the creative. For more details, see [Modifiers](#modifiers) below.<br>**Default:** `NULL` |
| `biases` | array | The biases applied to demand side objects: Buyer Groups, Buyer Members. For more details, see [Biases](#biases) below.<br>**Default:** `NULL` |
| `floors` | array | The floor prices applied based on inventory and user targeting. For more details, see [Floors](#floors) below.<br>**Default:** `NULL` |
| `last_modified` | timestamp | Time of last modification to this yield management profile.<br>**Default:** `N/A` |

### Modifiers

| Field | Type | Description |
|:---|:---|:---|
| `technical_attributes` | array | This is an array specifying the technical attributes that the yield management modifier should be applied to.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` |

### Modifiers - Technical attributes

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the technical attribute (as found in the [Technical Attribute Service](technical-attribute-service.md)) for which the modifier should be applied.<br>**Default:** `None`<br>**Required On:** `POST`, `PUT` |
| `name` | name | This is the name of the technical attribute.<br>**Default:** `N/A` |
| `type` | enum<br>(`'bias-pct'`,<br>`'bias-cpm'`,<br>`'floor-pct'`,<br>`'floor-cpm'`) | This determines which value to use for the modifier, represented as a percentage or a flat CPM, and what the modifier should be applied to -- the bid or the floor.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` |
| `amount_pct` | double | This is the % amount the bid or floor should be modified by. If `bias_pct = 5`, then the net bid will be increased 5%.<br>**Default:** `0.00`<br>**Required On:** `POST`, `PUT` (if `type` is `'bias-pct'` or `'floor-pct'`). |
| `amount_cpm` | double | This is the CPM increase/decrease that the bid or floor should be modified by.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` (if `type` is `'bias-cpm'` or `'floor-cpm'`). |

### Biases

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for a yield management bias.<br>**Default:** Auto-incremented Number (i.e. 123).<br>**Required On:** `PUT` |
| `code` | string | A optional custom code used to reference a yield management bias.<br>**Default:** `NULL` |
| `name` | string | A name used to describe a yield management bias.<br>**Default:** `None`<br>**Required On:** `POST` |
| `description` | string | An optional description how the yield management bias is being used.<br>**Default:** `NULL` |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a bias. A profile is a generic set of rules for targeting inventory, and certain biases may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md).<br>**Default:** `NULL` |
| `priority` | int | The priority field (optional) is used to create a hierarchy of how the bias should to be applied. Value may be between `1`-`10` where priority `10` is treated as the highest priority value.<br>**Default:** `5` |
| `members` | array | This is an array specifying the member(s) the yield management bias should be applied to.<br>**Default:** `NULL` |
| `buyer_groups` | array | This is an array specifying the buyer group(s) the yield management bias should be applied to.<br>**Default:** `NULL` |

### Biases - Buyer members

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the buyer member (as found in the [Platform Member Service](platform-member-service.md)) for which the bias should be applied.<br>**Default:** `None`<br>**Required On:** `POST`, `PUT` |
| `name` | string | This is the name of the buyer member.<br>**Default:** `N/A` |
| `type` | enum<br>(`'percent'`,`'cpm'`) | This determines which value to use for the bias, represented as a percentage or a flat CPM.<br>**Default:** `"percent"`<br>**Required On:** `POST`, `PUT` |
| `bias_pct` | double | This is the % amount the buyer member should be adjusted by. If `bias_pct = 5`, then the net bid will be increased 5%.<br>**Default:** `0.00`<br>**Required On:** `POST`, `PUT` (if `type` is `'percent'`). |
| `bias_cpm` | double | This is the CPM increase/decrease the buyer member should be adjusted by.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` (if `type` is `'cpm'`). |

### Biases - Buyer groups

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the buyer group for which the bias should be applied.<br>**Default:** None<br>**Required On:** `POST`, `PUT` |
| `name` | string | This is the name of the buyer group.<br>**Default:** `N/A` |
| `type` | enum<br>(`'percent'`,`'cpm'`) | This determines which value to use for the bias, represented as a percentage or a flat CPM.<br>**Default:** `"percent"`<br>**Required On:** `POST`, `PUT` |
| `bias_pct` | double | This is the % amount the buyer member should be adjusted by. If `bias_pct = 5`, then the net bid will be increased 5%.<br>**Default:** `0.00`<br>**Required On:** `POST`, `PUT` (if `type` is `'percent'`). |
| `bias_cpm` | double | This is the CPM increase/decrease the buyer member should be adjusted by.<br>**Default:** `NULL`<br>**Required On:** `POST`, `PUT` (if `type` is `'cpm'`). |

### Floors

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for a yield management floor.<br>**Default:** Auto-incremented Number (i.e. 123).<br>**Required On:** `PUT` |
| `code` | string | A optional custom code used to reference a yield management floor.<br>**Default:** `NULL` |
| `name` | string | A name used to describe a yield management floor.<br>**Default:** `None`<br>**Required On:** `POST` |
| `description` | string | An optional description how the yield management floor is being used.<br>**Default:** `NULL` |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a floor. A profile is a generic set of rules for targeting inventory, and certain floors may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md).<br>**Default:** `NULL` |
| `priority` | int | The priority field (optional) is used to create a hierarchy of how the floor should to be applied. Value may be between `1`-`10` where priority `10` is treated as the highest priority value.<br>**Default:** `5` |
| `hard_floor` | double | This cpm floor is used as the hard reserve price to be applied.<br>**Default:** `None`<br>**Required On:** `POST` |
| `soft_floor` | double | This cpm floor is used as the soft reserve, defined as the lowest price at which price reduction will occur - This must be >= the hard floor if set.<br>**Default:** `NULL` |
| `members` | array | This is an array specifying the member(s) the yield management floor should be applied to.<br>**Default:** `NULL` |
| `brands` | array | This is an array specifying the brand(s) the yield management floor should be applied to.<br>**Default:** `NULL` |
| `categories` | array | This is an array specifying the category(ies) the yield management floor should be applied to.<br>**Default:** `NULL` |
| `default_calculation_type` | enum<br>(`'gross'`,`'net'`) | This is used to determine if the floor should be applied to the gross or net bid.<br>**Default:** `gross` |
| `apply_floor_to_direct` | int | This is used to determine if the floor should be applied only to specified members or in addition to managed demand.<br>**Default:** `1` |

### Floors - Members

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the buyer member (as found in the [Platform Member Service](platform-member-service.md)) for which the floor should be applied.<br>**Required On:** `POST`, `PUT` |
| `name` | array | This is the name of the buyer member. |

### Floors - Brands

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the brand of the creative (as found in the [Brand Service](brand-service.md)) for which the floor should be applied.<br>**Required On:** `POST`, `PUT` |
| `name` | array | This is the name of the brand. |

### Floor - Categories

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the category of the creative of the creative (as found in the [Category Service](category-service.md)) for which the floor should be applied.<br>**Required On:** `POST`, `PUT` |
| `name` | array | This is the name of the category. |

## Example

### View a specific yield management profile

```
$ curl -b cookies -c cookies  "https://api.appnexus.com/ym-profile?id=8"
{
    "ym-profile": {
        "id": 1234,
        "member_id": 3,
        "active": true,
        "name": "Publisher X YMP",
        "description": "This profile will be used for publisher X.",
        "base_ym_bias_id": 125,
        "base_ym_floor_id": 1574,
        "last_modified": "2010-10-02 12:00:00",
        "modifiers": {
            "technical_attributes": [
                {
                    "id": 2,
                    "type": "bias-cpm",
                    "amount_pct": 0,
                    "amount_cpm": -1,
                    "name": "Flash"
                },
                {
                    "id": 3,
                    "type": "bias-pct",
                    "amount_pct": 10,
                    "amount_cpm": null,
                    "name": "Text"
                }
            ]
        },
        "biases": [
            {
                "id": 124,
                "name": "YMP Canada Bias",
                "description": "This rule will used to set the bias for a set of demand attributes across Canadian inventory.",
                "profile_id": 1241,
                "priority": 10,
                "members": [
                    {
                        "id": 100,
                        "name": "eBay",
                        "type": "percent",
                        "bias_pct": "9"
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
            },
            {
                "id": 125,
                "name": "Base YMP Bias",
                "description": "",
                "profile_id": null,
                "priority": 1,
                "members": null,
                "buyer_groups": null
            }
        ],
        "floors": [
            {
                "id": 1234,
                "name": "Germany Floor",
                "description": "This rule will used to set the floor for a set of demand attributes across Germany inventory.",
                "hard_floor": "1.20",
                "soft_floor": null,
                "default_calculation_type": "gross",
                "apply_floor_to_direct": true,
                "profile_id": 1542,
                "priority": 6,
                "members": [
                    {
                        "id": 100,
                        "name": "eBay"
                    },
                    {
                        "id": 256,
                        "name": "MiG"
                    }
                ],
                "brands": [
                    {
                        "id": 102,
                        "name": "Netflix"
                    },
                    {
                        "id": 256,
                        "name": "Blockbuster"
                    }
                ],
                "categories": [
                    {
                        "id": 2,
                        "name": "Apparel"
                    },
                    {
                        "id": 8,
                        "name": "Dating"
                    }
                ]
            },
            {
                "id": 1574,
                "name": "Base YM Floor",
                "description": "",
                "hard_floor": 1.00,
                "soft_floor": 1.50,
                "default_calculation_type": "gross",
                "apply_floor_to_direct": true,
                "profile_id": null,
                "priority": 1,
                "members": null,
                "brands": null,
                "categories": null
            }
        ]
    }
}
```
