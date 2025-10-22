---
title: Yield Management Auction Tier Service
description: Explore the Yield Management Auction Tier service, allowing you to modify the standard auction mechanics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Yield Management Auction Tier service

The Yield Management Auction Tier Service allows you to modify the standard auction mechanics such that certain bids will be considered before others, provided that those bids are associated with certain members and meet particular pricing requirements. You may also use this service to exclude certain members from consideration altogether.

> [!NOTE]
> Auction tiers must be associated with an existing [Yield Management Profile](yield-management-profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/ym-auction-tier](https://api.appnexus.com/ym-auction-tier)<br>(auction-tier JSON) | Add an auction tier. |
| `PUT` | [https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID](https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID)<br>(auction-tier JSON) | Modify an auction tier. |
| `GET` | [https://api.appnexus.com/ym-auction-tier](https://api.appnexus.com/ym-auction-tier) | View all of your auction tiers. |
| `GET` | [https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID](https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID) | View a specific auction tier. |
| `GET` | [https://api.appnexus.com/ym-auction-tier?id=1,2,3](https://api.appnexus.com/ym-auction-tier?id=1,2,3) | View multiple auction tiers by ID using a comma-separated list. |
| `DELETE` | [https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID](https://api.appnexus.com/ym-auction-tier?id=AUCTION_TIER_ID) | Delete an auction tier. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identifier for this auction tier.<br>Default: Auto-generated number.<br>**Required On:** `PUT`, in query string. |
| `name` | string | The name of this tier.<br>**Required On:** `POST` |
| `code` | string | An optional custom code that you can use to map between this object's identifier in your system and in ours.<br>**Default:** `null` |
| `description` | string | An optional description. |
| `profile_id` | int | An optional `profile_id` is used to determine when to apply a tier. A profile is a generic set of rules for targeting inventory, and certain tiers may only apply to certain slices of inventory. For details, see the [Profile Service](profile-service.md).<br>**Default:** `null` |
| `priority` | int | You'll rank each auction tier from `1` to `10` in ascending priority. Those with higher priorities are checked first for a match. If two tiers happen to match the bid in question, and their priorities are equal, the winner is chosen at random.<br>**Default:** `5` |
| `ym_profile_id` | int | An auction tier is associated with a [Yield Management Profile](yield-management-profile-service.md). This is that profile's identifier.<br>**Required On:** `POST` |
| `min_price` | decimal | The minimum price that must be bid by the members in the `buyer_members` array for inclusion in this tier. This can be `null` if the `member_action` is set to `"exclude"`.<br><br>**Note:** Whether a buyer has met the value of `min_price` is checked *after* AppNexus' revenue sharing fee has been removed; in other words, `min_price` is checked against their net bid. For example, if you've set `min_price` to `$2.00`, and the buyer bids `$2.00`, their net bid may be reduced to `$1.70`. This would mean they do not qualify for the tier. The solution is for buyers to take into account their revenue sharing agreement with AppNexus when submitting bids for inclusion in tiers.<br><br>**Default:** `null` |
| `member_action` | enum | This setting determines what action is to be taken against the `buyer_members` array. Permissible values are `"include"` and `"exclude"`.<br>**Default:** `exclude` |
| `member_id` | int | This is your member ID. |
| `buyer_members` | array of objects | This array includes the buyers you're targeting for inclusion or exclusion in this Auction Tier. For details, see the [Buyer Members Array](#buyer-members-array) below.<br>**Default:** `null` |

### Buyer members array

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the member you're targeting for inclusion or exclusion. |
| `name` | string | The name of the member you're targeting for inclusion or exclusion. |

## Examples

### View all of your auction tiers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/ym-auction-tier'

{
    "response": {
        "status": "OK",
        "count": 328,
        "start_element": null,
        "num_elements": null,
        "ym-auction-tiers": [
            {
                "id": 1,
                "name": "Buyer 1 Tier",
                "code": null,
                "description": null,
                "profile_id": null,
                "priority": 10,
                "ym_profile_id": 2785,
                "min_price": "3.000000",
                "member_action": "include",
                "member_id": 752,
                "buyer_members": [
                    {
                        "id": 1094,
                        "name": "Buyer 1"
                    }
                ]
            },
            {
                "id": 2,
                "name": "Buyer 2 Tier",
                "code": null,
                "description": null,
                "profile_id": null,
                "priority": 10,
                "ym_profile_id": 2785,
                "min_price": "4.000000",
                "member_action": "include",
                "member_id": 752,
                "buyer_members": [
                    {
                        "id": 232,
                        "name": "Buyer 2"
                    }
                ]
            },
            {
                "id": 3,
                "name": "Buyer 3 Tier",
                "code": null,
                "description": null,
                "profile_id": null,
                "priority": 10,
                "ym_profile_id": 2785,
                "min_price": "2.500000",
                "member_action": "include",
                "member_id": 752,
                "buyer_members": [
                    {
                        "id": 903,
                        "name": "Buyer 3"
                    }
                ]
            },
            ...
        ]
    }
}
```

### Add an auction tier - Exclude a member

We must include our `{{member_id}}` and the `{{ym_profile_id}}` we'd like to associate this tier with.

```
$ cat add-tier.json
{
    "ym-auction-tier": {
        "member_id": 67890,
        "ym_profile_id": 271828,
        "description": "Bidder 9 from Outer Space has advanced alien bidding technology. They must be stopped!",
        "name": "Exclude Bidder 9 from Outer Space",
        "member_action": "exclude",
        "priority": 10,
        "min_price": null,
        "buyer_members": [
        {
            "id": 12345,
            "name": "Bidder 9 from Outer Space"
        }
        ]
     }
}

$ curl -b cookies -X POST -d @update.json "https://api.appnexus.com/ym-auction-tier"
{
 "response": {
  "id": 1105,
  "ym-auction-tier": {
   "profile_id": null,
   "code": null,
   "id": 5813,
   "description": "Bidder 9 from Outer Space has advanced alien bidding technology. They must be stopped!",
   "name": "Exclude Bidder 9 from Outer Space",
   "member_id": 67890,
   "member_action": "exclude",
   "priority": 10,
   "buyer_members": [{"id":12345,"name":"Bidder 9 from Outer Space"}],
   "ym_profile_id": 271828,
   "min_price": null
  },
  "status": "OK",
  "start_element": null,
  "count": 1,
  "num_elements": null
 }
}
```

### Add an auction tier - Include a member

Notice that this member must meet an extremely high `{{min_price}}` in order for this tier to apply. Since we haven't specified a `{{priority}}`, it defaults to `5`.

```
$ cat add-tier.json
{
    "ym-auction-tier": {
    "ym_profile_id": 456,
    "name": "A High Bar for Member 12 to clear",
    "member_id":123,
    "member_action": "include",
        "min_price": "314159.00",
        "buyer_members": [
        {
        "id": 12,
        "name": "Member 12"
        }
    ]
    }
}



$ curl -b cookies -X POST -d @add-tier.json "https://api.appnexus.com/ym-auction-tier"
{
 "response": {
  "id": 1110,
  "ym-auction-tier": {
   "profile_id": null,
   "code": null,
   "id": 1110,
   "description": null,
   "name": "A high bar for Member 12 to clear",
   "member_id": 123,
   "member_action": "include",
   "priority": 5,
   "buyer_members": [
    {
     "id": 12,
     "name": "Member 12"
    }
   ],
   "ym_profile_id": 456,
   "min_price": "314159.000000"
  },
  "status": "OK",
  "start_element": null,
  "count": 1,
  "num_elements": null
 }
}
```

### Update an auction tier

We've modified our financial arrangement with Member 19, and we'd like them to bid a minimum $1.25 CPM in order to remain in their current Auction Tier.

```
$ cat update.json
{
    "ym-auction-tier": {
    "id": 001,
    "member_id": 19,
        "min_price": "1.25"
    }
}

$ curl -b cookies -X PUT -d @update.json "https://api.appnexus.com/ym-auction-tier?id=001"
{
 "response": {
  "id": 001,
  "ym-auction-tier": {
   "profile_id": null,
   "code": null,
   "id": 001,
   "description": null,
   "name": "Member 19's Tier",
   "member_id": 19,
   "member_action": "include",
   "priority": 7,
   "buyer_members": [
    {
     "id": 19,
     "name": "Member 19"
    }
   ],
   "ym_profile_id": 002,
   "min_price": "1.25"
  },
  "status": "OK",
  "start_element": null,
  "count": 1,
  "num_elements": null
 }
}
```

### Delete an auction tier

```
$ curl -b cookies -X DELETE "https://api.appnexus.com/ym-auction-tier?id=003"
{
 "response": {
  
  "status": "OK"
 }
}
```
