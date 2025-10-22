---
title: Access Platform User Role Service
description: In this article, learn about the Access Platform User Role service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Platform User Role service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-platform-user-role** service can be used to manage roles for users who are not associated with members.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-platform-user-role](https://api.appnexus.com/access-platform-user-role) | View all platform users and their roles. |
| `POST` | [https://api.appnexus.com/access-platform-user-role?user_id=UID&role_id=ROLE_ID](https://api.appnexus.com/access-platform-user-role?user_id=UID&role_id=ROLE_ID) | Create a platform user/role association. |
| `DELETE` | [https://api.appnexus.com/access-platform-user-role](https://api.appnexus.com/access-platform-user-role) | Delete a platform user/role association. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `description` | string | The description of the role. |
| `id` | int | The unique ID of the user/role association.<br>**Required On:** `DELETE`<br>**Default:** Auto-generated on `POST`. |
| `platform_role` | Boolean | Returns `true` if the role is a platform role; `false` if the role is a custom role. |
| `role_id` | string | The type of group. Value will be either `role` or `team`.<br>**Required On:** `POST` |
| `role_name` | object | The ID and name of each resource in the group. |
| `user_id` | int | The ID of the group.<br>**Required On:** `POST` |

## Examples

### View all platform user/role associations

```
$ curl -b cookies 'https://api.appnexus.com/access-platform-user-role'
"access-platform-user-role": [
    {
        "user_id": 123456,
        "role_id": 111,
        "role_name": "Test Role",
        "description": "Temporary Role for Testing",
        "platform_role": false,
        "id": 123
    }
]
```

### Create a new platform user/role association

```
$ cat platform-user-role.json
{
        "access-platform-user-role": 
                [
                        {
                                "user_id": 123456,
                                "role_id": 123
                        }
                ]
}
$ curl -b cookies 'https://api.appnexus.com/access-platform-user-role'
```

### Delete a platform user/role association

```
curl -b cookies 'https://api.appnexus.com/access-platform-user-role?id=123'
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
