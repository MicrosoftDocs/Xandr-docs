---
title: Terms Service
description: Use the Terms Service to record Tango member's acceptance of the Tango usage terms of service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Terms service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This service is used to record Tango member's acceptance of the Tango usage terms of service. Although this service was created to support a current Tango need, it may be used in the future for other terms of service needs.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/terms-of-service`<br>(`add_TOS` JSON) | Add a new terms of service acceptance record. |
| `GET` | `https://api.appnexus.com/terms-of-service` | View all terms of service records. |
| `GET` | `https://api.appnexus.com/terms-of-service?id=TERMS_OF_SERVICE_ID` | View a specific terms of service record. |
| `GET` | `https://api.appnexus.com/terms-of-service/meta` | Find out which fields you can filter and sort by. |

> [!NOTE]
> The calls below are visible to Xandr Employees only. These calls can only be made my administrators.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `PUT` | `https://api.appnexus.com/terms-of-service?id=TERMS_OF_SERVICE_ID`<br>(`modify_TOS` JSON) | Modify a terms of service record. |
| `DELETE` | `https://api.appnexus.com/terms-of-service?id=TERMS_OF_SERVICE_ID` | Delete a terms of service record. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the terms of service record.<br><br>**Default**: Auto-generated number |
| `user_id` | int | The ID of the user that has accepted the terms of service.<br><br>**Default**: `null`<br>**Required On**: `POST` |
| `terms_name` | string | The name of the terms of service that were accepted. Currently this should only be Tango related terms of service.<br><br>**Required On**: `POST` |
| `date_accepted` | date | The date the terms of service were accepted.<br><br>**Required On**: `POST` |
| `last_modified` | string | The date the record was last modified. |

## Examples

### Add a record of accepted terms of service

```
$ cat add_TOS
{
 "terms_of_service":
  {
    "user_id" : 1066,
    "terms_name" : "Test Terms",
    "date_accepted" : "2013-01-16 00:10:00"
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @add_TOS.json "https://api.appnexus.com/terms-of-service"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 19,
    "terms_of_service": {
      "id": 19,
      "user_id": 1066,
      "terms_name": "Test Terms",
      "date_accepted": "2013-01-16 00:10:00",
      "last_modified": "2013-10-09 15:43:53"
    },
  }
}
```

### View all terms of service records

```
$ curl -b cookies -c cookies "http://sand.api.appnexus.com/terms-of-service"
{
  "response": {
    "status": "OK",
    "count": 8,
    "terms_of_services": [
      {
        "id": 1,
        "user_id": 3920,
        "terms_name": "",
        "date_accepted": "0000-00-00 00:00:00",
        "last_modified": "2013-10-01 21:31:45"
      },
      {
        "id": 5,
        "user_id": 3920,
        "terms_name": "\"hey\"",
        "date_accepted": "2013-10-02 00:00:00",
        "last_modified": "2013-10-01 21:35:10"
      },
      {
        "id": 6,
        "user_id": 3920,
        "terms_name": "v1",
        "date_accepted": "0000-00-00 00:00:00",
        "last_modified": "2013-10-01 22:20:44"
      },
      {
        "id": 11,
        "user_id": 3920,
        "terms_name": "\"v1\"",
        "date_accepted": "0000-00-00 00:00:00",
        "last_modified": "2013-10-01 22:37:09"
      },
      {
        "id": 16,
        "user_id": 5870,
        "terms_name": "hey",
        "date_accepted": "2013-10-01 00:00:00",
        "last_modified": "2013-10-03 19:11:34"
      },
      {
        "id": 17,
        "user_id": 5870,
        "terms_name": "v1",
        "date_accepted": "2013-10-01 00:00:00",
        "last_modified": "2013-10-03 19:19:12"
      },
      {
        "id": 18,
        "user_id": 5870,
        "terms_name": "v0",
        "date_accepted": "2013-10-03 17:10:40",
        "last_modified": "2013-10-04 00:22:40"
      },
      {
        "id": 19,
        "user_id": 1066,
        "terms_name": "Test Terms",
        "date_accepted": "2013-01-16 00:10:00",
        "last_modified": "2013-10-09 15:43:53"
      }
    ],
  }
}
```

### View a specific terms of service record

```
$ curl -b cookies -c cookies "https://api.appnexus.com/terms-of-service?id=19"
{
  "response": {
    "status": "OK",
    "count": 1,
    "terms_of_service": {
      "id": 19,
      "user_id": 1066,
      "terms_name": "Test Terms",
      "date_accepted": "2013-01-16 00:10:00",
      "last_modified": "2013-10-09 15:43:53"
    },
  }
}
```

> [!NOTE]
> The examples below are visible to Xandr employees only. These calls can only be made my administrators.
>
> ### Modify a terms of service record
>
> ```
> $ cat modify_TOS
> {
>  "terms_of_service":
>   {
>     "terms_name" : "Usage Terms of Service"
>   }
> }
> $ curl -b cookies -c cookies -X PUT -d @modify_TOS.json "https://api.appnexus.com/terms-of-service?id=19"
> {
>   "response": {
>     "status": "OK",
>     "count": 1,
>     "id": 19,
>     "terms_of_service": {
>       "id": 19,
>       "user_id": 1066,
>       "terms_name": "Usage Terms of Service",
>       "date_accepted": "2013-01-16 00:10:00",
>       "last_modified": "2013-10-09 15:43:53"
>     },
>   }
> }
> ```
> 
> ### Delete a terms of service record
>
> ```
> $ curl -b cookies -c cookies -X DELETE "https://api.appnexus.com/terms-of-service?id=19"
> {
>   "response": {
>     "status": "OK",
>     "count": 1,
>   }
> }
> ```
