---
title: Sld Use Subdomain Service
description: The SLD Use Subdomain service allows users to add rows to the api.sld_use_subdomain table for tracking subdomains.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# SLD Use Subdomain service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Second Level Domain (SLD) Use Subdomain service is an admin-only service that allows users to add rows to the `api.sld_use_subdomain` table. This table is consumed by adserver to let them know for which second level domains they should track subdomains. Be careful when adding or updating objects using this service.

> [!WARNING]
> #iq-engineering must confirm all new entries to this service. DO NOT post new entries without confirmation.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` |`https://api.appnexus.com/sld-use-subdomain`<br>(template JSON) | Add a new entry to sld-use-subdomain. |
| `PUT` |  `https://api.appnexus.com/sld-use-subdomain?id=SETTING_ID`<br>(template JSON)<br><br>**Note**: `SETTING_ID` is an automatically generated value for the specific table and can be retrieved via `GET`.<br> | Modify an entry in sld-use-subdomain. |
| `DELETE` | `https://api.appnexus.com/sld-use-subdomain?id=SETTING_ID` | Delete an entry in sld-use-subdomain. |
| `GET` | `https://api.appnexus.com/sld-use-sudbomain?id=SETTING_ID` | View a specific entry in sld-use-sudbomain. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the sld-use-subomain record.<br><br>**Default**: Auto-generated number.<br>**Required On**: `PUT`/`DELETE`, in query string |
| `secondary_level_domain` | string(100) | The domain for which to track `secondary_level_domains`.<br><br>**Default**: `None`<br>**Required On**: `POST` |
| `active` | boolean | Whether the record is active or not.<br><br>**Default**: `true` |

## Examples

### View all `sld-use-subdomains`

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/sld-use-subdomain'
{
  "response": {
    "status": "OK",
    "count": 66,
    "start_element": 0,
    "num_elements": 100,
    "sld-use-subdomains": [
      {
        "id": 1,
        "secondary_level_domain": "co.uk",
        "active": true,
        "last_activity": "2010-07-27 20:40:17"
      },
      {
        "id": 2,
        "secondary_level_domain": "live.com",
        "active": true,
        "last_activity": "2011-02-04 14:59:47"
      },
      {
        "id": 3,
        "secondary_level_domain": "msn.com",
        "active": true,
        "last_activity": "2011-03-02 20:23:00"
      },
      {
        "id": 4,
        "secondary_level_domain": "mtv.com",
        "active": true,
        "last_activity": "2011-04-26 13:50:01"
      },
      {
        "id": 5,
        "secondary_level_domain": "live.ca",
        "active": true,
        "last_activity": "2011-06-09 18:17:22"
      },
        ...
        ]
}
```

### Add a new `sld-use-subdomain`

```
$ cat sld-use-subdomain

{
    "sld-use-subdomain": {
        "secondary_level_domain": "newdomain.com",
        "active": true
    }
}
```

```
$ curl -b cookies -c cookies -X POST -d @sld-use-subdomain 'https://api.appnexus.com/sld-use-subdomain'
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 73,
    "start_element": 0,
    "num_elements": 100,
    "sld-use-subdomain": {
      "id": 73,
      "secondary_level_domain": "newdomain.com",
      "active": true,
      "last_activity": "2015-01-14 22:05:02"
    },
    "dbg_info": {
      "instance": "10.hbapi.sand-08.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [
      ],
      "time": 2493.2899475098,
      "start_microtime": 1421273101.3622,
      "version": "1.15.327",
      "s1ave_lag": 0,
      "member_last_modified_age": 1421273101,
      "output_term": "sld-use-subdomain"
    }
  }
}
```

### Modify a `sld-use-subdomain`

```
$ cat sld-use-subdomain
 
{
    "sld-use-subdomain": {
        "secondary_level_domain": "newdomain.com",
        "active": true
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @template_update 'https://api.appnexus.com/template?id=73'
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 73,
    "start_element": 0,
    "num_elements": 100,
    "sld-use-subdomain": {
      "id": 73,
      "secondary_level_domain": "newdomain.com",
      "active": false,
      "last_activity": "2015-01-14 22:05:02"
    },
    "dbg_info": {
      "instance": "10.hbapi.sand-08.nym2",
      "s1ave_hit": false,
      "db": "master",
      "awesomesauce_cache_used": false,
      "count_cache_used": false,
      "warnings": [
      ],
      "time": 2493.2899475098,
      "start_microtime": 1421273101.3622,
      "version": "1.15.327",
      "s1ave_lag": 0,
      "member_last_modified_age": 1421273101,
      "output_term": "sld-use-subdomain"
    }
  }
}
```
