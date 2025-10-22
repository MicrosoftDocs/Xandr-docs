---
title: Digital Platform API - Operating System Service
description: This article provides information on the Operating System service with examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Operating System service

> [!NOTE]
> To retrieve operating system **versions** (Android 3.x, Apple iOS 6, etc.), you should use the [Operating System Extended Service](./operating-system-extended-service.md) instead of this service. To retrieve operating systems as a whole (Android, Windows, Linux, etc.), you should use the [Operating System Family Service](./operating-system-family-service.md).

## REST API

| HTTP Method | Endpoint | Example |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/operating-system` | View all operating systems. |
| `GET` | `https://api.appnexus.com/operating-system?search=SEARCH_TERM` | Search for operating systems with IDs or names containing certain characters. |
| `GET` | `https://api.appnexus.com/operating-system?id=OPERATING_SYSTEM_ID` | View a specific operating system. |
| `GET` | `https://api.appnexus.com/operating-system/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the operating system. |
| `last_modified` | string | The date and time the operating system version entry was last modified. |
| `name` | string | The name of the operating system version. |
| `os_family_id` | int | The ID of the operating system family to which the operating system version belongs. You can use the [Operating System Family Service](./operating-system-family-service.md) to get information about operating system families. |
| `os_family_name` | string | The name of the operating system family to which the operating system version belongs, e.g., `"Android"`, `"Apple iOS"`, `"Apple Mac/OSX"`, etc. |
| `platform_type` | enum | The type of platform on which the operating system version runs. Possible values: <br> - `"web"` <br> - `"mobile"` <br> - `"both"` |

## Examples

### View all operating systems

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/operating-system'
{
  "response": {
    "status": "OK",
    "count": 15,
    "start_element": 0,
    "num_elements": 100,
    "operating-systems": [
      {
        "id": 0,
        "name": "Unknown",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 1,
        "name": "Windows 7",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 2,
        "name": "Windows Vista",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 3,
        "name": "Windows XP",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 4,
        "name": "Windows 2000",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 5,
        "name": "Windows (other versions)",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 6,
        "name": "Android",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 7,
        "name": "Linux",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 8,
        "name": "iPhone",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 9,
        "name": "iPod",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 10,
        "name": "iPad",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 11,
        "name": "Mac",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 12,
        "name": "Blackberry",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 13,
        "name": "Windows Phone 7",
        "platform_type": "mobile",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      },
      {
        "id": 14,
        "name": "Windows 8",
        "platform_type": "web",
        "os_family_id": null,
        "last_modified": "2012-11-28 16:25:01",
        "os_family_name": null
      }
    ],
    "dbg_info": {
      ...
    }
  }
}
```

### View a specific operating system

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/operating-system?id=8'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "operating-system": {
            "id": 8,
            "name": "iPhone - iOS (other versions)",
            "platform_type": "mobile",
            "os_family_id": 3,
            "last_modified": "2013-02-21 21:37:12",
            "os_family_name": "Apple iOS"
        }
    }
}
```
