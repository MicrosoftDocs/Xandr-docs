---
title: Member Relation Service
description: The Member Relation service is an internal API service for monitoring financial arrangements between members, including clients, partners, buyers, and sellers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Member Relation service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only. This includes both clients and partners, as well as individual buyers and sellers. For example, a buyer member may want to set up a direct clearing relationship with a seller member rather than clearing through our platform.

In addition, the `apply_bid_landscape_priority` field allows sellers who are [Bid Landscape Feed](../log-level-data/bid-landscape-feed.md) clients to see all bids from a specific buyer in their bid landscape feed.

> [!NOTE]
> - The `member_relation` database table, upon which this API service is based, replaces the functionality of the legacy `member_clearing` table. The `member_clearing` table is no longer used.
> - You must go through Sales Ops to set up or edit a direct clear relationship because there is an impact on client billing and contracts. Setting up and/or editing a direct clear relationship without permission from Sales Ops could cause Xandr to get into financial or legal trouble with clients. If Sales Ops has given the green light, then Justin Pines or an IC will make the update.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/member-relation?buyer_member_id=MEMBER_ID` | View all of a member's financial relationships as a buyer with other sellers. |
| `GET` | `https://api.appnexus.com/member-relation?seller_member_id=MEMBER_ID` | View all of a member's financial relationships as a seller with other buyers. |
| `GET` |`https://api.appnexus.com/member-relation?id=1,2,3` | View multiple member relationship objects by ID using a comma-separated list. |
| `GET` | `https://api.appnexus.com/member-relation?member_id=100&id=1` | View a specific member financial relationship:. |
| `PUT` | `https://api.appnexus.com/member-relation?member_id=100&id=1` | Update a specific member financial relationship. |
| `POST` | `https://api.appnexus.com/member-relation?member_id=100` | Create a specific member financial relationship. |
| `GET` | `https://api.appnexus.com/member-relation/meta` | Find out what fields you can filter and sort by. |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | This object's system ID. |
| `buyer_member_id` | int | The member ID of a buyer member which has a relationship with this member.<br><br>**Required On**: `POST` |
| `seller_member_id` | int | The member ID of a seller member which has a relationship with this member.<br><br>**Required On**: `POST` |
| `expose_inventory_sources` | boolean | This field is not used.<br><br>**Default**: `true` |
| `clear_direct` | boolean | Whether Xandr collects cost of media or pays out seller payment for transactions between this buyer-seller pair. More precisely:<br><br> - If `true`, Xandr does not collect cost of media or pay out seller payment for transactions between this buyer-seller pair. Xandr collects only a direct clear fee from the buyer based on the value of `member_contract.direct_clear_fee` for all direct cleared activity in the month.<br><br> - If `false`, Xandr collects cost of media and pays out seller payment for transactions between this buyer-seller pair. Xandr collects either a buyer auction service deduction or fee or a seller deduction on all activity as determined by contracts.<br><br>**Default**: `false` |
| `apply_bid_landscape_priority` | boolean | Whether to include this buyer's bids in the bid landscape feed for the seller. More precisely:<br><br>If `true`, always include the buyer's bids in the bid landscape feed for the seller, even if this buyer's bids were neither in the top 15 nor the winning bid in the auction.<br><br>If `false`, treat the seller's bid landscape as we normally would.<br><br>**Default**: `true` |

## Examples

### View a specific financial relationship

In this example, we view a particular financial relationship by ID.

```
$ curl -b cookies https://api.appnexus.com/member-relation?member_id=100&id=1
{
    "response": {
        "dbg_info": {
            "member_last_modified_age": 1436,
            "s1ave_lag": 0,
            "version": "1.13.8.16",
            "start_microtime": 1358438257.7108,
            "time": 30.287027359009,
            "warnings": [],
            "awesomesauce_cache_used": false,
            "db": "06.mysql.sand-08.nym2",
            "s1ave_hit": true,
            "instance": "11.hbapi.sand-08.nym1"
        },
        "member_relation": {
            "apply_bid_landscape_priority": false,
            "clear_direct": true,
            "expose_inventory_sources": true,
            "seller_member_id": 1,
            "buyer_member_id": 2,
            "id": 1
        },
        "num_elements": "",
        "start_element": "",
        "count": 1,
        "status": "OK"
    }
}
```

### View all of a member's financial relationships where it acts as a buyer (or seller)

In this example, we view all of a member's relationships where it acts as the buyer from other sellers; in order to view all of the relationships wherein it acts as the seller to other buying members, change the parameter to `seller_member_id` instead:

```
$ curl -b cookies https://api.appnexus.com/member-relation?buyer_member_id=100
{
    "response": {
        "dbg_info": {
            "s1ave_miss": "no_service_index",
            "version": "1.13.13",
            "start_microtime": 1360770598.1499,
            "time": 22.953033447266,
            "warnings": [],
            "awesomesauce_cache_used": false,
            "db": "master",
            "s1ave_hit": false,
            "instance": "30.bm-hbapi.prod.nym1"
        },
        "member_relations": [
            {
                "apply_bid_landscape_priority": false,
                "clear_direct": true,
                "expose_inventory_sources": true,
                "seller_member_id": 72,
                "buyer_member_id": 100,
                "id": 4
            }
        ],
        "num_elements": "",
        "start_element": "",
        "count": 1,
        "status": "OK"
    }
}
```

### Update a specific member relationship object

```
$ cat update-member-relation.json

{
    "member_relation": {
        "expose_inventory_sources": false
    }
}
```

```
$ curl -b cookies -X PUT "https://api.appnexus.com/member-relation?member_id=1309&id=1"
{
    "response": {
        "dbg_info": {
            "master_time": 417.2089099884,
            "proxy": true,
            "master_instance": "05.hbapi.sand-08.lax1",
            "version": "1.13.8.17",
            "start_microtime": 1358958675.3114,
            "time": 762.11285591125,
            "warnings": [],
            "awesomesauce_cache_used": false,
            "parent_dbg_info": {
                "version": "1.13.8.17",
                "start_microtime": 1358958675.4393,
                "time": 417.2089099884,
                "warnings": [],
                "awesomesauce_cache_used": false,
                "db": "master",
                "s1ave_hit": false,
                "instance": "05.hbapi.sand-08.lax1"
            },
            "db": "master",
            "s1ave_hit": false,
            "instance": "10.hbapi.sand-08.nym1"
        },
        "member_relation": {
            "apply_bid_landscape_priority": false,
            "clear_direct": true,
            "expose_inventory_sources": false,
            "seller_member_id": 1,
            "buyer_member_id": 2,
            "id": 1
        },
        "num_elements": "",
        "start_element": "",
        "id": "1",
        "count": 1,
        "status": "OK"
    }
}
```

### Create a new member relationship object

```
$ cat new-member-relation.json

{
    "member_relation": {
        "expose_inventory_sources": true,
        "seller_member_id": 1308,
        "buyer_member_id": 1309,
        "clear_direct": true
    }
}
```

```
$ curl -b cookies -X POST -d @new-member-relation.json "https://api.appnexus.com/member-relation?member_id=1309"
{
    "response": {
        "dbg_info": {
            "master_time": 391.0858631134,
            "proxy": true,
            "master_instance": "05.hbapi.sand-08.lax1",
            "version": "1.13.8.17",
            "start_microtime": 1358963519.9095,
            "time": 556.19502067566,
            "warnings": [],
            "awesomesauce_cache_used": false,
            "parent_dbg_info": {
                "version": "1.13.8.17",
                "start_microtime": 1358963520.0377,
                "time": 391.0858631134,
                "warnings": [],
                "awesomesauce_cache_used": false,
                "db": "master",
                "s1ave_hit": false,
                "instance": "05.hbapi.sand-08.lax1"
            },
            "db": "master",
            "s1ave_hit": false,
            "instance": "11.hbapi.sand-08.nym1"
        },
        "member_relation": {
            "apply_bid_landscape_priority": false,
            "clear_direct": true,
            "expose_inventory_sources": true,
            "seller_member_id": 1312,
            "buyer_member_id": 1309,
            "id": 65
        },
        "num_elements": "",
        "start_element": "",
        "id": "65",
        "count": 1,
        "status": "OK"
    }
    }
```
