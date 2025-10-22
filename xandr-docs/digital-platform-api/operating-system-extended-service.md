---
title: Operating System Extended Service
description: The Operating System Extended service provides a list of specific operating system versions to target in the profile service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Operating System Extended service

This read-only service shows you the list of specific operating system versions that you can target in the [Profile Service](./profile-service.md).

> [!TIP]
> You can also target operating systems as a whole (all versions). To see the operating systems (Android, Apple iOS, Windows 7, etc.) registered in the system, use the [Operating System Family Service](./operating-system-family-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/operating-system-extended` | View all operating systems. |
| `GET` | `https://api.appnexus.com/operating-system-extended?search=SEARCH_TERM` | View all operating systems with IDs or names containing certain characters. |
| `GET` | `https://api.appnexus.com/operating-system-extended?family_id=OS_FAMILY_ID` | View all operating systems within a specific family. |
| `GET` | `https://api.appnexus.com/operating-system-extended?family_name=OS_FAMILY_NAME` | View all operating systems within a specific family. |
| `GET` | `https://api.appnexus.com/operating-system-extended?id=OPERATING_SYSTEM_ID` | View a specific operating system. |
| `GET` | `https://api.appnexus.com/operating-system-extended/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The Xandr ID of the operating system. |
| `family` | object | The operating system family, e.g., `"Android"`, `"Apple iOS"`, `"Apple Mac/OSX"`, etc. See [Family](#family) below, for more details. |
| `last_modified` | date | The date and time when the operating system entry was last modified. |
| `name` | string | The name of the specific operating system version. |

### Family

The `family` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The Xandr ID of the operating system family. |
| `name` | string | The name of the operating system family, e.g., `"Android"`, `"Apple iOS"`, `"Apple Mac/OSX"`, etc. |

## Examples

### View all operating systems

```
$ curl -b cookies -c cookies "https://api.appnexus.com/operating-system-extended"
{
  "response": {
    "status": "OK",
    "count": 87,
    "start_element": 0,
    "num_elements": 100,
    "operating-systems-extended": [
      {
        "id": 15,
        "name": "Android 2.2 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 16,
        "name": "Android 2.2.1 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 17,
        "name": "Android 2.2.2 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 18,
        "name": "Android 2.2.3 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 19,
        "name": "Android 2.3 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 20,
        "name": "Android 2.3.1 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 21,
        "name": "Android 2.3.2 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 22,
        "name": "Android 2.3.3 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 23,
        "name": "Android 2.3.4 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 24,
        "name": "Android 2.3.5 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 25,
        "name": "Android 2.3.6 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
...
      {
        "id": 95,
        "name": "Windows Phone 7",
        "last_modified": "2013-07-17 13:18:07",
        "family": {
          "id": "7",
          "name": "Microsoft Mobile"
        }
      },
      {
        "id": 96,
        "name": "Windows Phone 7.5",
        "last_modified": "2013-07-17 13:18:07",
        "family": {
          "id": "7",
          "name": "Microsoft Mobile"
        }
      },
      {
        "id": 97,
        "name": "Windows Phone 8",
        "last_modified": "2013-07-17 13:18:07",
        "family": {
          "id": "7",
          "name": "Microsoft Mobile"
        }
      },
      {
        "id": 98,
        "name": "Windows Mobile (all)",
        "last_modified": "2013-07-17 13:18:14",
        "family": {
          "id": "7",
          "name": "Microsoft Mobile"
        }
      },
      {
        "id": 99,
        "name": "Linux x64",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      },
      {
        "id": 100,
        "name": "Linux i86",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      },
      {
        "id": 101,
        "name": "Linux arm",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      }
    ],
  }
}
```

### View all operating systems with names containing certain characters

```
$ curl -b cookies -c cookies "https://api.appnexus.com/operating-system-extended?search=and"
{
  "response": {
    "status": "OK",
    "count": 32,
    "start_element": 0,
    "num_elements": 100,
    "operating-systems-extended": [
      {
        "id": 15,
        "name": "Android 2.2 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 16,
        "name": "Android 2.2.1 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 17,
        "name": "Android 2.2.2 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 18,
        "name": "Android 2.2.3 Froyo",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 19,
        "name": "Android 2.3 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 20,
        "name": "Android 2.3.1 Gingerbread",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
...
      {
        "id": 42,
        "name": "Android 4.1.1 Jelly Bean",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 43,
        "name": "Android 4.1.2 Jelly Bean",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 44,
        "name": "Android 4.2 Jelly Bean",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 45,
        "name": "Android 4.2.1 Jelly Bean",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      },
      {
        "id": 46,
        "name": "Android 4.2.2 Jelly Bean",
        "last_modified": "2013-07-17 13:16:44",
        "family": {
          "id": "2",
          "name": "Android"
        }
      }
    ],
  }
}
```

### View all operating systems within a specific family

```
$ curl -b cookies -c cookies "https://api.appnexus.com/operating-system-extended?family_id=8"
{
  "response": {
    "status": "OK",
    "count": 3,
    "start_element": 0,
    "num_elements": 100,
    "operating-systems-extended": [
      {
        "id": 99,
        "name": "Linux x64",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      },
      {
        "id": 100,
        "name": "Linux i86",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      },
      {
        "id": 101,
        "name": "Linux arm",
        "last_modified": "2013-07-17 13:18:28",
        "family": {
          "id": "8",
          "name": "Linux"
        }
      }
    ],
  }
}
```

### View a specific operating system

```
$ curl -b cookies -c cookies "https://api.appnexus.com/operating-system-extended?id=46"
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "operating-system-extended": {
      "id": 46,
      "name": "Android 4.2.2 Jelly Bean",
      "last_modified": "2013-07-17 13:16:44",
      "family": {
        "id": "2",
        "name": "Android"
      }
    },
  }
}
```
