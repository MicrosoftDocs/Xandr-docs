---
title: Data Science Toolkit - Bonsai Smart Leaves
description: Explore the concept of Bonsai Smart Leaves, with syntax explanations, input fields, and a comprehensive set of examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---

# Data Science Toolkit - Bonsai smart leaves

> [!NOTE]
> This page assumes you are already familiar with the [Bonsai Language](the-bonsai-language.md) and [Bonsai Features](bonsai-language-features.md).

You use the [Bonsai Language](the-bonsai-language.md) to write decision tree logic for custom predictive models. Each branch leads to a node, or "leaf", that evaluates to a simple numeric value representing the bid. Instead of evaluating a single static value, smart leaves evaluate a bid value that's dynamically modified based on a specified ad performance or delivery metric. Smart leaves also allow you to name individual leaves with an arbitrary string value. This is available in the [standard feed](../log-level-data/standard-feed.md) to aid debugging and performance analysis.  

> [!NOTE]
> Smart leaves are defined using a form similar to YAML, a human-readable data serialization format.

## compute() syntax

You can use smart leaves to specify a static value or a bid calculated from an advertising metric or to specify that no bid be made at all. If the value is calculated, it is determined by the `compute` expression, which uses the following format:

```
value: compute(input_field, multiplier, offset, min_value, max_value)
```

This is evaluated as the following equation:

```
max(min_value, min(max_value, input_field * multiplier + offset))
```

That is, the calculated value is the input field times the multiplier, plus an offset. If the result is less than the minimum value, the minimum value is returned instead. If the result is greater than the maximum value, the maximum value is returned. To omit a calculation (multiplier, offset, minimum value, or maximum value), use an underscore (\_) for the omitted value. If you omit to specify the multiplier value, the default value is 1.

> [!NOTE]
> The bids calculated by the model are always expressed in the currency set on the advertiser, even if you have specified a different currency for the campaign.

## Smart leaf fields

| Field | Field Type | Description | Default |
|:---|:---|:---|:---|
| `value` | text | The bid value. If the tree model is bid price, the bid is expressed in the currency set for this advertiser. If the tree model is bid modifier, the bid is a float or an integer. Possible values are:<br> - `compute(input_field, multiplier, offset, min_value, max_value)`<br>- `no_bid`<br>- a static value (number)<br><br>Specifying `compute` calculates a value based on one of the [Input Fields for compute()](#input-fields-for-compute) below. To omit a calculation (multiplier, offset, minimum value, or maximum value), use an underscore (_) for the omitted value. <br><br>**Warning:** Do not use `compute()` expressions that evaluate to negative numbers or to zero (0). These values are not supported and may provide unexpected results. It is best to specify `no_bid` explicitly. |  |
| `leaf_name` | string(7) | An optional string value that will be passed through to logs and reporting to aid with debugging and performance analysis. `leaf_name` may be up to seven ASCII (7-bit) characters and is not required to be unique.<br><br>**Note:** Because `leaf_name` is a string, the value must be enclosed by double quotation marks ("). |  |

## Input fields for compute()

The values for the input fields are determined by Xandr optimization. For more information, see the [Optimization Guide for the Augmented Line Item](../monetize/optimization-guide-ali.md) in the documentation (login required).

| Field | Type | Description |
|:---|:---|:---|
| `estimated_iab_viewthrough_rate` | float, integer | How likely this web display impression is to be measured as viewable by the IAB standard, from `0` to `1`.   |
| `predicted_iab_video_view_rate` | float, integer | How likely this video impression is to be measured as viewable by the IAB standard, from `0` to `1`. |
| `predicted_video_completion_rate` | float, integer | How likely the user is to watch this video impression fully, from `0` to `1`. Non-video inventory is `0`.    |
| `estimated_average_price` | float, integer | The median price for this impression. |
| `estimated_clearing_price` | float, integer | The 80th percentile price for this impression.   |
| `uniform` | float, integer | A uniform random number between `0` and `1` (`0` included, `1` excluded). |

## Use segments as input for compute()

You can perform calculations using the value or age of the user in a first-party or third-party segment to determine a bid value. If the user is not present in the segment, no bid is made. Use the [Segment Service](../digital-platform-api/segment-service.md) to retrieve segment IDs.

| Field | Type | Description |
|:---|:---|:---|
| `segment[ID].value`<br> | float, integer | The value of the user in a first-party or third-party segment. If the user is not present in the segment, no bid will be made.<br>`ID` is the segment ID. |
| `segment[ID].age` | float, integer | The age of a user in a first-party or third-party segment. If the user is not present in the segment, no bid will be made.<br>`ID` is the segment ID. |

## Use frequency or recency as inputs for compute()

You can perform calculations using frequency or recency to determine a bid value.

| Field | Type | Description |
|:---|:---|:---|
| `OBJECT[ID].day_frequency`<br> | float, integer | The number of ads seen by a user on the current day. This can be determined for an advertiser, line item, or campaign. If no frequency data is found, the frequency is marked as zero (0).<br><br>`OBJECT` is `advertiser`, `line_item`, or `campaign`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs. |
| `OBJECT[ID].lifetime_frequency` | float, integer | The number of ads seen by a user over the lifetime of an advertiser, line item, campaign, or creative. If no frequency data is found, the frequency is marked as zero (0).<br><br>`OBJECT` is `advertiser`, `line_item`, or `campaign`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs. |
| `OBJECT[ID].recency` | float, integer | The number of minutes since the user has seen an ad. This can be determined for all ads under an advertiser, line item, or campaign, or for an individual creative. If no recency data is found, no bid will be made.<br><br>`OBJECT` is `advertiser`, `line_item`, or `campaign`, or `creative`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs. |

## Examples

### Bid price with estimated average price

One leaf has a minimum allowable bid price but no limit on the maximum.

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
    # This tree determines a bid price as follows: 
    # 1. If the user is in California, bid the estimated average price * 1.05, plus $0.03.
    # 2. Otherwise, bid the estimated average price * .75, but don't bid less than $1.00. There is no maximum bound for bids.
     
    if region = "US:CA":
            leaf_name: "eap001"
            value: compute(estimated_average_price, 1.05, 0.03, _, _)       
    else:
            leaf_name: "eap002"
           value: compute(estimated_average_price, 0.75, 0.00, 1.00, _)
```

### Bid price tree with estimated clearing price, no bid, and static value smart leaves

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
# This tree determines a bid price as follows: 
# 1. If the user is in California, bid the estimated clearing price * 1.05, plus $0.03.
# 2. If the user is in New York, bid the estimated clearing price * .75, but don't bid less than $0.10 or more than $1.00. 
# 3. If the user is in Delaware, do not bid.
# 4. Otherwise, bid $0.50.
if region = "US:CA":
        leaf_name: "ecp_ca"
        value: compute(estimated_clearing_price, 1.05, 0.03, _, _)      
elif region = "US:NY":
        leaf_name: "ecp_ny"
        value: compute(estimated_clearing_price, 0.75, _, 0.10, 1.00)
elif region = "US:DE":
        leaf_name: "no_de"
        value: no_bid
else:
        leaf_name: "default"
        value: 0.50
```

### Bid price tree with estimated IAB viewthrough rate smart leaves

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
# This tree determines a bid modifier as follows: 
# 1. If the user is in California, bid the value determined by Xandr optimization multipled by the estimated IAB viewthrough rate and 0.50, plus $0.03.
# 2. If the user is in New York, bid the value determined by Xandr optimization multiplied by the estimated IAB viewthrough rate and 0.75. 
# 3. If the user is in Delaware, bid the estimated clearing price, but don't bid less than $0.10 or more than $1.00.
# 4. Otherwise, bid $0.50.
if every region = "US:CA":
        leaf_name: "t00001"
        value: compute(estimated_iab_viewthrough_rate, 0.50, 0.03, _, _)        
elif region = "US:NY":
        leaf_name: "t00002"
        value: compute(estimated_iab_viewthrough_rate, 0.70, 0.00, _, _)
elif region = "US:DE":
        leaf_name: "t00003"
        value: compute(estimated_clearing_price, 1.00, _, 0.10, 1.00)
else:
        leaf_name: "default"
        value: 0.50
```

### Bid based on segment value

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
#1. If the user is in California, bid the value of segment 111 times 2.0, plus 1.0.
#2. Otherwise, do not bid.
if region = "US:CA":
        leaf_name: "a00001"
        value: compute(segment[111].value, 2.0, 1.0, _, _)
else:
        value: no_bid
```

### Bid based on segment age

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
#1. If the user is in California, bid the segment age times -.2, plus 8.0, as long as the bid is under 8.0.
#2. Otherwise, do not bid.
 
if region = "US:CA":
        leaf_name: "b00001"
        value: compute(segment[111].age, -0.2, 8.0, 0.0, 8.0)
else:
        value: no_bid
```

### Bid based on daily frequency

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
#1. If the user is in California and in segment 111, bid the user's daily frequency for line item 222 times -.2, plus 5, with an upper bound of 4.
#2. Otherwise, do not bid.
 
if every region="US:CA", segment[111]:
        leaf_name: "d0001"
        value: compute(line_item[222].day_frequency, -0.2, 5.0, 0.0, 4.0)
else:
        leaf_name: "d0000"
        value: no_bid
```

### Bid based on lifetime frequency

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
#1. If the user is in California and in segment 111, bid the lifetime frequency for creative 333 times -.2, plus 8, with an upper bound of 6.
#2. Otherwise, do not bid.
 
if every region="US:CA", segment[111]:
        leaf_name: "e0001"
        value: compute(creative[333].lifetime_frequency, -0.2, 8.0, 0.0, 6.0)
else:
        leaf_name: "e0000"
        value: no_bid
```

### Bid based on recency

> [!NOTE]
> In the code example below, lines beginning with \# are comments to help you understand the logic of this tree.

```
#1. If the user is in California, bid the recency for creative 333 times -.2, plus 8, with an upper bound of 6.
#2. Otherwise, do not bid.
 
if region="US:CA":
        leaf_name: "f0001"
        value: compute(creative[333].recency, -0.2, 8.0, 0.0, 6.0)
else:
        leaf_name: "f0000"
        value: no_bid
```

## Related topics

- [Custom Models](custom-models.md)
- [The Bonsai Language](the-bonsai-language.md)
- [Bonsai Features](bonsai-language-features.md)
- [Custom Model Parser Service](custom-model-parser-service.md)
- [Custom Model Service](custom-model-service.md)
