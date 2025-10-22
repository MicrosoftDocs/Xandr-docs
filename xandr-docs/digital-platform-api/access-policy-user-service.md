---
title: Access Policy User Service
description: In this article, learn about the Access Policy User service, their JSON fields, and REST API with a thorough example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Policy User service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-policy-user** service allows you to identify which roles and teams a user is on.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-policy-user?user_id=USER_ID](https://api.appnexus.com/access-policy-user?user_id=USER_ID) | View a user's roles and teams. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `groups` | object | An object containing arrays of roles and teams to which this user is assigned. |
| `landing_pages` | array | The list of Console pages this user will see upon logon. Only one page is supported at this time. |
| `user_id` | int | The ID of the user.<br>**Default:** Auto-generated number.<br>**Required On:** `GET` |

### Groups

This object contains the role and teams to which a user is assigned.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `roles` | array | A list of role IDs for roles this user is assigned to. Only one role assignment is supported at this time. |
| `teams` | array | A list of team IDs for teams this user is assigned to. A user can be assigned to multiple teams. |

## Example

### View a user's teams and role

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-user?user_id=10'
{
    "user_id": 10,
    "landing_pages": [
    ],
    "groups": {
        "roles": [
            4
        ],
                "teams": [
                        20,
                        22
                ]
    }
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
