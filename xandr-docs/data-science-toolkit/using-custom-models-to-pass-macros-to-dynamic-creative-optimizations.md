---
title: Data Science Toolkit - Custom Models for Passing Macros to Dynamic Creative Optimizations
description: This article suggests using a macro and non-valuation custom model to ensure that the Dynamic Creative Optimizations (DCO) receive targeted segments.
ms.custom: data-science
ms.date: 10/28/2023
---

# Data Science Toolkit - Use custom models to pass macros to dynamic creative optimizations

This document provides a solution to use a macro combined with a non-valuation custom model to ensure the Dynamic Creative Optimizations (DCO) receives all the segments the user has been targeted on.

## Problem solutions

There are two solutions to ensuring the DCO receives all the segments the user has been targeted on.

### Utilize split's custom values

In, users can utilize the splits [custom value feature](../invest/create-a-programmable-split.md) (log-in required) to create a key-value pair and use the key as a macro.

#### Splits custom value method

- Use splits for segment targeting and then use the custom value field to assign a key-value pair to each split.
- Use the key as a macro for the split's creative tag. Xandr will then populate this macro with the value specified in the splits. The DCO can then use value to serve a dynamic ad.

#### Problems with this approach

- Only allows a limited number of splits per ALI (100 splits only in ).
- You can only have one key-value pair per split and therefore, only one custom macro per split.

### Use non-valuation custom model

Use a [non-valuation custom model](nonvaluation-custom-model.md) to create custom macros that to pass to the DCO. This solution is more flexible than using the split's custom value feature as it enables the user to create as many macros as needed for each condition.

#### Non-valuation custom model method

1. Create a non-valuation custom model:

    ```
    if segment[124541]:
        leaf_name: "Word"
        creative_macros["test1"]: "123456"
    elif segment[124683]:
        leaf_name: "yooo"
        creative_macros["test1"]: "67890"
    else:
        leaf_name: "nada"
        creative_macros["test1"]: "456123"
    ```

    If you only need one custom macro use the `leaf_name` field as your macro. When using the `leaf_name` field the macro is called `CUSTOM_MODEL_LEAF_NAME`. If you want to use test1, just use that as a macro, and once a creative request goes out, Xandr will return the value specified. For example, use test1 as a macro, and if you don't belong to any of the segments specified, the model should return the value 456123.

1. Use [base64 encoding](https://developer.mozilla.org/en-US/docs/Glossary/Base64) for the custom model you created. The following code can be used to base64 encode an object using the command line:  

    ```
     cat custom_model_1 | base64
    ```

1. Once the custom mode is base64 encoded create a JSON file:  

    ```
    {
        "custom_model": {
            "name": "Silver_car_DCO_TEST_1",
            "member_id" : 958,
            "advertiser_id": 3073078,
            "custom_model_structure": "decision_tree",
            "model_output": "bid",
            "model_text": "aWYgc2VnbWVudFsxMjQ1NDFdOgogIGxlYWZfbmFtZTogIldvcmQiCiAgY3JlYXRpdmVfbWFjcm9zWyJ0ZXN0MSJdOiA...
        }
    }
    ```

1. Make a `PUT` request to the [Custom Model Service](./custom-model-service.md) and attach the JSON file as the data.

1. If the `PUT` request is successful record the `custom_model_id`.

1. Make another `PUT` call, this time to the [Line Item Model Service](./line-item-model-service.md), attach a JSON file that contains the `custom_model_id`, type, and origin.

1. Use the macro in a creative tag In the example below `CUSTOM_MODEL_LEAF_NAME` and test1 are being used as the creative macro:  

    ```
    <script src="https://cdn.adacado.com/arb/arb.min.js"></script>
    <script type="text/javascript">
        !function(){var p={}
        /* Begin Ad Parameters */
        p["AudienceID"] = "${CUSTOM_MODEL_LEAF_NAME}";
        p["CustomModel1"] = "${test1}";
        p["prependUrl"] = "${CLICK_URL}";
        p["mediaDspId"] = "APN";
        p["mediaAuctionId"] = "${AUCTION_ID}";
        p["mediaBidPrice"] = "${BID_PRICE}";
        p["mediaPaidPrice"] = "${PRICE_PAID}";
        p["mediaInventoryClass"] = "${INV_CLASS}";
        p["mediaPublisherId"] = "${PUBLISHER_ID}";
        p["mediaReferer"] = "${REFERER_URL}";
        p["mediaAdvertiserId"] = "${ADV_ID}";
        p["mediaLineItemId"] = "${CPG_ID}";
        p["mediaCampaignId"] = "${CP_ID}";
        p["mediaAdvertiserFreq"] = "${ADV_FREQ}";
        p["mediaSessionFreq"] = "${SESSION_FREQ}";
        /* End Ad Parameters */
        adacado.doodad({ url:"//ads.adacado.com/adacadoWebV2/14189.js", p:p });
        }()
    </script>
    ```

#### Problems with this approach

- Non-Valuation Models only work for Augmented Line Items (ALIs) that don't have any splits. Splits are technically a custom model and would take priority over user-written models.
- The client needs to have the capability to write custom models.

## Related topic
[Custom Models](custom-models.md)
