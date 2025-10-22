---
title: Placement Set Service
description: Use the Placement Set service to support the creation and management of ad pods and linear groupings of ads designed to fit within a single video placement.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Placement Set service

The Placement Set Service supports the creation and management of ad pods, linear groupings of ads designed to fit within a single video placement.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/placement-set?publisher_id=PUBLISHER_ID` | View all of the placement sets for one of your publishers. |
| `GET` | `https://api.appnexus.com/placement-set?id=PLACEMENT_ID` | View a specific placement set for one of your publishers. |
| `POST` | `https://api.appnexus.com/placement-set?publisher_id=PUBLISHER_ID&member_id=MEMBER_ID` | Add a placement set (NETWORK). <br><br>**Note**: All ad pod placements associated with a placement group must belong to placement group's publisher. |
| `PUT` | `https://api.appnexus.com/placement-set?id=PLACEMENT_ID&publisher_id=PUBLISHER_ID&member_id=MEMBER_ID` | Modify an existing placement set (NETWORK). |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | The code associated with the placement set. <br><br>**Default**: `null` |
| `id` | int | The ID of the placement set. <br><br>**Required On**: `PUT` |
| `last_modified` | timestamp | The time stamp when activity was last performed on the placement set. <br><br>**Default**: `null` |
| `member_id` | int | The ID of the member associated with the publisher. <br><br>**Required On**: `POST` |
| `name` | string | The name for the placement set. The user would use this to identify their placement set. <br><br>**Default**: `null` |
| `placement_ids` | array of ints | The placements that are associated with the placement set. <br><br>**Default**: `null` |
| `publisher_id` | int | The ID of the publisher associated with the placement set. <br><br>**Required On**: `POST` |

## Examples

### Create a new placement set

```
$ cat ps_create

{
    "placement_set":{
        "code":"appnexus_example2",
        "name":"placement set test",
        "member_id":958,
        "publisher_id":123456,
        "placement_ids":[01234567, 12345678]
    }
}
$ curl -b cookies -c cookies -X POST -d @ps_create 'https://api.appnexus.com/placement-set?member_id=958&publisher_id=123456' 
```

### Update an existing placement set

```
$ cat ps_change
{
    "placement_set":{
        "id":2,
        "name":"new placement set name",
        "placement_ids":[01234567, 12345678]
    }
}

$ curl -b cookies -c cookies -X PUT -d @ps_change 'https://api.appnexus.com/placement-set?id=2&member_id=958&publisher_id=123456'
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "placement_set": {
            "id": 2,
            "name": "new placement set name",
            "code": "appnexus_example2",
            "member_id": 958,
            "publisher_id": 123456,
            "last_activity": "2017-05-01 03:06:51",
            "placement_ids": [
                "01234567",
                "12345678"
            ]
        },
        "count": 1
        }
    }
}
```

### View an existing placement set

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/placement-set?publisher_id=123456'
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "placement_sets": [
            {
                "id": 1,
                "name": "my first test",
                "code": "appnexus_example",
                "member_id": 958,
                "publisher_id": 123456,
                "last_activity": "2017-05-01 02:52:09",
                "placement_ids": null
            },
            {
                "id": 2,
                "name": "placement set test",
                "code": "appnexus_example2",
                "member_id": 958,
                "publisher_id": 123456,
                "last_activity": "2017-05-01 02:55:11",
                "placement_ids": [
                    "01234567",
                    "12345678"
                ]
            }
        ],
        "count": 2
        ...
        }
    }
}
```
