---
title: Multi-Buyer Deals API Setup
description: This article provides content to supplement the deal service and deal buyer access service documentation.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Multi-buyer deals API setup

The content of this page is intended to supplement the [Deal Service](./deal-service.md) and [Deal Buyer Access Service](./deal-buyer-access-service.md) documentation.

Multi-buyer deals use a combination of three new objects:

- `buyer_seats` - Array of seat name/IDs of buyers who can target this deal (see [Buyer Seats](#buyer-seats) below)
- `buyer_bidders` - Array of bidder name/IDs of buyers who can target this deal (see [Buyer Bidders](#buyer-bidders) below)
- `buyer_members` - Array of Xandr member name/IDs of buyers who can target this deal (see [Buyer Members](#buyer-members) below)

Multi-buyer deals must be implemented using deal line items (Deals v2). The `buyer_bidders` object is only supported using Deals v2 (even if only one buyer is used). If the `buyer_seats` object is used for multiple buyers (whether in `buyer_seats` or across other buyer objects), it must be implemented with Deals v2.

> [!NOTE]
> Deals v1 can support one buyer seat in the `buyer_seats` object. Additional buyer seats must be implemented using Deals v2 (for more information, see [Create a Simplified Deal Line Item](../monetize/create-a-simplified-deal-line-item.md)).

## JSON fields

The tables below outline the JSON fields required for setting up the Multi-buyer deals API.

For multi-buyer deals, you are required to include at least one of the following JSON fields in a `POST`: `buyer`, `buyer_bidders`, `buyer_members`, or `buyer_seats`. For single-buyer deals, you must include either `buyer` or `buyer_seats` in a `POST`.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `buyer` | object | The buying bidder and member who can target this deal. For single-buyer deals, a deal will only ever use the `buyer` field or the `buyer_seats` field, not both. The `buyer` field is not used in multi-buyer deals. For more details, see [Buyer](#buyer) below. <br>**Required On**: `POST` |
| `buyer _bidders` | object | The buying bidder who can target this deal. For more details, see [Buyer Bidders](#buyer-bidders) below. |
| `buyer _members` | object | The Xandr member ID of the buyer who can target this deal. For more details, see [Buyer Members](#buyer-members) below. |
| `buyer _seats` | object | The seat ID (the unique advertiser ID from their DSP) of the buyer who can target this deal. A deal will only ever use the `buyer` field or the `buyer_seats` field, not both. For more details, see [Buyer Seats](#buyer-seats) below. |

### Buyer

The `buyer` object is not used in multi-buyer deals. The `buyer` object can be set on a `POST`, but cannot be updated with a `PUT`. If you want to change the buyer, you need to create a new deal.

The `buyer` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id`  | int | The member ID of the buyer. <br>**Required On**: `POST` |
| `bidder_id` | int | **Read-only**. The bidder ID of the member. For buyers, this will always be `2`. |
| `name` | string | **Read-only**. The member name of the buyer. |

#### Example of the `buyer` object

```
"buyer": {
                "bidder_id": 2,
                "bidder_name": "",
                "id": 9155,
                "name": "Hearts & Science (AT&T)"
            },
"buyer_seats": null
```

### Buyer bidders

The `buyer_bidders` object is used in multi-buyer deals. The `buyer_bidders` object can be set on a `POST`, and can be updated with a `PUT`. When a seller is enabled for multi-buyer deals, the `buyer_bidders` object can be set in combination with `buyer_seats` and `buyer_members`.

The `buyer_bidders` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_name` | string | **Read-only**. The name of the bidder. |
| `id` | int | The bidder ID of the buyer. The bidder ID is `2`. <br>**Required On**: `POST`  |

#### Example of the `buyer_bidders` object

```
"buyer_bidders": [{
        "bidder_id": 1,
        "bidder_name": "Example Bidder"
}],
```

### Buyer members

The `buyer_members` object is used in multi-buyer deals. The `buyer_members` object can be set on a `POST`, and can be updated with a `PUT`. When a seller is enabled for multi-buyer deals, the `buyer_members` object can be set in combination with `buyer_seats` and `buyer_bidders`.

The `buyer_members` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_id` | int | **Read-only**. The bidder ID of the member. For Microsoft Invest buyers, this will always be `2`. |
| `bidder_name` | string | **Read-only**. The name of the bidder. |
| `id` | int | The member ID of the buyer. <br>**Required On**: `POST` |
| `name` | string | **Read-only**. The member name of the buyer. |

#### Example of the `buyer_members` object

```
"buyer_members": [{
        "bidder_id": 1,
        "bidder_name": "Example Bidder",
        "id": "456",
        "name": "Example Buyer Member"
}],
```

### Buyer seats

The `buyer_seats` object is used in multi-buyer deals. Deals with seats can be set up using the `buyer_seats` object via the API. When setting up a new deal via the API, use the `buyer_seats` object, and the API will be populated with this object.

Use the Microsoft Invest buyer's member ID in the `code` and `bidder_id=2` field. New deals with external DSP's can also be set up with buyer seat IDs. You can check which external DSPs are using buyer seat IDs [here](../monetize/external-dsps-using-buyer-seat-ids.md).

Some things to note:

- For sellers not enabled for multi-buyer deals, a deal can be set up with either `buyer` or `buyer_seats`, where `buyer` is a member, and `buyer_seats` is a seat.
- When a seller has buyer seat deals enabled, all deals with will be set up using `buyer_seats` (when the deal is set up using, deals with the `buyer` field can still be set up using API).
- When the deal is with a single buyer, it can be set up with either `buyer` or `buyer_seats`, where `buyer` is a member, and `buyer_seats` is a seat.
- `Code` is the seat code, in other words, the "seat ID" that the buyer will typically give. Since seat codes are only unique to a given bidder ID, you can expect to see some of the same seat codes across various DSPs. Because seat codes are only unique to a given `bidder_id`, providing a `code` and `bidder_id` are mandatory when creating a new deal.

The `buyer_seats` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_id` | int | The bidder ID of the member. <br>**Required On**: `POST` |
| `bidder_name` | string | The name of the bidder. |
| `code` | string | The identifier for the buyer seat. <br> **Required On**: `POST` |
| `name` | string | The name of buyer seat. |

#### Example of the `buyer_seats` object

```
"buyer": null,
"buyer_seats": [
                {
                    "bidder_id": 2,
                    "bidder_name": "",
                    "code": "9155",
                    "name": "Hearts & Science (AT&T)"
                }
            ],
```

## Multi-buyer deal example

### Add a multi-buyer deal

```
$ cat new_multibuyer_deal.json
   
{
    "deal": {
        "name": "Xandr Test Deal",
        "active": false,
        "start_date": "2020-12-01 00:00:00",
        "end_date": "2020-12-31 23:59:59",
        "buyer_seats": [{
            "code": 958,
            "bidder_id":2
        }],
        "buyer_members": [{
            "id": 1088
        }],
        "buyer_bidders": [{
            "id": 129
        }],
        "version":2
    }
}
 
$ curl -b cookies -c cookies -X POST -d @new_multibuyer_deal.json 'https://api.appnexus.com/deal'
 
{
    "response": {
        "status": "OK",
        "id": 234,
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "active": false,
            "ask_price": 0,
            "auction_type": {
                "id": 2,
                "name": "Standard Price"
            },
            "buyer": null,
            "buyer_bidders": [
                {
                    "bidder_name": "Platform Services Test Bidder",
                    "bidder_supports_hashed_user_ids": true,
                    "guaranteed_deals_support": "Enabled",
                    "id": 129
                }
            ],
            "buyer_members": [
                {
                    "bidder_id": 82,
                    "bidder_name": "The Trade Desk",
                    "bidder_supports_hashed_user_ids": true,
                    "guaranteed_deals_support": "Enabled",
                    "id": 1088,
                    "name": "The Trade Desk, Inc."
                }
            ],
            "buyer_seats": [
                {
                    "bidder_id": 2,
                    "bidder_name": "",
                    "bidder_supports_hashed_user_ids": false,
                    "code": "958",
                    "guaranteed_deals_support": "Enabled",
                    "name": "AppNexus Services Network"
                }
            ],
            "code": null,
            "currency": "USD",
            "description": null,
            "end_date": "2020-12-31 23:59:59",
            "floor_price": 0,
            "id": 123,
            "name": "Xandr Test Deal",
            "package_id": null,
            "payment_type": "default",
            "priority": 5,
            "profile_id": null,
            "seller": {
                "bidder_id": 2,
                "id": 2378,
                "name": "Member 2378"
            },
            "start_date": "2020-12-01 00:00:00",
            "type": {
                "id": 1,
                "name": "Open Auction"
            },
            "use_deal_floor": true,
            "version": 2
        }
    }
}
```
