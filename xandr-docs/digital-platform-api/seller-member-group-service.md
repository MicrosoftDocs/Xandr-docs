---
title: Seller Member Group Service
description: Buyers can use the Seller Member Group service to target seller member groups for access to a wider variety of inventory from newer and smaller publishers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Seller Member Group service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

A seller member group consists of one or more members that sell inventory. Buyers can target seller member groups in addition to individual members to have to access a greater variety of inventory, such as that from newer and smaller publishers.

Only admins can write to this service.  

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/seller-member-group` | View a list of all seller member groups |
| `GET` | `https://api.appnexus.com/seller-member-group?id=SELLER_MEMBER_GROUP_ID` | View a specific seller member group |
| `GET` | `https://api.appnexus.com/seller-member-group?id=1,2,3` | View multiple seller member groups by ID using a comma-separated list |

### Admin-only functions

Only Xandr employees can create, modify, or delete a seller member group.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/seller-member-group` <br>(seller member group JSON) | Add a new seller member group (admin only) |
| `PUT` | `https://api.appnexus.com/seller-member-group?id=SELLER_MEMBER_GROUP_ID` <br>(seller member group JSON) | Modify an existing seller member group (admin only) |
| `DELETE` | `https://api.appnexus.com/seller-member-group?id=SELLER_MEMBER_GROUP_ID` | Delete a seller member group (admin only) |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | Specifies the internal ID associated with the seller member group.<br><br>**Required On**: `PUT`, in query string. |
| `name` | string | Specifies the name of this seller member group.<br><br>**Required On**: `POST` |
| `description` | string | Specifies a description for this seller member group.<br>**Required On**: `POST` |
| `display_order` | int | Specifies the order in which this seller member group should appear in. Default is `5`. |
| `member_count` | int | Specifies the number of members currently in this seller member group. |
| `hidden` | Boolean | Indicates whether or not this seller member group should be hidden in.<br>`0`: (Default) Seller member group will not be hidden in.<br>`1`: Seller member group will be hidden in. |

## Examples

### View all seller member groups

```
$ curl -b cookies 'https://api.appnexus.com/seller-member-group'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "seller-member-groups": [
            {
                "id": 1,
                "name": " supply",
                "description": "Xandr seller member group",
                "display_order": 1,
                "hidden": false,
                "last_modified": "2016-03-08 15:30:02",
                "member_count": 103
            }
        ],
        "dbg_info": {
            "instance": "56.bm-hbapi.prod.lax1",
            "s1ave_hit": false,
            "db": "master",
            "user::reads": 3,
            "user::read_limit": 10000,
            "user::read_limit_seconds": 60,
            "user::writes": 0,
            "user::write_limit": 10000,
            "user::write_limit_seconds": 60,
            "reads": 0,
            "read_limit": 10000,
            "read_limit_seconds": 60,
            "writes": 0,
            "write_limit": 10000,
            "write_limit_seconds": 60,
            "awesomesauce_cache_used": false,
            "count_cache_used": false,
            "warnings": [],
            "time": 702.83794403076,
            "start_microtime": 1457486117.8624,
            "version": "1.16.479",
            "s1ave_miss": "no_s1aves_found",
            "s1ave_lag": 7,
            "member_last_modified_age": 1457486117,
            "output_term": "seller-member-groups"
        }
    }
}
```

### Add a seller member group (admins only)

```
$ cat seller-member-group
{
    "seller-member-group": {
        "name": "My SMG",
        "description": "New seller member group",
        "display_order": 9
    }
}
$ curl -b cookies -X POST -d @seller-member-group 'https://api.appnexus.com/seller-member-group'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 4,
        "start_element": 0,
        "num_elements": 100,
        "seller-member-group": {
            "id": 17,
            "name": "Test SMG",
            "description": "New seller member group",
            "display_order": 9,
            "hidden": false,
            "last_modified": "2016-02-26 23:38:38",
            "member_count": 0
        }
    }
}
```
