---
title: Data Science Toolkit - ALI Workflow with Custom Models
description: Explore a detailed guide on how to create and seamlessly associate custom models with an Augmented Line Item (ALI).
ms.custom: data-science
ms.date: 10/28/2023
---

# Data Science Toolkit - ALI workflow with custom models

Working with [Custom Models](custom-models.md) such as [Bonsai trees](the-bonsai-language.md) or Logistic Regression models and Augmented Line Items (ALI) is fairly similar to the process of working with traditional campaigns. This guide provides instructions for creating and associating custom models to an ALI. In the example below, we will create a Bonsai expected value [decision tree object](create-a-bonsai-decision-tree-custom-model.md) and use it as a bidding strategy for an ALI.

## Tree creation and validation

The syntax for Bonsai trees and the features currently available for campaigns is the same for trees that work with ALI. Use the Custom Model Service for creating your custom model. The Custom Model Parser Service can be utilized to validate the Bonsai decision tree. Documentation for these services can be found here:

- [Custom Model Service](custom-model-service.md)
- [Custom Model Parser Service](custom-model-parser-service.md)

### Example

For the purposes of this example, we will create a simple tree (a literal '`0`' character) under a test advertiser:

#### Custom model

##### `custom_model.json`

```
{
  "custom_model": {
    "name": "Test Custom Model",
    "code": "mcg-test-custom-model",
    "advertiser_id": 354236,
    "custom_model_structure": "decision_tree",
    "model_output": "bid",
    "model_text": "MAo="
  }
}
```

#### `POST`/Creation of tree model

##### `POST` model (response abbreviated)

```
$ curl -b dcc -c dcc -X POST -s -d '@json/custom-model.json' "https://api-test.appnexus.com/custom-model?advertiser_id=354236"  | jq '.'
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": "379792",
    "start_element": 0,
    "num_elements": 100,
    "custom_model": {
      "id": 379792,
      "name": "Test Custom Model",
      "code": "mcg-test-custom-model",
      "member_id": 958,
      "advertiser_id": 354236,
      "custom_model_structure": "decision_tree",
      "model_output": "bid",
      "compiled_text": null,
      "model_text": "MAo=",
      "original_text": "0
",
      "active": true,
      "last_modified": "2016-08-30 20:55:38"
    },
    "dbg_info": {...}
  }
}
```

## Create an ALI through API

Custom models are designed to enable Xandr API users to add decision-making logic to the valuation models, non-valuation models, and creative delivery of their Augmented Line Items or campaigns. For instructions on creating an ALI, [review the documentation](../digital-platform-api/line-item-service---ali.md).

## Associate a custom model with an ALI

On augmented line items, there is an array field titled, '`custom_models`' which lists custom models associated with a Line Item. Instructions for associating a custom model with an ALI can be found in the [Line Item Model Service documentation](line-item-model-service.md).

### Target IP addresses

Customers in countries or regions that conform to GDPR regulations should be aware that when targeting IP addresses or IP ranges, either in your line item, Bonsai tree, or logistic regression model, there is a possibility the address may be truncated. For details on this process, see our [Service Policies](../policies-regulations/index.yml).

### Multiple custom models

You will be able to associate multiple custom models of different types to the augmented line item. These include a number of custom model types that can be used to override portions of the impression's expected value calculation. An example below demonstrates how the process of associating multiple custom models to a Line Item may work:

#### Custom model example

##### `update_models.json`

```
// Update / Set a single model
{
  "line_item_model": {
      "custom_model_id": 123,
      "type": "click_imp"
    }
}
 
// Set / Update multiple models
{
  "line_item_models": [
    {
      "custom_model_id": 123,
      "type": "click_imp"
    },
    {
      "custom_model_id": 456,
      "type": "ev_click"
    }
  ]
}
```

#### Custom model types

The following model types can be associated as custom models to your Line Item:

| Model Name | Model Output | Output Type / Range |
|:---|:---|:---|
| `expected_value` | Overrides the Xandr Optimized expected value of the impression.<br> - *value in CPM* | Float |
| `creative_selection` | Dynamic selection of creatives associated to this line item. | Creatives, for more information, see [Creative Selection Custom Model](creative-selection-custom-model.md). |
| `ev_click` | Expected value of a click for this impression.<br> - *value in CPM*<br> - *$1 CPC represented as 1000* | Float |
| `click_imp` | Probability of a click for this impression. | Float - (0,1) |
| `ev_conv` | Expected value of a conversion for this impression.<br> - *value in CPM*<br> - *$1 CPC represented as 1000* | Float |
| `conv_imp` | Probability of a conversion for this impression. | Float - (0,1) |
| `conv_click` | Probability of a conversion, given a click. | Float - (0,1) |
| `bid_modifier` | Amount by which this bid on this impression will be multiplied. | Float |
| `nonvaluation` | Custom Macros, Learn Status, and other nonvaluation nodes. | Custom model output does not affect bid, though it will be used in reporting when the feature is implemented. For more information, see [Non-Valuation Custom Model](nonvaluation-custom-model.md). |
| `cadence` | Cadence modifier for this impression. | Float |

> [!NOTE]
> A '`goal_type`' of '`custom`' on your Line Item is only required in some scenarios, such as associating an '`expected_value`' model with your Line Item. Certain optimization features, such as Ranked Discovery will be disabled when using this `goal_type` with your custom models.
>
> Read the [Custom Models](custom-models.md) page to learn how the bid calculation is affected by Line Item goals and associated component models.
