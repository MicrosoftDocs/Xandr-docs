---
title: ASI Member Settings Service
description: In this article, find information on the ASI Member Setting service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# ASI Member Settings service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The ASI Member Setting is an admin-only service that allows users to add entries to the `api.asi_member_settings` table. This table is consumed by adserver and contains configuration settings for ASI members. Please be careful when modifying objects using this service.

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `POST` | `https://api.appnexus.com/asi-member-setting` <br> (asi_member_setting JSON) | Add a new ASI member setting |
| `PUT` | `https://api.appnexus.com/asi-member-setting?member_id=MEMBER_ID` <br> (asi_member_setting_update JSON) | Modify an ASI member setting |
| `GET` | `https://api.appnexus.com/asi-member-setting` | View all ASI member settings |
| `GET` | `https://api.appnexus.com/asi-member-setting?member_id=MEMBER_ID` | View a specific ASI member setting |
| `GET` | `https://api.appnexus.com/asi-member-setting/meta` | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type (Length) | Description |
|---|---|---|
| `member_id` | int | The ID of the ASI member. <br> **Required On**: `POST/PUT` |
| `use_second_price` | boolean | Setting to use second price auctions. <br> **Default**: `false` |
| `allow_cookieless` | boolean | Flag to indicate whether the ASI Member is enabled to send cookieless traffic. <br> **Default**: `false` |
| `append_pubclick` | boolean | Sets the append_pubclick field in the database. <br> **Default**: `false` |

## Examples

### View a specific ASI Member Setting

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/asi-member-setting?member_id=280'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "asi-member-settings": [
      {
        "member_id": 280,
        "use_second_price": true,
        "allow_cookieless": true,
        "append_pubclick": false,
        "last_activity": "2015-01-08 15:06:39"
      }
    ],
    "dbg_info": {
      "instance": "62.bm-hbapi.prod.nym2",
      "s1ave_hit": true,
      "db": "227.bm-mysql.prod.nym2",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [
      ],
      "time": 46.911001205444,
      "start_microtime": 1421274164.9374,
      "version": "1.15.329",
      "s1ave_lag": 0,
      "member_last_modified_age": 544565,
      "output_term": "asi-member-settings"
    }
  }
}
```

### Modify an ASI Member Setting

```
$ cat asi_member_setting_update

{
    "asi-member-setting": {
        "use_second_price":true
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @asi_member_setting_update 'https://api.appnexus.com/asi-member-setting?id=280'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "asi-member-settings": [
      {
        "member_id": 280,
        "use_second_price": false,
        "allow_cookieless": true,
        "append_pubclick": false,
        "last_activity": "2015-01-08 15:06:39"
      }
    ],
    "dbg_info": {
      "instance": "62.bm-hbapi.prod.nym2",
      "s1ave_hit": true,
      "db": "227.bm-mysql.prod.nym2",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [
      ],
      "time": 46.911001205444,
      "start_microtime": 1421274164.9374,
      "version": "1.15.329",
      "s1ave_lag": 0,
      "member_last_modified_age": 544565,
      "output_term": "asi-member-settings"
    }
  }
  }
```
