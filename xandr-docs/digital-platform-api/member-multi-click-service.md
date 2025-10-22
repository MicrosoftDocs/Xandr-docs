---
title: Member Multi Click Service
description: Use the Member Multi Click service to update the common.member_multi_click table.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member Multi Click service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Member Multi Click service is an admin-only service that allows updates to the `common.member_multi_click` table. This table configures members to track multiple clicks for specific cases. Be careful when adding or updating objects when using this service

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/member-multi-click` <br>(template JSON) | Add a new member-multi-click setting |
| `PUT` |  `https://api.appnexus.com/member-multi-click?id=MULTI_CLICK_ID*`<br><br>**Note**: `MULTI_CLICK_ID` is not the `member_id` but a uniquely generated ID for the setting. It can be retrieved via `GET`. <br>(template JSON) | Modify a member-multi-click setting |
| `DELETE` | `https://api.appnexus.com/member-multi-click?id=MULTI_CLICK_ID` | Delete a member-multi-click setting |
| `GET` |  `https://api.appnexus.com/member-multi-click` | View all member-multi-click settings |
| `GET` | `https://api.appnexus.com/member-multi-click?member_id=MEMBER_ID` | View a specific member's multi click setting |
| `GET` | `https://api.appnexus.com/member-multi-click/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the member multi click.<br><br>**Default**: Auto-generated number.<br>**Required On**: `PUT`/`DELETE`, in query string. |
| `member_id` | int | The `member_id` for which to set multiple click tracking.<br><br>**Default**: `None`<br>**Required On**: `POST` |
| `flag` | boolean | Boolean flag to enable/disable multiple click tracking.<br>**Default**: `True` |

## Examples

### View all member-multi-click settings

```
$ curl -b cookies -c cookies 'http:api.appnexus.com/member-multi-click'
{
  "response": {
    "status": "OK",
    "count": 2,
    "start_element": 0,
    "num_elements": 100,
    "member-multi-clicks": [
      {
        "id": 1,
        "member_id": "884",
        "flag": true,
        "last_modified": "2013-10-01 19:29:15",
        "created_on": "2013-10-01 19:29:15"
      },
      {
        "id": 2,
        "member_id": "1631",
        "flag": true,
        "last_modified": "2013-12-04 20:41:32",
        "created_on": "2013-12-04 20:41:32"
      }
    ],
    "dbg_info": {
      "instance": "63.bm-hbapi.prod.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [
      ],
      "time": 41.685104370117,
      "start_microtime": 1421350933.2934,
      "version": "1.15.326",
      "s1ave_miss": "no_service_index",
      "s1ave_lag": 0,
      "member_last_modified_age": 1421350933,
      "output_term": "member-multi-clicks"
    }
  }
}
```

### Add a member-multi-click setting for a member

```
$ cat member-multi-click

{
    "member-multi-click": {
        "member_id": 123,
        "flag": true
    }
}
```

```
$ curl -b cookies -c cookies -X POST -d @member-multi-click 'https://api.appnexus.com/member-multi-click'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "member-multi-click":{
        "id": 3,
        "member_id": "123",
        "flag": true,
        "last_modified": "2015-01-15 19:29:15",
        "created_on": "2013-01-15 19:29:15"
        }
}
```
