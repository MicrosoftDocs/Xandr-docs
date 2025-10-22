---
title: User UI Service
description: Explore the User UI service, which enables you to modify the requirement for a user's campaign peer approval.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# User UI service

> [!NOTE]
> User UI service is currently available to a limited set of clients and Microsoft employees only.
>
> This service is **deprecated** as of late June 2014, as part of the API 1.15 release. Because 1.15 is a breaking change release, this service will not actually go away until 60 days after the release of 1.15 (likely late August 2014).

The user UI service allows you to change whether campaign peer approval is required for users.

> [!NOTE]
> The User UI settings are not enforced in the service layer for campaign activation. This API service does not interact with API logic. The service cannot actually change user peer approval settings and cannot prevent unapproved campaign creation by a user in the API.  Rather, the User UI service's purpose is exclusively to maintain the permissions for GUI use cases around campaign activation, and to assist with workflow management in.
>
> This service is accessible only to the following user types:
>
> - `member`
> - `advertiser`
> - `member_advertiser`

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/user-ui`<br>(User UI JSON) | Create a new user UI object for a user. |
| `PUT` | `https://api.appnexus.com/user-ui?id=ID`<br><br>(User UI JSON) | Modify settings via a user UI object. |
| `GET` | `https://api.appnexus.com/user-ui` | View settings for all user UI objects. |
| `GET` | `https://api.appnexus.com/user-ui?id=ID` | View settings for a specific user UI object. |
| `DELETE` | `https://api.appnexus.com/user-ui?id=ID` | Remove settings for a user UI object. |
| `GET` | `https://api.appnexus.com/user-ui/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the corresponding user. Duplicate entries of the same user is not allowed.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `member_id` | int | **Read Only.** The ID of the member this user belongs to. |
| `require_campaign_approval` | boolean | Whether the campaigns created by this user require approval before they can be made active.<br>**Default:** `false` |

## Examples

### Add campaign approval requirements for a user by creating a new user UI object

```
$ cat user-ui.json
{
    "user-ui": {
        "id": "5771",
        "require_campaign_approval": "false"
    }
}
```

```
$ curl -b cookies -c cookies -X POST -d @user-ui.json 'https://api.appnexus.com/user-ui'
{
   "response" : {
      "user-ui" : {
         "require_campaign_approval" : false,
         "member_id" : 3897,
         "id" : 5771
      },
      "count" : 1,
      "status" : "OK",
      "id" : 5771
  }
}
```

### Modify campaign approval requirements for a user by modifying the user UI object

```
$ cat modify-user-ui.json
{
    "user-ui": {
        "id": "5771",
        "require_campaign_approval": "true"
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @modify-user-ui.json 'https://api.appnexus.com/user-ui?id=393404'
{
   "response" : {
      "user-ui" : {
         "require_campaign_approval" : true,
         "id" : 5771
      },
      "count" : 1,
      "status" : "OK",
      "id" : "5771"
   }
}
```

### View campaign approval requirements for a specific user

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/user-ui?id=5771'
{
   "response" : {
      "user-ui" : {
         "require_campaign_approval" : true,
         "id" : 5771
      },
      "count" : 1,
      "status" : "OK"
   }
}
```

### Delete a user UI object and the campaign approval requirements information it contains

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/user-ui?id=393404'
{
   "response" : {
      "status" : "OK"
   }
   }
```
