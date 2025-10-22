---
title: Mobile App Instance Service
description: Use the Mobile App Instance service to retrieve app instances, which can be created via the Mobile App Instance List service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Mobile App Instance service

This **read-only** service is used to retrieve app "instances". Each object retrieved by a call to this service is an "instance" of an app described in the [Mobile App Service](./mobile-app-service.md). App instances can be created via the [Mobile App Instance List Service](./mobile-app-instance-list-service.md).

You can add or remove mobile app instances from your campaign targeting the [Profile Service](./profile-service.md). See the [Examples](#examples) section below.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET`  | `https://api.appnexus.com/mobile-app-instance?id=8` | Retrieve a specific instance of a mobile app |
| `GET` |  `https://api.appnexus.com/mobile-app-instance` | View all of the mobile app instances in our system |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `instance-bundle` | array of objects | The identifying information associated with this particular instance of an app. For details, see [Instance Bundle](#instance-bundle) below. |
| `id` | int | The ID of this app instance. |
| `mobile_app_store_id` | int | The mobile app store this instance is available in. For more information, see the [Mobile App Store Service](./mobile-app-store-service.md). |
| `store.name` | string | The name of the mobile app store this instance of the app is available in. |
| `store.url` | string | The app store URL where this instance of the app can be found. |
| `mobile_app_store` | multi_object | The mobile app store this instance of the app can be found in. |
| `last_modified` | date | When this app instance was last updated in our system. |
| `created_on` | date | When this app instance was created in our system. |

### Instance bundle

| Name | Type | Description |
|:---|:---|:---|
| `bundle_id` | string | The bundle ID associated with this app. |
| `os_family_id` | int | The operating system family ID associated with this app. For details, see the [Operating System Family Service](./operating-system-family-service.md). |
| `last_modified` | date | When this instance's bundle was last updated in our system. |
| `created_on` | date | When this instance's bundle was created in our system. |

## Examples

### Get an existing mobile app instance

You can view an existing mobile app instance with a `GET` call:

```
$ curl -b cookies 'https://api.appnexus.com/mobile-app-instance?id=108
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "mobile-app-instance": {
            "id": 108,
            "last_modified": "2014-01-16 17:08:50",
            "created_on": "2014-01-16 17:08:50",
            "mobile_app_store": "",
            "instance-bundle": [
                {
                    "bundle_id": "3223423",
                    "os_family_id": 3,
                    "instance_priority_id": 1,
                    "last_modified": "2014-01-23 20:42:57",
                    "created_on": "2014-01-16 17:07:24"
                }
            ]
        }
    }
}
```

### Add a mobile app instance to your campaign targeting profile

```
$ cat profile-update.json
 
{
    "profile": {
        "mobile_app_instance_action_include": true,
        "mobile_app_instance_targets": [
            {
                "id": 56
            }
        ]
    }
}
 
$ curl -b cookies -X PUT -d @profile-update.json 'https://api.appnexus.com/profile?id=140537'
 
{
    "response":{
         "profile":{
             "mobile_app_instance_targets":[
                {
                    "deleted":false,
                     "os_family_id":2,
                     "bundle_id":"dsad.com.com",
                     "id":56
                }
            ],
             ...SNIP...
        },
         "num_elements":100,
         "start_element":0,
         "id":"140537",
         "count":1,
         "status":"OK"
    }
}
```

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
- [Mobile App Service](./mobile-app-service.md)
- [Mobile App Store Service](./mobile-app-store-service.md)
- [Mobile App Instance List Service](./mobile-app-instance-list-service.md)
