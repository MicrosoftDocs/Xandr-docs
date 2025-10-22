---
title: Config Platform Service
description: In this article, learn about the Config Platform service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Config Platform service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

Config Platform is an admin-only service to update very specific multi-bid settings for bidder members (stored in the `common.config_platform` table). Be very careful when adding or updating objects using this service.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/config-platform`<br>(config JSON) | Add a new config-platform setting. |
| `PUT` | `https://api.appnexus.com/config-platform?id=CONFIG_PLATFORM_ID`<br>(config_update JSON)<br><br>**Note:** `CONFIG_PLATFORM_ID` is a uniquely generated ID for the config platform setting and can be retrieved via `GET`. | Modify a config-platform setting. |
| `GET` | `https://api.appnexus.com/config-platform` | View all config-platform settings. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the config platform setting.<br>**Default:** Auto-generated number.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `key` | varchar(256) | The key value used by adserver.<br>**Required On:** `POST` |
| `value` | varchar(16834) | The value for the given key.<br>**Required On:** `POST` |
| `application` | varchar(256) | The application using the setting. Only `"impbus"` is supported currently.<br>**Required On:** `POST` |
| `json_value_type` | enum | The type of the given value. Possible values: `"string"`, `"array"`, `"numeric"`, or `"boolean"`.<br>**Required On:** `POST` |

## Examples

### View all `config-platform` settings

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/config-platform'
{
  "response": {
    "status": "OK",
    "count": 5,
    "start_element": 0,
    "num_elements": 100,
    "config-platforms": [
      {
        "id": 1,
        "key": "admarket_scale_pct",
        "value": "75",
        "instance": null,
        "application": "impbus",
        "depend": 0,
        "variation": null,
        "json_value_type": "numeric",
        "last_modified": "2013-02-18 13:57:02"
      },
      {
        "id": 2,
        "key": "threepe_bidder_id",
        "value": "55",
        "instance": null,
        "application": "impbus",
        "depend": 1,
        "variation": null,
        "json_value_type": "numeric",
        "last_modified": "2014-10-02 21:38:53"
      },
      {
        "id": 3,
        "key": "rmx_max_num_bids",
        "value": "5",
        "instance": null,
        "application": "impbus",
        "depend": 1,
        "variation": null,
        "json_value_type": "numeric",
        "last_modified": "2013-08-08 12:53:06"
      },
        ...
        ]
  }
}
```

### Modify a `config-platform` setting

```
$ cat config_platform_update

{
    "config-platform": {
        "value": 7
}
```

```
$ curl -b cookies -c cookies -X PUT -d @template_update 'https://api.appnexus.com/config-platform?id=3'
{
  "response": {
    "status": "OK",
    "count": 5,
    "start_element": 0,
    "num_elements": 100,
    "config-platform": {
        "id": 3,
        "key": "rmx_max_num_bids",
        "value": "7",
        "instance": null,
        "application": "impbus",
        "depend": 1,
        "variation": null,
        "json_value_type": "numeric",
        "last_modified": "2015-01-15 12:53:06"
        }
  }
  }
```
