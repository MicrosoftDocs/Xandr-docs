---
title: Digital Platform API - Operating System Family Service
description: Use the Operating System Family service to view registered operating systems for targeting in profiles, including Android, Apple iOS, and Microsoft Windows.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Operating System Family service

This read-only service lets you see what operating systems (Android, Apple iOS, Microsoft Windows, etc.) are registered in our system. You can use this service to retrieve operating system family IDs for targeting in [profiles](./profile-service.md).

> [!TIP]
> To see the specific **versions** of operating systems (Android 3x, AppleiOS 6, etc.) that you can target, use the [Operating System Extended Service](./operating-system-extended-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/operating-system-family` | View all operating system families. |
| `GET` | `https://api.appnexus.com/operating-system-family?id=OPERATING_SYSTEM_FAMILY_ID` | View a specific operating system family. |
| `GET` | `https://api.appnexus.com/operating-system-family/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the operating system family. |
| `last_modified` | timestamp | The date and time when the operating system family entry was last modified. |
| `name` | string | The name of the operating system family, e.g., `"Android"`, `"Apple iOS"`, `"Apple Mac/OSX"`, etc. |

## Examples

### View all operating system families

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/operating-system-family'
 
{
    "response": {
        "status": "OK",
        "count": 9,
        "start_element": 0,
        "num_elements": 100,
        "operating-system-families": [
            {
                "id": 1,
                "name": "Unknown",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 2,
                "name": "Android",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 3,
                "name": "Apple iOS",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 4,
                "name": "Apple Mac",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 5,
                "name": "Microsoft Windows",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 6,
                "name": "BlackBerry OS",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 7,
                "name": "Microsoft Mobile",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 8,
                "name": "Linux",
                "last_modified": "2013-07-09 18:41:36"
            },
            {
                "id": 9,
                "name": "Symbian OS",
                "last_modified": "2013-11-15 17:07:29"
            }
        ]
    }
}
```

### View a specific operating system family

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/operating-system-family?id=4'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "operating-system-family": {
            "id": 4,
            "name": "Apple Mac",
            "last_modified": "2013-07-09 18:41:36"
        }
    }
}
```
