---
title: User DRT Service
description: Explore the User DRT service to control access for users.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# User DRT service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The User DRT service was created to allow the DRT (the central user store owned & maintained by Corp-IT) to control access for users. Eventually, roles and permissions will be governed via the DRT service.

The central ID used by DRT is the `account_id`, which stores mapping data between the user ID and the account ID.

> [!NOTE]
> This service is accessible only to the following types of users:
>
> - Read access: All admins.
> - Write access: Only certain users specified in the config.

## REST API

| HTTP Method | Endpoint | Decsription |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/user-DRT`<br>(User DRT JSON) | Create a new user DRT object for a user. |
| `PUT` | `https://api.appnexus.com/user-DRT?id=ID`<br>(User DRT JSON) | Modify a user DRT object. |
| `GET` | `https://api.appnexus.com/user-DRT` | View DRT information for all users. |
| `GET` | `https://api.appnexus.com/user-DRT?id=ID` | View DRT information for a specific user. |
| `GET` | `https://api.appnexus.com/user-DRT?account_id=ACCOUNT_ID` | View DRT information for all users under a specific DRT account. |
| `DELETE` | `https://api.appnexus.com/user-DRT?id=ID`  | Remove DRT information for a user. |
| `GET` | `https://api.appnexus.com/user-DRT/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the corresponding user. Duplicate entries of the same user are not allowed.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `account_id` | int | The account ID in DRT table. This must be greater than `0`.<br> **Default:** `null` |
| `username` | string | **Read Only.** The login name of the user. |
| `first_name` | string | **Read Only.** The user's first name. |
| `last_name` | string | **Read Only.** The user's last name. |
| `email` | string | **Read Only.** The email address of the user. |
| `user_type` | string | **Read Only.** The type of user. <br>Possible values:<br>- `"member"`<br>- `"bidder"`<br>- `"publisher"`<br>- `"advertiser"`<br>- `"member_advertiser"`<br>- `"member_publisher"` |
| `entity_id` | int | **Read Only.** The ID of the entity (member or bidder) to which the user belongs. |
| `read_only` | boolean | **Read Only.** If `true`, the user is not allowed to make changes via the API.  |

## Examples

### Create a new user DRT object

```
$ cat user-DRT.json
{
    "user-DRT": {
        "id": "11",
        "account_id": "123"
    }
}
```

```
$ curl -b cookies -c cookies -X POST -d @user-DRT.json 'https://api.appnexus.com/user-DRT'
{
   "response" : {
      "count" : 1,
      "status" : "OK",
      "num_elements" : 100,
      "user-DRT" : {
         "user_type" : "member",
         "last_name" : null,
         "username" : "dwm6",
         "account_id" : 123,
         "email" : null,
         "entity_id" : "6",
         "read_only" : "0",
         "id" : 11,
         "first_name" : null
      },
      "id" : 11,
      "start_element" : 0
   }
}
```

### Modify DRT information for a user

```
$ cat modify-user-DRT.json
{
    "user-DRT": {
        "account_id": "321"
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @modify-user-DRT.json 'https://api.appnexus.com/user-DRT?id=11'
{
   "response" : {
      "count" : 1,
      "status" : "OK",
      "num_elements" : 100,
      "user-DRT" : {
         "user_type" : "member",
         "last_name" : null,
         "username" : "dwm6",
         "account_id" : 223,
         "email" : null,
         "entity_id" : "6",
         "read_only" : "0",
         "id" : 11,
         "first_name" : null
      },
      "id" : "11",
      "start_element" : 0
   }
}
```

### View DRT information for a specific user

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/user-DRT?id=11'
{
   "response" : {
      "count" : 1,
      "status" : "OK",
      "num_elements" : 100,
      "user-DRT" : {
         "user_type" : "member",
         "last_name" : null,
         "username" : "dwm6",
         "account_id" : 223,
         "email" : null,
         "entity_id" : "6",
         "read_only" : "0",
         "id" : 11,
         "first_name" : null
      },
      "start_element" : 0
   }
}
```

### View DRT information for all user under a specific account

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/user-DRT?account_id=123'
{
   "response" : {
      "count" : 2,
      "status" : "OK",
      "num_elements" : 100,
      "user-DRTs" : [
         {
            "user_type" : "member",
            "last_name" : null,
            "username" : "data-provider",
            "account_id" : 123,
            "email" : null,
            "entity_id" : "3",
            "read_only" : "0",
            "id" : 6,
            "first_name" : null
         },
         {
            "user_type" : "member",
            "last_name" : null,
            "username" : "dwm273",
            "account_id" : 123,
            "email" : null,
            "entity_id" : "273",
            "read_only" : "0",
            "id" : 12,
            "first_name" : null
         }
      ],
      "start_element" : 0
   }
}
```

### Delete a user DRT object and the campaign approval requirements information it contains

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/user-DRT?id=11'
{
   "response" : {
      "status" : "OK",
      "dbg_info" : {
         "warnings" : [],
         "db" : "master",
         "version" : "trunk",
         "time" : 89.476108551025,
         "start_microtime" : 1396626820.4141,
         "awesomesauce_cache_used" : false,
         "count_cache_used" : false,
         "instance" : "localhost",
         "output_term" : "not_found",
         "s1ave_hit" : false
      }
   }
}
```
