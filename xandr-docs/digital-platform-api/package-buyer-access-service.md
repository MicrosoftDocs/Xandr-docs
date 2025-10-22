---
title: Digital Platform API - Package Buyer Access Service
description: Buyers can view and generate deals for sellers' packages through Package Buyer Access service. Packages are deals sellers are prepared to offer to buyers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Package Buyer Access service

This read-only service lets buyers view information about sellers' packages. A package is a deal that a seller is prepared to offer to any buyer. Buyers browse through available packages and then use the [Deal From Package Service](./deal-from-package-service.md) to generate deals for themselves.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET`  | `https://api.appnexus.com/package-buyer-access` | View all available packages. |
| `GET` | `https://api.appnexus.com/package-buyer-access?member_id=SELLER_MEMBER_ID`  | View all packages offered by a specific seller. |
| `GET`  | `https://api.appnexus.com/package-buyer-access?id=PACKAGE_ID` | View a specific package. |
| `GET`  | `https://api.appnexus.com/package-buyer-access?id=1,2,3` |  View multiple packages by ID using a comma-separated list. |
| `GET` | `https://api.appnexus.com/package-buyer-access?sizes=WIDTHxHEIGHT,WIDTHxHEIGHT`  | View all packages including specific sizes. |
| `GET`  | `https://api.appnexus.com/package-buyer-access?search=PACKAGE_ID or NAME` | Search for a package by name or ID. |
| `GET` |`https://api.appnexus.com/package/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the package. |
| `name` | string | The name of the package. |
| `description` | string | The description of the package. Sellers generally use this to provide buyers greater insight into the deal. |
| `active` | Boolean | If `true`, the package is active. If `false`, you cannot generate deals from the package and all associated deals will stop serving.   |
| `default_ask_price` | double | The ask price that will be applied to all deals generated from the package. When you generate a deal, the [Deal Buyer Access Service](./deal-buyer-access-service.md) will automatically calculate the `suggested_min_bid_price` by adding the auction service charge specified in your Xandr contract to the value in this field. For more information on the `suggested_min_bid_price`, see the [Deal Buyer Access Service](./deal-buyer-access-service.md).<br><br>**Note**: This field is relevant only if `default_use_deal_floor` is `true`. |
| `default_currency` | string | The ask price currency that will be applied to all deals generated from the package. |
| `default_use_deal_floor` | Boolean | If `true`, the `default_ask_price`  will be applied to deals generated from the package.<br><br>**Note**: When  `default_use_deal_floor` is `true`, the deal's ask price overrides any other floors the seller may have, i.e., in placements or yield management profiles. |
| `last_modified` | timestamp | The day and time when the package was last modified. |
| `data_protected` | Boolean | **Not yet supported**. |
| `allow_creative_add_on_view` | Boolean | **Not yet supported**. |
| `allow_creative_add_on_click` | true | **Not yet supported**. |
| `visibility_profile_id` | int | **Not yet supported**. |
| `seller_rank` | int | The seller's ranking for the package. This controls where the package will appear in the seller's full list of packages in. Allowed range: `1` - `65355`, where `1` is the highest ranking. |
| `size_preference` | string | Specifies how this package handles private sizes. Private sizes are placement sizes that the seller can allow to serve in a package. There are two options:<br> - `standard`: Private sizes are not available for this package.<br> - `append`: Private sizes can be used in addition to the specified placement size. |
| `technical_attribute_restrict` | Boolean | Specifies whether the package is restricted only to the technical attributes listed in the [Technical Attributes](#technical-attributes) object.<br> - `true`: Package is restricted only to the listed technical attributes.<br> - `false`: Other technical attributes are also allowed to serve. |
| `seller` | object | The name and ID of the seller who is offering the package. For more details, see [Seller](#seller) below. |
| `default_deal_type` | object | The deal type that will be applied to all deals generated from the package. For more details, see [Default Deal Type](#default-deal-type) below. |
| `setting` | object | The type of content included in the package. For more details, see [Setting](#setting) below. |
| `technical_attributes` | array of objects | The technical attributes of creatives that are eligible for the package. For more details, see [Technical Attributes](#technical-attributes) below. |
| `sizes` | array of objects | The creative sizes included in the package. For more details, see [Sizes](#sizes) below. |

### Seller

The `seller` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The member ID of the seller. |
| `name` | string | The member name of the seller. |

### Default deal type

The `default_deal_type` object contains the following fields. By default, all packages will generate deals with an open auction deal type.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID representing the type of deal. Possible values: `1` (Open Auction) or `2` (Private Auction). For more information about open and private auctions, see the [Deal Service](./deal-service.md).   |
| `name` | string | **Read-only**. The name of the type of deal. Possible values: `"Open Auction`" or `"Private Auction"`. |

### Setting

This information is used to give buyers a general understanding of the inventory included in the package. The `setting` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `has_inventory` | Boolean | If `true`, the package includes publisher, placement, site, or content category targets. |
| `inventory_description` | string | If `has_inventory` is set to `true`, this field provides a description of the inventory included in the package. |
| `has_segments` | Boolean | If `true`, the package includes segment targets. |
| `segments_description` | string | If `has_segments` is set to `true`, this field provides a description of the segments included in the package. |
| `has_sizes` | Boolean | If `true`, the package includes size targets. For the specific sizes included, see the [sizes array](#sizes). |

### Technical attributes

Each `technical_attribute` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the technical attribute that is eligible for the package. You can use the [Technical Attribute Service](./technical-attribute-service.md) to retrieve technical attribute IDs. |
| `name` | string | The name of the technical attribute that is eligible for the package. |
| `override` | Boolean |  If set to `true`, a technical attribute can serve for a package even if the ad quality profile would have blocked it. |

### Sizes

Each object in the `sizes` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `width` | string | The width of the creative. |
| `height` | string | The height of the creative. |

## Examples

### View all available packages

```
$ curl -b cookies -c cookies "https://api.appnexus.com/package-buyer-access"
{
  "response": {
    "status": "OK",
    "count": 102,
    "packages": [
      {
        "id": 1,
        "name": "Test Pkg",
        "description": "this is a test package",
        "active": true,
        "default_ask_price": 2.5,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-05-30 15:02:33",
        "seller_rank": 100,
        "seller": {
          "id": 5581,
          "name": "Test University"
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
        "setting": {
          "has_inventory": true,
          "inventory_description: "Description of inventory.",
          "has_segments": true,
          "segment_description": "Description of segments.",
          "has_sizes": false
        },
        "technical_attributes":null,
        "sizes": null
      },
      {
        "id": 2,
        "name": "High Performance & Viewability!",
        "description": "This is an artisanal, hand-picked collection of extremely high performing placements that are visible at least 90% of the time. Viewability audit performed daily by our proprietary View-O-Matic technology and verified by a trusted 3rd party.",
        "active": true,
        "default_ask_price": 8.8,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-06-26 22:12:31",
        "seller_rank": 100,
        "seller": {
          "id": 55570,
          "name": "Seller ABC"
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
        "setting": {
          "has_inventory": true,
          "inventory_description: "Description of inventory.",
          "has_segments": true,
          "segment_description": "Description of segments.",
          "has_sizes": true
        },
        "sizes": [
          {
            "width": "120",
            "height": "600"
          },
          {
            "width": "160",
            "height": "600"
          },
          {
            "width": "300",
            "height": "250"
          },
          {
            "width": "468",
            "height": "60"
          },
          {
            "width": "480",
            "height": "80"
          },
          {
            "width": "640",
            "height": "360"
          }
        ]
      },
      ...
    ]
  }
}
```

### View all packages offered by a specific seller

```
$ curl -b cookies -c cookies "https://sand.api.appnexus.com/package-buyer-access?member_id=55586"
{
  "response": {
    "status": "OK",
    "count": 2,
    "packages": [
      {
        "id": 108,
        "name": null,
        "description": null,
        "active": true,
        "default_ask_price": 1,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-07-16 20:49:30",
        "seller_rank": 100,
        "seller": {
          "id": 55586,
          "name": "Tyroo Media Pvt. Ltd."
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
        "setting": {
          "has_inventory": true,
          "inventory_description: "Description of inventory.",
          "has_segments": true,
          "segment_description": "Description of segments.",
          "has_sizes": false
        },
        "technical_attributes": null,
        "sizes": null
      }
    ],
    {
        "id": 5,
        "name": "Package of inventory with data",
        "description": "This package includes inventory X and data X.",
        "active": false,
        "default_ask_price": 11.26,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-06-06 18:10:47",
        "seller_rank": 100,
        "seller": {
          "id": 55586,
          "name": "Tyroo Media Pvt. Ltd."
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
        "setting": {
          "has_inventory": true,
          "inventory_description: "Description of inventory.",
          "has_segments": true,
          "segment_description": "Description of segments.",
          "has_sizes": true
        },
        "sizes": [
          {
            "width": "160",
            "height": "600"
          },
          {
            "width": "300",
            "height": "50"
          }
        ]
      },
  }
}
```

### View a specific package

```
$ curl -b cookies -c cookies "https://api.appnexus.com/package?id=109"
{
  "response": {
    "status": "OK",
    "count": 1,
    "package": {
      "id": 109,
      "name": "Updated Package 1",
      "description": null,
      "active": true,
      "default_ask_price": 1,
      "default_currency": "USD",
      "default_use_deal_floor": true,
      "last_modified": "2014-07-21 17:14:16",
      "seller_rank": 100,
      "seller": {
        "id": 5558,
        "name": "TMP Ltd."
      },
      "default_deal_type": {
        "id": 1,
        "name": "Open Auction"
      },
      "setting": {
          "has_inventory": true,
          "inventory_description: "Description of inventory.",
          "has_segments": true,
          "segment_description": "Description of segments.",
          "has_sizes": false
      },
      "technical_attributes": null,
      "sizes": null     
    }
  }
}
```
