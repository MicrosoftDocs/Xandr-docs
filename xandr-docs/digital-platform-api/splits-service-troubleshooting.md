---
title: Splits Service Troubleshooting
description: This article explains error messages and common issues that may occur when using the Splits service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Splits service troubleshooting

This page explains error messages and common issues that may occur when using the [Splits Service](./splits-service.md).

## Error messages

This table lists common error messages and their meanings.

| Error Message | Fix |
|:---|:---|
| `Splits are missing allocation_percent:[Split-Name]` | One of the individual splits is missing an allocation percentage. Make sure all splits have allocation percentages and the sum of the allocation percentages is 100. |
| `Splits should sum to 100 but summed to:XX` | The sum of the allocations for all splits must equal 100. Modify the `allocation_percent` for the splits. |
| `"splits" at position 1 fails because [child "allocation_strategy" fails because ["allocation_strategy" must be one of [unconstrained, constrained]]]"` | At least one split has no allocation strategy set. Make sure each split has an `allocation_strategy` equal to `"constrained"` or `"unconstrained"`. |
| `"child "Default Split" fails because [child "allocation_strategy" fails because ["allocation_strategy" must be one of[unconstrained]]]` | The allocation strategy for the default split must be `"unconstrained"`. |
| `There should be exactly 1 active split with is_default =true` | Make sure the `budget_splitter` array contains one active default split (whose name is `“Default”` or `“default”`) and which has `is_default` set to `“True”`. This marks the line item remainder split. |
| `child "Default Split" fails because child "bid_modifier" fails because "bid_modifier" must be one of [1, null]` | The bid modifier for the default split must be set to either `1` or `null`. When revenue type is CPM and optimization is disabled, the bid modifier should be `1`. For all other booked revenue and optimization combinations, the bid modifier should be set to `null`. |
| `child "Default Split" fails because child "conditions" fails because "conditions" is not allowed` | The default split may not have any conditions. Remove any conditions specified for the default split in your JSON. The default split must be the last split in the budget-splitter array. |
| `The default split must be the last split in the splits array` | The default split must be the last split in the budget-splitter array. |
| `child "Default Split" fails [because child "name" fails [because "name" must be one of [Default, default]]]` | The default split must be named `"Default"` or `"default"`. |
| `Splits have duplicate orders: "Split 1" has order 1 and "Split 2" has order 1 and "Default" has order 1"` | Each split must have a unique priority (order value). |
| `"order" is required` | At least one split does not have a priority assigned. Assign a value to order for all splits. |
| `Duplicate campaign IDs found` | Currently, your budget-splitter array assigns the same ID to more than one split. Split IDs must be unique. |
| `An inactive split cannot have an allocation_percent` | An inactive split cannot have an allocation percentage greater than `0` even if the allocations for all the active splits equals `100`. Explicitly set any inactive splits to `0`. |
| `"operator" must be one of[any, not_any, every, not_every],"value" must be an array` | If you use the operators `"in"` or `"not_in"` in a condition, the value must be an array. |
| `"Payload" must contain at least 2 items` | You are trying to set up a budget-splitter object containing only one split. The budget-splitter must contain two or more splits, including the default split. |
| `"You cannot supply both expected_value and bid_modifier for splits"` | You can only supply either an expected value or a bid modifier on a split. The required setup depends on the combination of the ALI booked revenue and optimization, as detailed below. |
| `"operator" must be one of [in, not_in, all, not_all]"`  | You are using an invalid operator for the `device_type` condition. |
| `An internal server error occurred` | This error can mean multiple things. Some possibilities to check are:<br> - You are trying to create splits for a line item which already has a custom model attached. Line items cannot have both splits and custom models. Remove the custom model before creating the splits.<br> - You are trying to set the default split as active with an allocation percentage of `100` and set all other splits as `inactive`. The default split cannot be the only active split. |
| `Invalid request payload JSON format` | This error can mean multiple things. Some possibilities to check out are:<br> - You have more than one split defined as the default split. Make sure only one split has the name `"Default"` or `"default"` and has `is_default` set to `"true"`.<br> - You are using the operator `“in”` or `“not_in”` and have not included the value/s in an array. Make sure that arrays are user for certain conditions and value/s are listed inside square brackets ([]).<br> - You have failed to enclose a string value inside quotation marks (""). |

## Booked revenue, optimization, and bid modifiers/expected value

This table describes all the functional combinations of booked revenue + optimization + inclusion of bid modifiers/expected values on splits.

| ALI Booked Revenue | Optimization | Set Bid Modifiers/EVs on Splits? |
|:---|:---|:---|
| Cost Plus | Yes | Neither |
| Cost Plus | No | EVs |
| CPM | Yes | Neither |
| CPM | No | Bid Modifiers |
| CPC | Required | Neither |
| dCPM | Yes | Neither |
| dCPM | No | EVs |
| vCPM | Required | Neither |

## Frequently asked questions

### How do I include multiple conditions in a split?

The correct way to do this is to include multiple conditions inside a single conditions array:

```
"conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8,10,11
                ]
            }
            {
                "field": "country",
                "operator": "in",
                "value": [
                    233
                ]
            }
        ],
```

It is **incorrect** to include multiple conditions inside a single `budget-splitter` array. In the following example, the API call will run, but only the first `conditions` array will be used in the split's targeting. The second `conditions` array will be ignored.

```
"conditions": [
            {
                "field": "browser",
                "operator": "in",
                "value": [
                    8,10,11
                ]
            }
        ],
        "conditions": [
            {
                "field": "country",
                "operator": "in",
                "value": [
                    233
                ]
            }
        ],
```

### Can I include decimal points in allocation percentages?

Yes, as long as the sum of all allocation percentages is 100.

### If I do not include allocation perceptions in the API call, what happens?

The line item will spend as normal and the splits targeting will be used for reporting only.

## Related topic

[Splits Service](./splits-service.md)
