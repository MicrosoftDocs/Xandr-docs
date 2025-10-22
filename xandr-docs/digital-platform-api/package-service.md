---
title: Package Service
description: Sellers can use the Package Service to create and manage their packages.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Package service

Sellers use this service to create and manage their packages. Packages are pre-made combinations of inventory and/or data. Buyers can use the [Package Buyer Access Service](package-buyer-access-service.md) to browse packages and then use the [Deal From Package Service](./deal-from-package-service.md) to create deals from them "off-the-shelf", or they can use packages as a jumping-off point for deal negotiations.

In cases where packages don't meet a buyer's needs, sellers can use the [Deal Service](./deal-service.md) to create one-off custom deals.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/package`<br><br>(`add_package` JSON) | Add a new package. |
| `PUT` | `https://api.appnexus.com/package?id=PACKAGE_ID`<br><br>(`modify_package` JSON) | Update a package. |
| `GET` | `https://api.appnexus.com/package` | View all of your packages. |
| `GET` | `https://api.appnexus.com/package?id=PACKAGE_ID` | View a specific package. |
| `DELETE` | `https://api.appnexus.com/package?id=PACKAGE_ID` | Delete a package. <br><br>**CAUTION**: Deleting a package deletes all of its associated deals as well. Campaigns targeting these associated deals will stop serving. The deletions are permanent and cannot be reverted. Although deleted deals continue to be available in reporting, you will no longer have visibility into their specific settings. |
| `GET` | `https://api.appnexus.com/package/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Name | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the package.<br><br>**Default**: Auto-generated number<br>**Required On**: `PUT`, `DELETE` |
| `name` | string (255) | The name of the package. |
| `description` | string (65535) | The description of the package. You can use this field to provide buyers additional insight and details about the package. |
| `active` | Boolean | If `true`, the package is active. If `false`, buyers cannot generate deals from the package and all associated deals will stop serving.<br><br>**Default**: `true` |
| `profile_id` | int | The ID of the profile associated to the package. You can use a profile to specify publishers, placements, sites, content categories, segments, segment groups, or sizes that need to be involved in the auction in order for the deal to be available to the buyer. For more details, see `publisher_targets`, `placement_targets`, `content_category_targets`, `segment_targets`, `segment_group_targets`, `site_targets` , and `size_targets` in the [Profile Service](./profile-service.md).<br><br>**CAUTION**: Any other targeting settings in the associated profile will not be respected.<br><br>**Required On**: `POST` |
| `default_ask_price` | double | The ask price that will be applied to all deals generated from the package. When a buyer generates a deal, the [Deal Service](./deal-service.md) will automatically calculate the `floor_price` by subtracting the seller revenue share specified in your contract from the value in this field. This is the price shown to the buyer. It is the minimum they must bid in order to compete for the inventory.<br><br>**Note**: You must use the `member_ask_price` field to set pricing when `visibility_type` is set to `2`. When `visibility_type` is set to `1`, you can use the `member_ask_price` field to set different pricing for select buyers.<br><br>**Required On**: `POST` |
| `default_currency` | enum | The ask price currency that will be applied to all deals generated from the package. For a full list of available currencies, use the read-only [Currency Service](./currency-service.md).<br><br>**Default**: `"USD"` |
| `default_use_deal_floor` | Boolean | If `true`, the `default_ask_price` will be applied to deals generated from the package. The deal's floor price will override any other floors you may have, i.e., in placements or yield management profiles.<br><br>**Note**: If `default_use_deal_floor` is `false`, `default_ask_price` must be set to `0`. In this case, note that although the ask price is shown as `0`, no deal floor is actually applied; if you have any other floors (in placements or yield management profiles), they will be applied, or if you do not have any other floors, the standard second-price auction mechanics will apply.<br><br>**Default**: `true` |
| `last_modified` | timestamp | The day and time when the package was last modified. |
| `data_protected` | Boolean | **Not yet supported**.<br>**Default**: `false` |
| `allow_creative_add_on_view` | Boolean | **Not yet supported**.<br>**Default**: `false` |
| `allow_creative_add_on_click` | true | **Not yet supported**.<br>**Default**: `true` |
| `visibility_profile_id` | int | **Not yet supported**.<br>**Default**: `null` |
| `seller_rank` | int | The seller's ranking for the package. This controls where the package will appear in the seller's full list of packages in the UI. Allowed range: `1` - `65355`, where `1` is the highest ranking.<br><br>**Default**: `100` |
| `size_preference` | enum | Specifies how this package handles private sizes. Private sizes are placement sizes (set in the `private_sizes` array in the [Placement Service](./placement-service.md)) that can be allowed to serve in a package. There are two options:<br> - `standard`: Private sizes are not available for this package.<br> - `append`: Private sizes can be used in addition to the specified placement size. |
| `technical_attribute_restrict` | Boolean | Specifies whether the package is restricted only to the technical attributes listed in the [Technical Attributes](#technical-attributes) object.<br> - `true`: Package is restricted only to the listed technical attributes.<br> - `false`: Other technical attributes are also allowed to serve.<br><br>**Default**: `true` |
| `seller` | object | The name and ID of the seller who is offering the package. For more details, see [Seller](#seller) below.<br><br>**Required On**: `POST` |
| `default_deal_type`  | object | The deal type that will be applied to all deals generated from the package. For more details, see [Default Deal Type](#default-deal-type) below. |
| `visibility_type` | object | Defines if the package is visible to all buyers or select buyers. For more details, see [Visibility Type](#visibility-type) below. |
| `members` | array of objects | If `visibility_type` is set to `"private"`, only the members listed in this field will be able to view the package. You can also use this field to define special pricing for select buyers. For more details, see [Members](#members) below. |
| `setting` | object | The type of content included in the package. For more details, see [Setting](#setting) below. |
| `technical_attributes` | array of objects | The technical attributes of creatives that are eligible for the package. For more details, see [Technical Attributes](#technical-attributes) below. |
| `sizes` | array of objects | If the profile associated with the package has size targets set, you can use this field to expose the specific sizes to buyers. For more details, see [Sizes](#sizes) below. |
| `default_deal_priority` | Int | The bidding priority when `id` in the `default_deal_type` object = `2`/Private Auction.<br>Possible values: `1` - `20`, where `20` is the highest priority.<br><br>**Default**: `5` |
| `allowed_media_types` | array of objects | The media types allowed for the package. To learn more, see [Allowed Media Types](#allowed-media-types) below. |
| `allowed_media_subtypes` | array of objects | The media subtypes allowed for the package. To learn more, see [Allowed Media Subtypes](#allowed-media-subtypes) below. |
| `media_preference` | string | Specifies how this package handles media types/subtypes. There are two options:<br> - `standard` = use whatever media types are already on the auction (based on the placement settings)<br> - `append` = include the media types on the auction + any private media types set on the placement<br><br>If a deal is created from a package, this setting is copied from the package to the deal. |

### Seller

The `seller` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | **Read-only**. The member ID of the seller.<br><br>**Default**: Seller's member ID<br>**Required On**: `POST` |
| `name` | string | **Read-only**. The member name of the seller.<br><br>**Default**: Seller's member name |

### Default deal type

The `default_deal_type` object contains the following fields. By default, all packages will generate deals with an open auction deal type.

| Field | Type | Description |
|:---|:---|:---|
| `id`  | int | The ID representing the type of deal. Possible values: `1` (Open Auction) or `2` (Private Auction). For more information about open and private auctions, see the [Deal Service](./deal-service.md).<br><br>**Default**: `1` |
| `name` | string | **Read-onl**y. The name of the type of deal. Possible values: `"Open Auction"` or `"Private Auction"`.<br><br>**Default**: `"Open Auction"` |

### Visibility type

The `visibility_type` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id`  | int | The ID of the visibility level for your package. Possible values:<br> - `1` = console<br>A "console" package is visible to all buyers. Any buyer can create a deal from the package. Use the `members` array to define special pricing for select buyers. For more information, see [Members](#members) below.<br><br> - `2` = private<br>A "private" package is only visible to the buyers specified in the `members` array. Only those buyers can create a deal from the package. Use the `members` array to define unique pricing for each of these buyers. For more information, see [Members](#members) below.<br><br> - `3` = hidden<br>A "hidden" package is not visible to any buyers.<br><br>**Note**: Hiding a package with associated deals will not affect the associated deals; however buyers can not generate any new deals from the package.<br><br>**Default**: `1` |
| `name` | string | **Read-only**. The name of the visibility level for your package. Possible values: <br> - `"console"` <br> - `"private"` <br> - `"hidden"` |

### Members

If `visibility_type` is set to `"private"`, only the buyers listed in this array can view the package. If `visibility_type` is set to `"console"`, all buyers can view the package but you can define a different ask price for each of the buyers listed in this array. Each `member` object in this array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id`  | int | The member ID of the buyer. |
| `name` | string | **Read-only**. The member name of the buyer.<br>**Default**: Buyer's member name |
| `member_use_deal_floor` | Boolean | If `true`, the `member_ask_price` will be applied to deals that the buyer generates from the package. This value will override any other floors you may have, i.e., in placements or yield management profiles. <br><br>**CAUTION**: The `default_ask_price` value will never apply to buyers in the members array. You must use the `member_ask_price` field to define an ask price for buyers listed in the members array.<br><br>**Default**: `true` |
| `member_ask_price` | int | The ask price that will be applied to deals the buyer generates from the package. When the buyer generates a deal, the [Deal From Package Service](./deal-from-package-service.md) will automatically calculate the `floor_price` by subtracting the seller revenue share specified in your contract from the value in this field. This is the price shown to the buyer. It is the minimum they must bid in order to compete for the inventory.<br><br>**Note**: If `member_use_deal_floor` is `false`, this field must be set to `0`. In this case, note that although `0` is shown as the floor price, no deal floor is actually applied; if you have any other floors (in placements or yield management profiles), they will be applied, or if you do not have any other floors, the standard second-price auction mechanics will apply. |

### Setting

This information is used to give buyers a general understanding of the inventory included in the package. The `setting` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `has_inventory` | Boolean | Set this field to `true` if the profile associated with the package has publisher, placement, site, or content category targets set. For more information, see the `profile_id` field.<br><br>**Default**: `false` |
| `inventory_description` | string | If `has_inventory` is set to `true`, use this field to provide a description of the inventory included in the package. Buyers cannot see the specific targets you have set so it is important to provide them with additional insight into the package contents. |
| `has_segments` | Boolean | Set this field to `true` if the profile associated with the package has segment or segment group targets set. For more information, see the `profile_id` field.<br><br>**Default**: `false` |
| `segments_description` | string | If `has_segments` is set to `true`, use this field to provide a description of the segments included in the package. Buyers cannot see the specific targets you have set so it is important to provide them with additional insight into the package contents. |
| `has_sizes` | Boolean | Set this field to `true` if the profile associated with the package has size targets set. For more information, see the `profile_id` field. If you want buyers to see the specific sizes you have included, use the `sizes` field.<br><br>**Default**: `false` |

### Sizes

Each object in the `sizes` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `width` | string | The width of the creative. |
| `height` | string | The size of the creative. |

### Technical attributes

Each `technical_attribute` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id`  | int | The ID of the technical attribute that is eligible for the package. You can use the [Technical Attribute Service](./technical-attribute-service.md) to retrieve technical attribute IDs. |
| `name` | string | The name of the technical attribute that is eligible for the package. |
| `override` | Boolean | Set to `true` to allow a technical attribute to serve for a package even if the ad quality profile would have blocked it.<br><br>**Default**: `false` |

### Allowed media types

You can use this array to limit the media type, the general display style of creatives, that can serve on placements that are part of deals made from this package.

Each `allowed_media_types` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the media type. |
| `name` | string | The name of the allowed media type, for example `"Banner"`. |
| `media_type_group_id` | int | The group ID for the media type. |
| `uses_sizes` | enum | Whether the media type has size specifications. Possible values:<br> - `always`<br> - `sometimes`<br> - `never` |
| `last_modified` | date | When the `allowed_media_type` object was last updated. |

### Allowed media subtypes

You can use this array to limit the media subtype, the specific display style of creatives, that can serve on placements that are part of deals made from this package.

Each `allowed_media_subtypes` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `permitted_sizes` | array of objects | The permitted sizes for creatives of the media subtype. See [Permitted Sizes](#permitted-sizes) below for more details.<br><br>**Note**: Not all media subtypes have permitted size requirements. |
| `native_assets` | array of objects | An array describing constraints on elements of native ads for this media subtype. Elements of a native ad can include the title, body content, and more. The format's constraints could be whether body content is required or recommended, or how long the text may be. For more information, see [Native Assets](#native-assets) below. |
| `id` | int | The ID of the `allowed_media_subtype`. `PUT` and `POST` on JSON file |
| `name` | string | The name of the `allowed_media_subtype`. |
| `last_modified` | date | When the `allowed_media_subtype` array was last modified. |
| `mediatype_id` | int | The ID of the `media_type`. |
| `media_type_name` | string | The name of the `media_type`. |
| `media_type_group_id` | int | The ID of the group for the media type. |

### Permitted sizes

Each `permitted_sizes` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `platform_width` | int | The actual rendering width, in pixels, for creatives of this media subtype. This is also the width that appears in reporting. |
| `platform_height` | int | The actual rendering height, in pixels, for creatives of this media subtype. This is also the height that appears in reporting. |
| `validate_image_size` | boolean | If `true`, the image for creatives of this media subtype will be validated against the requirements defined by the following fields in this object: `scaling_permitted`, `aspect_ratio_tolerance`, `min_image_width`, `max_image_width`, `min_image_height`, and `max_image_height`. |
| `scaling_permitted` | boolean | If `true`, the image for creatives of this media subtype must have the same aspect ratio as `platform_width`/`platform_height`.<br><br>If `false`, the image for creatives of this media subtype must have a width and height exactly matching `platform_width` and `platform_height`. |
| `aspect_ratio_tolerance` | double | If `validate_image_size` and `scaling_permitted` are both `true`, the image can deviate from the aspect ratio of `platform_width` and `platform_height` by this amount. For example, the aspect ratio for a `platform_width` and `platform_height` of 254x133 is 1.19:1. If the `aspect_ratio_tolerance` is 0.03, an aspect ratio between 1.16:1 and 1.22:1 would be acceptable. |
| `min_image_width` | int | If `validate_image_size` is `true`, the minimum acceptable image width, in pixels, for creatives of this media subtype. |
| `max_image_width` | int | If `validate_image_size` is `true`, the maximum acceptable image width, in pixels, for creatives of this media subtype. |
| `min_image_height` | int | If `validate_image_size` is `true`, the minimum acceptable image height, in pixels, for creatives of this media subtype. |
| `max_image_height` | int | If `validate_image_size` is `true`, the maximum acceptable image height, in pixels, for creatives of this media subtype. |

### Native assets

Each `native_assets` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `native_asset_name` | string | The title of the ad. |
| `min_text_length` | int | The minimum length for the text. |
| `max_text_length` | int | The maximum length for the text. |
| `requirement` | enum | Whether this asset is required by this particular media subtype. This field can contain several levels of "requiredness":<br> - `"required"`<br> - `"recommended"`<br> - `"optional"` |

## Examples

### Create a new package for any buyer

```
$ cat add_package

{
 "package":
  { "name" : "Package 1",
    "seller" : {
        "id" : 5555
        },
    "profile_id" : 555540,
    "default_ask_price" : "1.00"
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @add_package.json "https://api.appnexus.com/package"

{
    "response": {
        "status": "OK",
        "count": 1,
        "package": {
            "id": 109,
            "name": "Package 1",
            "description": null,
            "active": true,
            "profile_id": 555540,
            "default_ask_price": 1,
            "default_currency": "USD",
            "default_use_deal_floor": true,
            "last_modified": "2014-07-16 20:53:03",
            "seller": {
                "id": 5555,
                "name": "Seller 1"
            },
            "default_deal_type": {
                "id": 1,
                "name": "Open Auction"
            },
            "visibility_type": {
                "id": 1,
                "name": "console"
            },
            "members": null,
            "setting": null,
            "technical_attributes": null,
            "sizes": null
        }
    }
}
```

### Create a new package with custom pricing for selected buyers

In this example, we create a new package that is visible to all buyers with a price of $3.00. For a few select buyers we set custom pricing below $3.00.

```
$ cat add_package_custom_pricing

{
 "package":
  { "name" : "Package 2",
    "seller" : {
        "id" : 5555
        },
    "profile_id" : 555540,
    "default_ask_price" : "1.00",
    "members" : [
          {
            "id": 5524,
            "member_use_deal_floor": true,
            "member_ask_price": 2.15,
            "name": "Buyer 1"
          },
          {
            "id": 5561,
            "member_use_deal_floor": true,
            "member_ask_price": 2.25,
            "name": "Buyer 2"
          }
        ]
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @add_package_custom_pricing.json "https://api.appnexus.com/package"

{
  "response": {
    "status": "OK",
    "count": 1,
    "package": {
      "id": 128,
      "name": "Package 2",
      "description": null,
      "active": true,
      "profile_id": 555540,
      "default_ask_price": 3,
      "default_currency": "USD",
      "default_use_deal_floor": true,
      "last_modified": "2014-08-19 20:55:15",
      "seller": {
        "id": 5555,
        "name": "Seller 1"
      },
      "default_deal_type": {
        "id": 1,
        "name": "Open Auction"
      },
      "visibility_type": {
        "id": 1,
        "name": "console"
      },
      "members": [
        {
          "id": 5524,
          "member_use_deal_floor": true,
          "member_ask_price": 2.15,
          "name": "Buyer 1"
        },
        {
          "id": 5561,
          "member_use_deal_floor": true,
          "member_ask_price": 2.25,
          "name": "Buyer 2"
        }
      ],
      "setting": null,
      "technical_attributes": null,
      "sizes": null
    }
  }
}
```

### Create a new package only visible to selected buyers

In this example, we create a new package that is only visible to two buyers. We have set a different ask price for each buyer.

```
$ cat add_package_specific_buyer

{
 "package":
  { "name" : "Package 2",
    "seller" : {
        "id" : 5555
        },
    "profile_id" : 555540,
    "default_ask_price" : "3.00",
    "visibility_type" : {
        "id" : 2
    },
    "members" : [
          {
            "id": 5524,
            "member_use_deal_floor": true,
            "member_ask_price": 2.15,
            "name": "Buyer 1"
          },
          {
            "id": 5561,
            "member_use_deal_floor": true,
            "member_ask_price": 2.25,
            "name": "Buyer 2"
          }
        ]
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @add_package_specific_buyer.json "https://api.appnexus.com/package"

{
  "response": {
    "status": "OK",
    "count": 1,
    "package": {
      "id": 128,
      "name": "Package 2",
      "description": null,
      "active": true,
      "profile_id": 555540,
      "default_ask_price": 1,
      "default_currency": "USD",
      "default_use_deal_floor": true,
      "last_modified": "2014-08-19 20:55:15",
      "seller": {
        "id": 5555,
        "name": "Seller 1"
      },
      "default_deal_type": {
        "id": 1,
        "name": "Open Auction"
      },
      "visibility_type": {
        "id": 2,
        "name": "private"
      },
      "members": [
        {
          "id": 5524,
          "member_use_deal_floor": true,
          "member_ask_price": 2.15,
          "name": "Buyer 1"
        },
        {
          "id": 5561,
          "member_use_deal_floor": true,
          "member_ask_price": 2.25,
          "name": "Buyer 2"
        }
      ],
      "setting": null,
      "technical_attributes": null,
      "sizes": null
    }
  }
}
```

### Modify a package

In this example, we update the name of the package.

```
$ cat modify_package

{
 "package":
  { "name" : "Updated Package 1"
  }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @modify_package.json "https://api.appnexus.com/package?id=109

{
  "response": {
    "status": "OK",
    "count": 1,
    "package": {
      "id": 109,
      "name": "Updated Package 1",
      "description": null,
      "active": true,
      "profile_id": 555540,
      "default_ask_price": 1,
      "default_currency": "USD",
      "default_use_deal_floor": true,
      "last_modified": "2014-07-21 17:14:16",
      "seller": {
        "id": 5555,
        "name": "Tyroo Media Pvt. Ltd."
      },
      "default_deal_type": {
        "id": 1,
        "name": "Open Auction"
      },
      "visibility_type": {
        "id": 1,
        "name": "console"
      },
      "members": null,
      "setting": null,
      "technical_attributes": null,
      "sizes": null
    }
  }
}
```

### View all of your packages

```
$ curl -b cookies -c cookies "https://api.appnexus.com/package"

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
        "profile_id": 555540,
        "default_ask_price": 1,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-07-16 20:49:30",
        "seller": {
          "id": 5555,
          "name": "Tyroo Media Pvt. Ltd."
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
      "visibility_type": {
        "id": 1,
        "name": "console"
      },
      "members": null,
      "setting": null,
      "sizes": null
      },
      {
        "id": 109,
        "name": "Updated Package 1",
        "description": null,
        "active": true,
        "profile_id": 555540,
        "default_ask_price": 1,
        "default_currency": "USD",
        "default_use_deal_floor": true,
        "last_modified": "2014-07-21 17:14:16",
        "seller": {
          "id": 5555,
          "name": "Tyroo Media Pvt. Ltd."
        },
        "default_deal_type": {
          "id": 1,
          "name": "Open Auction"
        },
      "visibility_type": {
        "id": 1,
        "name": "console"
      },
      "members": null,
      "setting": null,
      "technical_attributes": null,
      "sizes": null
      }
    ]
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
      "profile_id": 555540,
      "default_ask_price": 1,
      "default_currency": "USD",
      "default_use_deal_floor": true,
      "last_modified": "2014-07-21 17:14:16",
      "seller": {
        "id": 5555,
        "name": "Tyroo Media Pvt. Ltd."
      },
      "default_deal_type": {
        "id": 1,
        "name": "Open Auction"
      },
      "visibility_type": {
        "id": 1,
        "name": "console"
      },
      "members": null,
      "setting": null,
      "technical_attributes": null,
      "sizes": null
    }
  }
}
```

### Delete a package

```
$ curl -b cookies -c cookies -DELETE "https://api.appnexus.com/package?id=109"

{
  "response": {
    "status": "OK",
    "count": 1
  }
}
```
