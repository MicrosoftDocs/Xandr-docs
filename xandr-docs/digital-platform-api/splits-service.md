---
title: Splits Service
description: Use the Splits service to create and modify programmable splits for augmented line items, allowing for targeting, budget allocation, and creative distribution.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Splits service

> [!WARNING]
> The `segment[]`condition is no longer used and has been deprecated on August 21, 2022. When setting up targeting for new line items, use [Segment Group](#segment-group) (`segment_group`). instead.

The Splits Service creates and modifies programmable splits for [augmented line items](./line-item-service---ali.md). When you create a line item, you specify the inventory you'd like to target, the budget you'd like to spend over the flight, how you want to track revenue, and how to use Xandr optimization. **Programmable splits** can further target subsets of that total inventory, allocate the specified budget to different targets, set bidding criteria, and distribute creatives. The targeting on the line item acts as a filter; impressions must match the criteria specified by the line item before they'll be passed on to splits. For more information on how splits work, see [Understanding Splits](../invest/understanding-splits.md) in the UI documentation.

The Splits Service allows you to specify:

- Targeting conditions
- Bidding rules
- Budget allocation
- Which creatives are associated with a split.

> [!NOTE]
> Using splits with custom models is not currently supported. You will receive an error if you attempt to create or modify splits on a line item that has a custom model attached.

## REST API

The Splits service works a little differently from most of Xandr's other API services. By default, the budget-splitter (Splits) service creates or modifies all the splits on the line item at the same time instead of creating or modifying a single split. Rather than creating a single split, the service creates a `budget-splitter` object (an array) that is associated with the line item. The `budget-splitter` array contains two or more splits, and must meet the following requirements:

- The sum of the budget allocation for all splits on a line item must always equal 100. This ensures that all impressions for a line item are accounted for by at least one split.
- Each split must be assigned a priority, which determines the split to which an incoming impression will be assigned if the impression meets the targeting requirements for more than one split. The same priority cannot be used for more than one split.
- One split must be defined as the default split. This is the fallback split to which impressions will be assigned if they don't meet the conditions of any of the other splits. The default split is referred to as the "Line Item Remainder" in the UI.
- The default split must be named `"Default"` or `"default"` and appear as the last split listed in the `budget-splitter` array. It cannot be assigned any conditions or assigned a capped (constrained) allocation strategy, because it is meant as a fallback in case other conditions don't apply. You can, however, allocate 0% of your budget to the default split, which means it will never serve.
- The default split may only have a bid modifier of `"1"` or `null`.
- The default split must be assigned an order, but no matter what order it is assigned, it will be prioritized last.

The `POST` method is not supported for the Split service.

To modify an individual split, you must use the `PATCH` method as described in the examples below.

> [!NOTE]
> You cannot use the `PATCH` method to modify split allocation. Because the sum of the budget allocation for all splits on a line item must equal 100, it is not valid to change the allocation on one split without changing the allocation on at least one other split.

Unlike other Xandr API services, the JSON for the `budget-splitters` array does not appear inside a wrapper named after the object. It appears simply as an unnamed array. For example, this is the JSON file to create a `budget-splitters` array with three splits:

### Example budget-splitter object

```
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 2,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 1,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "expected_value": 0.5,
        "is_default": true,
        "name": "Default",
        "order": 3
    }
```

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `PUT` | `https://api.appnexus.com/budget-splitter/LINE-ITEM-ID/splits` <br>(budget-splitter JSON) | Add splits to a line item which has none. |
| `GET` | `https://api.appnexus.com/budget-splitter/LINE-ITEM-ID/split`s | View all splits for a line item. |
| `PUT` | `https://api.appnexus.com/budget-splitter/LINE-ITEM-ID/splits` <br>(budget-splitter JSON) | Update all splits for a line item. |
| `DELETE` | `https://api.appnexus.com/budget-splitter/LINE-ITEM-ID/splits` | Delete all splits from a line item. This will delete all splits from the line item permanently. The information for past splits traffic will still appear in reporting. |
| `PATCH` | `https://api.appnexus.com/budget-splitter/LINE-ITEM-ID/splits`<br>(split-update JSON)<br><br>The split ID must appear in the split-update JSON. | Modify a single split. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the split.<br>**Example**: `"id":21197314`<br><br>**Default**: Auto-generated number.<br>**Required On**: `PUT`/`PATCH`/`DELETE`, in JSON. |
| `name` | string (255) | The name you assign the split.<br>**Example**: `"name":"Split 123"`<br><br>**Note**: The default split must be named `"Default"` or `"default"`. |
| `is_default` | boolean | Specifies whether this is the default split, which is used when an impression does not meet the targeting requirements for any other splits. Every line item must have one and only one default split. The default split must be named `"Default"` or `"default"` and cannot have any conditions. Possible values are `"true"` and `"false"`.<br>**Example**: `"is_default":true` |
| `conditions` | array | The targeting conditions for the split. A condition is specified by an array containing a field, an operator, and a value.<br>**Example**: <br>`"conditions":[{"field":"city","operator":"in","value":[196646]}]`<br><br>See [Conditions](#conditions) below for more information. |
| `active` | boolean | Specifies the status of a split. Possible values are `"true"` or `"false"`.<br>**Example**:<br>`"active":true` |
| `order` | int | The priority of this split in the `budget_splitters` array. In the UI, this field is referred to as `"Priority"`.<br>If an impression meets the targeting requirements for multiple splits, the priority determines the split to which the impression will be assigned. For example, suppose that Split A (priority 1) is targeting `"domain=cnn.com"` and Split B (priority 2) is targeting `"city=Boston"`, and an impression is available from a user in Boston visiting [cnn.com](https://edition.cnn.com/). The impression will be assigned to Split A because it has a higher priority than Split B.<br><br>You cannot set the same priority for multiple splits.<br><br> The order can start at any value, so long as the values are sequential. For example, the order for three splits can be `0`, `1`, `2` or `4`, `5`, `6`.<br>**Example**: `"order":1` |
| `allocation_percent` | int | The percentage of the line item budget assigned to this split. The allocation for each split should be between `0` and `100`. The sum of the allocation percentages for all splits in a line item must equal `100`.<br>**Example**: `"allocation_percent":30` |
| `allocation_strategy` | enum | Specifies how to handle conflicts between the split allocation goal and the line item delivery goal. Possible values are:<br> - `"unconstrained"` - Line item delivery is prioritized over allocation. When a line item with uncapped splits is underdelivering, the uncapped splits are permitted to exceed the allocation goal to reach the line item delivery goal. In the UI, this state is called "uncapped".<br> - `"constrained"` - Allocation is prioritized over delivery. Even when line items are underdelivering, capped splits are not permitted to exceed the allocation goal to help the line item reach its delivery goal. This will prevent overspend on a split, but may cause the line item to underdeliver. In the UI, this state is called "capped".<br>For more information, see [Understanding Splits](../invest/understanding-splits.md) in the UI documentation.<br>**Example**:<br>`"allocation_strategy":"unconstrained"`<br><br>**Default**: `"unconstrained"` |
| `bid_modifier` | float | The number used to modify the bid for this split. A bid modifier can only be applied to a split when the line item's booked revenue type is CPM and optimization is not enabled. The value of the bid modifier will be multiplied by the CPM booked revenue to serve as the maximum CPM that the split can bid.<br>**Example**: `"bid_modifier":1.25`<br><br>**Note**: <br> - The default split may only have a bid modifier of `"1"` or `null`. Inactive splits must be assigned a bid modifier of `"0"`.<br> - The `bid_modifier` field is not used by GDALI. |
| `expected_value` | float | The expected value of the impression for this split. An expected value must be included for each split when the line item's booked revenue type is cost plus or dCPM and optimization is not enabled. The expected value serves as the maximum CPM that the split can bid.<br>**Example**: `"expected_value":10.50`<br><br>**Note**: The `expected_value` field is not used by GDALI. |
| `creatives` | array | Optional. The IDs of the creatives to be served on this split.<br>**Example**:<br>`"creatives":[{"creative_id":123},{"creative_id":456}]` |
| `creative_macros` | array of strings | Optional. Any creative macros that are added to the served creative.<br>For more information, see [Creative Macro Check Service](./creative-macro-check-service.md).<br><br>**Note**: The `creative_macros` field is not used by GDALI. |
| `user_test_group_percent` | int | **Optional**. Targets distinct groups of users per split for A/B testing.<br><br>**Note**:<br>When the Line Item Remainder split is set to `"active"` or has a budget allocation greater than 0%, the line item remainder will always include the remaining pool of users not targeted by the other splits. Additionally, the Line Item Remainder split will always include cookieless users.<br><br>If you do not want to serve cookieless users:<br> - If you're using allocations, on the default split, set `allocation_percent` to `"0"`.<br> - If you're not using allocations, on the default split, set `active` to `"false"`. |

### Conditions

A condition is specified by an array containing a field, an operator, and a value. For example, to create a condition that targets impressions from the United States, the condition is:

```
"conditions": [
  {
    "field": "country",
    "operator": "=",
    "value": [
      233
    ]
  }
]
```

### Custom categories

Evaluate impressions based on specific custom categories present.

| Field  | Operator | Value |
|:---|:---|:---|
| `content_category` | `=`, `in`, `not_in` | Custom category ID. Use the [Content Category Service](content-category-service.md) to retrieve custom category IDs. <br><br>**Warning**: Custom categories should only be targeted to managed inventory. |

### Key-value

Evaluate impressions based on specific key-values present.

| Field  | Operator | Value |
|:---|:---|:---|
| `key_group` | `and`, `or` | A nested conditions array that specifies key groups. Each key group array includes key ID(s), action(s) (`"include"` or `"exclude"`), and value(s):<br><br>**Warning**: Key-values should only be targeted to managed inventory. <br><br>- `key_id` - the ID of the key. Use the [Targeting Key Service](./targeting-key-service.md) to retrieve key IDs. <br>- `action` - can be `"include"` or `"exclude"`. <br> - `value_equals` is an array of value IDs that must be matched in the auction for the split to be eligible to serve. Use the [Targeting Key Service](./targeting-key-service.md) to retrieve value IDs. When one value is passed, that key-value combination must be present on the request for the split to be eligible to serve. When multiple values are defined in the array, one of the key-value combinations must be present. <br>- `value_less` is the high end of the range of permitted values, exclusive. <br> - `value_greater` is the low end of the range of permitted values, exclusive.Key-values may be passed on the impression request. See Xandr’s [Seller Tag (AST)](../seller-tag/seller-tag.md) for more information. |

The following Key-Value example (see JSON below) evaluates to

`[ [include Key ID 123: value ID: [1 OR 2 OR 9] ] AND [exclude Key ID 234: value ID: [20] ] ] OR [include Key ID 789: value ID: [15] ]`

```
{
   "conditions": [{
      "field": "key_group",
      "operator": "or",
      "value": [
         [{
               "key_id": 123,
               "action": "include",
               "value_equals": [1, 2, 9]
            },
            {
               "key_id": 234,
               "action": "exclude",
               "value_equals": [20]
            }
         ],
         [{
            "key_id": 789,
            "action": "include",
            "value_equals": [15]
         }]
      ]
   }]
}
```

### Country

Evaluate impressions based on the user's country.

| Field  | Operator | Value |
|:---|:---|:---|
| `country` |  `=`, `in`, `not_in` | Country ID or code, such as `233` or `"US"`.Use the [Country Service](./country-service.md) to retrieve these IDs or codes. |

### Region

Evaluate impressions based on the user's geographic region.

| Field  | Operator | Value |
|:---|:---|:---|
| `region` |  `=`, `in`, `not_in` | Region ID or country/region code combination, such as `"US:NY"`.<br>Use the [Region Service](./region-service.md) to retrieve these IDs and codes. |

### City

Evaluate impressions based on the user's city.

| Field  | Operator | Value |
|:---|:---|:---|
| `city` |  `=`, `in`, `not_in` |  City ID or country/region/city code combination, such as `"US:NY:New York"`.<br>Use the [City Service](./city-service.md) to retrieve these IDs and codes. |

### DMA

Evaluate impressions based on the user's DMA (designated market area).

| Field  | Operator | Value |
|:---|:---|:---|
| `dma` |  `=`, `in`, `not_in` |  DMA ID, such as `602` (for Chicago metro area).<br>Use the [City Service](./city-service.md) to retrieve DMA IDs. |

### Postal code

Evaluate impressions based on the user's postal code. Postal code is available only for some mobile impressions and impressions from external supply partners.

| Field  | Operator | Value |
|:---|:---|:---|
| `postal_code` |  `=`, `in`, `not_in` |  Postal code ID (an integer) or country/postal code combination (a string such as `"CA:J0K 1B0"` or `"US:10010"`). Includes US zip codes.<br><br>Use the Postal Code Service (documented in the [Profile Service](./profile-service.md)) to retrieve postal code IDs. |

### Postal code list

Evaluate impressions based on the user's post codes in the postal code list.

| Field  | Operator | Value |
|:---|:---|:---|
| `postal_code_list` |  `in`, `not_in` |  Postal code list ID (an integer).<br><br>Use the Postal Code List Service (documented in [Postal Code List Service](./postal-code-list-service.md)) to retrieve postal code list IDs. |

### Size

Evaluate impressions based on placement size. Please note that in case `promo_sizes` are passed in the ad call, the evaluation will be performed using the primary size only.

| Field  | Operator | Value |
|:---|:---|:---|
| `size` |  `=`, `in`, `not_in` |  String representing placement dimensions, formatted as `"WIDTHxHEIGHT"`. |

### Inventory URL ID

Evaluate impressions based on specific inventory url IDs.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `inventory_url_id` |  `=`, `in`, `not_in` |  Inventory URL ID.<br>Use [Validate Inventory Item Service](./validate-inventory-item-service.md) to retrieve these IDs. |

### Domain

Evaluate impressions based on domain.

> [!NOTE]
> - Not supported by GDALI.
> - This feature is not supported in the Microsoft Invest. If you will also be using the UI to manage your splits, use the Inventory URL ID feature (within this service) instead.

| Field  | Operator | Value |
|:---|:---|:---|
| `domain` | `=`, `in`, `not_in` | String representing a top-level domain name, such as `"food.com"` or `"books"`. |

### Mobile app

Evaluate impressions based on specific mobile apps.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `mobile_app_bundle` | `=`, `in`, `not_in` | Mobile app ID or names.<br><br>Use [Mobile App Service](./mobile-app-service.md) to retrieve these IDs or names. |

### Placement

Evaluate impressions based on specific placements.

| Field  | Operator | Value |
|:---|:---|:---|
| `placement` | `=`, `in`, `not_in` | Placement ID.<br><br>Placement ID is listed as `tag_id` in log-level data. |

### Publisher

Evaluate impressions based on specific publishers.

| Field  | Operator | Value |
|:---|:---|:---|
| `publisher` | `=`, `in`, `not_in` | Publisher ID.<br><br>**Tip**:<br>Publisher ID is listed as `publisher_id` in log-level data. |

### Seller member

Evaluate impressions based on specific seller members.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `seller_member_id` | `=`, `in`, `not_in` | Member ID of the seller. |

### Deal ID

Target deal inventory.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `deal_id` | `=`, `in`, `not_in` | Deal ID. |

### Deal list ID

Target deal list inventory.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `deal_list` | `in`, `not_in` | Deal List ID. |

### Operating system family

Evaluate impressions based on the user's operating system.

| Field  | Operator | Value |
|:---|:---|:---|
| `os_family` | `=`, `in`, `not_in` | Operating System Family ID or name, such as `2` or `"Android"`.<br><br>Use the [Operating System Family Service](./operating-system-family-service.md) to retrieve these IDs and names. |

### Operating system version

Evaluate impressions based on the specific **version** of the user's operating system.

| Field  | Operator | Value |
|:---|:---|:---|
| `os_extended` | `=`, `in`, `not_in` | Operating System Extended ID, such as `81` for `"10.8 Mountain Lion"`.<br>Use the [Operating System Extended Service](./operating-system-extended-service.md) to retrieve these IDs.<br><br>**Note**:<br>Operating system ID is listed as `operating_system` in log-level data. |

### Browser

Evaluate impressions based on the user's browser.

| Field  | Operator | Value |
|:---|:---|:---|
| `browser` | `=`, `in`, `not_in` | Browser ID or name, such as `8` or `"Chrome (all versions)"`.<br><br>Use the [Browser Service](./browser-service.md) to retrieve these IDs and names. |

### Browser language

Evaluate impressions based on the browser language.

| Field  | Operator | Value |
|:---|:---|:---|
| `language` | `=`, `in`, `not_in` | Language ID.<br><br>Use the [Language Service](./language-service.md) to retrieve these IDs. |

### Device type

Evaluate impressions based on specific types of physical devices.

| Field  | Operator | Value |
|:---|:---|:---|
| `device_type` | `=`, `in`, `not_in` | Device type name. Possible values:<br> - `"pc & other devices"` - Use this value to target desktops and laptops.<br> - `"phone"` - Use this value to target mobile phones.<br> - `"tablet"` - Use this value to target mobile tablets. |

### Device model

Evaluate impressions based on specific models of physical devices.

| Field  | Operator | Value |
|:---|:---|:---|
| `device_model` | `=`, `in`, `not_in` | Device model ID.<br>Use the [Device Model Service](./device-model-service.md) to retrieve these IDs.<br><br>Device model ID is listed as `device_id` in log-level data. |

### Carrier

Evaluate impressions based on specific mobile carriers.

| Field  | Operator | Value |
|:---|:---|:---|
| `carrier` | `=`, `in`, `not_in` | Mobile carrier ID or name, such as `14` or "`Verizon"`.<br><br>Use the [Carrier Service](./carrier-service.md) to retrieve these IDs and names. |

### Predicted IAB viewability rate

Previously known as "Estimated IAB Viewability Rate". Evaluate web display impressions by how likely they are to be measured as viewable by the IAB standard, as determined by the Optimization Guide (available in the UI documentation).

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `predicted_iab_view_rate` | `<`, `<=`, `=`, `>`, `>=` | Decimal number between `0` and `1`, representing a percentage. |

### Predicted IAB video viewability rate

Evaluate web video impressions by how likely they are to be measured as viewable by the IAB standard, as determined by the [Optimization Guide](../monetize/optimization-guide.md) (available in the UI documentation).

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `predicted_iab_video_view_rate` | `<`, `<=`, `=`, `>`, `>=` | Decimal number between `0` and `1`, representing a percentage. |

### Predicted video completion rate

Evaluate web video impressions by how likely they are to be completed, as determined by the [Optimization Guide](../monetize/optimization-guide.md) (available in the UI documentation).

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `estimated_video_completion_rate` | `<`, `<=`, `=`, `>`, `>=` | Decimal number between `0` and `1`, representing a percentage. `0` represents non-video inventory. |

### Creative

The creatives to serve on this split.

| Field  | Operator | Value |
|:---|:---|:---|
| `creative` | `in` | List of creative IDs.<br><br>Use the [Creative Service](./creative-service.md) to retrieve these IDs. |

### Segment group

| Field  | Operator | Value |
|:---|:---|:---|
| `segment_group`<br><br>Use [Segment Service](./segment-service.md) to retrieve segment IDs. | `and`, `or` | A nested conditions array that specifies segment groups. Each `segment_group` array includes `segment_ID`, `age`, `value`, and `action` (`"include"` or `"exclude"`).<br> - `action` may be `"include"` or `"exclude"`.<br> - `start_minutes` is the lower bound of minutes since the user has been added to this segment, inclusive. `"start_minutes": 5` includes users who have been added to the segment from the five-minute mark, including 5:00.<br> - `expire_minutes` is the upper bound of minutes since the user has been added to this segment, inclusive. `"expire_minutes": 10` includes users who have been added to the segment until the ten-minute mark, including 10:00.<br> - `value_less` is the low end of the range of permitted values, exclusive. `"value_less" : 5` includes only values greater than, but not including, 5.<br> - `value_greater` is the high end of the range of permitted values, exclusive. `"value_greater" : 10` includes only values up to, but not including, `10`.<br> - `value_equals` is the exact match to the permitted value. `“value_equals” : 5` includes only values equal to `5`.<br> - Unlike the [Profile Service](./profile-service.md), the Splits service allows you to target segment values of zero (0). See [example](#example-for-the-value_equals-field) for `value_equals` below. <br>Segment values may be passed in a number of ways, for example, through the Batch Segment Service or a first-party or third-party segment query string. |

#### Example for the `value_equals` field

```
"conditions": [
{
"field": "segment_group",
"operator": "and",
"value": [
[
{
"segment_ID": SEGMENT_ID,
"action": SEGMENT_ACTION,
"start_minutes": YOUNGEST_SEGMENT_AGE,
"expire_minutes": OLDEST_SEGMENT_AGE,
"value_less": LOWER_BOUND_SEGMENT_VALUE,
"value_greater": UPPER_BOUND_SEGMENT_VALUE,
"value_equals": EXACT_SEGMENT_VALUE
}

]
]
}
]
```

### Segment

> [!WARNING]
> The `segment[]`condition is no longer used and has been deprecated on August 21, 2022. When setting up targeting for new line items, use [Segment Group](#segment-group) (`segment_group`) instead.

| Field  | Operator | Value |
|:---|:---|:---|
| `segment[SEGMENTID,...]`<br>where `SEGMENTID` is an optional list of segment IDs.<br>Use [Segment Service](./segment-service.md) to retrieve segment IDs. | `<`, `<=`, `=`, `>`, `>=`, `present`, `absent` | A nested conditions array that specifies segment age, value, or presence.<br> - Segment presence is `"present"` or `"absent"`.<br> - Segment age is measured in minutes and must be a positive integer.<br> - Segment value is a non-zero, positive integer representing a user-defined value. See [example](#example-for-the-value-field) for `value` below.<br>Segment values may be passed in a number of ways, for example, through the [Batch Segment Service](./batch-segment-service.md) or a first-party or third-party segment query string. |

#### Example for the `value` field

Evaluate impressions based on the presence, absence, value, or segment age of the user in a first-party or third-party segment.

```
"conditions": [
{
"field": "segment[]",
"operator": "any",
"value": [
{
"conditions": [
{
"field": "age",
"operator": "<=",
"value": 1440
}
],
"id": 275913
}
]
}
],
```

### Daily frequency

The number of ads seen by a user for an advertiser, line item, or split on the current day.

| Field  | Operator | Value |
|:---|:---|:---|
| `OBJECT[ID].day_frequency`<br>where the object is `advertiser`, `line_item`, or `campaign` (representing split), and ID is the object ID. Use the [Advertiser Service](./advertiser-service.md), [Line Item Service](./line-item-service.md), or Splits Service to retrieve IDs. | `>`, `=>`, `<`, `=<`, `=`<br><br>**Important**: Although the operator `=` is supported for frequency and recency, we **strongly recommend** that you do not use it, as it tends to cause underdelivery. This is because when you target an impression with `frequency=5`, you exclude impressions with frequencies equal to `0`, `1`, `2`, `3`, or `4`. | Positive integer. `0` indicates no frequency information is available (the user has not seen this object on the current day). |

### Lifetime frequency

The number of ads seen by a user over the lifetime of an advertiser, line item, or split.

| Field  | Operator | Value |
|:---|:---|:---|
| `OBJECT[ID].lifetime_frequency`<br>where the object is `advertiser`, `line_item`, or `campaign` (representing split), and ID is the object ID. Use the [Advertiser Service](./advertiser-service.md), [Line Item Service](./line-item-service.md), or Splits Service to retrieve IDs.<br><br>**CAUTION**: Although the operator `=` is supported for frequency and recency, we strongly recommend that you do not use it, as it tends to cause underdelivery. This is because when you target an impression with `frequency=5`, you exclude impressions with frequencies equal to `0`, `1`, `2`, `3`, or `4`. | `>`, `=>`, `<`, `=<`, `=` | Positive integer. `0` indicates no frequency information is available (the user has never seen this object). |

### Recency

The number of minutes since a user has seen an ad. This can be determined for a user for all ads under an advertiser, line item, or split.

| Field  | Operator | Value |
|:---|:---|:---|
| `OBJECT[ID].recency`<br>where the object is `advertiser`, `line_item`, or `campaign` (representing split), and ID is the object ID. Use the [Advertiser Service](./advertiser-service.md), [Line Item Service](./line-item-service.md), or Splits Service to retrieve IDs. | `>`, `=>`, `<`, `=<`, `=`<br><br>**Important**: Although the operator `=` is supported for frequency and recency, we strongly recommend that you do not use it, as it tends to cause underdelivery. This is because when you target an impression with `frequency=5`, you exclude impressions with frequencies equal to `0`, `1`, `2`, `3`, or `4`. | A positive integer indicating the number of minutes since a user has seen an impression, rounded down. 59 seconds will evaluate to `0`, 61 seconds will evaluate to `1`. `0` means the impression was seen very recently. `Null` means no recency data is available (the user has not seen this impression before). |

### Inventory type

The type of inventory ("app" or "web") targeted by the split. "App" targets mobile app inventory and "web" targets web inventory (including pages shown in mobile web browsers).

| Field  | Operator | Value |
|:---|:---|:---|
| `inventory_type` | `=`, `in`, `not_in` | `"web"`, `"app"`<br>See [Example](#example-for-the-inventory_type-field). |

#### Example for the `inventory_type` field

```
"conditions": [
{
"field": "inventory_type",
"operator": "in",
"value": [
"app",
"web"
]
}
]
```

### Inventory URL list

Target an allowlist or blocklist established at the Network level. You can only target a single list.

> [!NOTE]
> Not supported by GDALI.

| Field  | Operator | Value |
|:---|:---|:---|
| `inventory_url_list` | `all`, `not in` | Inventory list ID.<br><br>`"conditions":[{"field":"inventory_url_list","operator":"not in","value":[12345]}]`<br><br>To create an inventory list, or retrieve the list IDs for use in split targeting, use the [Inventory List Service](./inventory-list-service.md). |

## Examples

### Create splits for a line item with cost-plus booked revenue and optimization disabled

This example creates three splits for Line Item `6377624`:

- Split 1 - User must be using the Chrome browser. Impressions are assigned an expected value of `2`. Forty percent of the line item's traffic is allocated to this split, which is first in priority. Allocation is unconstrained.
- Split 2 - Impressions must belong to Segment `275913` and must have been added within the last 1440 minutes. They are assigned an expected value of ``1. Thirty percent of the line item's traffic is allocated to this split, which is second in priority. Allocation is unconstrained.
- Split 3 (unnamed) - The default split. Impressions are assigned an expected value of `0.5`. Thirty percent of the line item's traffic is allocated to this split, which is third in priority. Allocation is unconstrained.

Since optimization is disabled, we are setting expected values for the splits.

```
$ cat ali_cost_plus_ev.json
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 2,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 1,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "expected_value": 0.5,
        "is_default": true,
        "name": "Default",
        "order": 3
    }

$ curl -b cookies -X PUT -s -d '@ali_cost_plus_ev.json' "https://api.appnexus.com/budget-splitter/6377624/splits"   
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 2,
        "id": 24025228,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": 1,
        "id": 24025229,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "expected_value": 0.5,
        "id": 24025230,
        "is_default": true,
        "name": "Default",
        "order": 3
    }
]
```

### Create splits for a line item with cost-plus booked revenue and optimization enabled

This example creates three splits for Line Item `6377631`:

- Split 1 - User must be using the Chrome browser. Impressions are assigned an expected value of `2`. Forty percent of the line item's traffic is allocated to this split, which is first in priority. Allocation is unconstrained.
- Split 2 - Impressions must belong to Segment `275913` and must have been added within the last 1440 minutes. They are assigned an expected value of `1`. Thirty percent of the line item's traffic is allocated to this split, which is second in priority. Allocation is unconstrained.
- Split 3 (unnamed) - The default split. Impressions are assigned an expected value of `0.5`. Thirty percent of the line item's traffic is allocated to this split, which is third in priority. Allocation is unconstrained.

```
$ cat ali_cost_plus_opt.json
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "expected_value": null,
        "is_default": true,
        "name": "Default",
        "order": 3
    }


$ curl -b cookies -X PUT -s -d '@ali_cost_plus_opt.json' "https://api.appnexus.com/budget-splitter/6377631/splits"
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "id": 24025315,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "id": 24025316,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": null,
        "expected_value": null,
        "id": 24025317,
        "is_default": true,
        "name": "Default",
        "order": 3
```

### Create splits for a line item with CPM booked revenue and optimization disabled

This example creates three splits for Line Item `6377633`:

- Split 1 - User must be using the Chrome browser. Bids are multiplied by `0.5`. Forty percent of the line item's traffic is allocated to this split, which is first in priority. Allocation is unconstrained.
- Split 2 - Impressions must belong to Segment `275913` and must have been added within the last 1440 minutes. Bids are multiplied by `0.4`. Thirty percent of the line item's traffic is allocated to this split, which is second in priority. Allocation is unconstrained.
- Split 3 (unnamed) - The default split. Bids are multiplied by `1` (they remain the same). Thirty percent of the line item's traffic is allocated to this split, which is third in priority. Allocation is unconstrained.

Since optimization is disabled, we are setting bid modifiers for each split.

```
$ cat ali_cpm_bid_modifier.json
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 0.5,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 0.4,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 1,
        "expected_value": null,
        "is_default": true,
        "name": "Default",
        "order": 3
    }

$ curl -b cookies -X PUT -s -d '@ali_cpm_bid_modifier.json' "https://api.appnexus.com/budget-splitter/6377633/splits"   
[
    {
        "active": true,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 0.5,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "id": 24025342,
        "is_default": false,
        "name": "Split 1",
        "order": 1
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 0.4,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creative_macros": [],
        "creatives": [],
        "expected_value": null,
        "id": 24025343,
        "is_default": false,
        "name": "Split 2",
        "order": 2
    },
    {
        "active": true,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "bid_modifier": 1,
        "expected_value": null,
        "id": 24025344,
        "is_default": true,
        "name": "Default",
        "order": 3
    }
]
```

### Update one split on a line item

In this example, Line Item `5200075` already has 3 splits, all with unconstrained allocation strategies. We update `Split 1` to use a constrained allocation strategy.

```
# View the current splits
$ curl -b cookies 'https://api.appnexus.com/budget-splitter/5200075/splits'
    {
        "id": 24025093,
        "name": "Split 1",
        "is_default": false,
        "active": true,
        "bid_modifier": null,
        "expected_value": 2,
        "allocation_percent": 40,
        "allocation_strategy": "unconstrained",
        "order": 1,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creatives": [

        ],
        "creative_macros": [

        ]
    },
    {
        "id": 24025094,
        "name": "Split 2",
        "is_default": false,
        "active": true,
        "bid_modifier": null,
        "expected_value": 1,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "order": 2,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creatives": [

        ],
        "creative_macros": [

        ]
    },
    {
        "id": 24025096,
        "name": "Default",
        "is_default": true,
        "active": true,
        "bid_modifier": null,
        "expected_value": 0.5,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "order": 3
    }
]

# View the split1-update JSON 
$ cat split1-update.json
[
    {
        "id": 24025093,
        "name": "Split 1",
        "is_default": false,
        "active": true,
        "bid_modifier": null,
        "expected_value": 2,
        "allocation_percent": 40,
        "allocation_strategy": "constrained",
        "order": 1,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creatives": [
        ],
        "creative_macros": [
        ]
    }
]

# Update Split 1

$ curl -b cookies -X PATCH -d @split1_update.json 'https://api.appnexus.com/budget-splitter/5200075/splits'
[
    {
        "id": 24025093,
        "name": "Split 1",
        "is_default": false,
        "active": true,
        "bid_modifier": null,
        "expected_value": 2,
        "allocation_percent": 40,
        "allocation_strategy": "constrained",
        "order": 1,
        "conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8
                ]
            }
        ],
        "creatives": [

        ],
        "creative_macros": [

        ]
    },
    {
        "id": 24025094,
        "name": "Split 2",
        "is_default": false,
        "active": true,
        "bid_modifier": null,
        "expected_value": 1,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "order": 2,
        "conditions": [
            {
                "field": "segment_group",
                "operator": "and",
                "value": [
                            [
                                {
                                "segment_id": 275913,
                                "start_minutes": 0,
                                "expire_minutes": 1440
                                }
                            ]
                         ]    
            }
        ],
        "creatives": [

        ],
        "creative_macros": [

        ]
    },
    {
        "id": 24025096,
        "name": "Default",
        "is_default": true,
        "active": true,
        "bid_modifier": null,
        "expected_value": 0.5,
        "allocation_percent": 30,
        "allocation_strategy": "unconstrained",
        "order": 3
    }
]
```

## Related topics

- [Line Item Service - ALI](./line-item-service---ali.md)
- [Splits Service Troubleshooting](./splits-service-troubleshooting.md)
