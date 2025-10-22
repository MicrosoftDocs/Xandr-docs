---
title: Digital Platform API - Deal Buyer Access Service
description: The Deal Buyer Access service allows buyers to view negotiated deals with UI sellers and external supply partners for preferential pricing, exclusive inventory, and reduced competition. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Deal Buyer Access service

This read-only service lets buyers view information about the negotiated deals they have with Xandr's UI sellers and external supply partners. A deal may provide a buyer preferential pricing, access to exclusive inventory, reduced competition on inventory, or other opportunities. Each deal is valid for a single buyer, but note that inventory included in a deal may be encompassed by deals with other buyers as well.

Buyers can use the `deal_targets` field in the [Profile Service](./profile-service.md) to target deals. Sellers can use the [Deal Service](./deal-service.md) to set up and manage deals.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/deal-buyer-access` | View all deals you have with sellers |
| `GET` | `https://api.appnexus.com/deal-buyer-access?seller_member_id=SELLER_MEMBER_ID`  | View all deals you have with a specific seller |
| `GET` | `https://api.appnexus.com/deal-buyer-access?id=DEAL_ID`  | View a specific deal |
| `GET` | `https://api.appnexus.com/deal-buyer-access?id=1,2,3` | View multiple deals by ID using a comma-separated list |
| `GET` | `https://api.adnxs.com/deal-buyer-access?search="Deal_ID,DEAL_NAME,orCODE"`  | Search for a deal by name, ID, or code |
| `GET` | `https://api.appnexus.com/deal-buyer-access/meta`  | Find out which fields you can filter and sort by |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `active` | boolean | If `true`, the deal is active. Note that the deal will be available to the buyer only when this field is `true`, `start_date` is in the past (or `null`), and `end_date` is in the future (or `null`). |
| `ask_price` | int | The  price associated with the deal. This is the minimum amount the seller will accept for this inventory. |
| `audit_status_option` | string | Specifies how the deal handles creatives.<br> - `none`: Creatives use existing ad quality settings.<br> - `provisional`: Creatives in `"pending"` audit status will serve. Once these creatives are audited, the existing ad quality settings are used.<br> - `max_trust`: Any creative is allowed to serve for this deal.<br>Creatives specifically listed in the [Creatives](#creatives) object will override these settings. |
| `brands` | array of objects | The brands of creatives that are eligible for the deal. For more details, see [Brands](#brands) below. |
| `brand_restrict` | Boolean | Specifies whether the deal is restricted only to the brands listed in the [Brands](#brands) object.<br> - `true`: Deal is restricted only to the listed brands.<br> - `false`: Other brands are also allowed to serve. |
| `buyer` | object | The buying member who can target this deal. For more details, see [Buyer](#buyer) below. |
| `categories` | array of objects | The categories that describe the creatives that are eligible for the deal. For more details, see [Categories](#categories) below. |
| `category_restrict` | Boolean | Specifies whether the deal is restricted only to the categories listed in the [Categories](#categories) object.<br>- `true`: Deal is restricted only to the listed categories.<br>- `false`: Other categories are also allowed to serve. |
| `code` | string (100) | The custom code for the deal. For deals with external supply partners, this is generally the string that you will use to identify the deal. |
| `creatives` | array of objects | A list of creatives that are specifically approved or banned for the deal. This list overrides any other ad quality setting. For more details, see [Creatives](#creatives) below. |
| `currency` | enum | The currency for the `floor_price`. For a full list of available currencies, use the read-only [Currency Service](./currency-service.md).  |
| `description` | string (65535) | The description of the deal. For deals with external supply partners, the description may provide additional insight or details about the deal. |
| `end_date` | timestamp | The day and time when the deal stops being available to the buyer. Null corresponds to "indefinitely". |
| `floor_price` | double | **Deprecated**. Refer to the `ask_price` field instead. The minimum CPM value that the buyer must bid to be eligible for the deal.<br><br>**Note**:<br>If `use_deal_floor` is `false`, `floor_price` will be `0`. In this case, note that although `0` is shown as the floor price, no deal floor is applied; if the seller has any other floors (in placements or yield management profiles), they will be applied, or if the seller does not have any other floors, the standard second-price auction mechanics will apply. |
| `id` | int | The ID of the deal. |
| `languages` | array of objects | The language associated with creatives that are eligible for the deal. For more details, see [Languages](#languages) below. |
| `language_restrict` | Boolean | Specifies whether the deal is restricted only to the languages listed in the [Languages](#languages) object.<br>- `true`: Deal is restricted only to the listed languages.<br>- `false`: Other languages are also allowed to serve. |
| `last_modified` | timestamp | The date and time when the deal was last modified. |
| `name` | string (255) | The name of the deal. |
| `payment_type` | string | Specifies the payment type for the deal:<br><br>- `default`: This deal uses the default payment type for the buyer of this deal. Includes CPM and may also include CPA, CPC, or both.<br>- `cpvm`: This deal uses the Viewable CPM payment type. Only viewable impressions result in payment from the buyer. |
| `seller` | object | The selling member who is offering the deal. For more details, see [Seller](#seller) below. |
| `sizes` | array of objects | The sizes of creatives that are eligible for the deal. For more details, see [Size Targets](#sizes) below.<br><br>**Note**: If this array is not present in the response, there are no creative size requirements for the deal. |
| `size_preference` | string | Specifies how this deal handles private sizes. Private sizes are placement sizes that a seller can allow to serve for a deal. There are two options:<br> - `standard`: Private sizes are not available for this deal.<br> - `append`: Private sizes can be used in addition to the specified placement size. |
| `start_date` | timestamp | The day and time when the deal starts being available to the buyer. Null corresponds to "immediately". |
| `suggested_min_bid_price` | int | The minimum amount that will likely clear the ask price. This is the sum of the `ask_price` and the auction service charge specified in your Xandr contract. For deals with external suppliers, this amount will include additional margin to account for discrepancies.<br>Bidding the `suggested_min_bid_price` helps ensure that you are eligible for the deal but there is no guarantee that your bid will win. |
| `technical_attributes` | array of objects | The technical attributes of creatives that are eligible for the deal. For more details, see [Technical Attributes](#technical-attributes) below. |
| `technical_attribute_restrict` | Boolean | Specifies whether the deal is restricted only to the technical attributes listed in the [Technical Attributes](#technical-attributes) object.<br> - `true`: Deal is restricted only to the listed technical attributes.<br>- `false`: Other technical attributes are also allowed to serve. |
| `type` | object | The type of deal. For sellers, a deal can be an open auction or a private auction. For external supply partners, a deal can also be first-look access. For more details, see [Type](#type) below. |
| `use_deal_floor` | Boolean | If true, the `floor_price` is applied for the deal.<br><br>**Note**:<br>When `use_deal_floor` is `true`, the deal's floor price overrides any other floors the seller may have, i.e., in placements or yield management profiles. |

### Seller

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | **Read-only**. The member ID of the seller. |
| `name` | string | **Read-only**. The member name of the seller. |

### Buyer

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The member ID of the buyer. |
| `bidder_id` | int | The bidder ID of the member. For Xandr's UI buyers, this will always be 2. |
| `name` | string | The member name of the buyer. |

### Type

The `Type` object contains the following fields.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID representing the type of deal. Possible values:<br>`1` = Open Auction<br>In an `"Open Auction"`, **buyers targeting the deals and buyers targeting the inventory via other means compete for the impression**. If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction, paying either the second-highest bid or the deal floor price, whichever is higher. If one of the non-deal buyers submits the highest bid, that buyer wins the auction, paying either the second-highest bid or ECP, whichever is higher. <br><br>`2` = Private Auction<br>In a `"Private Auction"`, **buyers targeting the private deals compete for the impression first**. Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction, paying either the second-highest bid from the private auction or the deal floor price, whichever is higher. If no private auction deals clear their floors, the highest bid in the open auction wins, paying either the second-highest bid from the open auction or ECP, whichever is higher.<br><br>`3` = First Look<br>Deals considered `"First Look"` are offered only by external supply partners and have extremely varied auction logic depending on both the supply partner and the seller. You must contact the supply partner for details about how the deal works. Xandr as a buying platform can make no guarantee that first look deals actually give you the first look at an impression.  |
| `name` | string (255) | The name of the type of deal. Possible values: <br> - `"Open Auction"` <br> - `"Private Auction"` <br> - `"First Look"`. |

### Brands

Each `brands` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand that is eligible for the deal. You can use the [Brand Service](./brand-service.md) to retrieve brand IDs. |
| `name` | string | The name of the brand that is eligible for the deal. |
| `override` | Boolean | If set to `true`, a brand can serve for a deal even if the ad quality profile would have blocked it. |

### Categories

Each categories object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the categories that is eligible for the deal. You can use the [Category Service](./category-service.md) to retrieve category IDs. |
| `name` | string | The name of the category that is eligible for the deal. |
| `override` | Boolean |  If set to `true`, a category can serve for a deal even if the ad quality profile would have blocked it. |

### Languages

Each `languages` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the language that is eligible for the deal. You can use the [Language Service](./language-service.md) to retrieve language IDs. |
| `name` | string | The name of the language that is eligible for the deal. |
| `override` | Boolean |  If set to `true`, a language can serve for a deal even if the ad quality profile would have blocked it. |

### Technical attributes

Each `technical_attribute` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the technical attribute that is eligible for the deal. You can use the [Technical Attribute Service](./technical-attribute-service.md) to retrieve technical attribute IDs. |
| `name` | string | The name of the technical attribute that is eligible for the deal. |
| `override` | Boolean | If set to `true`, a technical attribute can serve for a deal even if the ad quality profile would have blocked it. |

### Creatives

The `creatives` array is limited to 100 creatives. Each `creatives` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative that is approved or banned for the deal. You can use the [Creative Service](./creative-service.md) to retrieve creative IDs. |
| `status` | string | Specifies how this creative will be handled for this deal.<br> - `approved`: This creative can always serve in this deal, regardless of any other ad quality settings or overrides.<br> - `banned`: This creative can never serve in this deal, regardless of any other ad quality settings or overrides. |

### Sizes

Each object in the `size_targets` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `width` | string | The width of the creative. |
| `height` | string | The height of the creative. |

## Examples

### View all deals you have with sellers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-access'
{ 
    "response": {
        "status": "OK",
        "count": 6,
        "start_element": 0,
        "num_elements": 100,
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
                    "id": 100004,
                    "name": "Seller 123"
                },
                "buyer": {
                    "id": 100005,
                    "bidder_id": 2,
                    "name": "Buyer 123"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1,
                                                "name": "Example Brand"
                    },
                                "ask_price": 2.75,
                                "suggested_min_bid_price": 3,
                "sizes": [
                    {
                        "width": "300",
                        "height": "250"
                    }
                ]
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
                    "id": 100006,
                    "name": "Seller 456"
                },
                "buyer": {
                    "id": 100007,
                    "bidder_id": 2,
                    "name": "Buyer 456"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1,
                                                "name": "Example Brand"
                    }
                ]
            },
            ...
        ]
    }
}
```

### View all deals you have with a specific seller

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-access?seller_member_id=100006'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
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
                    "id": 100007,
                    "bidder_id": 2,
                    "name": "Buyer 456"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1,
                                                "name": "Example Brand"
                    }
                ],
                                "ask_price": 2.75,
                                "suggested_min_bid_price": 3,
                "sizes": [
                    {
                        "width": "300",
                        "height": "250"
                    }
                ]  
            }
        ]
    }
}
```

### View a specific deal

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-access?id=63'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
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
                "id": 100007,
                "bidder_id": 2,
                "name": "Buyer 456"
            },
            "type": {
                "id": 2,
                "name": "Private Auction"
            },
            "brands": [
                {
                    "id": 1,
                                        "name": "Example Brand"
                }
            ],
                        "ask_price": 2.75,
                        "suggested_min_bid_price": 3,
            "sizes": [
                {
                    "width": "300",
                    "height": "250"
                }
            ]
        }
    }
}
```

### View all deals that have not expired

In this example, assuming today is December 4, 2018, we want to find all deals that have not expired. To do this, we pass the `min_end_date=2018-12-04` filter in the query string. Note, however, that deals with no end date will not show up in the response.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-access?min_end_date=2018-12-04'
{
    "response": {
        "status": "OK",
        "count": 4,
        "start_element": 0,
        "num_elements": 100,
        "deals": [
            {
                "id": 60,
                "code": null,
                "name": null,
                "description": null,
                "active": true,
                "start_date": "2018-12-01 00:00:00",
                "end_date": "2018-12-31 23:59:00",
                "floor_price": 3.2,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2018-12-04 18:47:39",
                "seller": {
                    "id": 100006,
                    "name": "Seller 456"
                },
                "buyer": {
                    "id": 100007,
                    "bidder_id": 2,
                    "name": "Buyer 456"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": null,
                                "ask_price": 3.5,
                                "suggested_min_bid_price": 3.75,
            },
            {
                "id": 62,
                "code": null,
                "name": "Private deal for buyer 1085 with floor of 2.5",
                "description": null,
                "active": false,
                "seller_member_id": 1066,
                "start_date": "2018-12-01 00:00:00",
                "end_date": "2018-12-31 23:59:59",
                "profile_id": null,
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2018-12-04 20:15:38",
                "seller": {
                    "id": 100006,
                    "name": "Seller 456"
                },
                "buyer": {
                    "id": 100007,
                    "bidder_id": 2,
                    "name": "Buyer 456"
                },
                "type": {
                    "id": 2,
                    "name": "Private Auction"
                },
                "brands": [
                    {
                        "id": 1,
                                                "name": "Example Brand"
                    }
                ]
            },
            ...
        ]
    }
}
```
