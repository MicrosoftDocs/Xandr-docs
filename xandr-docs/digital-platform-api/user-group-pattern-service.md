---
title: User Group Pattern Service
description: Explore the User Group Pattern service, allowing you to segment a hypothetical audience into five distinct buckets.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# User Group Pattern service

The User Group Pattern Service allows you to divide a hypothetical audience into up to five discrete buckets, each bucket defined to cover a percentage of total users. The most common use case for doing this is defining user groups for A/B testing of campaign targeting strategies. For more information, see [Test and Control Targeting](../monetize/test-and-control-targeting.md) in documentation.

> [!NOTE]
> It is important to note that a pattern does not perform any actual targeting; it simply helps you calculate user group targeting values that you can manually apply to your campaign profiles.

Here's the general process:

1. You create a JSON file that defines your pattern.
1. You make the `POST` request shown below.
1. The response includes `usergroup_target` values for your pattern. You update the relevant profiles with these values. For more details, see `user_group_targets` in the [Profile Service](profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/usergroup-pattern?id=USER_GROUP_PATTERN_ID](https://api.appnexus.com/usergroup-pattern?id=USER_GROUP_PATTERN_ID) | View a specific user group pattern. |
| `GET` | [https://api.appnexus.com/usergroup-pattern](https://api.appnexus.com/usergroup-pattern) | View all of your user group patterns. |
| `POST` | [https://api.appnexus.com/usergroup-pattern](https://api.appnexus.com/usergroup-pattern) | Add a new user group pattern. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `cookieless` | boolean | If `true`, the first user group in the `groups` array will be set to include cookieless users. By default, this is set to `false` because you cannot track clicks or conversions for cookieless users and, therefore, cannot test performance on them.<br>**Required On:** `POST` <br>**Default:** `false` |
| `groups` | array of objects | The user groups in the pattern. No more than five groups can be included. For more details, see [Groups](#groups) below.<br>**Required On:** `POST` |
| `id` | int | The ID of the user group pattern. |
| `last_modified` | timestamp | The date on which the user group pattern was last modified. |
| `member_id` | in | The member to which the user group pattern belongs.<br>**Required On:** `POST` |
| `name` | string (255) | The name of the user group pattern.<br>**Required On:** `POST` |

### Groups

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the user group. |
| `name` | string | The name of the user group.<br>**Required On:** `POST` |
| `percent` | int | The percent of users that this group will target. The total for all user groups must add up to 100%.<br>**Required On:** `POST` |
| `usergroup_target` | object | This object is returned on `POST` and `GET` and specifies the information that you would use in the `user_group_targets` array of a [profile](profile-service.md). For formatting, see the [example](#examples) below. |

## Examples

### Add a new user group pattern

```
$ cat pattern
{
    "usergroup-pattern": {
        "name": "Test pattern",
        "member_id": 1066,
        "cookieless": false,
        "groups": [
            {
                "name": "Group 1",
                "percent": 25
            },
            {
                "name": "Group 2",
                "percent": 25
            },
            {
                "name": "Group 3",
                "percent": 25
            },
            {
                "name": "Group 4",
                "percent": 25
            }
        ]
    }
}
$ curl -b cookies -c cookies -X POST -d @pattern 'https://api.appnexus.com/usergroup-pattern'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 43,
        "start_element": 0,
        "num_elements": 100,
        "usergroup-pattern": {
            "id": 43,
            "member_id": 1066,
            "name": "Test pattern",
            "cookieless": false,
            "groups": [
                {
                    "id": 1,
                    "name": "Group 1",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 0,
                                "high": 24
                            }
                        ]
                    }
                },
                {
                    "id": 2,
                    "name": "Group 2",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 25,
                                "high": 49
                            }
                        ]
                    }
                },
                {
                    "id": 3,
                    "name": "Group 3",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 50,
                                "high": 74
                            }
                        ]
                    }
                },
                {
                    "id": 4,
                    "name": "Group 4",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 75,
                                "high": 99
                            }
                        ]
                    }
                }
            ],
            "last_modified": "2011-12-13 20:18:02"
        }
    }
}
```

### View user group pattern 43

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/usergroup-pattern?id=40'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "usergroup-pattern": {
            "id": 43,
            "member_id": 1066,
            "name": "Test pattern",
            "cookieless": false,
            "groups": [
                {
                    "id": 1,
                    "name": "Group 1",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 0,
                                "high": 24
                            }
                        ]
                    }
                },
                {
                    "id": 2,
                    "name": "Group 2",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 25,
                                "high": 49
                            }
                        ]
                    }
                },
                {
                    "id": 3,
                    "name": "Group 3",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 50,
                                "high": 74
                            }
                        ]
                    }
                },
                {
                    "id": 4,
                    "name": "Group 4",
                    "percent": 25,
                    "usergroup_target": {
                        "include_cookieless_users": false,
                        "groups": [
                            {
                                "low": 75,
                                "high": 99
                            }
                        ]
                    }
                }
            ],
            "last_modified": "2011-12-13 20:18:02"
        }
    }
}
```
