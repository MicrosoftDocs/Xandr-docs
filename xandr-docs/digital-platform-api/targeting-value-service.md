---
title: Targeting Value Service
description: Use the Targeting Value and Targeting Key services to create your own key/value combinations for targeting line items and campaigns. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Targeting Value service

The targeting-value service works in conjunction with the targeting-key service to allow you to create your own key/value combinations for use in targeting on line items, campaigns, and so on. See [Custom Key Value Targeting](./custom-key-value-targeting.md) for more information.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/targeting-value?targeting_key_id=TARGETING_KEY_ID` | View all targeting values for a specific key. |
| `GET` | `https://api.appnexus.com/targeting-value?targeting_key_id=TARGETING_KEY_ID&id=TARGETING_VALUE_ID` | View a specific targeting value. |
| `POST` | `https://api.appnexus.com/targeting-value?targeting_key_id=TARGETING_KEY_ID` | Add a new targeting value. |
| `POST` | `https://api.appnexus.com/targeting-value?targeting_key_id=TARGETING_KEY_ID` | Add multiple new targeting values. |
| `PUT` | `https://api.appnexus.com/targeting-value?id=TARGETING_VALUE_ID` | Modify a targeting value. |
| `DELETE` | `https://api.appnexus.com/targeting-value?id=TARGETING_VALUE_ID` | Delete a targeting value. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `created_on` | date | **Read-only**. The date and time the targeting value was created. |
| `id` | int | The ID of the targeting value.<br><br>**Required On**: `PUT` and `DELETE`<br>**Default**: auto-generated number. |
| `label` | string | A label for the value, used for reporting purposes. This value is not required, but if you supply a value it must be unique within the a key. Labels can be a maximum of 190 characters. |
| `last_modified` | date | **Read-only**. The date and time the targeting value was last modified. |
| `name` | string | The name of the targeting value. This name must be unique within a given targeting key. |
| `targeting_key_id` | int | The ID of the associated targeting key. The targeting key must exist before a value can be created. See [Targeting Key Service](./targeting-key-service.md).<br><br>**Required On**: `POST` and `GET` |

## Value requirements

| Value Requirements | Details |
|:---|:---|
| - You can have up to 100,000 values per key. <br><br>**Note**: <br> The maximum limit for number of values to include in one payload is 100.<br><br>- You can have up to 2,500,000 total active values at one time. | - Value names are not case-sensitive.<br> - Maximum value name length is 100 characters.<br> - Value names may contain whitespace, so they can be more than one word.<br> - Value names cannot contain any of the following special characters:<br> - " (double quotes)<br> - ' (apostrophe)<br> - = (equal sign)<br> - ! (exclamation point)<br> - + (plus sign)<br> - # (hashtag)<br> - * (asterisk)<br> - ~ (tilde)<br> - ; (semicolon)<br> - ^ (caret)<br> - () (parentheses)<br> - < > (angle brackets)<br> - [] (square brackets)<br> - , (comma)<br> - & (ampersand)<br> - @ (at)<br> - : (colon)<br> - ? (question mark)<br> - % (percent)<br> - / (forward slash) |

## Examples

### View all targeting values for a given key

```
$ curl -b cookies 'https://api.appnexus.com/targeting-values?targeting_key_id=12'
 
"targeting-values": [
    {
        "id": 1,
        "targeting_key_id": 12,
        "name": "value1",
        "label": null,
        "created_on": "2016-08-26 08:52:43",
        "last_modified": "2016-08-26 08:52:43"
    },
    {
        "id": 4,
        "targeting_key_id": 12,
        "name": "value2",
        "label": null,
        "created_on": "2016-08-26 09:24:33",
        "last_modified": "2016-08-26 09:24:33"
    }
],...
```

### View a specific targeting value

```
$ curl -b cookies 'https://api.appnexus.com/targeting-value?id=4'
  
"targeting-value": {
    "id": 4,
    "targeting_key_id": 12,
    "name": "value2",
    "label": null,
    "created_on": "2016-08-26 09:24:33",
    "last_modified": "2016-08-26 09:24:33"
},
```

### Add a targeting value (string)

```
$ cat create_targeting_value.json
 
{
    "targeting-value": {
        "name": "value1"
    }
}
  
$ curl -b cookies -X POST -d @create_targeting_value.json 'https://api.appnexus.com/targeting-value?targeting_key_id=12'
```

### Add multiple targeting values (string)

```
$ cat create_multi_targeting_value.json
 
{
    "targeting-values": [
        {
            "name": "value1"
        },
        {
            "name": "value2"
        }
    ]
}
  
$ curl -b cookies -X POST -d @create_multi_targeting_value.json 'https://api.appnexus.com/targeting-value?targeting_key_id=12'
```

### Add a targeting value (numeric)

The `name` field requires a string value (enclosed in quotes). However, if the key has been defined with a `type` of numeric, that string must contain numeric characters.

```
$ cat create_targeting_value.json
 
{
    "targeting-value": {
        "name": "22"
    }
}
  
$ curl -b cookies -X POST -d @create_targeting_value.json 'https://api.appnexus.com/targeting-value?targeting_key_id=12'
```

### Modify a targeting value

```
$ cat update_targeting_value.json
 
{
"targeting-value":
    {
        "name": "newvalue2"
         
    }
}
  
$ curl -b cookies -X PUT -d @update_targeting_value.json 'https://api.appnexus.com/targeting-value?id=4'
```

### Sort by value name

You can sort your results by `id`, `name`, `label`, `created_on`, or `last_modified`. You can sort in ascending (`asc`) or descending (`desc`) order.

```
$ curl -b cookies 'https://api.appnexus.com/targeting-value?targeting_key_id=4&sort=name.asc'
  
"targeting-values": [
    {
        "id": 10,
        "targeting_key_id": 12,
        "name": "a test value",
        "label": null,
        "created_on": "2016-08-26 08:52:43",
        "last_modified": "2016-08-26 08:52:43"
    },
    {
        "id": 7,
        "targeting_key_id": 12,
        "name": "test value",
        "label": null,
        "created_on": "2016-08-26 09:24:33",
        "last_modified": "2016-08-26 09:24:33"
    }
],...
```

### Delete a targeting value

```
$ curl -b cookies -X DELETE 'https://api.appnexus.com/targeting-value?id=4'
```

## Related topics

- [Targeting Key Service](./targeting-key-service.md)
- [Custom Key Value Targeting](./custom-key-value-targeting.md)
