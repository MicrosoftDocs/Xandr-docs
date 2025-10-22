---
title: Targeting Key Service
description: Use the Targeting Key and Targeting Value services to define your own key/value combinations for use in targeting on line items and campaigns.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Targeting Key service

The **targeting-key** service works in conjunction with the **targeting-value** service to allow you to define your own key/value combinations for use in targeting on line items, campaigns, and so on. See [Custom Key Value Targeting](./custom-key-value-targeting.md) for more information.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/targeting-key`<br>(`create_target_key` JSON) | Add a new targeting key. |
| `PUT` | `https://api.appnexus.com/targeting-key?id=TARGETING_KEY_ID`<br>(`update_targeting_key` JSON) | Modify a targeting key. |
| `GET` | `https://api.appnexus.com/targeting-key` | View all targeting keys. |
| `GET` | `https://api.appnexus.com/targeting-key?id=TARGETING_KEY_ID` | View a specific targeting key. |
| `GET` | `https://api.appnexus.com/targeting-key?name=TARGETING_KEY_NAME1,TARGETING_KEY_NAME2,TARGETING_KEY_NAME3` | View a set of targeting keys by name. |
| `DELETE` | `https://api.appnexus.com/targeting-key?id=TARGETING_KEY_ID` | Delete a targeting key. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the targeting key.<br><br>**Default**: Auto-generated number<br>**Required On**: `PUT`/ `DELETE`, in query string |
| `type` | enum | The data type of the key and its associated values. Must be one of the following values:<br> - `string`<br> - `numeric`<br>**Required On**: `POST` |
| `name` | string | The name of the targeting key.<br>The value must be one word, with no spaces. This name must be unique within your member.<br><br>**Required On**: `POST` |
| `label` | string | A label for the key, to be used for reporting. This value is not required, but if you do include a value, it must be unique within your member. Label can be a maximum of 190 characters. |
| `state` | enum | The state of the targeting key. Possible values are `active` and `inactive`.<br><br>**Default**: `active` |
| `created_on` | date | **Read-only**. The date and time the targeting key was created. |
| `last_modified` | date | **Read-only**. The date and time the targeting key was last modified. |

### Key requirements

#### Number of keys

- You can have up to 500 active keys at one time.
- You can have up to 100,000 values per key.
- You can have up to 2,500,000 total active values at one time.

#### Key naming

- Key names are not case-sensitive.
- Maximum key name length is 50 characters.
- Key names must be one word, with no whitespace.
- Key names cannot contain any of the following special characters:
  - " (double quotes)
  - ' (apostrophe)
  - = (equal sign)
  - ! (exclamation point)
  - \+ (plus sign)
  - \# (hashtag)
  - \* (asterisk)
  - ~ (tilde)
  - ; (semicolon)
  - ^ (caret)
  - () (parentheses)
  - \< \> (angle brackets)
  - \[ \] (square brackets)
  - , (comma)
  - & (ampersand)
  - @ (at)
  - : (colon)
  - ? (question mark)
  - % (percent sign)
  - / (forward slash)

## Examples

### View all targeting keys

```
$ curl -b cookies 'https://api.appnexus.com/targeting-key'

{
    "targeting-keys": [
        {
            "id": 7,
            "type": "string",
            "name": "key1",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:29:29",
            "last_modified": "2016-08-26 06:29:29"
        },
        {
            "id": 11,
            "type": "string",
            "name": "testkey",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:30:37",
            "last_modified": "2016-08-26 06:30:37"
        },
        {
            "id": 12,
            "type": "string",
            "name": "testkey3",
            "label": "This is a test",
            "state": "active",
            "created_on": "2016-08-26 08:04:42",
            "last_modified": "2016-08-26 08:15:02"
        }
    ]...
}
```

### View a specific targeting key

```
$ curl -b cookies 'https://api.appnexus.com/targeting-key?id=12'
 
{
    "targeting-key": {
        "id": 12,
        "type": "string",
        "name": "testkey3",
        "label": "This is a test",
        "state": "active",
        "created_on": "2016-08-26 08:04:42",
        "last_modified": "2016-08-26 08:15:02"
    }...
}
```

### Add a targeting key

```
$ cat create_targeting_key.json
{
    "targeting-key": {
        "name": "testkey4",
        "type": "string"
    } 
}
 
$ curl -b cookies -H "Content-Type:application/json" -X POST -d '@create_targeting_key.json' 'https://api.appnexus.com/targeting-key'
```

### Modify a targeting key

```
$ cat update_targeting_key.json
{
    "targeting-key": {
        "name": "newtestkey3",
        "label": "This is a test"
    } 
}
 
$ curl -b cookies -H "Content-Type:application/json" -X PUT -d @update_target_key.json 'https://api.appnexus.com/targeting-key?id=12'
```

### Filter targeting keys by name

```
$ curl -b cookies 'https://api.appnexus.com/targeting-key?name=key1,key2'

{
    "targeting-keys": [
        {
            "id": 7,
            "type": "string",
            "name": "key1",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:29:29",
            "last_modified": "2016-08-26 06:29:29"
        },
        {
            "id": 8,
            "type": "string",
            "name": "key2",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:30:37",
            "last_modified": "2016-08-26 06:30:37"
        }
    ]...
} 
```

### Search within a name or label

This example searches for the string `"car"` anywhere within the `name` or `label` fields.

```
$ curl -b cookies 'https://api.appnexus.com/targeting-key?search=car'

{
    "targeting-keys": [
        {
            "id": 1,
            "type": "string",
            "name": "bluecar",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:29:29",
            "last_modified": "2016-08-26 06:29:29"
        },
        {
            "id": 2,
            "type": "string",
            "name": "key5",
            "label": "Scary values",
            "state": "active",
            "created_on": "2016-08-26 06:29:29",
            "last_modified": "2016-08-26 06:29:29"
        },
        {
            "id": 3,
            "type": "string",
            "name": "car",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:30:37",
            "last_modified": "2016-08-26 06:30:37"
        }
    ]...
} 
```

### Sort by last modified date

You can sort your results by `id`, `name`, `label`, `created_on`, or `last_modified`. You can sort in ascending (`asc`) or descending (`desc`) order.

```
$ curl -b cookies 'https://api.appnexus.com/targeting-key?sort=last_modified.asc'

{
    "targeting-keys": [
        {
            "id": 7,
            "type": "string",
            "name": "key1",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:29:29",
            "last_modified": "2016-08-26 06:29:29"
        },
        {
            "id": 10,
            "type": "string",
            "name": "akey",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 04:45:07",
            "last_modified": "2016-08-26 12:52:29"
        },
        {
            "id": 8,
            "type": "string",
            "name": "key2",
            "label": null,
            "state": "active",
            "created_on": "2016-08-26 06:30:37",
            "last_modified": "2016-08-30 10:34:37"
        }
    ]...
} 
```

### Delete a targeting key

Deleting a targeting key will automatically delete all values under that key.

```
$ curl -b cookies -X DELETE 'https://api.appnexus.com/targeting-key?id=12'
```

## Related topics

- [Targeting Value Service](./targeting-value-service.md)
- [Custom Key Value Targeting](./custom-key-value-targeting.md)
