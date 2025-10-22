---
title: TinyTag Service
description: Learn how TinyTag Service enables you to create TinyTag IDs as well as modify and view them. This page also covers how TinyTag IDs can be used in TinyTags, which are placed directly on publisher pages.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# TinyTag service

The TinyTag Service enables you to create TinyTag IDs as well as modify and view them.

The IDs are associated with information about the ad space such as size, reserve price, and what brands or creatives are allowed to run in that space. This information is stored server side with Xandr and is easy to modify.

TinyTag IDs can be used in TinyTags, which are placed directly on publisher pages and take the basic form `https://ib.``adnxs``.com/tt?id=1`. Further information can be passed in a TinyTag using [Dynamic TinyTag Parameters](dynamic-tinytag-parameters.md).

Note that the member associated with the TinyTag ID has rights of first refusal on the inventory, and receives credit (or cash) if another member purchases it.

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| DELETE | [https://api.adnxs.com/tt/MEMBER_ID/TAG_ID](https://api.adnxs.com/tt/MEMBER_ID/TAG_ID) | Delete an existing TinyTag. |
| GET | [https://api.adnxs.com/tt/MEMBER_ID](https://api.adnxs.com/tt/MEMBER_ID) | View all TinyTags for a member. |
| GET | [https://api.adnxs.com/tt/MEMBER_ID/TAG_ID](https://api.adnxs.com/tt/MEMBER_ID/TAG_ID) | View a particular TinyTag. |
| POST | [https://api.adnxs.com/tt/MEMBER_ID](https://api.adnxs.com/tt/MEMBER_ID) <br> (tag JSON) | Create a new TinyTag. |
| PUT | [https://api.adnxs.com/tt/MEMBER_ID/TAG_ID](https://api.adnxs.com/tt/MEMBER_ID/TAG_ID) <br> (tag JSON) | Modify an existing TinyTag. |

## JSON fields

| Field | Required | Type | Description |
|--|--|--|--|
| `acb_code` | no | string(32) | Not commonly used. |
| `active` | no, default is active | int | Boolean value determines whether the segment can be used |
| `ad_profile_id` | no | int | This is the ID of the [ad approval profile](ad-profile-service.md) used for creative quality standards. |
| `audit_level` | no | enum | Values for self-auditing only. <br> **Note**:  Self-audits at the site level can be overridden at the placement (tinytag) level. <br> Possible values: <br> - "tinytag" - Use this value if the audited field is set to true in the placement. <br> - "site" - Use this value if the audited field is set to false in the placement but true in the site. |
| `audited` | no | boolean | If true, the placement has been self-audited by the owner. |
| `code` | no | string(100) | User-defined field for calling tag via codes. More info can be found on the [Tinytag Page](tinytags.md). |
| `code2` | no | string(100) | Second code, if desired. |
| `content_retrieval_timeout_ms` | no | int | <br> - If `0`, the ad server uses the value from the [Member Service](member-service.md). <br> - Defaults to `0` if not provided to the API on `PUT` or `POST` calls. <br> - If ad server reads a 0 in this field, it performs a member lookup and use the default timeout defined by the [Member Service](member-service.md) (assuming it's also non-zero). <br> - When creating a TinyTag, none of the values are copied into this field from the member's default settings. You must explicitly specify them in your calls to `POST`. For more information, see the `default_content_retrieval_timeout_ms` field of the [Member Service](member-service.md). |
| `default_calculation_type` | no | enum | This determines the bid price threshold below which a default creative is served. You can choose whether this threshold is the network's gross revenue or the publisher's net revenue. If there are no additional eligible campaigns, nor any default creatives available, a PSA is served. Possible values: "gross" or "net". |
| `default_creative_id` | no | int | The default creative to run if no bids meet the reserve price. |
| `default_creatives` | no | array | The default creatives that display instead of a PSA when there is no auction winner. For each default creative, the reserve price is set with the "price" field in the array. See [Default Creatives](#default-creatives) below for more details. <br> **Note**: For pops placements: The placement does not pop if the reserve price is not met, except in the case of a prepop. |
| `default_referrer_url` | no | string | If a visibility profile is set to hide inventory urls in your bid requests, you can set this field to pass a vanity url instead. This is particularly useful in cases where publishers do not want to share actual domains but nonetheless want buyers to be able to identify them by domain. Note, however, that the vanity domain cannot be targeted directly by Xandr campaigns, although it can be targeted by external bidders. |
| `enable_for_mediation` | no | boolean | - This is the source of truth for whether a TinyTag should accept mediated content <br> - Unless set on `PUT` or `POST`, this field inherits its default value from the member. If the default value is changed on the [Member Service](member-service.md), that action does not retroactively impact TinyTags created previously; they continue to be set to the old default value. In other words, the value of this field cannot be updated retroactively by setting the member default. For more information, see the `default_enable_for_mediation` field of the [Member Service](member-service.md). |
| `estimated_clear_prices` | no |  | The bid amount that has historically won the majority (95%) of the 3rd party auctions in which it participates. See [Estimated Clear Price](#estimated-clear-prices) below for more details. |
| `exclusive` | no, default is false | boolean | **Read-only**. This field has been **Deprecated**. This field formerly served as the default value for the exclusive behavior on a TinyTag. This setting is now controlled via the `rtb` field in the `marketplace_map` object of the `site` service. |
| `floor_application_target` | no | enum | The type of bids to which the reserve price is applied. Possible values: <br> -"external_only" - The reserve price is applied only to external bids (buying member and selling member are different). Use this option if you would rather serve an available managed learn impression than serve a default, even if this means exceeding the maximum % of daily volume for learn. <br> - "external_non_preferred" - The reserve price is applied to external bids (buying member and selling member are different) or when the impression is an available managed learn impression that exceeds the maximum % of daily volume for learn. Use this option if you would rather serve a default than serve an available managed learn impression that would exceed the maximum % of daily volume for learn. <br> - "all" - The reserve price is applied to all bids except managed learn impressions within the maximum % of daily volume for learn. |
| `height` | no | int | The height of the tag in pixels. |
| `hide_referer` |  | boolean | Do not display the referer page. |
| `id ` | no, only on modify | int | Xandr ID assigned by the API to reference this tag. |
| `intended_audiences` | no | enum | Values for self-auditing only. Possible values: "general", "children", "young_adult", or "mature". |
| `inventory_attributes` | no | array | Values for self-auditing only. This is an array of objects with IDs. Please see the [Inventory Attribute Service](inventory-attribute-service.md) for a list of IDs. |
| `is_resizable` | no | boolean | If the placement uses a friendly iFrame and you want the placement to resize to fit smaller or larger creatives, set this field to true. |
| `last_activity` | no | timestamp | The timestamp of last modification to this tiny tag. |
| `media_subtypes` | no | enum | **Deprecated**. Please use supported_media_types and supported_media_subtypes instead. |
| `member_id` | yes | int | The member ID that owns this tag. Required for call, but not JSON. |
| `name` | no | string | Name associated with the TinyTag |
| `pixel_type` | no | enum | Identifies the type of pixel. Possible values are "script" or "image". |
| `pixel_url` | no | string | The location that the pixel notifies when a user clicks on that placement. |
| `pixel_url_secure` | no | boolean | Indicates whether the pixel URL points to an encyrpted web page. |
| `pop_values` | no | array | If the supported_media_type is "Pop", or the supported_media_subtypes is "Popup" or "Popunder", this array defines the behavior of the pop. See [Pop Values](#pop-values) below for more details. |
| `position` | no | enum | "above", "below", or "unknown" - the position of the TinyTag relative to the page fold |
| `publisher_id` | no | int | The ID of the publisher associated with the site that the tag is on. |
| `reserve_price` | no, default is $0 | double | The reserve price of the ad in $CPM - This is the lowest price that inventory owner is willing to sell for, otherwise the default creative is served.<br> **Note** : this field is listed as "price" in the /meta listing. |
| `segments` | no | Array of objects | A user viewing this TinyTag is placed into all of the specified segments Example: `"segments": [ {"segment_id":1} ]` |
| `site_id` | yes | int | The ID of the site that the tag is associated with. The hierarchy is **Sites** > **Tags**. For more information about the Site Service, make a `GET` call to [https://api.adnxs.com/site/meta](https://api.adnxs.com/site/meta). |
| `supported_media_subtypes` | no | array | The media subtypes that are allowed to serve on the placement. See [Supported Media Subtypes](#supported-media-types) below for more details. |
| `supported_media_types` | no | array | The media types that are allowed to serve on the placement. See [Supported Media Types](#supported-media-types) below for more details. |
| `tag_data` | no | string | Other information, often demographic or descriptive data. Sent only to the owner's bidder. See also qs_data in [TinyTags](tinytags.md). <br> **Note**: this field is listed as "other_data" in the /meta listing. |
| `use_detected_domain` | no, default is true. | boolean | **Read-only**. Whether to use the detected domain versus the reported domain. Defaults to true for all clients. |
| `visibility_profile_id` | no | int | The ID of the visibility profile assigned directly to the placement. |
| `width` | no | int | The width of the tag in pixels. |

### Supported media types

Creatives are categorized by media type and media subtype. Media type defines the general display style of the creative, for example, "Banner", and media subtype defines the specific display style of creatives, for example, "Standard Banner" or "In-Banner Video". You can use this array to limit the media type, the general display style of creatives, that can serve on a placement. To limit the media subtype, the specific display style of creatives, use the supported_media_subtypes array (see [Supported Media Subtypes](#supported-media-subtypes) below).

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the allowed media subtype. |
| `name` | string | **Read-only**. The name of the allowed media subtype. |

### Supported media subtypes

Creatives are categorized by media type and media subtype. Media type defines the general display style of the creative, for example, "Banner", and media subtype defines the specific display style of creatives, for example, "Standard Banner" or "In-Banner Video". You can use this array to limit the media subtype, the specific display style of creatives, that can serve on a placement. To limit the media type, the general display style of creatives, use the supported_media_types array (see [Supported Media Subtypes](#supported-media-subtypes) above).

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the allowed media subtype. |
| `name` | string | **Read-only**. The name of the allowed media subtype. |

**Notes on Supported Media Types and Media Subtypes**

- If you do not specify either supported media types or supported media subtypes, the "Banner" media type is allowed by default.

- You can combine the "Banner" and "Text" media types, and any combination of their media subtypes, on a single placement, but you cannot combine any of the other media types and media subtypes. This limitation ensures that only appropriate creatives are served on a placement. For example, a placement that allows creatives of the media type "Video" is intended to be fed to a video player; it would not make sense to allow creatives of any other media type, such as "Interstitial", to serve on the placement.

- You can set a placement to allow the "Expandable" media type or any of its subtypes for direct inventory. If you want to support expandable creatives for placements that are available for reselling to other platform members, please provide the URL to [support](https://support.ads.microsoft.com) for verification.

### Default Creatives

You use this array to assign default creatives to the placement. Please note the following requirements:

- A default creative must not be expired. See the is_expired field in the Creative Service for more information.
- A default creative must be assigned to a creative template that matches the supported_media_types and supported_media_subtypes of the placement. For example, if the placement allows creatives of the "Banner" media type, you would not be able to associate default creatives that use a creative template for the "Interstitial" media type. See the template field in the [Creative Service](creative-service.md) for more information.
- If the placement is sized (the "width" and "height" fields are defined for the placement), this array should contain only one creative with the matching dimensions.

| Field | Type | Description |
|--|--|--|
| `height` | int | The height of the default creative. |
| `id` | int | The ID of the default creative. |
| `name` | string | **Read-only**. The name of the default creative. |
| `price` | double | The reserve price for the default creative. A winning bid must be above this price. |
| `width` | int | The width of the default creative. |

### Pop values

If the supported_media_type is "Pop", or the supported_media_subtypes is "Popup" or "Popunder", these fields should be included in the "pop_values" array. Please see below for an example.

| Field | Type | Description | Default |
|--|--|--|--|
| pop_freq_duration | int | See pop_freq_times. | No frequency cap |
| pop_freq_times | int | Number of times that the tag can be popped to a unique user in pop_frequency_duration seconds. Has no effect when pop_is_prepop is set to true. | No frequency cap |
| pop_is_prepop | boolean | If true, the tag is a prepop tag and serves into a window that the publisher page has already popped. | false |
| pop_max_height | int | The max height of the creative. If pop_max_height is specified, any creative shown by the tag must have a height equal to or smaller than pop_max_height | no max height |
| pop_max_width | int | If pop_max_width is specified, any creative shown by the tag must have a width equal to or smaller than pop_max_width | no max width |

### Estimated clear prices

| Field | Type | Description |
|--|--|--|
| average_price | double | This is the average of all bids submitted for this placement. |
| clear_price | int | The bid amount that has historically won the majority (95%) of the 3rd party auctions in which it participates for this placement. |
| height | int | When exporting sizeless placement tags to be served, this determines the height of the placement. |
| verified | boolean | Indicates whether the created prices are verified. |
| width | int | When exporting sizeless placement tags to be served, this determines the width of the placement. |

## Example

### Step 1. Create a JSON-formatted file with the relevant parameters

``` 
$ cat tag
 {
     
"tinytag": 
{
         
"width": "728",
         
"height": "90",
         
"reserve_price": "5.00",
         
"default_creative_id": 212,
         
"active": true,
         
"tag_data": "male/22",
         
"ad_profile_id": 234
     }
 }
```

### Step 2. Add the TinyTag file to the Imp Bus cache using your member ID

``` 
$ curl -b cookies -c cookies -X POST --data-binary @tag https://api.adnxs.com/tt/1/
{
    "response": {
        "status": "OK",
        "id": "1234"
    }
}
```

### Step 3. View the tag you have created using the tag ID `1234`

$ curl -b cookies -c cookies [https://api.adnxs.com/tt/1/1234](https://api.adnxs.com/tt/1/1234)

```

$ curl -b cookies -c cookies [adnxs.com/tt/1/1234](https://api.adnxs.com/tt/1/1234)

{
    "response": {
        "tinytag": {
            "id": 1234,
            "width": "728",
            "height": "90",
            "member_id": 1,
            "reserve_price": 5.00,
            "default_creative_id": 212,
            "tag_data": "male\/22",
            "active": true,
            "ad_profile_id": 234
        },
        "status": "OK"
    }
}
```

## Related topics

- [TinyTags](tinytags.md)
- [Dynamic TinyTag Parameters](dynamic-tinytag-parameters.md)