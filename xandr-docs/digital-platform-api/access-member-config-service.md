---
title: Access Member Config Service
description: In this article, learn about the Access Member Config service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Member Config service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-member-config** service allows you to manage which members on the platform are subject to access control enforcement. This service is available only to Xandr administrators.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/access-member-config?member_id=MEMBER_ID](https://api.appnexus.com/access-member-config?member_id=MEMBER_ID) | Enable a member's access control. |
| `PUT` | [https://api.appnexus.com/access-member-config?member_id=MEMBER_ID](https://api.appnexus.com/access-member-config?member_id=MEMBER_ID) | Modify a member's access control settings. |
| `GET` | [https://api.appnexus.com/access-member-config?member_id=MEMBER_ID](https://api.appnexus.com/access-member-config?member_id=MEMBER_ID) | View a member's access control settings. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `enable_access_control` | boolean | Defines whether or not the member is under access control.<br>**Default:** `false` |
| `last_modified` | timestamp | The date and time this object was last modified. |
| `member_id` | bigint | The ID of the member.<br>**Required On:** `POST` and `PUT` |
| `team_object_limit` | bigint | The maximum number of objects (advertisers, insertion orders, publishers, placements groups, and placements) that can be assigned to any one team for this member.<br>**Default:** `1000` |

## Examples

### Retrieve a member's access control settings

```
$ curl -b cookies 'https://api.appnexus.com/access-member-config?member_id=1234'
{
    "response": {
        "status": "OK",
        "access-member-config": [
            {
                "member_id": 1234,
                "enable_access_control": false,
                "team_object_limit": 1000,
                "last_modified": "2016-06-22 15:37:49"
            }
        ]
    }
}
```

### Turn on access control for a member

```
$ cat access-control.json
{
    "access-member-config":
        {
            "member_id":1234,
            "enable_access_control": true
        }
}
$ curl -b cookies -X POST -d '@access-control.json' 'https://api.appnexus.com/access-member-config?member_id=1234'
```

### Modify the number of objects allowed in a team

```
$ cat limit.json
{
    "access-member-config":
        {
            "member_id":1234,
            "team_object_limit": 2000
        }
}
$ curl -b cookies -X PUT -d '@limit.json' 'https://api.appnexus.com/access-member-config?member_id=1234'
```

## Related topic

[Working with Roles using the API](working-with-roles-using-the-api.md)
