---
title: Data Science Toolkit - Custom Models
description: This page provides an overview of how to get started with Custom Models for various use cases, including Bid Valuation, Creative Selection, and Non-Valuation Purposes.    
ms.custom: data-science
ms.date: 10/28/2023
---


# Data Science Toolkit - Custom models

This page provides information on Custom Models, how Bid Value and Expected Value are derived and lists the different types of Custom Models.

## Overview

Custom Models enable Xandr API users to use [Bonsai Decision Trees](the-bonsai-language.md) and/or [Logistic Regression Models](logistic-regression-models.md) to add
decision making logic for Bid Valuation, Creative Delivery and Non-Valuation purposes to their Augmented Line Items (ALI) or campaigns. This page provides an overview on how to get started using Custom Models for the various use-cases:  
  
- Bid Valuation: to override Xandr Optimization algorithms, or individual components of the algorithms.
- Creative Selection: to support your Dynamic Creative Optimization strategies.
- Non Valuation Purposes: to insert custom creative macros into impression tracking calls to enhance reporting or affect learn status.

## Use cases

**Bid valuation custom models**

Custom Models are designed to allow data scientists, through the Xandr API, to break out specific portions of their Bid Valuation model by associating multiple Bonsai Decision Tree and/or Logistic Regression Models to an [Augmented Line Item](../digital-platform-api/line-item-service---ali.md) or campaign to create a custom buying strategy. By associating specific types of models to the Expected Value and/or Cadence Modifier and/or Bid Modifier calculations for an impression, it is possible to override portions of Xandr Optimization, and to allow our system to only handle aspects of valuation that your own models do not cover.

:::image type="content" source="./media/datascience-a.png" alt-text="Screenshot of Bid Valuation.":::

Please refer to our [Bid Valuation with Custom Models](bid-valuation-with-custom-models.md) documentation for more information on this use case.

**Creative selection custom models**

By default, Xandr randomly distributes the creatives associated with a line item. Custom Models enable users to override this default feature and assign a creative to a line item. Users can write a decision tree using any of our Bonsai language's [features](bonsai-language-features.md) or logic to determine which creative should be served.  For example:

``` 
$cat creative-tree
 
if user_hour = 1:
    leaf_name: "cs_1"
    creatives: {12345: 30, 67890: 20}
else:
    leaf_name: "cs_2"
    creatives: {12347: 1}
```

Please refer to our [Creative Selection Custom Models](creative-selection-custom-model.md) documentation for more information on this use case.

**Non-valuation custom models**

Non-valuation custom models do not affect bid valuation. They're used to insert custom creative macros into impression tracking calls, which can eventually be used for other functions, such as affecting Learn status.

Please refer to our [Non-Valuation Custom Models](nonvaluation-custom-model.md) documentation for more information on this use case.

## Get started

**Step 1: Decide on your use case**

Decide which use case(s) you want to proceed with and learn more about how the Custom Models product can help you achieve your goals:

- [Bid Valuation with Custom Models](bid-valuation-with-custom-models.md)
- [Creative Selection Custom Models](creative-selection-custom-model.md)
- [Non Valuation Custom Models](nonvaluation-custom-model.md)

**Step 2: Learn about Bonsai decision trees and logistic regression models**

Learn more about the two language types we support and select the one that matches the needs to achieve your goals. For Bid Valuation Custom Models use either Bonsai decision trees and/or Logistic Regression Models. For Creative Selection or Non-Valuation Custom Models use Bonsai decision trees.

- [Bonsai Language](the-bonsai-language.md)
- [Logistic Regression Models](logistic-regression-models.md)

**Step 3: Learn how to upload custom models via API**

Once you have built a Bonsai decision tree or Logistic Regression Model, learn how to attach them to your ALI and which API services to use:

- [ALI Workflow with Custom Models](ali-workflow-with-custom-models.md)
- [Custom Model API Reference](custom-model-api-reference.md)

**Step 4: Learn how to use log-level custom model feed**

When your ALI or campaign, with attached Custom Models, is live, it is useful to analyze and report on them. The [Log-Level Custom Model Feed](log-level-custom-model-feed.md) enables users to review specific data on models associated with your ALI or campaign and the values calculated by each model.

## Related topics

- [ALI Workflow with Custom Models](ali-workflow-with-custom-models.md)
- [Bid Valuation With Custom Models](bid-valuation-with-custom-models.md)
- [Bonsai Language](the-bonsai-language.md)
- [Creative Selection Custom Model](creative-selection-custom-model.md)
- [Custom Model API Reference](custom-model-api-reference.md)
- [Logistic Regression Models](logistic-regression-models.md)
- [NonValuation Custom Model](nonvaluation-custom-model.md)
