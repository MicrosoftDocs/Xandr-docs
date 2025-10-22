---
title: Entitlement Type Service
description: Use the Entitlement Type service to assign specific code features to members through the member service, such as keyword targeting or deal discovery.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Entitlement Type service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **entitlement-type** service allows you to define a code that will be assigned to members through the [Member Service](./member-service.md). This code is used to provide certain features for only specific members. For example, we might have members who are allowed to do keyword targeting or deal discovery. After using this service to create entitlement types, you can assign one or more entitlement types to a member.

## REST API

| HTTP Method | Enpoints | Descriptions |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/entitlement-type` | View all entitlement types |
| `POST` | `https://api.appnexus.com/entitlement-type` | Create an entitlement type |
| `PUT` | `https://api.appnexus.com/entitlement-type?id=ENTITLEMENT_TYPE_ID` | Modify an entitlement type |
| `DELETE` | `https://api.appnexus.com/entitlement-type?id=ENTITLEMENT_TYPE_ID` | Delete an entitlement type |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the entitlement type. This value is auto-generated on `POST`.<br><br>**Default**: Auto-generated number. |
| `code` | string | The code associated with the entitlement. This value is set by the engineer and should be provided by them. |
| `description` | object | A description of the entitlement. This value is optional and has no effect on the actual entitlement. Description is the only field that can be modified after the entitlement type has been created. |
| `created_on` | timestamp | The date and time the entitlement was created.<br><br>**Default**: Auto-generated on creation. |
| `last_activity` | timestamp | The date and time the entitlement was last modified.<br><br>**Default**: Auto-generated at each modification. |

## Examples

### View all entitlement types

```
$ curl -b cookies 'https://api.appnexus.com/entitlement-type'
{
    "response": {
        "status": "OK",
        "count": 4,
        "start_element": 0,
        "num_elements": 100,
        "entitlement-types": [
            {
                "id": 1,
                "code": "seller_external_uid",
                "description": "Boolean, when true allows external uid mapping for a seller",
                "last_activity": "2016-10-12 15:39:28",
                "created_on": "2016-10-12 15:39:28"
            },
            {
                "id": 2,
                "code": "seller_deal_discovery",
                "description": "Boolean, when true allows deal discovery for a seller",
                "last_activity": "2016-10-13 16:43:51",
                "created_on": "2016-10-13 16:43:51"
            },
            {
                "id": 3,
                "code": "seller_keyword_targeting",
                "description": "Boolean, when true allows keyword targeting for a seller",
                "last_activity": "2016-10-13 16:43:51",
                "created_on": "2016-10-13 16:43:51"
            },
            {
                "id": 4,
                "code": "seller_keyword_segment_targeting",
                "description": "Boolean, when true allows keyword-based segment targeting for a seller",
                "last_activity": "2016-10-13 16:43:51",
                "created_on": "2016-10-13 16:43:51"
            }
        ],
...
}
```

### Create an entitlement type

```
$cat entitlement_type.json
{
    "entitlement-type": {
        "code": "test_entitlement_code",
        "description": "testing entitlement type"
    }
}
```

```
$ curl -b cookies -X POST -d @entitlement_type.json 'https://api.appnexus.com/entitlement-type'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1,
        "start_element": 0,
        "num_elements": 100,
        "entitlement-type": {
            "id": 1,
            "code": "test_entitlement_code",
            "description": "testing entitlement type",
            "last_activity": "2016-12-02 16:47:47",
            "created_on": "2016-12-02 16:47:47"
        }, ...
}
```

### Modify an entitlement type

```
 $cat entitlement_type_update.json

{
    "entitlement-type": {
        "description": "entitlement type for testing"
    }
}
```

```
$ curl -b cookies -X POST -d @entitlement_type_update.json 'https://api.appnexus.com/entitlement-type?id=1'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1,
        "start_element": 0,
        "num_elements": 100,
        "entitlement-type": {
            "id": 1,
            "code": "test_entitlement_code",
            "description": "entitlement type for testing",
            "last_activity": "2016-12-02 16:56:48",
            "created_on": "2016-12-02 16:47:47"
        }, ...
}
```

## Related topic

[Member Service](./member-service.md)
