---
title: Developer Data Service
description: Use the Developer Data service to add data about API objects.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Developer Data service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Developer Data Service is used to add data about API objects. The Developer Data Service is flexible, allowing developers to store anything that might be useful when the user accesses the object again. Some examples of how this service can be used:

- Xandr uses it to store data on users not used by ad serving (e.g., if the user has seen or dismissed certain notifications within).
- Xandr uses it to keep track of certain campaign state as the user is creating a campaign.

To write to the Developer Data Service, you must:

- be a valid and authenticated developer.
- own the object for which you are adding data.
- add data for a unique combination of `object_type` and `object_id` (e.g., you can add only one set of data for profile 1234).
- restrict the data object to 500 characters or less.
- be switched into a user.
  
  > [!NOTE]
  > You cannot write to the service by passing the `developer_id` through the command line or in the object JSON. You must be switched into a user.

The Developer Data Service is only available for the following objects:

- `Creative`
- `Profile`
- `Segment`
- `Member`

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/developer-data` | Add new developer data |
| `PUT` | `https://api.appnexus.com/developer-data` | Modify existing developer data |
| `GET` | `https://api.appnexus.com/developer-data?id=ID`<br><br>`https://api.appnexus.com/developer-data?object_id=OBJECT_ID` | View specific developer data |
| `GET` | `https://api.appnexus.com/developer-data` | View all developer data |
| `DELETE` | `https://api.appnexus.com/developer-data` | Delete developer data |
| `GET` | `https://api.appnexus.com/developer-data/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the developer data object.<br>**Default**: Auto-generated number. |
| `object_id` | int | The ID of the object to which you are adding data.<br>**Required On**: `POST`, `PUT`, `DELETE`<br>**Default**: N/A |
| `object_type` | string | The type of object to which you are adding data. Possible values: <br> - `creative` <br> - `profile` <br> - `segment` <br> - `member` <br><br> **Required On**: `POST`, `PUT`, `DELETE`<br>**Default**: N/A |
| `data` | string | The data being added to the object. Must be formatted as an object.<br>**Default**: N/A<br>**Note**: Must be less than 500 characters. |

> [!NOTE]
> The table below is for Xandr employees.

| Field | Type | Description |
|:---|:---|:---|
| `developer_id` | string | **Admin Only**. The ID of the developer.<br>**Default**: Auto-generated number |

## Examples

### Add new developer data

```
$ cat developer_data
{
        "developer_data": {
                "object_id": 10,
                "object_type": "profile",
                "data": "{\"plugin_ids\":{\"segment\":1}}"
        }
}
$ curl -b cookies -X POST -d @developer_data 'https://api.appnexus.com/developer-data'
{
  "response": {
    "status": "OK",
    "count": 6118352,
    "start_element": 0,
    "num_elements": 1,
    "developer-datas": [
      {
                "id": 1,
                "object_id": 10,
                "object_type": "profile",
                "data": "{\"plugin_ids\":{\"segment\":1}}"
                }
        ]
}
```

### View all developer data

```
$ curl -b cookies 'https://api.appnexus.com/developer-data'
{
  "response": {
    "status": "OK",
    "count": 6118352,
    "start_element": 0,
    "num_elements": 100,
    "developer-datas": [
      {
        "id": 1,
        "object_id": 726837,
        "object_type": "profile",
        "data": {
          "plugin_ids": {
            "segment": "2"
          },
          "usergroup_targeting": null
        }
      },
      {
        "id": 3,
        "object_id": 735066,
        "object_type": "profile",
        "data": {
          "plugin_ids": {
            "segment": "2"
          },
          "usergroup_targeting": null
        }
      },
  ...
    ],
    "dbg_info": {
      "instance": "61.bm-hbapi.prod.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [],
      "time": 5967.670917511,
      "start_microtime": 1437417138.3324,
      "version": "1.15.568",
      "s1ave_miss": "no_service_index",
      "s1ave_lag": 0,
      "member_last_modified_age": 1437417138,
      "output_term": "developer-datas"
    }
  }
}
```

### View specific developer data

```
$ curl -b cookies 'http:api.appnexus.com/developer-data?id=3'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "developer-data": {
      "id": 3,
      "object_id": 735066,
      "object_type": "profile",
      "data": {
        "plugin_ids": {
          "segment": "2"
        },
        "usergroup_targeting": null
      }
    },
    "dbg_info": {
      "instance": "65.bm-hbapi.prod.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [],
      "time": 44.665098190308,
      "start_microtime": 1437418438.3285,
      "version": "1.15.568",
      "s1ave_miss": "no_service_index",
      "s1ave_lag": 0,
      "member_last_modified_age": 1437418438,
      "output_term": "developer-data"
    }
  }
}
```
