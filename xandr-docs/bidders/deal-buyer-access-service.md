---
title: Bidders - Deal Buyer Access Service
description: Retrieve exclusive deals using REST API, employ JSON. Gain priority access to pricing, inventory, and opportunities on the platform.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Deal buyer access service

This read-only service lets bidders view information about the negotiated deals they have with sellers on Xandr's platform. A deal may provide a buyer preferential pricing, access to exclusive inventory, reduced competition on inventory, or other opportunities. Each deal is valid for a single buyer, but note that inventory included in a deal may be encompassed by deals with other buyers as well.

## REST API

> [!TIP]
> When logged in with a member user, the following calls will return only deals available to that member. When logged in with a bidder user, the following calls will return deals available to all members or buyer seats under that bidder.

| HTTP Method | Endpoint | Description |
|--|--|--|
| GET | `https://api.adnxs.com/deal-buyer-access` | View all deals you have with sellers. |
| GET | `https://api.adnxs.com/deal-buyer-access?seller_member_id=SELLER_MEMBER_ID` | View all deals you have with a specific seller. |
| GET | `https://api.adnxs.com/deal-buyer-access?id=DEAL_ID` | View a specific deal. |
| GET | `https://api.adnxs.com/deal-buyer-access?id=1,2,3` | View multiple deals by ID using a comma-separated list. |
| GET | `https://api.adnxs.com/deal-buyer-access?search="Deal_ID, DEAL_NAME, or CODE`| Search for a deal by name, ID, or code. |
| GET | `https://api.adnxs.com/deal-buyer-access/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type (Length) | Description |
|---|---|---|
| `active` | boolean | If `true`, the deal is active. Note that the deal will be available only when this field is `true`, `start_date` is in the past (or null), and `end_date` is in the future (or null). |
| `ask_price` | int | The  price associated with the deal. This is the minimum amount the seller will accept for this inventory. |
| `brands` | array of objects | The brands of creatives that are eligible for the deal. For more details, see [Brands](deal-buyer-access-service.md#brands) below. |
| `buyer` | object | The buying bidder and member who can target this deal. For more details, see [Buyer](deal-buyer-access-service.md#buyer) below. |
| `buyer_bidders` | array of objects | The buying bidder who can target this deal. For more details, see [Buyer Bidders](deal-buyer-access-service.md#buyer-bidders) below. |
| `buyer_members` | array of objects | The buying bidder and members who can target this deal. For more details, see [Buyer Members](deal-buyer-access-service.md#buyer-members) below. |
| `buyer_seats` | array of objects | The buying bidder and seats who can target this deal. For more details, see [Buyer Seats](deal-buyer-access-service.md#buyer-seats) below. |
| `code` | string (100) | The custom code for the deal. |
| `currency` | enum | The currency for the `floor_price`. |
| `description` | string (65535) | The description of the deal. |
| `end_date` | timestamp | The day and time when the deal stops being available to the buyer. Null corresponds to "indefinitely". |
| `floor_price` | double | **Deprecated. Please refer to** `ask_price` **instead**. The minimum CPM value that the bidder must bid to be eligible for the deal.<br>**Note**: If `use_deal_floor` is `false`, `floor_price` will be 0. In this case, note that although 0 is shown as the floor price, no deal floor is applied; if the seller has any other floors (in placements or yield management profiles), they will be applied, or if the seller does not have any other floors, the standard second-price auction mechanics will apply. |
| `id` | int | The ID of the deal. This is the field you will receive on the bid request. **Note**: If you set up a deal with an external seller and funnel it through Xandr, we will turn their code into this ID. |
| `last_modified` | timestamp | The date and time when the deal was last modified. |
| `name` | string (255) | The name of the deal. |
| `seller` | object | The selling member who is offering the deal. For more details, see [Seller](deal-buyer-access-service.md#seller) below.|
| `sizes` | array of objects | The sizes of creatives that are eligible for the deal. For more details, see [Sizes](deal-buyer-access-service.md#sizes) below.<br>**Note**: If this array is not present in the response, there are no creative size requirements for the deal.|
| `start_date` | timestamp | The day and time when the deal starts being available to the buyer. Null corresponds to "immediately". |
| `suggested_min_bid_price` | int | The same amount as the `ask_price`.<br>**Note**: Your minimum bid should be higher than the `ask_price` to account for the auction service charges specified in your Xandr contract. For deals with external suppliers, your bid should also include additional margin to account for discrepancies. Bidding the more than the `ask_price` helps ensure that you are eligible for the deal but there is no guarantee that your bid will win. |
| `type` | object | The type of deal. A deal can be an open auction or a private auction. For more details, see [Type](deal-buyer-access-service.md#type) below. |
| `use_deal_floor` | boolean | If `true`, the `floor_price` is applied for the deal.<br>**Note**: When `use_deal_floor` is `true`, the deal's floor price overrides any other floors the seller may have, i.e., in placements or yield management profiles. |

## Seller

The `seller` object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `id` | int | The member ID of the seller. |
| `name` | string | The member name of the seller. |

## Buyer

The buying bidder and member who can target this deal. For a seller who uses single-buyer deals, a deal will only ever use the `buyer` field or the `buyer_seats` field, not both. The `buyer` field supports a single member, not an array.
The `buyer` field is not used by sellers who are enabled for multi-buyer deals. Since multi-buyer deals is still in beta for sellers, you can expect some sellers to continue using the buyer field for single-buyer deals for the time being.  
  
The `buyer` field cannot be updated by the seller. Once a deal is created with a `buyer` field, it will not change.
  
The `buyer` object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `bidder_id` | int | The bidder ID of the member. |
| `id` | int | The member ID of the buyer. |
| `name` | string | The member name of the buyer. |

## Buyer members

The buying bidder and members who can target this deal. For a seller who uses multi-buyer deals, the `buyer_members` object can be set in combination with `buyer_seats` and `buyer_bidders`. They cannot be set in combination with buyer.

The `buyer_members` field is used by sellers who are enabled for multi-buyer deals. It functions like the `buyer` field except for two main differences: `buyer_members` supports an array of objects and can be edited after creation. Multi-buyer deals is still a beta feature so not all sellers will have access to set up deals using `buyer_members`.

A DSP should read this field if they:

- Can accept deals where multiple buyers are eligible: in this case, they should read this field as an array of objects with potentially multiple objects.
- Cannot accept deals where multiple buyers are eligible: read this field as an array of objects with one object. If a DSP cannot accept multiple buyers, they should read this field in the exact same way they read buyer. Even a DSP that has transitioned to seats might see old deals with a legacy member populated here.

The `buyer` object contains the following fields.

| Field | Type | Description |
| --- | --- | --- |
| `bidder_id` | int | The bidder ID of the member. |
| `bidder_name` | string | The name of the bidder. |
| `id` | int | The member ID of the buyer. |
| `name` | string | The member name of the buyer. |

## Buyer seats

The buying bidder and seats who can target this deal. For a seller who uses multi-buyer deals, the `buyer_seats` object can be set in combination with `buyer_members` and `buyer_bidders`. For a seller who uses single-buyer deals, the `buyer_seats` object can be set up on its own. The `buyer_seats` object cannot be set in combination with buyer.
  
All sellers, both ones setting up single buyer and multi-buyer deals, have the ability to set up deals using `buyer_seats`.  
  
A DSP should read this field if they:

- Are transitioned to using [buyer seats](seat-service.md).
  
- Can accept deals where multiple buyers are eligible: in this case, they should read this field as an array of objects with potentially multiple objects.
- Cannot accept deals where multiple buyers are eligible: read this field as an array of objects with one object.

The `buyer_seats` object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `bidder_id` | int | The bidder ID of the member. |
| `bidder_name` | string | The name of the bidder. |
| `id` | int | The member ID of the buyer. |
| `name` | string | The member name of the buyer. |

## Buyer bidders

The buying bidders who can target this deal. For a seller who uses multi-buyer deals, the `buyer_bidders` object can be set in combination with `buyer_seats` and `buyer_members`. They cannot be set in combination with buyer.
  
The `buyer_bidders` field is used by sellers who are enabled for multi-buyer deals. When this seat is used on a deal, all buyers within the DSP are eligible. This field corresponds to a deal being sent with a blank pmp.deals.wseat on the OpenRTB bid request. Multi-buyer deals is still a beta feature so not all sellers will have access to set up deals using `buyer_bidders`.
  
A DSP should read this field if:

- Can accept a deal with a blank `pmp.deals.wseat` on the OpenRTB bid request.

The `buyer_bidders` object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `bidder_name` | string | Read-only. The name of the bidder. |
| `bid` | int | The bidder ID of the member. |

## Type

The `type` object contains the following fields.

| Field | Type | Description |
|---|---|---|
| `id`  | int | The ID representing the type of deal. Possible values:<br> - 1 = Open Auction<br>In an "Open Auction", **buyers targeting the deals and buyers targeting the inventory via other means compete for the impression.** If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction, paying either the second-highest bid or the deal floor price, whichever is higher. If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid or ECP, whichever is higher. <br> - 2 = Private Auction<br>In a "Private Auction", **buyers targeting the private deals compete for the impression first.** Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction, paying either the second-highest bid from the private auction or the deal floor price, whichever is higher. If no private auction deals clear their floors, the highest bid in the open auction wins, paying either the second-highest bid from the open auction or ECP, whichever is higher.<br>For examples showing how these different types of auctions work, see [Deal Auction Mechanics](deal-auction-mechanics.md).  |
| `name` | string | The name of the type of deal. Possible values: "Open Auction", "Private Auction", or "First Look". |

## Brands

Each `brands` object contains the following fields.

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the brand that is eligible for the deal. You can use the [Brand Service](brand-service.md) to retrieve brand IDs. |
| `name` | string | The name of the brand that is eligible for the deal. You can use the [Brand Service](brand-service.md) to retrieve brand names. |

## Sizes

Each object in the `sizes` array contains the following fields.

| Field | Type | Description |
|--|--|--|
| `width` | string | The width of the creative. |
| `height` | string | The height of the creative. |

## Examples

**View all deals you have with sellers**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access'
{ 
    "response": {
        "status": "OK",
        "count": 6,
        "deals": [
            {
                "id": 62,
                "code": null,
                "name": "Private deal for buyer 1085 with floor of 2.5",
                "description": null,
                "active": false,
                "start_date": "2013-12-01 00:00:00",
                "end_date": "2013-12-31 23:59:59",
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2013-12-04 20:15:38",
                "seller": {
                    "id": 1004,
                    "name": "Seller 1004"
                },
                "buyer": {
                    "id": 1005,
                    "bidder_id": 2,
                    "name": "Buyer 1005"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1
                    }
                ],
                                "ask_price": 2.75,
                                "suggested_min_bid_price": 2.75,
                "sizes": [
                    {
                        "width": "300",
                        "height": "250"
                    }
                ],
            },
            {
                "id": 63,
                "code": null,
                "name": "Private deal for buyer 1085 with floor of $2.50",
                "description": null,
                "active": false,
                "start_date": "2013-12-01 00:00:00",
                "end_date": "2013-12-31 23:59:59",
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2013-12-04 20:39:57",
                "seller": {
                    "id": 1006,
                    "name": "Seller 1006"
                },
                "buyer": {
                    "id": 1007,
                    "bidder_id": 2,
                    "name": "Buyer 1007"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1
                    }
                ]
            },
            ...
        ]
    }
}
```

**View all deals you have with a specific seller**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access?seller_member_id=100006'
{
    "response": {
        "status": "OK",
        "count": 1,
        "deals": [
            {
                "id": 63,
                "code": null,
                "name": "Private deal for buyer 1085 with floor of $2.50",
                "description": null,
                "active": false,
                "start_date": "2013-12-01 00:00:00",
                "end_date": "2013-12-31 23:59:59",
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2013-12-04 20:39:57",
                "seller": {
                    "id": 100006,
                    "name": "Seller 456"
                },
                "buyer": {
                    "id": 1007,
                    "bidder_id": 2,
                    "name": "Buyer 1007"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1
                    }
                ],
                                "ask_price": 2.75,
                                "suggested_min_bid_price": 2.75,
            }
        ]
    }
}
```

**View a specific deal**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access?id=63'
{
    "response": {
        "status": "OK",
        "count": 1,
        "deal": 
        "deals": {
            "id": 63,
            "code": null,
            "name": "Private deal for buyer 1085 with floor of $2.50",
            "description": null,
            "active": false,
            "start_date": "2013-12-01 00:00:00",
            "end_date": "2013-12-31 23:59:59",
            "floor_price": 2.5,
            "currency": "USD",
            "use_deal_floor": true,
            "last_modified": "2013-12-04 20:39:57",
            "seller": {
                "id": 100006,
                "name": "Seller 456"
            },
            "buyer": {
                "id": 1007,
                "bidder_id": 2,
                "name": "Buyer 1007"
            },
            "type": {
                "id": 2,
                "name": "Private Auction"
            },
            "brands": [
                {
                    "id": 1
                }
            ],
                        "ask_price": 2.75,
                        "suggested_min_bid_price": 2.75
        }
    }
}
```

**View a specific deal (w/ Seat Code)**

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access?id=689280'
{
        "response": {
                "count": 1,
                "dbg": {
                        "output_term": "deal",
                        "version": "1.18.1370",
                        "warnings": []
                },
                "deal": {
                        "active": false,
                        "adserver_lists": null,
                        "adserver_restrict": false,
                        "allow_creative_add_on_click": true,
                        "allow_creative_add_on_view": false,
                        "allowed_media_subtypes": null,
                        "allowed_media_types": null,
                        "ask_price": 1,
                        "auction_type": {
                                "id": 2,
                                "name": "Standard Price"
                        },
                        "audit_status_option": "none",
                        "bidder_guaranteed_deals_support_id": null,
                        "brand_restrict": false,
                        "brands": null,
                        "buyer": null,
                        "buyer_exposure": {
                                "id": 1,
                                "name": "Single buyer"
                        },
                        "buyer_seats": [{
                                "bidder_id": 100,
                                "bidder_name": "Buyer 100",
                                "bidder_supports_hashed_user_ids": true,
                                "code": "A123D",
                                "guaranteed_deals_support": "Disabled",
                                "name": "buyer seat id deal test"
                        }],
                        "categories": null,
                        "category_restrict": false,
                        "code": null,
                        "created_by": "seller",
                        "creatives": null,
                        "currency": "USD",
                        "data_protected": false,
                        "description": "Test Deal with seller 958",
                        "end_date": "2019-12-31 23:59:59",
                        "external_metadata": null,
                        "id": 689280,
                        "language_restrict": false,
                        "languages": null,
                        "last_modified": "2019-11-13 17:33:40",
                        "media_preference": "standard",
                        "name": "buyer seat test",
                        "package_id": null,
                        "payment_type": "default",
                        "priority": 10,
                        "seller": {
                                "bidder_id": 2,
                                "id": 958,
                                "name": "Member 958"
                        },
                        "size_preference": "standard",
                        "sizes": null,
                        "start_date": "2019-11-11 00:00:00",
                        "suggested_min_bid_price": 1,
                        "technical_attribute_restrict": false,
                        "technical_attributes": null,
                        "type": {
                                "id": 2,
                                "name": "Private Auction"
                        },
                        "use_deal_floor": true,
                        "version": 1,
                        "visibility_profile_id": null
                }
        }
}

```

**View all deals that have not expired**

In this example, assuming today is December 4, 2013, we want to find all deals that have not expired. To do this, we pass the `min_end_date="2013-12-04 00:00:00"` filter in the query string. Please note that however, that deals with no end date will not show up in the response.

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/deal-buyer-access?min_end_date="2013-12-04 00:00:00"'
{
    "response": {
        "status": "OK",
        "count": 4,
        "deals": [
            {
                "id": 60,
                "code": null,
                "name": null,
                "description": null,
                "active": true,
                "start_date": "2013-12-01 00:00:00",
                "end_date": "2013-12-31 23:59:00",
                "floor_price": 3.2,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2013-12-04 18:47:39",
                "seller": {
                    "id": 100006,
                    "name": "Seller 456"
                },
                "buyer": {
                    "id": 1007,
                    "bidder_id": 2,
                    "name": "Buyer 1007"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": null,
                                "ask_price": 3.5,
                                "suggested_min_bid": 3.5
            },
            {
                "id": 62,
                "code": null,
                "name": "Private deal for buyer 1085 with floor of 2.5",
                "description": null,
                "active": false,
                "seller_member_id": 1066,
                "start_date": "2013-12-01 00:00:00",
                "end_date": "2013-12-31 23:59:59",
                "profile_id": null,
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2013-12-04 20:15:38",
                "seller": {
                    "id": 1006,
                    "name": "Seller 1006"
                },
                "buyer": {
                    "id": 1007,
                    "bidder_id": 2,
                    "name": "Buyer 1007"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1
                    }
                ],
                                "ask_price": 3.5,
                                "suggested_min_bid_price": 3.5,
            },
            ...
        ]
    }
}

```
