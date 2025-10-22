---
title: Member DC Setting Service
description: Use the Member Datacenter Setting service to add entries to the api.member_dc_setting table.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member DC Setting service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

Member Datacenter Setting is an admin-only service that allows users to add entries to the `api.member_dc_setting` table. This table is consumed by impression bus and used to configure datacenter-specific settings for bidder members. Be careful when modifying objects using this service.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/member-dc-setting` <br>(`datacenter_setting` JSON) | Add a new Member Datacenter Setting |
| `PUT` | `https://api.appnexus.com/member-dc-setting?id=DATACENTER_SETTING_ID` <br>(`datacenter_setting_update` JSON)<br><br>**Note**: The `DATACENTER_SETTING_ID` is a uniquely generated ID in the table; it's not the same as `member_id`. This value can be retrieved via `GET`. | Modify a Member Datacenter Setting |
| `DELETE` | `https://api.appnexus.com/member-dc-setting?id=DATACENTER_SETTING_ID` | Delete a Member Datacenter Setting. |
| `GET` | `https://api.appnexus.com/member-dc-setting` | View all Member Datacenter Settings. |
| `GET` | `https://api.appnexus.com/member-dc-setting?member_id=MEMBER_ID` | View a specific member's Datacenter Setting. |
| `GET` | `https://api.appnexus.com/member-dc-setting/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the member datacenter setting.<br><br>**Default**: Auto-generated number.<br>**Required On**: `PUT`/`DELETE`, in query string. |
| `member_id` | int | The ID of the bidder member.<br><br>**Required On**: `POST` |
| `datacenter` | object | Object containing the ID of the datacenter for the specific setting (to see a list of datacenters, use the Datacenter Service).<br><br>**Default**: `null` |
| `default_auction_timeout_ms` |  | The default auction timeout for the bidder member. Can be up to 350.<br><br>**Default**: `null` |
| `throttle_pct` | decimal(5,2) | The throttle percentage for the member. Can be between 0 and 100 percent.<br><br>**Default**: `null` |

## Examples

### View a specific member's DC setting

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/member-dc-setting?member_id=280'
{
  "response": {
    "status": "OK",
    "count": 3,
    "start_element": 0,
    "num_elements": 100,
    "member-dc-settings": [
      {
        "id": 31,
        "member_id": 280,
        "default_auction_timeout_ms": 350,
        "throttle_pct": null,
        "last_modified": "2014-08-29 02:30:13",
        "datacenter": {
          "id": 7,
          "name": "fra1"
        }
      },
      {
        "id": 28,
        "member_id": 280,
        "default_auction_timeout_ms": 350,
        "throttle_pct": null,
        "last_modified": "2014-08-01 03:37:50",
        "datacenter": {
          "id": 8,
          "name": "sin1"
        }
      },
      {
        "id": 32,
        "member_id": 280,
        "default_auction_timeout_ms": 350,
        "throttle_pct": null,
        "last_modified": "2014-08-01 03:38:03",
        "datacenter": {
          "id": 12,
          "name": "ams3"
        }
      }
    ]
  }
}
```

### Add a member datacenter setting

```
$ cat member_dc_setting

{
    "member-dc-setting": {
        "member_id":123,
        "default_auction_timeout_ms":100,
        "datacenter":{
            "id":7
        }
    }
}
```

```
$ curl -b cookies -c cookies -X POST -d @template 'https://api.appnexus.com/member-dc-setting'
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "member-dc-settings": [
      {
        "id": 401,
        "member_id": 123,
        "default_auction_timeout_ms": 100,
        "throttle_pct": null,
        "last_modified": "2015-01-15 02:30:13",
        "datacenter": {
          "id": 7,
          "name": "fra1"
        }
      }
    ]
  }
}
```
