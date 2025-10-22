---
title: Carrier Netblock Service
description: In this article, learn about the Carrier Netblock service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Carrier Netblock service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This admin-only service can be used to map blocks of IP addresses to internet providers, enabling advertisers with mobile campaigns to target specific internet providers.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/carrier-netblock](https://api.appnexus.com/carrier-netblock)<br>(add_mapping JSON) | Add a new carrier-netblock mapping. |
| `PUT` | [https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID](https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID)<br>(update_mapping JSON) | Modify an existing carrier-netblock mapping. |
| `GET` | [https://api.appnexus.com/carrier-netblock](https://api.appnexus.com/carrier-netblock) | View all carrier-netblock mappings. |
| `GET` | [https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID](https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID) | View a specific carrier-netblock mapping. |
| `DELETE` | [https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID](https://api.appnexus.com/carrier-netblock?id=CARRIER_NETBLOCK_MAPPING_ID) | Delete a carrier-netblock mapping. |
| `GET` | [https://api.appnexus.com/carrier-netblock/meta](https://api.appnexus.com/carrier-netblock/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the carrier-netblock mapping.<br>**Default:** Auto-generated number.<br>**Required On:** `PUT` |
| `carrier_id` | int | The ID of the internet carrier. You can use the [Carrier Service](carrier-service.md) to see the list of available carriers and their ID's.<br>**Required On:** `POST` |
| `start_ip` | int | The IP address at the start of the range of IP addresses you wish to map. This value must be entered as a flattened integer. Convert the IP address using a tool such as [this](https://www.smartconversion.com/unit_conversion/IP_Address_Converter.aspx), in order to get a flattened integer to `POST` or `PUT`.<br>**Required On:** `POST` |
| `end_ip` | int | The IP address at the end of the range of IP addresses you wish to map. Convert the IP address using a tool such as [this](https://www.smartconversion.com/unit_conversion/IP_Address_Converter.aspx), in order to get a flattened integer to `POST` or `PUT`.<br>**Required On:** `POST` |
| `notes` | string | Any notes relevant to the carrier-netblock mapping.<br>**Default:** `null` |
| `last_activity` | date | The date and time on which the carrier-netblock mapping was last modified. |

## Examples

### Add a carrier-netblock mapping

```
$ cat add_mapping

{
        "carrier-netblock": {
             "carrier_id": 26,
             "start_ip": "2886794753",
             "end_ip": "4294967295"                
        }
}
```

```
$ curl -b cookies -c cookies -X POST -d @add_mapping.json "https://api.appnexus.com/carrier-netblock"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 11829,
    "start_element": 0,
    "num_elements": 100,
    "carrier-netblock": {
      "id": 11829,
      "carrier_id": 26,
      "start_ip": 2886794753,
      "end_ip": 4294967295,
      "notes": null,
      "last_activity": "2013-09-12 13:47:04"
    },
  }
}
```

### Update a carrier-netblock mapping

```
$ cat update_mapping

{
        "carrier-netblock": {
             "start_ip": "3221225471",
             "end_ip": "4294967295"               
        }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @update_mapping.json "https://api.appnexus.com/carrier-netblock?id=11829"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": "11829",
    "start_element": 0,
    "num_elements": 100,
    "carrier-netblock": {
      "id": 11829,
      "carrier_id": 26,
      "start_ip": 3221225471,
      "end_ip": 4294967295,
      "notes": null,
      "last_activity": "2013-09-12 14:55:28"
    },
  }
}
```

### View all carrier-netblock mappings

```
$ curl -b cookies -c cookies "https://api.appnexus.com/carrier-netblock"
{
  "response": {
    "status": "OK",
    "count": 6950,
    "start_element": 0,
    "num_elements": 100,
    "carrier-netblocks": [
      {
        "id": 4,
        "carrier_id": 165,
        "start_ip": 3452776960,
        "end_ip": 3452777215,
        "notes": "Seed",
        "last_activity": "2013-08-07 20:49:55"
      },
      {
        "id": 5,
        "carrier_id": 165,
        "start_ip": 3452811776,
        "end_ip": 3452812031,
        "notes": "Seed",
        "last_activity": "2013-08-07 20:49:55"
      },
      {
        "id": 6,
        "carrier_id": 165,
        "start_ip": 3517383936,
        "end_ip": 3517384191,
        "notes": "Seed",
        "last_activity": "2013-08-07 20:49:55"
      },
      {
        "id": 46,
        "carrier_id": 14,
        "start_ip": 68665344,
        "end_ip": 68665351,
        "notes": "Seed",
        "last_activity": "2012-11-27 16:11:25"
      },
      {
        "id": 48,
        "carrier_id": 14,
        "start_ip": 204593600,
        "end_ip": 204593615,
        "notes": "Seed",
        "last_activity": "2012-11-27 16:11:25"
      },
      {
        "id": 51,
        "carrier_id": 14,
        "start_ip": 214464808,
        "end_ip": 214464815,
        "notes": "Seed",
        "last_activity": "2012-11-27 16:11:25"
      },
 ...
      {
        "id": 1219,
        "carrier_id": 151,
        "start_ip": 3582880768,
        "end_ip": 3582885887,
        "notes": "Seed",
        "last_activity": "2013-05-15 15:15:00"
      },
      {
        "id": 1220,
        "carrier_id": 151,
        "start_ip": 3584180736,
        "end_ip": 3584180991,
        "notes": "Seed",
        "last_activity": "2013-05-15 15:15:00"
      },
      {
        "id": 1221,
        "carrier_id": 151,
        "start_ip": 3584181248,
        "end_ip": 3584182015,
        "notes": "Seed",
        "last_activity": "2013-05-15 15:15:00"
      },
      {
        "id": 1252,
        "carrier_id": 199,
        "start_ip": 44040192,
        "end_ip": 45088767,
        "notes": "Seed",
        "last_activity": "2013-05-15 15:18:07"
      },
      {
        "id": 1255,
        "carrier_id": 199,
        "start_ip": 1050537728,
        "end_ip": 1050537731,
        "notes": "Seed",
        "last_activity": "2013-05-15 15:18:07"
      }
    ],
  }
}
```

### View a specific carrier-netblock mapping

```
$ curl -b cookies -c cookies "https://api.appnexus.com/carrier-netblock?id=46"
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "carrier-netblock": {
      "id": 46,
      "carrier_id": 14,
      "start_ip": 68665344,
      "end_ip": 68665351,
      "notes": "Seed",
      "last_activity": "2012-11-27 16:11:25"
    },
  }
}
```
