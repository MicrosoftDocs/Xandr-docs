---
title: Mobile App Service
description: Use the Mobile App service to retrieve audited mobile apps and their associated instances, with mobile apps being the canonical representation.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Mobile App service

This read-only service is used to retrieve **mobile apps that have been audited by Xandr**, as well as their associated instances. For the purposes of this service, a *mobile app* is defined as the canonical representation of an application, while a version of that app designed to run on a particular device (a "port") would be an *instance* of that app. This is analogous to the distinction between a class and an instance of a class.

For example, if `"Happy Pirate Party Pro"` is a mobile app, in order to represent the app, its instances would include the Android version, the iOS version, the Windows Phone version, and any other versions that run as apps on mobile devices.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/mobile-app` | Retrieve all mobile apps registered with the system |
| `GET` | `https://api.appnexus.com/mobile-app?id=4` | Retrieve information about a single mobile app, including its instances |
| `GET` | `https://api.appnexus.com/mobile-app?search="The app name"` | Search for a mobile app |

## JSON fields

| Name | Type (length) | Description |
|:---|:---|:---|
| `created_on` | date | When this object was registered with our system. |
| `id` | int | The unique ID associated with this app. |
| `last_modified` | date | When this object was last updated. |
| `mobile-app-instance` | array of objects | A list of the instances of this app that are registered with our system. This field is returned only when requesting a specific mobile app.<br>For more information about an individual app instance, use the [Mobile App Instance Service](./mobile-app-instance-service.md). |
| `name` | string | The name of the app. |

### Mobile app instance

Each object in the `mobile-app-instance` array contain the following fields, which describe an instance of an app. For more information, see the [Mobile App Instance Service](./mobile-app-instance-service.md) (for reading) and [Mobile App Instance List Service](./mobile-app-instance-list-service.md) (for writing).

| Name | Type | Description |
|:---|:---|:---|
| `created_on` | date | When this instance was created. |
| `id` | int | The ID associated with this instance. |
| `instance-bundle` | array of objects | The identifying information associated with the instance of an app. |
| `last_modified` | date | When this instance was last updated. |
| `mobile_app_store` | array of objects | This wrapper object holds the name, URL, and ID of the app store where this instance of the app is being made available. |

## Examples

### Retrieve all mobile apps registered with the system

```
$ curl -b cookies https://api.appnexus.com/mobile-app
{
    "response": {
        "status": "OK",
        "count": 163,
        "start_element": 0,
        "num_elements": 100,
        "mobile-apps": [
            {
                "id": 1,
                "name": "Best App Ever, no Really",
                "last_modified": "2013-10-24 13:50:32",
                "created_on": "2013-10-24 13:50:32"
            },
            ...
        ],
        ...
        }
}
```

### Retrieve information about a single mobile app, including its instances

In this example, we retrieve information about a single mobile app, including information about its registered instances. You can use the instance ID to get information using the [Mobile App Instance Service](./mobile-app-instance-service.md).

```
$ curl -b cookies https://api.appnexus.com/mobile-app?id=4
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "mobile-app": {
            "id": 4,
            "name": "AutoCreated_958_2i0H2F2d7o9x6k5r4M7l4I1s8r4l4y9",
            "verified": false,
            "last_modified": "2014-02-13 17:07:32",
            "created_on": "2014-02-13 17:07:32",
            "mobile-app-instance": [
                {
                    "id": 4,
                    "last_modified": "2014-02-13 17:07:32",
                    "created_on": "2014-02-13 17:07:32",
                    "mobile_app_store": null,
                    "instance-bundle": [
                        {
                            "bundle_id": "Android, com.king.candycrushsaga",
                            "os_family_id": 2,
                            "instance_priority_id": 1,
                            "last_modified": "2014-02-13 17:07:32",
                            "created_on": "2014-02-13 17:07:32"
                        }
                    ]
                }
            ]
        }
    }
    }
```

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
- [Mobile App Instance Service](./mobile-app-instance-service.md)
- [Mobile App Instance List Service](./mobile-app-instance-list-service.md)
