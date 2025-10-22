---
title: Access Policy Member Config Service
description: In this article, learn about the Access Policy Member Config service, their JSON fields, and REST API with a thorough example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Policy Member Config service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-policy-member-config** service is available only to Xandr administrators. This service allows you to identify whether a member account has been enabled for access control.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-policy-member-config?member_id=MEMBER_ID](https://api.appnexus.com/access-policy-member-config?member_id=MEMBER_ID) | View a customer's access settings. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `member_id` | int | The ID of the member. |
| `enable_access_control` | boolean | Determines whether the member account is configured for access control.<br>**Default:** `false` |
| `team_object_limit` | int | The total number of resources a member can have assigned to all teams.<br>**Default:** `1000` |
| `last_modified` | date | The date and time when the member configuration was last modified. |
| `enable_2fa` | boolean | If `true`, two factor authentication (2FA) has been enabled for this member. |

## Example

### View a member's access control status

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-member-config?member_id=1234'
            {
            "member_id": 1234,
            "enable_access_control": true,
            "team_object_limit": 1000,
            "last_modified": "2016-07-07 18:01:06",
            "enable_2fa": false
            }
```

## Related topic

[Working with Roles using the API](working-with-roles-using-the-api.md)
