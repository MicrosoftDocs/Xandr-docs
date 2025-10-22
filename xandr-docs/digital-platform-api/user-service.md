---
title: Digital Platform API - User Service
description: Explore the User service, enabling member-level users to create, modify, and retrieve information about existing users.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - User service

"User" refers to people or groups able to log in to  or API. Users are classified by a `user_type`, which determines what type of information they have access to. This service allows member-level users to create other users, as well as modify and retrieve information about existing users.

## User types

> [!NOTE]
> Once a user has been created, the `user_type` cannot be changed. To grant someone a new `user_type`, you must create a new user for that person. Also, if you create a user through , the `api_login` field is set to `false` by default (i.e., that user will not have access to the API). You may only change the value of the `api_login` field for a user via the API.

| User Type | Description |
|:---|:---|
| `member` | Network-level user with access to all aspects of the member's account (Advertisers, Publishers, Apps, etc.). |
| `member_advertiser` | Somewhat limited network-level user with access to a subset of advertisers. No API access by Xandr policy. |
| `member_publisher` | Somewhat limited network-level user with access to a subset of publishers. No API access by Xandr policy. |
| `advertiser` | Very limited user with access to one advertiser (mainly for reporting, available in both and API). You must specify an `advertiser_id` when you create this user. |
| `publisher` | Very limited user with access to one publisher (mainly for reporting, available in both and API). You must specify a `publisher_id` when you create this user. |

### Mapping of UI terms to API terms

For more information on UI terms, see documentation for your application.

| UI user role | API `user_type` | Read_only |
|:---|:---|:---|
| Network | `member` | false |
| Network Observer | `member` | true |
| Network Advertiser Manager | `member_advertiser` | false |
| Network Publisher Manager | `member_publisher` | false |
| Advertiser | `advertiser` | false |
| Publisher | `publisher` | false |

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/user](https://api.appnexus.com/user)<br>(user JSON) | Add a new user. |
| `PUT` | [https://api.appnexus.com/user?id=user_id](https://api.appnexus.com/user?id=user_id)<br>(user JSON) | Modify an existing user. |
| `GET` | [https://api.appnexus.com/user](https://api.appnexus.com/user) | View all users associated with this member. |
| `GET` | [https://api.appnexus.com/user?id=user_id](https://api.appnexus.com/user?id=user_id) | View a specific user. |
| `GET` | [https://api.appnexus.com/user?id=1,2,3](https://api.appnexus.com/user?id=1,2,3) | View multiple users by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/user?current](https://api.appnexus.com/user?current) | View the current user. |
| `GET` | [https://api.appnexus.com/user/meta](https://api.appnexus.com/user/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The internal ID associated with the user.<br>**Required On:** `PUT`, in query string. |
| `state` | string | The state of the user. <br>Possible values:<br>- `"active"`<br>- `"inactive"`<br>**Default:** `"active"` |
| `username` | string | The login name of the user.<br>**Required On:** `POST` <br><br>**Note:** The username should not contain any special characters such as $, #, and ". Additionally, after a user is created, the username cannot be changed. |
| `password` | string | The password used to authenticate the user. Not shown on `GET` requests.<br>**Required On:** `POST` |
| `email` | string | The email address of the user.<br>**Required On:** `POST` |
| `first_name` | string | The user's first name.<br>**Required On:** `POST` |
| `last_name` | string | The user's last name.<br>**Required On:** `POST` |
| `custom` data | string | Any information relevant to the user can be entered here. |
| `phone` | string | The user's contact phone number. |
| `user_type` | enum | The type of user. Possible values:<br>- `"member"`<br>- `"bidder"`<br>- `"publisher"`<br>- `"advertiser"`<br>- `"member_advertiser"`<br>- `"member_publisher"`<br><br>For more details on each user type, see [User Types](#user-types) table above.<br>**Required On:** `POST`<br><br>**Note:** This field cannot be modified on `PUT`. To change a user's `user_type`, you must add a new user. |
| `read_only` | boolean | If `true`, the user is not allowed to make changes via the API.<br>**Default:** `false` |
| `api_login` | boolean | **Admin-only.** If `true`, the user can access and use the API.<br>**Default:** `false` |
| `entity_id` | int | The ID of the entity (member or bidder) to which the user belongs. <br><br>**Note:** The `entity_id` is the same as the `member_id`, which is used in other services.<br>**Required On:** `POST` (if `user_type` is `"member"`). |
| `entity_name` | string | The name of the entity (member or bidder) to which the user belongs. |
| `publisher_id` | int | The ID of the publisher with which the user is associated, if `user_type` is `"publisher"`.<br>**Required On:** `POST` (if `user_type` is `"publisher"`). |
| `advertiser_id` | int | The ID of the advertiser with which the user is associated, if `user_type` is `"advertiser"`.<br>**Required On:** `POST` (if `user_type` is `"advertiser"`). |
| `advertiser_access` | array | The advertiser(s) that the user can access, if `user_type` is `"member_advertiser"`.<br>**Required On:** `POST` (if `user_type` is `"member_advertiser"`). |
| `publisher_access` | array | The publisher(s) that the user can access, if `user_type` is `"member_publisher"`.<br>**Required On:** `POST` (if `user_type` is `"member_advertiser"`). |
| `reporting_decimal_type` | enum | The character used for decimals in reporting. <br>Possible values:<br>- `"comma"`<br>- `"decimal"` (period)<br>This setting can be overridden at the report level (see `reporting_decimal_type` in the [Report Service](report-service.md)).<br>**Default:** `reporting_decimal_type` from [member](member-service.md). |
| `decimal_mark` | enum | The character separating the integer part from the fractional part of a number. <br>Possible values:<br>- `"period"`<br>- `"comma"`<br>This character must be different than the character used for `thousand_separator`.<br><br>**Default**: `"period"`<br><br>**Note:** This field controls how the user enters and views numbers in only. It does not affect numbers in the API. |
| `thousand_separator` | enum | The character separating digit groups in a number. Possible values:<br>- `"comma"`<br>- `"space"`<br>- `"period"`<br>This character must be different than the character used for `decimal_mark`.<br><br>**Default:** `"comma"` <br><br>**Note:** This setting controls how the user enters and views digit groups in only. It does not affect digit groups in the API. |
| `send_safety_budget_notifications` | boolean | If `true`, the user will receive email notifications when the daily safety budget threshold is approached. For more details, see the `daily_budget` field on the [Member Service](member-service.md).<br>**Default:** `"false"`  |
| `is_developer` | boolean | **Read-only.** This flag gives a user rights to access certain developer-focused services such as the Plugin and Plugin Instance services, which are used by apps. It is set to `true` by a Xandr admin on a case-by-case basis.<br>**Default:** `"false"`  |
| `last_modified` | timestamp | The date and time when the user was last modified. |
| `timezone` | string | The user's timezone. |
| `password_expires_on` | timestamp | When the user's password expires. |
| `entity_reporting_decimal_type` | enum | Whether number values are separated by a comma or a decimal in reports. If this field is set to `decimal`, the value returned would be formatted like this: `1234.56`. Whereas, if this field is set to `comma`, the value returned would be formatted like this: `1234.56`.<br>Possible values:<br>- `decimal`<br>- `comma`<br>**Default:** `"decimal"` |

## Examples

### Add a network user

```
$ cat user
{
    "user":{
        "username":"testuser",
        "password":"testpassword",
        "user_type":"member",
        "entity_id":123,
        "first_name":"Test",
        "last_name":"User",
        "email":"test@testuser.com"
    }
}
$ curl -b cookies -X POST -d @user 'https://api.appnexus.com/user'
{
    "response":{
        "status":"OK",
        "id":258
    }
}
```

### Add a network observer user

```
$ cat user
{
    "user":{
        "username":"testuser",
        "password":"testpassword",
        "user_type":"member",
        "entity_id":123,
        "first_name":"Test",
        "last_name":"User",
        "email":"test@testuser.com",
        "read_only": true
    }
}
$ curl -b cookies -X POST -d @user 'https://api.appnexus.com/user'
{
    "response":{
        "status":"OK",
        "id":259
    }
}
```

### Add a publisher user

```
$ cat user
{
    "user":{
        "username":"testuser",
        "password":"testpassword",
        "user_type":"publisher",
        "publisher_id":1234,
        "first_name":"Test",
        "last_name":"User",
        "email":"test@testuser.com"
    }
}
$ curl -b cookies -X POST -d @user 'https://api.appnexus.com/user'
{
    "response":{
        "status":"OK",
        "id":260
    }
}
```

### Add an advertiser user

```
$ cat user
{
    "user":{
        "username":"testuser",
        "password":"testpassword",
        "user_type":"advertiser",
        "advertiser_id":1234,
        "first_name":"Test",
        "last_name":"User",
        "email":"test@testuser.com"
    }
}
$ curl -b cookies -X POST -d @user 'https://api.appnexus.com/user'
{
    "response":{
        "status":"OK",
        "id":261
    }
}
```

### View the current user

```
$ curl -b cookies 'https://api.appnexus.com/user?current'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "user": {
            "id": 2513,
            "first_name": "Ron",
            "last_name": "Jacob",
            "phone": "",
            "username": "rjacob",
            "email": "rjacob@example.com",
            "user_type": "member",
            "read_only": false,
            "api_login": true,
            "entity_id": 1446,
            "publisher_id": null,
            "advertiser_id": null,
            "custom_data": null,
            "send_safety_budget_notifications": false,
            "entity_name": "Test Member",
            "timezone": "EST5EDT",
            "entity_reporting_decimal_type": "decimal",
            "reporting_decimal_type": null,
            "decimal_mark": "period",
            "thousand_separator": "comma",
            "last_modified": "2012-06-27 21:53:38",
            "is_developer": false,
            "state": "active",
            "advertiser_access": null,
            "publisher_access": null
        }
    }
}
```
