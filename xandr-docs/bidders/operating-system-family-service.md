---
title: Bidders - Operating System Family Service
description: In this article, learn about bidders operating system family service, their JSON fields, and REST API with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Operating system family service

This read-only service lets you see what operating systems (Android, Apple iOS, Microsoft Windows, etc.) are registered in the Xandr system. You can use this service to retrieve operating system family IDs for targeting in [Profiles](../digital-platform-api/profile-service.md).

> [!TIP]
> To see the specific **versions** of operating systems (Android 3x, Apple iOS 6, etc.) that you can target, use the [Operating System Extended Service](../digital-platform-api/operating-system-extended-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/operating-system-family](https://api.adnxs.com/operating-system-family) | View all operating system families. |
| `GET` | [https://api.adnxs.com/operating-system-family?id=OPERATING_SYSTEM_FAMILY_ID](https://api.adnxs.com/operating-system-family?id=OPERATING_SYSTEM_FAMILY_ID) | View a specific operating system family. |
| `GET` | [https://api.adnxs.com/operating-system-family/meta](https://api.adnxs.com/operating-system-family/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the operating system family. |
| `last_modified` | timestamp | The date and time when the operating system family entry was last modified. |
| `name` | string | The name of the operating system family, e.g., "Android", "Apple iOS", "Apple Mac/OSX", etc. |

## Examples

### View all operating system families

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/operating-system-family'
 
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
        ],
        "dbg_info": {
            ...
        }
    }
}
```

### View a specific operating system family

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/operating-system-family?id=4'
 
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
        },
        "dbg_info": {
            ...
        }
    }
}
```

## Related topic

[Legacy Bidder Profile Service](legacy-bidder-profile-service.md)
