---
title: Mobile App Store Service
description: Use the Mobile App Store service to see all of the mobile app stores that are registered in the system.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Mobile App Store service

The Mobile App Store Service is a **read-only** service that you can use to see all of the mobile app stores that are registered in our system.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/mobile-app-store?id=3` | View a single app store |
| `GET` | `https://api.appnexus.com/mobile-app-store` | View all of your app stores registered in our system |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the app store. |
| `last_modified` | date | When this app store description was last updated in our system. |
| `name` | string | The name of the app store. |
| `os_family_id` | int | The operating system family ID of the operating system that uses this app store. |
| `os_family_name` | string | The operating system family name of the OS that uses this app store. |
| `url` | string | The URL associated with the app store. |

## Example

### See all the app stores registered in our system

You can see all of the app stores registered in our system with a single `GET` request:

```
$ curl -b cookies https://api.appnexus.com/mobile-app-store
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "mobile-app-stores": [
            {
                "id": 1,
                "name": "Android",
                "url": "https://play.google.com",
                "last_modified": "2013-10-24 13:50:20",
                "os_family_id": 1,
                "os_family_name": "Unknown"
            }
        ],
            ...
    }
}
```

## Related topics

- [Mobile App Instance Service](./mobile-app-instance-service.md)
- [Mobile App Instance List Service](./mobile-app-instance-list-service.md)
- [Mobile App Service](./mobile-app-service.md)
- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
