---
title: Mobile App Instance List Service
description: The Mobile App Instance List service provides a list of mobile app instances for campaigns that can be used to create new mobile apps in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Mobile App Instance List service

The Mobile App Instance List Service is used to define a list of [mobile app instances](./mobile-app-instance-service.md) that you can target with campaigns. Think of it as the mobile app version of the [Domain List Service](./domain-list-service.md).

Remember that a mobile app instance is a concrete representation of the "mobile app" abstraction. For example, there will be multiple "instances" of an application for each platform it targets, such as Android or iOS. For more information about this distinction, see the [Mobile App Service](./mobile-app-service.md).

This service also has the side effect of creating mobile apps in the system if they don't already exist. These apps can then be viewed using the [Mobile App Service](./mobile-app-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/mobile-app-instance-list?id=4` | View a single mobile app instance list. |
| `POST` | `https://api.appnexus.com/mobile-app-instance-list` <br>(mobile app instance list JSON) | Add a mobile app instance list to the system. |
| `GET` | `https://api.appnexus.com/mobile-app-instance-list` | View all of your mobile app instance lists. |
| `GET` | `https://api.appnexus.com/mobile-app-instance-list?search=SEARCH_TERM` | Search for mobile app instances with names or descriptions containing certain characters. |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `apps` | array of objects | A list of app instances associated with this particular app ID. |
| `id` | int | The ID of this instance list. |
| `name` | string | The name of this instance list.<br>**Required On**: `POST` |
| `description` | string | An optional description of this instance list. |
| `member_id` | int | The member ID associated with this app instance list. |
| `last_modified` | date | When this app instance list was last updated. |
| `created_on` | date | When this app instance list was created. |

### Apps

| Name | Type | Description |
|:---|:---|:---|
| `instance_id` | int | The instance ID associated with this app instance. |
| `bundle_id` | string | The bundle ID associated with this app instance.<br>**Required On**: `POST` |
| `os_family_id` | int | The OS family ID associated with this app instance. For a complete listing of OS family IDs, see the [Operating System Family Service](./operating-system-family-service.md). |
| `last_modified` | date | When this app instance was last updated. |

## Examples

### Add a mobile app instance list to the system

In this example, we add a small mobile app instance list to the system with a `POST` call.

```
$ cat the-list.json
 
{
    "mobile-app-instance-list": {
        "name": "A Series of Unfortunate Apps",
        "description": "Mobile games which we'd like to exclude from our campaigns due to their complete lack of smurfiness.",
        "apps": [
            {
                "bundle_id": "com.unfortunate.screamfest",
                "os_family_id": 2
            },
            {
                "bundle_id": "com.unfortunate.eggsmash",
                "os_family_id": 2
            }
        ]
    }
}
 
$ curl -b cookies -c cookies -X POST -d @the-list.json https://api.appnexus.com/mobile-app-instance-list?member_id=1309
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 77,
        "start_element": 0,
        "num_elements": 100,
        "mobile-app-instance-list": {
            "id": 77,
            "name": "A Series of Unfortunate Apps",
            "description": "Mobile games which we'd like to exclude from our campaigns due to their complete lack of smurfiness.",
            "member_id": 1309,
            "last_modified": "2014-02-04 20:39:03",
            "created_on": "2014-02-04 20:39:03",
            "apps": [
                {
                    "instance_id": 220,
                    "last_modified": "2014-02-04 20:39:03",
                    "bundle_id": "com.unfortunate.screamfest",
                    "os_family_id": 2
                },
                {
                    "instance_id": 221,
                    "last_modified": "2014-02-04 20:39:03",
                    "bundle_id": "com.unfortunate.eggsmash",
                    "os_family_id": 2
                }
            ]
        },
        ... 
    }
}
```

### View an existing mobile app instance list

A simple `GET` request with the object ID in the query string fetches the object.

```
$ curl -b cookies https://api.appnexus.com/mobile-app-instance-list?id=77
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "mobile-app-instance-list": {
            "id": 77,
            "name": "A Series of Unfortunate Apps",
            "description": "Mobile games which we'd like to exclude from our campaigns due to their complete lack of smurfiness.",
            "member_id": 1309,
            "last_modified": "2014-02-04 20:39:03",
            "created_on": "2014-02-04 20:39:03",
            "apps": [
                {
                    "instance_id": 220,
                    "last_modified": "2014-02-04 20:39:03",
                    "bundle_id": "com.unfortunate.screamfest",
                    "os_family_id": 2
                },
                {
                    "instance_id": 221,
                    "last_modified": "2014-02-04 20:39:03",
                    "bundle_id": "com.unfortunate.eggsmash",
                    "os_family_id": 2
                }
            ]
        },
    ...
    }
}
```

### Add a mobile app instance list to your targeting profile

In this example, we add a fictional mobile app instance list to our targeting profile for use by campaigns. The profile object we get back should reflect the update. For more information about profiles, see the [Profile Service](./profile-service.md).

```
$ cat update.json
 
{
    "profile": {
        "mobile_app_instance_list_targets": [
            {
                "id": 2
            }
        ],
        "mobile_app_instance_list_action_include": true
    }
}
 
$ curl -b cookies -X PUT -d @update.json 'https://api.appnexus.com/profile?id=140537'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "140537",
        "start_element": 0,
        "num_elements": 100,
        "profile": {
            "mobile_app_instance_targets": "",
            "mobile_app_instance_list_targets": [
                {
                    "id": 2,
                    "name": "Angry List",
                    "description": "List of games that will be played by everyone",
                    "deleted": false
                }
            ],
        ...SNIP...
        }
    }
}
```

### Searching for mobile app instance lists with names or descriptions containing `"test"`

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/mobile-app-instance-list?search=test'
 
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "mobile-app-instance-lists": [{
                "id": 31,
                "name": "Sample Test IPHONE list",
                "description": "",
                "member_id": 927,
                "last_modified": "2014-02-24 18:55:57",
                "created_on": "2014-02-24 18:45:57",
                "apps": [{
                        "instance_id": 2,
                        "last_modified": "2014-02-24 18:55:57",
                        "bundle_id": "it.studios.fish",
                        "os_family_id": 3
                    },
                    {
                        "instance_id": 14576,
                        "last_modified": "2014-02-24 18:55:57",
                        "bundle_id": "587033035",
                        "os_family_id": 3
                    },
                    {
                        "instance_id": 14576,
                        "last_modified": "2014-02-24 18:55:57",
                        "bundle_id": "com.cshomegrown.LX-Player",
                        "os_family_id": 3
                    },
                    {
                        "instance_id": 14576,
                        "last_modified": "2014-02-24 18:55:57",
                        "bundle_id": "561921433",
                        "os_family_id": 3
                    }
                ],
                "num_apps": 4
            },
            {
                "id": 61,
                "name": "test",
                "description": "test APP 428312806",
                "member_id": 2350,
                "last_modified": "2014-03-13 13:13:55",
                "created_on": "2014-03-13 13:13:55",
                "apps": [{
                        "instance_id": 225,
                        "last_modified": "2014-03-13 13:13:55",
                        "bundle_id": "com.wordfeud.free",
                        "os_family_id": 3
                    },
                    {
                        "instance_id": 225,
                        "last_modified": "2014-03-13 13:13:55",
                        "bundle_id": "428312806",
                        "os_family_id": 3
                    }
                ],
                "num_apps": 2
            }
        ]
    }
}
```

## Related topics

- [Mobile App Instance Service](./mobile-app-instance-service.md)
- [Mobile App Service](./mobile-app-service.md)
- [Mobile App Store Service](./mobile-app-store-service.md)
- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
