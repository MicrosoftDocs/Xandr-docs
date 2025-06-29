---
title: Deal Service
description: Use the deal service to let buyers, sellers, and external bidders set up and manage negotiated deals.
ms.date: 06/30/2025
ms.custom: digital-platform-api
---

# Deal service

The Deal Service lets buyers, sellers, and external bidders set up and manage negotiated deals. Deals may provide buyers:

- Preferential pricing on inventory
- Access to exclusive inventory
- Reduced competition on inventory
- Other opportunities

Each deal is valid for a single buyer.

> [!NOTE]
> - The inventory included in a deal may be encompassed by other deals as well.
> - Buyers can use the [Deal Buyer Access Service](./deal-buyer-access-service.md) to view the deals available to them. To target deals, buyers **Seller Restricted Targeting** can use the `deal_targets` field in the [Profile Service](./profile-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | https://api.appnexus.com/deal | View all deals you have with buyers. |
| `GET` | https://api.appnexus.com/deal?id=DEAL_ID  | View a specific deal. |
| `GET` | https://api.appnexus.com/deal?id=1,2,3 | View multiple deals by ID using a comma-separated list. |
| `GET` | https://api.appnexus.com/deal/meta | Find out which fields you can filter and sort by. |
| `POST` | https://api.appnexus.com/deal | Add a new deal. |
| `PUT` | https://api.appnexus.com/deal?id=DEAL_ID | Modify an existing deal. |
| `DELETE` | https://api.appnexus.com/deal?id=DEAL_ID | Delete a deal.<br><br>**Warning**: If you delete a deal, all campaigns targeting the deal will stop serving. Deletions are permanent and cannot be reverted. Although deleted deals continue to be available in reporting, you will no longer have visibility into their specific settings. |

## JSON fields

| Field | Type (Length) | Description |
|:---|:---|:---|
| `active` | boolean | If `true`, the deal is active.<br><br>**Default**: `true`<br>**Note**: The deal will be available to the buyer only when this field is `true`, `start_date` is in the past (or `null`), and `end_date` is in the future (or `null`). |
| `adserver_lists` | array of objects | Each object identifies an ad server list that will be applied to the deal. To learn more, see [Ad Server Lists](#ad-server-lists) below.<br><br>**Default**: `null` |
| `allow_creative_add_on_click` | boolean | If `true`, allow any creative to serve that adds users to a segment on click.<br><br>**Default**: `true` |
| `allow_creative_add_on_view` | boolean | If `true`, allow any creative to serve that adds users to a segment on view.<br><br>**Default**: `false` |
| `allowed_media_subtypes` | array of objects | The media subtypes allowed for the deal. To learn more, see [Allowed Media Subtypes](#allowed-media-subtypes) below. |
| `allowed_media_types` | array of objects | The media types allowed for the deal. To learn more, see [Allowed Media Types](#allowed-media-types) below. |
| `ask_price` | double | The `floor_price` plus the seller revenue share specified in your contract. This is the price shown to the buyer. It is the minimum they must bid in order to compete for the inventory.<br><br>**Note**: This field is required for Programmatic Guaranteed deals and is the agreed upon price between the seller and the buyer.<br><br>**Required On**: `PUT` and `POST`<br><br>**Default**: auto-generated number |
| `auction_type` | object | The auction type for the deal. A deal can have the following auction types: first price, second price, and fixed price. For more information, see [Auction Type](#auction-type) below. |
| `audit_status_option` | string | Specifies how the deal handles creatives.<br> - `none`: Creatives use existing ad quality settings.<br> - `provisional`: Creatives in `"pending"` audit status will serve. Once these creatives are audited, the existing ad quality settings are used.<br> - `max_trust`: No ad profile restrictions will be applied to this deal.<br>Creatives specifically listed in the [Creatives](#creatives) object will override these settings.<br><br>**Default**: `none` |
| `brands` | array of objects | The brands of creatives that are eligible for the deal. For more details, see [Brands](#brands) below.<br><br>**Default**: null |
| `brand_restrict` | boolean | Specifies whether the deal is restricted only to the brands listed in the [Brands](#brands) object.<br> - `true`: Deal is restricted only to the listed brands.<br> - `false`: Other brands are also allowed to serve.<br><br>**Default**: `true` |
| `buyer` | object | The buying bidder and member who can target this deal. A deal will only ever use the `buyer` field or the `buyer_seats` field, not both. For more details, see [Buyer](#buyer) below.<br><br>**Required On**: `POST` |
| `buyer_seats` | object | The buying bidder and seat who can target this deal. A deal will only ever use the `buyer` field or the `buyer_seats` field, not both. For more details, see [Buyer Seats](#buyer-seats) below. |
| `buyer_bidders` | object | The buying bidder who can target this deal. For more details, see [Buyer Bidders](#buyer-bidders) below.<br><br>**Default**: `null` |
| `buyer_members` | object | The Xandr member ID of the buyer who can target this deal. For more details, see [Buyer Members](#buyer-members) below.<br><br>**Default**: `null` |
| `categories` | array of objects | The categories that describe the creatives that are eligible for the deal. For more details, see [Categories](#categories) below. |
| `category_restrict` | boolean | Specifies whether the deal is restricted only to the categories listed in the [Categories](#categories) object.<br>- `true`: Deal is restricted only to the listed categories.<br> - `false`: Other categories are also allowed to serve.<br><br>**Default**: `true` |
| `code` | string (100) | The custom code for the deal.<br><br>**Note**: This field is mandatory and represents your internal deal ID, passed in the bid request through the [PMP's object deal ID field](../supply-partners/incoming-bid-request-from-ssps.md).<br><br>**Required On**: `POST`<br>**Default**: `null` |
| `created_by` | string | Specifies whether this deal was created by the seller or the buyer (using the [Deal From Package Service](./deal-from-package-service.md)). |
| `creatives` | array of objects | A list of creatives that are specifically approved or banned for the deal. This list overrides any other ad quality setting. For more details, see [Creatives](#creatives) below. |
| `currency` | enum | The currency for the `floor_price`. For a full list of available currencies, use the read-only [Currency Service](./currency-service.md). <br><br>**Default**: `"USD"` |
| `data_protected` | boolean | If `true`, settings for `allow_creative_add_on_view`, `allow_creative_add_on_click`, and `visibility_profile_id` are used for this deal. If `false`, network and publisher settings are used.<br><br>**Default**: `false` |
| `description` | string (65535) | The description of the deal. You can use this field to provide the buyer additional insight or details about the deal.<br><br>**Default**: `null` |
| `end_date` | timestamp | The day and time when the deal stops being available to the buyer, in local time. If this is set, the format must be `"YYYY-MM-DD HH:MM:SS"`.<br><br>**Default**: `null` (immediately) |
| `floor_price` | double | The minimum CPM value that the buyer must bid to be eligible for the deal.<br><br>**Note**:<br> - If `use_deal_floor` is `false`, this field must be set to `0`. In this case, note that although `0` is shown as the floor price, no deal floor is actually applied; if you have any other floors (in placements or yield management profiles), they will be applied, or if you do not have any other floors, the standard second-price auction mechanics will apply.<br> - As of 2017, only `ask_price` is used. API `POST` and `PUT` calls referencing `floor_price` and `use_deal_floor` will work as follows:<br> * If the API call includes `ask_price` only, this is the value that will be used.<br> * If the API call includes only a `floor_price` value, this value will be converted into the `ask_price` value.<br><br>**Default**: `0`, if `use_deal_floor` is `false` |
| `id` | int | The ID of the deal.<br><br>**Required On**: `PUT` and `DELETE`<br><br>**Default**: auto-incremented number |
| `languages` | array of objects | The language associated with creatives that are eligible for the deal. For more details, see [Languages](#languages) below. |
| `language_restrict` | boolean | Specifies whether the deal is restricted only to the languages listed in the [Languages](#languages) object.<br> - `true`: Deal is restricted only to the listed languages.<br> - `false`: Other languages are also allowed to serve.<br><br>**Default**: `true` |
| `last_modified` | timestamp |**Read Only**. The date and time when the deal was last modified, in local time. |
| `media_preference` | string | Specifies how this deal handles media types/subtypes. There are two options:<br> - `standard` = use whatever media types are already on the auction (based on the placement settings)<br> - `append` = include the media types on the auction + any private media types set on the placement<br><br>If a deal is created from a package, this setting is copied from the package to the deal. |
| `name` | string (255) | The name of the deal.<br>**Default**: `null` |
| `package_id` | int | The package ID for the package from which the deal was created, if applicable. See [Deal From Package Service](./deal-from-package-service.md).<br><br>**Default**: `null` |
| `payment_type` | string | Specifies the payment type for the deal:<br> - `default`: This deal uses the default payment type for the buyer of this deal. Includes CPM and may also include CPA, CPC, or both.<br> - `cpvm`: This deal uses the Viewable CPM payment type. Only viewable impressions result in payment from the buyer.<br><br>**Default**: `default` |
| `priority` | int | The bidding priority for deals when `id` in the `type` object = `2`/Private Auction.<br>Possible values: `1` - `20`, where `20` is the highest priority.<br><br>**Default**: `5` |
| `profile_id` | int | The ID of the profile associated to the deal. You can use a profile to specify publishers, placements, content categories, geographical areas, segments, segment groups, or sizes that need to be involved in the auction in order for the deal to be available to the buyer. For more details, see `publisher_targets`, `placement_targets`, `content_category_targets`, `country_targets`, `region_targets`, `city_targets`, `dma_targets`, `segment_targets`, `segment_group_targets`, `site_targets`, and `size_targets` in the [Profile Service](./profile-service.md).<br><br>**Warning**: Any other targeting settings in the associated profile will not be respected.<br><br>**Default**: `null` |
| `seller` | object | **Read Only**. The selling member who is offering the deal. For more details, see [Seller](#seller) below. |
| `size_preference` | string | Specifies how this deal handles private sizes. Private sizes are placement sizes (set in the `private_sizes` array in the [Placement Service](./placement-service.md)) that can be allowed to serve for a deal. There are two options:<br> - `standard`: Private sizes are not available for this deal.<br> - `append`: Private sizes can be used in addition to the specified placement size.<br><br>If a deal is created from a package, this setting is copied from the package to the deal. |
| `start_date` | timestamp | The day and time when the deal starts being available to the buyer, in local time. If this is set, the format must be `"YYYY-MM-DD HH:MM:SS"`.<br><br>**Default**: `null` (immediately) |
| `technical_attributes` | array of objects | The technical attributes of creatives that are eligible for the deal. For more details, see [Technical Attributes](#technical-attributes) below. |
| `technical_attribute_restrict` | boolean | Specifies whether the deal is restricted only to the technical attributes listed in the [Technical Attributes](#technical-attributes) object.<br> - `true`: Deal is restricted only to the listed technical attributes.<br> - `false`: Other technical attributes are also allowed to serve.<br><br>**Default**: `true` |
| `type` | object | The type of deal. For sellers, a deal can be an open auction or a private auction. For more details, see [Type](#type) below. |
| `use_deal_floor` | boolean | If `true`, the `floor_price` is applied for the deal.<br><br>**Note**:<br> - When `use_deal_floor` is `true`, the deal's floor price overrides any other floors you may have, i.e., in placements or yield management profiles.<br> - As of 2017, only `ask_price` is used. API `POST` and `PUT` calls referencing `floor_price` and `use_deal_floor` will work as follows:<br> * If the API call includes `ask_price` only, this is the value that will be used.<br> * If the API call includes only a `floor_price` value, this value will be converted into the `ask_price` value.<br><br>**Default**: `true` |
| `version` | int | Specifies the version of the deal object. Possible values are:<br>`1` = External supply partner deals and legacy Monetize setups<br>`2` = Monetize seller deals<br><br>**Required On**: `POST`<br>**Default**: `1` |
| `visibility_profile_id` | int | The unique ID of the visibility profile that will be applied to a deal. This ID can be retrieved from the [Visibility Profile Service](./visibility-profile-service.md). |
| `line_item_ids` | array of int | A list consists of line items' IDs present in a deal. This array is filled when deal version is 2, otherwise this is a null array. This is a **read-only** field returned in a `GET` request. |
| `seller_targeting_restriction` | object | Indicates whether the deal restricts which attributes an Invest buyer can target whilst also targeting this deal. See [Seller Restricted Targeting](#seller-restricted-targeting) below. |

### Seller

The `seller` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int |  - **Read Only**.<br> - Seller's member ID<br>The member ID of the seller. |
| `name` | string |  - **Read Only**.<br> - Seller's member name<br>The member name of the seller. |

### Buyer

The buyer object can be set on a `POST`, but cannot be updated with a `PUT`. If you want to change the buyer, you need to create a new deal.

The `buyer` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The member ID of the buyer.<br>**Required On**: `POST` |
| `bidder_id` | int | **Read Only**. The bidder ID of the member. For buyers, this will always be `2`. |
| `name` | string | **Read Only**. The member name of the buyer. |

**Example of the `buyer` object**

```
"buyer": {
                "bidder_id": 2,
                "bidder_name": "Microsoft Invest",
                "id": 9155,
                "name": "Hearts & Science (AT&T)"
            },
"buyer_seats": null
```

### Buyer bidders

The `buyer_bidders` object can be set on a `POST`, and can be updated with a `PUT`. When a seller is enabled for multi-buyer deals. the `buyer_bidders` object can be set in combination with `buyer_seats` and `buyer_members`.

The `buyer_bidders` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_name` | string | **Read Only**. The name of the bidder. |
| `id` | int | The bidder ID of the buyer. The bidder ID is `2`.<br>**Required On**: `POST` |


**Example of the `buyer_bidders` object**

```
"buyer_bidders": [{
    "bidder_id": 1,
    "bidder_name": "Example Bidder"
}],
```

### Buyer members

The `buyer_members` object can be set on a `POST`, and can be updated with a `PUT`. When a seller is enabled for multi-buyer deals, the `buyer_members` object can be set in combination with `buyer_seats` and `buyer_bidders`.

The `buyer_members` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_id` | int | **Read Only**. The bidder ID of the member. For Invest buyers, this will always be `2`. |
| `bidder_name` | string | **Read Only**. The name of the bidder. |
| `id` | int | The member ID of the buyer.<br>**Required On**: `POST` |
| `name` | string | **Read Only**. The member name of the buyer. |

**Example of the `buyer_members` object**

```
"buyer_members": [{
    "bidder_id": 1,
    "bidder_name": "Example Bidder",
    "id": "456",
    "name": "Example Buyer Member"
}],
```

### Buyer seats

Deals with seats can be set up using the `buyer_seats` object via the API.

When a new deal is set up via  with, the API will be populated with the `buyer_seats` object. You can use the Invest buyer's member ID in the `code` field as well as `bidder_id`. New deals with external DSPs can also be set up with buyer seat IDs. You can check which external DSPs are using buyer seat IDs [here](../monetize/external-dsps-using-buyer-seat-ids.md).

> [!NOTE]
> - A deal can be set up with either `buyer` or `buyer_seats`, where `buyer` is a member, and `buyer_seats` is a seat.
> - When a seller has buyer seat deals enabled, all deals with will be set up using `buyer_seats` (when the deal is set up using , deals with the `buyer` field can still be set up using API).
> - `Code` is the seat code, in other words, the "seat ID" that the buyer will typically give. It's unique to a given `bidder_id`, so when creating a new deal, `code` and `bidder_id` are mandatory.

The `buyer_seats` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bidder_id` | int | The bidder ID of the member.<br>**Required On**: `POST` |
| `bidder_name` | string | The name of the bidder. |
| `code` | string | The identifier for the buyer seat.<br>**Required On**: `POST` |
| `name` | string | The name of buyer. |

**Example of the `buyer_seats` object**

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

### Type

The `type` object contains the following fields:

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID representing the type of deal. Possible values:<br>`1` = Open Auction<br>In an `"Open Auction"`, buyers targeting the deals and buyers targeting the inventory via other means compete for the impression. If a buyer targeting a deal submits the highest bid and the bid clears the deal's floor, that buyer wins the auction. If one of the non-deal buyers submits the highest bid, that buyer wins the auction instead. <br><br>`2` = Private Auction<br>In a `"Private Auction"`, buyers targeting the private deals compete for the impression first. Then, if none of the deal buyers win, the auction is opened to buyers targeting the inventory via other means. If a buyer targeting a deal submits a bid higher than the deal's floor and higher than any other private auction bids, that buyer wins the auction. If no private auction deals clear their floors, the highest bid in the open auction wins.<br><br>`4` = Programmatic Guaranteed<br>In `"Programmatic Guaranteed"`, buyers target Programmatic Guaranteed (PG) deals. PG deals bring the targeting, messaging, and reporting benefits of programmatic advertising to guaranteed media buys. They offer an automated solution for getting guaranteed access to media from publishers and provide an efficient approach that eliminates many of the additional steps required when buying via an insertion order.<br><br>`5` = Curated Auction<br>In a `"Curated Auction"`, buyers target supply across any seller members that the Curator Member has packaged together. Buyers targeting a curated deal are subject to the auction dynamics set by the underlying seller in the curated deal, which can be either an Open or Private auction type, depending on how the Curator has configured their deal.<br><br>**Default**: `1` |
| `name` | string (255) | **Read Only**. The name of the type of deal. Possible values:  <br> - `"Open Auction"` <br> - `"Private Auction"` <br> - `"Curated"` <br> - `"Programmatic Guaranteed"`<br><br>**Default**: `"Open Auction"` |

### Auction type

The `auction_type` object contains the following fields:

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the auction type:<br>`1` = First price<br>`2` = Standard price <br>`3` = Fixed price<br><br>**Default**: `2` |
| `name` | string | **Read Only**. The name of the auction type. Possible values: <br> - `"first_price"` <br> - `"standard_price"` <br> - `"fixed_price"`<br><br>**Default**: `"standard_price"` |

### Brands

Each `brands` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand that is eligible for the deal. You can use the [Brand Service](./brand-service.md) to retrieve brand IDs. |
| `name` | string | The name of the brand that is eligible for the deal. |
| `override` | boolean | Set to `true` to allow a brand to serve for a deal even if the ad quality profile would have blocked it.<br><br>**Default**: `false` |

### Allowed media types

You can use this array to limit the media type, the general display style of creatives, that can serve on placements that are part of this deal.

Each `allowed_media_types` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the media type.<br>**Required On**: `PUT` and `POST` |
| `last_modified` | date | When the `allowed_media_type` object was last updated. |
| `media_type_group_id` | int | The group ID for the media type. |
| `name` | string | The name of the allowed media type, for example `"Banner"`. |
| `uses_sizes` | enum | Whether the media type has size specifications. Possible values:<br> - `always`<br> - `sometimes`<br> - `never` |

### Allowed media subtypes

You can use this array to limit the media subtype, the specific display style of creatives, that can serve on placements that are part of this deal.

Each `allowed_media_subtypes` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the `allowed_media_subtype`. `PUT` and `POST` on JSON file |
| `last_modified` | date | When the `allowed_media_subtype` array was last modified. |
| `mediatype_id` | int | The ID of the `media_type`. |
| `media_type_group_id` | int | The ID of the group for the media type. |
| `media_type_name` | string | The name of the `media_type`. |
| `name` | string | The name of the `allowed_media_subtype`. |
| `native_assets` | array of objects | An array describing constraints on elements of native ads for this media subtype. Elements of a native ad can include the title, body content, and more. The format's constraints could be whether body content is required or recommended, or how long the text may be. For more information, see [Native Assets](#native-assets) below. |
| `permitted_sizes` | array of objects | The permitted sizes for creatives of the media subtype. See [Permitted Sizes](#permitted-sizes) below for more details.<br><br>**Note**: Not all media subtypes have permitted size requirements.<br><br>**Required On**: `PUT` and `POST` |

### Permitted sizes

Each `permitted_sizes` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `aspect_ratio_tolerance` | double | If `validate_image_size` and `scaling_permitted` are both `true`, the image can deviate from the aspect ratio of `platform_width` and `platform_height` by this amount. For example, the aspect ratio for a `platform_width` and `platform_height` of 254x133 is 1.19:1. If the `aspect_ratio_tolerance` is 0.03, an aspect ratio between 1.16:1 and 1.22:1 would be acceptable. |
| `max_image_height` | int | If `validate_image_size` is `true`, the maximum acceptable image height, in pixels, for creatives of this media subtype. |
| `max_image_width` | int | If `validate_image_size` is `true`, the maximum acceptable image width, in pixels, for creatives of this media subtype. |
| `min_image_height` | int | If `validate_image_size` is `true`, the minimum acceptable image height, in pixels, for creatives of this media subtype. |
| `min_image_width` | int | If `validate_image_size` is `true`, the minimum acceptable image width, in pixels, for creatives of this media subtype. |
| `platform_width` | int | The actual rendering width, in pixels, for creatives of this media subtype. This is also the width that appears in reporting. |
| `platform_height` | int | The actual rendering height, in pixels, for creatives of this media subtype. This is also the height that appears in reporting. |
| `scaling_permitted` | boolean | If `true`, the image for creatives of this media subtype must have the same aspect ratio as `platform_width`/`platform_height`.<br>If `false`, the image for creatives of this media subtype must have a width and height exactly matching `platform_width` and `platform_height`. |
| `validate_image_size` | boolean | If `true`, the image for creatives of this media subtype will be validated against the requirements defined by the following fields in this object: `scaling_permitted`, `aspect_ratio_tolerance`, `min_image_width`, `max_image_width`, `min_image_height`, and `max_image_height`. |

### External metadata

The `external_metadata` object is applicable for Programmatic Guaranteed deals.

Each `external_metadata` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `impressions` | int | The impression budget amount for external Programmatic Guaranteed deals. The numerical value for this field must be greater than 0.<br><br>**Note**: This field is required for Programmatic Guaranteed deals.<br>**Required On**: `PUT` and `POST` |

### Native assets

Each `native_assets` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `max_text_length` |  int | The maximum length for the text |
| `min_text_length` |  int | The minimum length for the text |
| `native_asset_name` | string | The title of the ad |
| `requirement` | enum  | Whether this asset is required by this particular media subtype. This field can contain several levels of "requiredness":<br> - `"required"`<br> - `"recommended"`<br> - `"optional"` |

### Categories

Each `categories` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the categories that is eligible for the deal. You can use the [Category Service](./category-service.md) to retrieve category IDs. |
| `name` | string | The name of the category that is eligible for the deal. |
| `override` | boolean | Set to `true` to allow a category to serve for a deal even if the ad quality profile would have blocked it.<br><br>**Default**: `false` |

### Languages

Each `languages` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the language that is eligible for the deal. You can use the [Language Service](./language-service.md) to retrieve language IDs. |
| `name` | string | The name of the language that is eligible for the deal. |
| `override` | Boolean | Set to `true` to allow a language to serve for a deal even if the ad quality profile would have blocked it.<br><br>**Default**: `false` |

### Technical attributes

Each `technical_attribute` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the technical attribute that is eligible for the deal. You can use the [Technical Attribute Service](./technical-attribute-service.md) to retrieve technical attribute IDs. |
| `name` | string | The name of the technical attribute that is eligible for the deal. |
| `override` | boolean | Set to `true` to allow a technical attribute to serve for a deal even if the ad quality profile would have blocked it.<br><br>**Default**: `false` |

### Creatives

The `creatives` array is limited to 100 creatives. Each `creatives` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the creative that is approved or banned for the deal. You can use the [Creative Service](./creative-service.md) to retrieve creative IDs. |
| `status` | string | Specifies how this creative will be handled for this deal.<br>- `approved`: This creative can always serve in this deal, regardless of any other ad quality settings or overrides.<br> - `banned`: This creative can never serve in this deal, regardless of any other ad quality settings or overrides. |

### Ad server lists

Each `adserver_lists` object contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the ad server list that will be applied to this deal.<br>**Required On**: `POST` |
| `name` | string | The name of the ad server list. |
| `override` | boolean | If `true`, apply this ad server list to the deal. |

### Seller restricted targeting

A deal can specify which attributes an Invest buyer is allowed to target whilst also targeting this deal. The options are:

- no restrictions - Invest buyers can target all attributes on their line item whilst targeting this deal.
- some restrictions - Invest buyers can target certain attributes on their line item.
- all restrictions - Invest buyers can target no other attributes whilst targeting this deal.

Your member may be configured to use one of these settings by default when new deals are created.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | Possible values are:<br> - `1` (no restrictions)<br> - `2` (some restrictions)<br> - `3` (all restrictions) |
| `name` | string | **Read Only**. The name of the configured targeting restrictions (see `id`). |

If a deal is configured for some restrictions, the visibility profile associated with the deal (see the `visibility_profile_id` field in the [JSON Fields](#json-fields) section) determines the selection of attributes a buyer can target. The following visibility profile fields may be used to restrict a buyer's allowed targeting:

| Field | Targeting restrictions for Invest buyers |
|:---|:---|
| `expose_city_default` | City |
| `expose_datetime_default` | Daypart |
| `expose_device_type_default` | Device Type |
| `expose_dma_default` | DMA |
| `expose_postal_code_default` | Postal code, postal code lists, political districts |
| `expose_segment_groups_default` | Segments |
| `expose_state_default` | Region |
| `expose_video_content_duration_default` | Video Content Duration (e.g. long-form, short-form) |
| `expose_video_content_genres_default` | Video Content Genres |
| `expose_video_content_networks_default` | Video Content Network |
| `expose_video_content_ratings_default` | Video Content Ratings |
| `expose_video_context_default` | Video Context (e.g. pre-roll, mid-roll, etc.) |
| `expose_video_delivery_types_default` | Video Delivery Type (e.g. live, VOD) |
| `expose_video_program_types_default` | Video Program Types |

> [!NOTE]
> - Any targeting restrictions defined with the fields above will be applied to all buyers on the deal regardless of any buyer member-level or bidder-level overrides configured on the visibility profile.
> - Also, sellers cannot simultaneously enable Data Protection (see the `data_protected` field in the [JSON Fields](#json-fields) section) and [Seller Restricted Targeting](#seller-restricted-targeting) features on the same deal.

## Examples

### Add a private auction deal with a floor of $2.50

```
$ cat new_deal
 
{
    "deal": {
        "name": "Private deal for buyer 1234 with floor of $2.50",
        "active": false,
        "start_date": "2016-12-01 00:00:00",
        "end_date": "2016-12-31 23:59:59",
        "floor_price": 2.5,
        "currency": "USD",
        "use_deal_floor": true,
        "buyer": {
                "id": 1234
        },
        "type": {
                "id": 2
        },
        "brands": [
                {
                        "id": 1
                }
            ]
    }
}
 
$ curl -b cookies -c cookies -X POST -d @new_deal.json 'https://api.appnexus.com/deal'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 63,
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 63,
            "code": null,
            "name": "Private deal for buyer 1234 with floor of $2.50",
            "description": null,
            "active": false,
            "seller_member_id": 2345,
            "start_date": "2013-12-01 00:00:00",
            "end_date": "2013-12-31 23:59:59",
            "profile_id": null,
            "package_id": null,
            "floor_price": 2.5,
            "currency": "USD",
            "use_deal_floor": true,
            "last_modified": "2013-12-04 20:39:57",
            "seller": {
                "id": 1066,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 1234,
                "bidder_id": 6,
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
            "ask_price": 0,
            "size_preference": null
        }
    }
}
```

### Add a private auction deal with no floor

```
$ cat new_deal_nofloor
 
{
    "deal": {
        "name": "Private deal for buyer 1234 with no floor",
        "active": false,
        "start_date": "2016-12-01 00:00:00",
        "end_date": "2016-12-31 23:59:59",
        "floor_price": 0,
        "use_deal_floor": false,
        "buyer": {
                "id": 1234
        },
        "type": {
                "id": 2
        },
        "brands": [
                {
                        "id": 1
                }
            ]
    }
}
 
$ curl -b cookies -c cookies -X POST -d @new_deal_nofloor.json 'https://api.appnexus.com/deal'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 64,
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 64,
            "code": null,
            "name": "Private deal for buyer 1234 with no floor",
            "description": null,
            "active": false,
            "start_date": "2013-12-01 00:00:00",
            "end_date": "2013-12-31 23:59:59",
            "profile_id": null,
            "package_id": null,
            "floor_price": 0,
            "currency": "USD",
            "use_deal_floor": false,
            "last_modified": "2013-12-04 20:43:44",
            "seller": {
                "id": 2345,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 1234,
                "bidder_id": 6,
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
            "ask_price": 0,
            "size_preference": null
        }
    }
}
```

### Modify a deal

In this example, we add another eligible brand to the deal and we extend the end date.

```
$ cat deal_update
 
{
    "deal": {
        "end_date": "2017-01-31 23:59:59",
        "brands": [
                {
                        "id": 1
                },
            {
                "id": 5
            }
            ]
    }
}
 
$ curl -b cookies -c cookies -X PUT -d @deal_update.json 'https://api.appnexus.com/deal?id=64'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "64",
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 64,
            "code": null,
            "name": "Private deal for buyer 1234 with no floor",
            "description": null,
            "active": false,
            "start_date": "2016-12-01 00:00:00",
            "end_date": "2016-01-31 23:59:59",
            "profile_id": null,
            "package_id": null,
            "floor_price": 0,
            "currency": "USD",
            "use_deal_floor": false,
            "last_modified": "2016-12-04 20:51:35",
            "seller": {
                "id": 2345,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 1234,
                "bidder_id": 6,
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
                },
                {
                    "id": 5,
                    "name": "Another Brand"
                }
            ],
            "ask_price": 0,
            "size_preference": null
        }
    }
}
```

### Modify a deal to add overrides and ban certain creatives

In this example, we update a deal to allow user- and auto-initiated audio creatives to always serve regardless of ad quality settings. We also specifically ban two creative IDs.

```
$ cat deal_override
 
{
    "deal": {
        "id": 201,
        "technical_attributes": [
            {
                "id": 7,
                "name": "Audio: user-initiated",
                "override": true
            },
            {
                "id": 8,
                "name": "Audio: auto-initiated",
                "override": true
            }
        ],
        "creatives": [
            {
                "id": 987654,
                "status": "banned"
            },
            {
                "id": 123456,
                "status": "banned"
            }
        ]
    }
}
 
$ curl -b cookies -c cookies -X PUT -d @deal_override.json 'https://api.appnexus.com/deal?id=64'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "64",
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 201,
            "code": null,
            "name": "Private deal for buyer 1085 with no floor",
            "description": null,
            "active": false,
            "start_date": "2016-12-01 00:00:00",
            "end_date": "2017-01-31 23:59:59",
            "profile_id": null,
            "package_id": null,
            "floor_price": 0,
            "currency": "USD",
            "use_deal_floor": false,
            "last_modified": "2016-12-04 20:51:35",
            "seller": {
                "id": 2345,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 1234,
                "bidder_id": 6,
                "name": "Buyer 456"
            },
            "type": {
                "id": 2,
                "name": "Private Auction"
            },
            "technical_attributes": [
                {
                    "id": 7,
                    "name": "Audio: user-initiated",
                    "override": true
                },
                {
                    "id": 8,
                    "name": "Audio: auto-initiated",
                    "override": true
                }
            ],
            "creatives": [
                {
                    "id": 987654,
                    "status": "banned"
                },
                {
                    "id": 123456,
                    "status": "banned"
                }
            ],
            "ask_price": 0,
            "size_preference": null
        }
    }
}
```

### View all deals you have with buyers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal'
{
    "response": {
        "status": "OK",
        "count": 7,
        "start_element": 0,
        "num_elements": 100,
        "deals": [
            {
                "id": 63,
                "code": null,
                "name": "Private deal for buyer 1234 with floor of $2.50",
                "description": null,
                "active": false,
                "seller_member_id": 2345,
                "start_date": "2016-12-01 00:00:00",
                "end_date": "2016-12-31 23:59:59",
                "profile_id": null,
                "package_id": null,
                "floor_price": 2.5,
                "currency": "USD",
                "use_deal_floor": true,
                "last_modified": "2016-12-04 20:39:57",
                "seller": {
                    "id": 2345,
                    "name": "Seller 123"
                },
                "buyer": {
                    "id": 1234,
                    "bidder_id": 6,
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
                "ask_price": 3,
                "size_preference": null
            },
            {
                "id": 64,
                "code": null,
                "name": "Private deal for buyer 1234 with no floor",
                "description": null,
                "active": false,
                "start_date": "2016-12-01 00:00:00",
                "end_date": "2016-12-31 23:59:59",
                "profile_id": null,
                "package_id": null,
                "floor_price": 1.2,
                "currency": "USD",
                "use_deal_floor": false,
                "last_modified": "2016-12-04 20:43:44",
                "seller": {
                    "id": 2345,
                    "name": "Seller 123"
                },
                "buyer": {
                    "id": 1234,
                    "bidder_id": 2,
                    "name": "Buyer ABC"
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
                "ask_price": 0,
                "size_preference": null
            }
        ]
    }
}
```

### View a specific deal

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal?id=64'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "deal": {
            "id": 64,
            "code": null,
            "name": "Private deal for buyer 1234 with no floor",
            "description": null,
            "active": false,
            "start_date": "2016-12-01 00:00:00",
            "end_date": "2017-01-31 23:59:59",
            "profile_id": null,
            "package_id": null,
            "floor_price": 1,
            "currency": "USD",
            "use_deal_floor": false,
            "last_modified": "2016-12-04 20:51:35",
            "seller": {
                "id": 2345,
                "name": "Seller 123"
            },
            "buyer": {
                "id": 1234,
                "bidder_id": 2,
                "name": "Buyer ABC"
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
                {
                    "id": 5,
                    "name": "Another Brand"
                }
            ],
            "ask_price": 1.25,
            "size_preference": null
        }
    }
}
```

### Delete a deal

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/deal?id=61'
{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```
