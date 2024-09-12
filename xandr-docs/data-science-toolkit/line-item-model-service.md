---
title: Data Science Toolkit - Line Item Model Service
description: Learn how Line Item Model service provides distinction between client uploaded models and Xandr generated models, and why this distinction is important.
ms.custom: data-science
ms.date: 10/28/2023
---

# Data Science Toolkit - Line item model service

The Line Item Model service is used to associate custom models to the custom models array. Compared to the standard Line Item service, the Line Item Model service allows for the distinction between client uploaded models and Xandr generated models. The distinction between client and Xandr models is important for the following:

- Reporting with the custom model Log Level Data feed.
- Associating cadence models, and other model types that Xandr also generates for Line Items.  
  - Xandr generated models are automatically appended to Line Items as part of the V8 optimization system. The bidder should defer to client uploaded models when evaluating the custom models associated with line items.
  - Xandr automated processes should not overwrite client uploaded models.

## Usage

### End points

- **Domain**: `https://api.appnexus.com/`
- **Path**: `/line-item-model`

### Authentication

`/line-item-model` supports Xandr API [standard Authentication Methods](../digital-platform-api/authentication-service.md).

## Supported methods and fields

| Method | Endpoint | Purpose |
|--|--|--|
| DELETE | `/line-item-model?id={line_item_id}` | Delete a single custom-model association on a Line Item, given a 'line-item-model' JSON object |
| GET | `/line-item-model?id={line_item_id}` | Get a list of custom-models associated with a Line Item |
| POST |  | Method not supported. |
| PUT | `/line-item-model?id={line_item_id}` | Add or update existing custom-models associated with a line-item, given a 'line-item-model' JSON object. |

### Parameters

| Name | Data Type | Description | Example |
|--|--|--|--|
| `line-item-id` | int | The ID of the Line Item object of which we would like to query<br>**Required on**: GET, PUT, DELETE | `/line-item-model?id=123` |

### Fields

| Name | Data Type | Description | Returned On | Example |
|--|--|--|--|--|
| `custom_model_id` | int | The ID of the custom-model associated with the Line Item | GET, PUT | `"custom_model_id": 211973` |
| `line-item-models` | string, and array of custom-models | The ID of the Line Item that we have queried, along with the array of custom-models associated with that line-item | GET, PUT | ```"line_item_models": { "4125657": [ { "custom_model_id": 139527, "type": "cadence" }, { "custom_model_id": 130004, "type": "expected_value" } ] }``` |
| `type` | string | The "type" of this model association. A full list of conditional component model types can be found on the [Bid Valuation with Custom Models](bid-valuation-with-custom-models.md) page. | GET, PUT | `"type": "ev_click"` |

## Usage examples

### GET example

\`GET\` custom-models associated to a Line Item

``` 
curl -H 'Authorization: {api_token}' 'https://api.appnexus.com/line-item-model?id=123'
```

**Response:**

``` 
{
  "response": {
    "dbg_info": {...},
    "num_elements": null,
    "start_element": null,
    "count": 2,
    "line_item_models": {
      "123": [
        {
          "custom_model_id": 139527,
          "type": "cadence"
        },
        {
          "custom_model_id": 130004,
          "type": "expected_value"
        }
      ]
    },
    "status": "OK"
  }
}
```

### PUT example

\`PUT\` - Create and Update custom-models associated with a Line Item

> [!NOTE]
> Important Usage Info
>
> `PUT` will only add new models to a line-item, or update existing models. If a model is not referenced in your `line_item_model` array, it is not affected by your request, **unless** one of the models listed in your array is of the same `type` as a model already associated to the line-item.

``` 
curl -H 'Authorization: {api_token}' -d @update_models.json -X PUT 'https://api.appnexus.com/line-item-model?id=12345'
```

**update_models.json**

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

**Response:**

``` 
{
  "response": {
    "dbg_info": {...},
    "num_elements": null,
    "start_element": null,
    "count": 1,
    "line_item_models": {
      "12345": [
        {
          "custom_model_id": 123,
          "type": "click_imp"
        },
                {
          "custom_model_id": 456,
          "type": "ev_click"
        }
      ]
    },
    "status": "OK"
  }
}
```

### DELETE example

\`DELETE\` a custom-model associated to a Line Item

``` 
curl -H 'Authorization: {api_token}' -d @detach_model.json -X DELETE 'https://api.appnexus.com/line-item-model?id=:line_item_id'
```

**detach_model.json**

``` 
{
  "line_item_model": {
        "type": "cadence"
  }
}
```

**Response:**

``` 
{
  "response": {
    "dbg_info": {...},
    "num_elements": null,
    "start_element": null,
    "count": 1,
    "status": "OK"
  }
}
```
