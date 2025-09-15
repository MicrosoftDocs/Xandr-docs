---
title: Placement Service
description: Use the Placement service to create and modify ad tags for managed publishers or direct media buys with customizable IDs stored server-side.
ms.date: 09/15/2025
ms.custom: digital-platform-api
---

# Placement service

The Placement Service enables you to create placement ad tags as well as modify and view them. You will use placements for managed publishers or for direct media buys.

- Placement IDs and their associated information are stored server-side with Xandr and are easy to modify.
- When you create a placement, you specify the types of creatives that are allowed to serve on it (see `supported_media_types` and `supported_media_subtypes` below).

> [!NOTE]
> Targeting of advertisers, line items, or campaigns via this service will override any targeting defined by the [Payment Rule Service](./payment-rule-service.md).

## Tag format

Once you have the placement ID, you format the placement tag as follows and hand it to the publisher you represent or with whom you have a guaranteed buy.

> [!NOTE]
> `"id"` is the placement ID.
> [!TIP]
> You can include placeholders to pass in additional query string parameters to our platform during the ad call.
> [!IMPORTANT]
> When serving your placement tags on secure inventory (SSL), you should alter the below tags to use the host: `"https://secure.adnxs.com/..."`

### IFRAME

```
<!-- BEGIN IFRAME TAG < - DO NOT MODIFY -->
<IFRAME SRC="https://ib.adnxs.com/tt?id=2704"
    FRAMEBORDER="0"
    SCROLLING="no"
    MARGINHEIGHT="0"
    MARGINWIDTH="0"
    TOPMARGIN="0"
    LEFTMARGIN="0"
    ALLOWTRANSPARENCY="true"
    WIDTH="120"
    HEIGHT="600"></IFRAME>
<!-- END TAG -->
```

### JavaScript

```
<!-- BEGIN JS TAG < - DO NOT MODIFY -->
<SCRIPT SRC="https://ib.adnxs.com/ttj?id=2704" TYPE="text/javascript"></SCRIPT>
<!-- END TAG -->
```

## REST API

> [!NOTE]
> The `code`, `placement_code`, `site_code`, and `publisher_code` can be used in place of the corresponding IDs in the calls below.

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` |`https://api.appnexus.com/placement?publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/placement?site_id=SITE_ID`<br>(placement JSON) | Add a placement (NETWORK). |
| `PUT` | `https://api.appnexus.com/placement?id=PLACEMENT_ID&publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/placement?code=PLACEMENT_ID&site_id=SITE_ID`<br>(placement JSON) | Modify an existing placement (NETWORK). |
| `DELETE` | `https://api.appnexus.com/placement?id=PLACEMENT_ID&publisher_id=PUBLISHER_ID`<br><br>`https://api.appnexus.com/placement?code=PLACEMENT_CODE&publisher_code=PUBLISHER_CODE` | Delete an existing placement. |
| `GET` | `https://api.appnexus.com/placement?publisher_id=PUBLISHER_ID` | View all of the placements for one of your publishers. |
| `GET` | `https://api.appnexus.com/placement?id=PLACEMENT_ID` | View a specific placement for one of your publishers. |
| `GET` | `https://api.appnexus.com/placement?id=1,2,3` | View all placements for a site. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the placement.<br><br>**Default**: Auto-incremented number (i.e. 123)<br>**Required On**: `PUT`, in query string |
| `name` | string (100) | The name of the placement.<br><br>**Required On**: `POST` |
| `code` | string (100) | The custom code for the placement.<br><br>**Note**: Codes must be alphanumeric and cannot contain spaces. The following characters are also permitted:<br> - period (".")<br> - underscore ("_")<br> - hyphen ("-")<br> - percent ("%") |
| `code2` | string (100) | The second custom code for the placement.<br><br>**Note**: Codes must be alphanumeric and cannot contain spaces. The following characters are also permitted:<br> - period (".")<br> - underscore ("_")<br> - hyphen ("-")<br> - percent ("%") |
| `code3` | string (100) | The third custom code for the placement.<br><br>**Note**: Codes must be alphanumeric and cannot contain spaces. The following characters are also permitted:<br> - period (".")<br> - underscore ("_")<br> - hyphen ("-")<br> - percent ("%") |
| `state` | enum | The state of the placement. Possible values: `"active"` or `"inactive"`.<br><br>**Default**: `"active"` |
| `width` | int | The width of the placement. |
| `height` | int | The height of the placement. |
| `is_resizable` | Boolean | If the placement uses a friendly iFrame and you want the placement to resize to fit smaller or larger creatives, set this field to `true`.<br><br>**Default**: `false` |
| `default_position` | enum | The default position of the placement on the page. Possible values:  - `"above"` (above the fold) <br> `"below"` (below the fold) <br>`"unknown"`<br><br>**Default**: `"unknown"` |
| `publisher_id` | int | The ID of the publisher associated with the placement.<br><br>**Required On**: `POST` |
| `publisher_name` | string (100) | The name of the publisher associated with the placement. |
| `site_id` | int | The ID of this placement's parent site. Each placement must belong to a site.<br><br>**Default**: Site of publisher |
| `site_name` | string (100) | The name of the site on which the placement is used. |
| `inventory_source_id` | int | **Deprecated**. |
| `ad_profile_id` | int | The ID of the ad profile associated with the placement.<br><br>**Note**: The preferred way to "assign" an ad profile to a placement is as follows: Create an Ad Quality Rule with a targeting profile (the profile "targets" the placement). Link the Ad Profile to the Ad Quality Rule. Assign the Ad Quality Rule to the publisher. That way you can enjoy a greater flexibility using the targeting profile. |
| `supported_media_types` | array of objects | The media types that are allowed to serve on the placement. See [Supported Media Types](#supported-media-types) below for more details. <br><br>**Attention**: If you do not specify either `supported_media_types` or `supported_media_subtypes`, the `"Banner"` media type and all of its subtypes will be allowed by default. |
| `supported_media_subtypes` | array of objects | The media subtypes that are allowed to serve on the placement. See [Supported Media Subtypes](#supported-media-subtypes) below for more details. |
| `pop_values` | array | **Deprecated**. |
| `default_creative_id` | int | **Deprecated**. Please use `default_creatives` instead. |
| `default_creatives` | array | The default creatives that will be displayed instead of a PSA when there is no auction winner. For each default creative, the reserve price is set with the `"price"` field in the array. See [Default Creatives](#default-creatives) below for more details.<br><br>**Note**: The placement will not pop if the reserve price is not met, except in the case of a prepop. |
| `reserve_price` | double | The reserve price for each of the placement's default creatives is set in the `default_creatives` array (see [Default Creatives](#default-creatives) below). If the placement does not have default creatives, a reserve price can be set here for the placement; this is not best practice, however, as the reserve price may cause the display of a PSA. <br><br>**Important**: A Yield Management Profile will supersede any reserve price settings at the Placement level. If you have such a profile, you must set your desired reserve price via a hard floor. |
| `hide_referer` | Boolean | If `true`, the referrer will not be reported. |
| `default_referrer_url` | string | If a [Visibility Profile](./visibility-profile-service.md) is set to hide inventory URLs in your bid requests, you can set this field to pass a vanity URL instead. This is particularly useful in cases where publishers do not want to share actual domains but nonetheless want buyers to be able to identify them by domain. |
| `visibility_profile_id` | int | The ID of the visibility profile assigned directly to the placement. For more details about visibility profiles, see the [Visibility Profile](./visibility-profile-service.md). |
| `exclusive` | Boolean | **Read-only**.<br>To designate whether a placement's inventory is to be made available for resale, use the `rtb` field in the `marketplace_map` object of the placement's site. See [Site Service](./site-service.md) for a description of this field. All inventory made available for resale is part of the RTB Marketplace.<br><br>**Default**: `False` |
| `pixel_url` | string | Piggyback call upon user loading placement.<br><br>**Default**: `null` |
| `pixel_type` | enum | Identifies the type of pixel. Possible values are `"javascript"` or `"image"`.<br><br>**Default**: `image` |
| `content_categories` | array | A list of Content Categories associated with this placement. At most 20 categories can be specified for a placement. |
| `filtered_advertisers` | array | A list of advertisers that are allowed to target the placement. |
| `filtered_line_items` | array | A list of line items that are allowed to target the placement. |
| `filtered_campaigns` | array | A list of campaigns that are allowed to target the placement. |
| `segments` | array | A list of segments that users will be added to upon viewing this placement. |
| `estimated_clear_prices` | array of objects | The bid amount that has historically won the majority (95%) of the 3rd party auctions in which it participates. See [Estimated Clear Prices](#estimated-clear-prices) below for more details. |
| `media_subtypes` | array | **Deprecated**. Please use `supported_media_types` and `supported_media_subtypes` instead. |
| `intended_audience` | enum | Values for self-auditing only. Possible values: <br> - `"general"` <br> - `"children"` <br> - `"young_adult"` <br> - `"mature"` |
| `inventory_attributes` | array | The sensitive attributes contained by the placement.<br><br>**Tip**: The `inventory_attributes` can also be applied at the site level, and in this case will influence objects at the placement level, as well. This is an array of objects with IDs. Please see the [Inventory Attribute Service](./inventory-attribute-service.md) for a list of IDs. |
| `audited` | Boolean | If `true`, the placement has been self-audited by the owner.<br><br>**Default**: `false` |
| `audit_level` | enum | Values for self-auditing only.<br><br>**Note**: The self-audits at the site level can be overridden at the placement level. Possible values:<br> - `"site"` - Use this value if the `audited` field is set to `false` in the placement but `true` in the site.<br> - `"placement"` - Use this value if the `audited` field is set to `true` in the placement.<br><br>**Default**: `"site"` |
| `default_calculation_type` | enum | This determines the bid price threshold below which a default creative will be served. You can choose whether this threshold is the network's gross revenue or the publisher's net revenue. If there are no additional eligible campaigns, nor any default creatives available, a PSA is served. Possible values: `"gross"` or `"net"`.<br><br>**Default**: `"gross"` |
| `apply_floor_to_direct` | Boolean | **Removed**. Please use `floor_application_target` instead. |
| `demand_filter_action` | string | Indicates demand sources which can be included or excluded.<br><br>**Default**: `default` |
| `floor_application_target` | enum | The type of bids to which the reserve price is applied. Possible values:<br> - `"external_only"` - The reserve price is applied only to external bids (buying member and selling member are different). Use this option if you would rather serve an available managed learn impression than serve a default, even if this means exceeding the maximum % of daily volume for learn (`max_learn_pct` field in [Publisher Service](./publisher-service.md)).<br> - `"external_non_preferred"` - The reserve price is applied to external bids (buying member and selling member are different) or when the impression is an available managed learn impression that exceeds the maximum % of daily volume for learn. Use this option if you would rather serve a default than serve an available managed learn impression that would exceed the maximum % of daily volume for learn.<br> - `"all"` - The reserve price is applied to all bids except managed learn impressions within the maximum % of daily volume for learn.<br><br>**Default**: `"all"` |
| `pixel_url_secure` | string | Secure piggyback call upon user loading placement.<br><br>**Default**: `null` |
| `site_audit_status` | enum | Indicates how the site has decided to perform creative audits. Possible values are `"self"` or `"unaudited"`.<br><br>**Default**: `unaudited` |
| `toolbar` | object | Sellers must declare all toolbar and browser-plugin inventory. If a seller assigns the "toolbar" inventory attribute, this additional meta data must also be included. |
| `acb_code` | string (32) | **Deprecated**. |
| `tag_data` | string | **Deprecated**. |
| `cost_cpm` | double | If a value exists, it will be used as the payment information for the placement. This will override any payment rules associated with the publisher.<br><br>**Default**: `null` |
| `is_prohibited` | Boolean | **Read-only**. If `true`, the placement has been prohibited due to violation of Xandr content policies. Direct and third-party auctions will not be run for a prohibited placement.<br><br>**Default**: `false` |
| `last_modified` | timestamp | **Read-only**. The date and time when the placement was last modified. |
| `stats` | object | The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](./report-service.md) to obtain statistical information instead. |
| `content_retrieval_timeout_ms` | int | The timeout this placement will set on content retrieved from "mediated" creatives, i.e., creatives whose `content_source` is set to `"mediation"`. For more information, see the [Creative Service](./creative-service.md). <br> - If set to `0`, the ad server will use the value from the [Member Service](./member-service.md)<br>- Defaults to `0` if not provided to the API on `PUT` or `POST` calls.<br>- If ad server reads a `0` in this field, it will perform a member lookup and use the default timeout defined by the [Member Service](./member-service.md) (assuming it's also non-zero).<br> - When creating a placement, no values will be copied into this field from the member's default settings. You must explicitly specify them in your calls to `POST`. For more information, see the `default_content_retrieval_timeout_ms` field of the [Member Service](./member-service.md).<br><br>**Default**: `0` |
| `enable_for_mediation` | Boolean | This will be the source of truth for whether a placement should accept mediated content. Unless set on `PUT` or `POST`, this field will inherit its default value from the member. If the default value is changed on the [Member Service](./member-service.md), that action will not retroactively impact placements created previously; they will continue to be set to the old default value. In other words, the value of this field cannot be updated retroactively by setting the member default. For more information, see the `default_enable_for_mediation` field of the [Member Service](./member-service.md).<br><br>**Default**: Inherited from `default_enable_for_mediation` field of the [Member Service](./member-service.md). |
| `private_sizes` | array of objects | The list of placement sizes that may be allowed to serve in deals and packages. See [Private Sizes](#private-sizes) below for more details. |
| `video` | object | The media subtype allowed to serve on the placement. See [Video Settings](#video-settings) below for more details.<br><br>**Default**: `null` |
| `ad_types` | array of objects | Contains information relating to placement types, including the ad type ID and information about the renderer. For more information, see [Ad Types](#ad-types) below.<br><br>**Default**: `null`<br>**Required On**: `PUT` |
| `use_detected_domain` | boolean | **Read-only**. Whether to use the detected domain versus the reported domain. Defaults to `true` for all clients.<br><br>**Default**: `true` |
| `mime_types` | array of strings | The list of mime types to include or exclude on the placement. `supported_mime_types_action_include` below is used to specify whether to include or exclude those mime types. For a list of the strings used to identify each mime types, see [Supported Mime Types](#supported-mime-types).<br><br>**Default**: `empty` |
| `supported_mime_types_action_include` | boolean | If `true`, the mime types listed in the `mime_types` array will be included.<br><br>**Default**: `false` |
| `handles_mixed_media` | boolean | This tells our platform whether the video player can support a VAST file with different mime types.<br><br>**Default**: `true` |
| `tinytag_renderer_asset_floor_prices` | array of objects | Associates floor prices to native creatives that have been assigned to the placement. For additional information, see [Tinytag Renderer Asset Floor Prices](#tinytag-renderer-asset-floor-prices).<br><br>**Required On**: `PUT` |
| `is_ss_native_assembly_enabled` | boolean | When enabled, although the original request will be a banner request, the requests that are sent to bidders will have native info set in order to receive native assets back in the responses. The final response will be set back to a banner ad type with a native assembled ad markup attached. If `true` then yes. |

### Supported media types

Creatives are categorized by media type and media subtype. Media type defines the general display style of the creative, for example,
`"Banner"`, and media subtype defines the specific display style of creatives, for example, `"Standard Banner"` or `"In-Banner Video"`. You can use this array to limit the media type, the general display style of creatives, that can serve on a placement. To limit the media subtype, the specific display style of creatives, use the `supported_media_subtypes` array (see [Supported Media Subtypes](#supported-media-types) below).


| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the allowed media type. You can use the [Media Type Service](./media-type-service.md) to view all media types.<br><br>**Default**: `1` |
| `name` | string | The name of the allowed media type.<br><br>**Default**: `"Banner"` |
| `media_type_group_id` | int | The group ID for the media type. |
| `uses_sizes` | enum | Whether the media type has size specifications. Possible values: <br> - `"always"` <br> - `"sometimes"` <br> - `"never"` |
| `last_modified` | date | When the `allowed_media_type` object was last updated. |

### Supported media subtypes

Creatives are categorized by media type and media subtype. Media type defines the general display style of the creative, for example, `"Banner"`, and media subtype defines the specific display style of creatives, for example, `"Standard Banner"` or `"In-Banner Video"`. You can use this array to limit the media subtype, the specific display style of creatives, that can serve on a placement. To limit the media type, the general display style of creatives, use the `supported_media_types` array (see [Supported Media Types](#supported-media-types) above).

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the allowed media subtype. You can use the [Media Subtype Service](./media-subtype-service.md) to view all media subtypes.<br><br>**Default**: `null` |
| `name` | string | The name of the allowed media subtype. |
| `is_private` | boolean | Whether the media subtype is set to private. If `true` then yes. |
| `media_type_group_id` | int | The group ID for the media type. |

> [!NOTE]
> **Supported Media Types and Media Subtypes**
>
> - If you do not specify either supported media types or supported media subtypes, the `"Banner"` media type and all of its subtypes will be allowed by default.
> - You can combine the `"Banner"` and `"Text"` media types, and any combination of their media subtypes, on a single placement, but you cannot combine any of the other media types and media subtypes. This limitation ensures that only appropriate creatives are served on a placement. For example, a placement that allows creatives of the media type `"Video"` is intended to be fed to a video player; it would not make sense to allow creatives of any other media type, such as `"Interstitial"`, to serve on the placement.
> - You can set a placement to allow the `"Expandable"` media type or any of its subtypes for direct inventory. If you want to support expandable creatives for placements that are available for reselling to other platform members, please provide the placement's ID to [Customer Support Portal](https://support.ads.microsoft.com) for verification.

### Supported mime types

The `mime_types` array of objects supports the mime types shown in the following table. If no mime types are specified, all mime types will be accepted. The Placement API uses the string in the **Name** column. If you need to pass this information in a tag, use the ID.

| Name | Id |
|:---|:---|
| `application/x-shockwave-flash` | 1 |
| `video/x-flv` | 2 |
| `video/mp4` | 3 |
| `video/webm` | 4 |
| `application/javascript` | 5 |
| `application/octet-stream` | 6 |
| `image/jpeg` | 7 |
| `image/gif` | 8 |
| `image/png` | 9 |
| `application/zip` | 10 |
| `application/vnd.ms-asf`  | 11 |
| `video/x-ms-wmv` | 12 |
| `video/ogg` | 13 |
| `video/x-msvideo` | 14 |
| `video/mpeg` | 15 |
| `video/quicktime` | 16 |
| `video/3gpp` | 17 |
| `video/3gpp2` | 18 |
| `video/x-m4v` | 19 |
| `audio/ogg` | 20 |
| `audio/x-pn-realaudio` | 21 |
| `audio/mpeg` | 22 |
| `text/css` | 23 |
| `text/html` | 24 |
| `text/plain` | 25 |
| `audio/mp4` | 26 |

### Video settings

If the `supported_media_type` is `"video"` or the `supported_media_subtypes` is `"Standard VAST"`, these fields should be included in the `video` object. Please see [Examples](#examples) below.

> [!NOTE]
> The following settings affect auction outcomes: for Outstream player settings, which determine the ultimate behavior of the Outstream video player, see "Outstream Video Player Settings" in our UI documentation.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int |A unique ID for the video settings object.|
| `width` | int | The width of the video creative. |
| `max_duration_secs` | int | The maximum duration of a video ad that is allowed to be played on the placement.<br> - If `maximum_number_ads` is > `1`, then the max duration applies to the entire length of an ad pod (a linear grouping of more than one ad designed to fill a single placement).<br><br>**Note**: This field must be set in order to enable ad pods. |
| `maximum_ad_duration_secs` | int | The maximum video ad duration in seconds of any single ad that can be played on the placement. This only applies to ad pods. |
| `maximum_number_ads` | int | The maximum number of ads that are allowed to be played on the placement. If `maximum_number_ads` is > `1`, then the placement can be an ad pod (a linear grouping of more than one ad designed to fill a single placement). |
| `start_delay_secs` | int | The start delay in seconds for the placement. If the start delay value is > `0`, then the position of the placement is `"mid-roll"`.<br><br>**Note**: This field must be set if the context is `"mid-roll"`. |
| `skipoffset_seconds` | int | The number of seconds that is allowed for the video to play, before it can be skipped.<br>The default value is `null`. <br><br>**CAUTION**: If you set this value to anything but `null`, the `supports_skippable` field must be set to `true`. (See below). |
| `supports_skippable` | boolean | The ad slot is skippable.<br>Possible values: `"true"` or `"false"` |
| `context` | string | Roll position of the video creative.<br>Possible Values: `"pre-roll"`, `"mid-roll"`, `"post-roll"`.<br><br>**Important**: This field must be set in order to enable ad pods. |
| `layback_method` | string | The different playback methods are:<br> - `Auto-play, sound-on`<br> - `Auto-play, sound-off`<br> - `Click-to-play`<br> - `Mouse-over`<br>- `Auto-play, sound unknown`<br><br>Possible values: <br> - `"auto_play_sound_on"` <br> - `"auto_play_sound_off"` <br> - `"click_to_play"` <br> - `"mouse_over"` <br> - `"auto_play_sound_unknown"` <br> - `null` |
| `frameworks` | array of strings | The framework of the placement. Options include:<br> - `VPAID 1.0`<br> - `VPAID 2.0`<br> - `MRAID-1`<br> - `ORMMA`<br> - `MRAID-2`<br>Possible values: <br> - `"vpaid_1_0"` <br> - `"vpaid_2_0"` <br> - `"mraid_1"` <br> - `"ormma"` <br> - `"mraid_2"` |
| `video_bumpers` | array of objects | The bumpers that can be associated with the ad pod. Bumper duration is not included in the overall duration of the ad pod. See [video bumpers](#video-bumpers) object. |
| `player_vast_version` | string | This field specifies the highest vast version the placement supports, and should be set to highest value that your player supports. Creatives that require a vast version higher than your player version will not be eligible to serve in your placement.<br>Possible values:<br> - `2.0`<br> - `3.0`<br> - `4.0`<br><br> **CAUTION**: Specifying a value higher than your player supports may cause errors when unsupported creatives are rendered. |
| `vmin_ad_duration` | int | The minimum creative duration allowed, in seconds. |
| `minbitrate` | int | The minimum bitrate in kbps. |
| `mf_min_width` | int | The minimum width of the video creative. |
| `mf_min_height` | int | The minimum height of the video creative. |
| `aspect_ratios` | array of objects | The creative aspect ratio that can serve for a video placement. The array contains `ratio_width` and `ratio_height`. |

### Video bumpers

This array of objects contains information relating to the bumpers on an ad pod.

| Field | Type | Description |
|:---|:---|:---|
| `video_bumper_type` | string | The type of bumper. Options include:<br> - `intro`<br> - `outro`<br>**Default**: `null` |
| `max_duration_secs` | int | The max duration of the bumper.<br><br>**Default**: `null` |

### Aspect ratios

This array of objects contains information about creative aspect ratio that can serve for a video placement.

| Field | Type | Description |
|:---|:---|:---|
| `ratio_width` | int | The width of the aspect ratio |
| `ratio_height` | int | The height of the aspect ratio |

### Ad types

This array of objects contains information relating to placement types, including the ad type ID and information about the renderer.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the `ad_type`.<br>Possible values:<br>`1` = Banner<br>`2` = Video<br>`3` = Native<br><br>**Default**: `null`<br>**Required On**: `POST`/`PUT` |
| `renderer_id` | int | The ID of the renderer.<br>Possible values:<br>`1` = outstream banner<br>`2` = outstream video<br><br>**Default**: `null`<br>**Required On**: `POST`/`PUT` |
| `name` | string | The name of the `ad_type` in all lowercase letters for example `video` or `banner`. |
| `display_name` | string | The display name of the `ad_type`, shown as the ad type with initial caps, for example `Video` or `Banner`. |
| `renderer` | multi object | An object consisting of the `id` and `display_name` of the renderer.<br><br>**Default**: `null`<br>**Required On**: `POST`/`PUT` |

### Tinytag renderer asset floor prices

This array of objects is used to associate floor prices to native creatives that have been assigned to the placement.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `renderer_id` | int | The ID of the renderer.<br><br>**Required On**: `POST`/`PUT` |
| `ad_type_id` | int | The ID of the `ad_type`. This will always be 3 since you can only associate floor prices with native creatives.<br><br>**Default**: `3`<br>**Required On**: `POST`/`PUT` |
| `asset_type` | string | The asset type.<br>Possible values include:<br> - `main_image`<br> - `video`<br>**Required On**: `POST`/`PUT` |
| `floor_price` | double | The preferred bid amount in exchange for the native asset's impressions.<br><br>**Required On**: `POST`/`PUT` |

### Default creatives

You use this array to assign default creatives to the placement. Please note the following requirements:

- A default creative must not be expired. See the `is_expired` field in the [Creative Service](./creative-service.md) for more information.
- A default creative must be assigned to a creative template that matches the `supported_media_types` and `supported_media_subtypes` of the placement. For example, if the placement allows creatives of the `"Banner"` media type, you would not be able to associate default creatives that use a creative template for the `"Interstitial"` media type. See the `template` field in the [Creative Service](./creative-service.md) for more information.

- If the placement is sized (the `"width"` and `"height"` fields are defined for the placement), this array should contain only one creative with the matching dimensions.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the default creative. |
| `width` | int | The width of the default creative. |
| `height` | int | The height of the default creative. |
| `price` | double | The reserve price for the default creative. A winning bid must be above this price. |
| `name` | string | **Read-only**. The name of the default creative. |

### Pop values

If the `supported_media_type` is `"Pop"`, or the `supported_media_subtypes` is `"Popup"` or `"Popunder"`, these fields should be included in the `pop_values` array. See below for an example.

| Field | Type | Description |
|:---|:---|:---|
| `pop_freq_times` | int | Number of times that the tag can be popped to a unique user ID in `pop_frequency_duration` seconds. Has no effect when `pop_is_prepop` is set to `true`.<br><br>**Default**: `No frequency cap` |
| `pop_freq_duration` | int | See `pop_freq_times`.<br><br>**Default**: `No frequency cap` |
| `pop_is_prepop` | Boolean | If `true`, the tag is a prepop tag and will serve into a window that the publisher page has already popped.<br><br>**Default**: `false` |
| `pop_max_width` | int | If `pop_max_width` is specified, any creative shown by the tag must have a width equal to or smaller than `pop_max_width`<br><br>**Default**: `no max width`. |
| `pop_max_height` | int | The max height of the creative. If `pop_max_height` is specified, any creative shown by the tag must have a height equal to or smaller than `pop_max_height`.<br><br>**Default**: `no max height` |

### Estimated clear prices

| Field | Type | Description |
|:---|:---|:---|
| `clear_price` | int | The bid amount that has historically won the majority (95%) of the 3rd party auctions in which it participates for this placement. |
| `average_price` | double | This is the average of all bids submitted for this placement. |
| `width` | int | When exporting sizeless placement tags to be served, this determines the width of the placement. |
| `height` | int | When exporting sizeless placement tags to be served, this determines the height of the placement. |
| `verified` | Boolean | Indicates whether the creative has been verified. |
| `geo_country` | string | The country code for the geographical location associated with the impression. |

### Private sizes

This array determines the specific placement sizes that are allowed to serve for a custom deal or in a package. The `override_size_preference` in the [Deal Service](./deal-service.md) or [Package Service](./package-service.md) must be set to `append` for these private sizes to serve along with the standard placement sizes.

| Field | Type | Description |
|:---|:---|:---|
| `width` | int | The width of the placement. |
| `height` | int | The height of the placement. |

### Stats

The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](./report-service.md) to obtain statistical information instead.

#### Toolbar & browser plug-in declaration

According to [platform policy](./placement-service.md), sellers must identify all toolbar/browser plug-in inventory and segregate it from other inventory on its own placements. To identify toolbar inventory, sellers must:

- Set the `inventory_attribute` appropriately.
- Send the required information in the toolbar array, described here:

| Parameter | Type | Description |
|:---|:---|:---|
| `name` | string | The common trade name of the toolbar. |
| `company` | string | The developer of the toolbar. Please identify the legal business entity, not a trade name. |
| `tos_url` | string | A link to a web page where our auditors can find complete terms of service. |
| `install_url` | string | A link to a web page where our auditors can install the toolbar. |

## Examples

### Viewing all placements for one of your publishers

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/placement?publisher_id=88888'

{
    "response": {
        "status": "OK",
        "count": 4,
        "start_element": 0,
        "num_elements": 100,
        "placements": [
            {
                "id": 594595,
                "name": "Test Placement 1",
                "code": null,
                "code2": null,
                "code3": null,
                "state": "active",
                "cost_cpm": null,
                "publisher_id": 88888,
                "site_id": 188040,
                "reserve_price": null,
                "width": 300,
                "height": 250,
                "default_position": "unknown",
                "default_creative_id": null,
                "ad_profile_id": null,
                "acb_code": null,
                "tag_data": null,
                "hide_referer": false,
                "inventory_source_id": null,
                "pixel_url": "",
                "pixel_type": "image",
                "last_modified": "2011-10-24 19:45:31",
                "media_subtypes": [
                    "banner"
                ],
                "intended_audience": "general",
                "audited": true,
                "audit_level": "placement",
                "default_calculation_type": "gross",
                "publisher_name": "National Public Radio",
                "site_name": "[Test Publisher 1] - ROS",
                "site_audit_status": "unaudited",
                "demand_filter_action": "include",
                "is_resizable": true,
                "pixel_url_secure": "",
                "floor_application_target": "all",
                "pop_values": null,
                "inventory_attributes": [
                    {
                        "id": 2,
                        "name": "Political opinion"
                    },
                    {
                        "id": 16,
                        "name": "Blogs"
                    }
                ],
                "supported_media_types": [
                    {
                        "name": "Banner",
                        "id": 1
                    }
                ],
                "supported_media_subtypes": null,
                "content_categories": [
                    {
                        "id": 7,
                        "name": "Arts & Entertainment",
                        "is_system": true
                    },
                    {
                        "id": 17,
                        "name": "News",
                        "is_system": true
                    },
                    {
                        "id": 25,
                        "name": "Society",
                        "is_system": true
                    },
                    {
                        "id": 11445,
                        "name": "Books & Literature",
                        "is_system": true
                    }
                ],
                "segments": null,
                "estimated_clear_prices": [
                    {
                        "clear_price": 1,
                        "average_price": 0.5,
                        "width": 0,
                        "height": 0,
                        "verified": true
                    }
                ],
                "filtered_advertisers": [
                    {
                        "id": 35081,
                        "name": "Test Advertiser 1"
                    }
                ],
                "filtered_line_items": null,
                "filtered_campaigns": null,
                "default_creatives": null
            },
            {
                "id": 605055,
                "name": "Test Placement 2",
                "code": null,
                "code2": null,
                "code3": null,
                "state": "active",
                "cost_cpm": null,
                "publisher_id": 88888,
                "site_id": 188040,
                "reserve_price": null,
                "width": null,
                "height": null,
                "default_position": "unknown",
                "default_creative_id": null,
                "ad_profile_id": null,
                "acb_code": null,
                "tag_data": null,
                "hide_referer": false,
                "inventory_source_id": null,
                "pixel_url": null,
                "pixel_type": "image",
                "last_modified": "2012-03-08 00:49:50",
                "media_subtypes": null,
                "intended_audience": null,
                "audited": false,
                "audit_level": "site",
                "default_calculation_type": "gross",
                "publisher_name": "Test Publisher 1",
                "site_name": "[Test Publisher 1] - ROS",
                "site_audit_status": "unaudited",
                "demand_filter_action": "default",
                "is_resizable": false,
                "pixel_url_secure": null,
                "floor_application_target": "all",
                "pop_values": null,
                "inventory_attributes": null,
                "supported_media_types": [
                    {
                        "id": 1,
                        "name": "Banner"
                    },
                    {
                        "id": 5,
                        "name": "Text"
                    }
                ],
                "supported_media_subtypes": null,
                "content_categories": null,
                "segments": null,
                "estimated_clear_prices": [
                    {
                        "clear_price": 1,
                        "average_price": 0.5,
                        "width": 0,
                        "height": 0,
                        "verified": true
                    }
                ],
                "filtered_advertisers": null,
                "filtered_line_items": null,
                "filtered_campaigns": null,
                "default_creatives": null
            },
            {
                "id": 605056,
                "name": "Test Placement 3",
                "code": null,
                "code2": null,
                "code3": null,
                "state": "active",
                "cost_cpm": null,
                "publisher_id": 88888,
                "site_id": 188040,
                "reserve_price": null,
                "width": null,
                "height": null,
                "default_position": "unknown",
                "default_creative_id": null,
                "ad_profile_id": null,
                "acb_code": null,
                "tag_data": null,
                "hide_referer": false,
                "inventory_source_id": null,
                "pixel_url": null,
                "pixel_type": "image",
                "last_modified": "2012-03-08 00:54:37",
                "media_subtypes": null,
                "intended_audience": null,
                "audited": false,
                "audit_level": "site",
                "default_calculation_type": "gross",
                "publisher_name": "Test Publisher 1",
                "site_name": "[Test Publisher 1] - ROS",
                "site_audit_status": "unaudited",
                "demand_filter_action": "default",
                "is_resizable": false,
                "pixel_url_secure": null,
                "floor_application_target": "all",
                "pop_values": null,
                "inventory_attributes": null,
                "supported_media_types": null,
                "supported_media_subtypes": [
                    {
                        "id": 3,
                        "name": "In-Banner Video",
                        "media_type": {
                            "id": 1
                        }
                    }
                ],
                "content_categories": null,
                "segments": null,
                "estimated_clear_prices": [
                    {
                        "clear_price": 1,
                        "average_price": 0.5,
                        "width": 0,
                        "height": 0,
                        "verified": true
                    }
                ],
                "filtered_advertisers": null,
                "filtered_line_items": null,
                "filtered_campaigns": null,
                "default_creatives": null
            },
            {
                "id": 605057,
                "name": "Test Placement 4",
                "code": null,
                "code2": null,
                "code3": null,
                "state": "active",
                "cost_cpm": null,
                "publisher_id": 88888,
                "site_id": 188040,
                "reserve_price": null,
                "width": 1,
                "height": 1,
                "default_position": "unknown",
                "default_creative_id": null,
                "ad_profile_id": null,
                "acb_code": null,
                "tag_data": null,
                "hide_referer": false,
                "inventory_source_id": null,
                "pixel_url": null,
                "pixel_type": "image",
                "last_modified": "2012-03-08 01:07:47",
                "media_subtypes": null,
                "intended_audience": null,
                "audited": false,
                "audit_level": "site",
                "default_calculation_type": "gross",
                "publisher_name": "Test Publisher 1",
                "site_name": "[Test Publisher 1] - ROS",
                "site_audit_status": "unaudited",
                "demand_filter_action": "default",
                "is_resizable": false,
                "pixel_url_secure": null,
                "floor_application_target": "all",
                "pop_values": null,
                "inventory_attributes": null,
                "supported_media_types": [
                    {
                        "id": 3,
                        "name": "Interstitial"
                    }
                ],
                "supported_media_subtypes": null,
                "content_categories": null,
                "segments": null,
                "estimated_clear_prices": [
                    {
                        "clear_price": 1,
                        "average_price": 0.5,
                        "width": 0,
                        "height": 0,
                        "verified": true
                    }
                ],
                "filtered_advertisers": null,
                "filtered_line_items": null,
                "filtered_campaigns": null,
                "default_creatives": null
            }
        ]
    }
}
```

### Viewing a specific placement

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/placement?id=605057'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": 0,
        "num_elements": 100,
        "placement": {
            "id": 605057,
            "name": "Test Placement 4",
            "code": null,
            "code2": null,
            "code3": null,
            "state": "active",
            "cost_cpm": null,
            "publisher_id": 88888,
            "site_id": 188040,
            "reserve_price": null,
            "width": 1,
            "height": 1,
            "default_position": "unknown",
            "default_creative_id": null,
            "ad_profile_id": null,
            "acb_code": null,
            "tag_data": null,
            "hide_referer": false,
            "inventory_source_id": null,
            "pixel_url": null,
            "pixel_type": "image",
            "last_modified": "2012-03-08 01:07:47",
            "media_subtypes": null,
            "intended_audience": null,
            "audited": false,
            "audit_level": "site",
            "default_calculation_type": "gross",
            "publisher_name": "Test Publisher 1",
            "site_name": "[Test Publisher 1] - ROS",
            "site_audit_status": "unaudited",
            "demand_filter_action": "default",
            "is_resizable": false,
            "pixel_url_secure": null,
            "floor_application_target": "all",
            "pop_values": null,
            "inventory_attributes": null,
            "supported_media_types": [
                {
                    "id": 3,
                    "name": "Interstitial"
                }
            ],
            "supported_media_subtypes": null,
            "content_categories": null,
            "segments": null,
            "estimated_clear_prices": [
                {
                    "clear_price": 1,
                    "average_price": 0.5,
                    "width": 0,
                    "height": 0,
                    "verified": true
                }
            ],
            "filtered_advertisers": null,
            "filtered_line_items": null,
            "filtered_campaigns": null,
            "default_creatives": null
        }
    }
}
```

### Adding a placement that allows only creatives with the `"Interstitial"` media type

```
$ cat placement

{
    "placement": {
        "name": "Placement for Interstitials",
        "publisher_id": 88888,
        "supported_media_types": [
            {
                "id": 3
            }
        ],
        "video": 10,
        "supports_skippable": true,
        "player_vast_version" "3.0"
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @placement 'https://api.appnexus.com/placement'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 605058,
        "start_element": 0,
        "num_elements": 100,
        "placement": {
            "id": 605058,
            "name": "Placement for Interstitials",
            "code": null,
            "code2": null,
            "code3": null,
            "state": "active",
            "cost_cpm": null,
            "publisher_id": 88888,
            "site_id": 188040,
            "reserve_price": null,
            "width": 1,
            "height": 1,
            "default_position": "unknown",
            "default_creative_id": null,
            "ad_profile_id": null,
            "acb_code": null,
            "tag_data": null,
            "hide_referer": false,
            "inventory_source_id": null,
            "pixel_url": null,
            "pixel_type": "image",
            "last_modified": "2012-03-08 01:41:52",
            "media_subtypes": null,
            "intended_audience": null,
            "audited": false,
            "audit_level": "site",
            "default_calculation_type": "gross",
            "publisher_name": "Test Publisher 1",
            "site_name": "[Test Publisher 1] - ROS",
            "site_audit_status": "unaudited",
            "demand_filter_action": "default",
            "is_resizable": false,
            "pixel_url_secure": null,
            "floor_application_target": "all",
            "pop_values": null,
            "inventory_attributes": null,
            "supported_media_types": [
                {
                    "id": 3,
                    "name": "Interstitial"
                }
            ],
            "supported_media_subtypes": null,
            "content_categories": null,
            "segments": null,
            "estimated_clear_prices": [
                {
                    "clear_price": 1,
                    "average_price": 0.5,
                    "width": 0,
                    "height": 0,
                    "verified": true
                }
            ],
            "filtered_advertisers": null,
            "filtered_line_items": null,
            "filtered_campaigns": null,
            "default_creatives": null
        }
    }
}
```

### Adding a placement that allows only creatives with the `"In-Banner Video"` media subtype

```
$ cat placement

{
    "placement": {
        "name": "Placement for In-Banner Video",
        "publisher_id": 88888,
        "supported_media_subtypes": [
            {
                "id": 3
            }
        ],
        "video": 10,
        "supports_skippable": true,
        "player_vast_version" "3.0"
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @placement 'https://api.appnexus.com/placement'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 605059,
        "start_element": 0,
        "num_elements": 100,
        "placement": {
            "id": 605059,
            "name": "Placement for In-Banner Video",
            "code": null,
            "code2": null,
            "code3": null,
            "state": "active",
            "cost_cpm": null,
            "publisher_id": 88888,
            "site_id": 188040,
            "reserve_price": null,
            "width": null,
            "height": null,
            "default_position": "unknown",
            "default_creative_id": null,
            "ad_profile_id": null,
            "acb_code": null,
            "tag_data": null,
            "hide_referer": false,
            "inventory_source_id": null,
            "pixel_url": null,
            "pixel_type": "image",
            "last_modified": "2012-03-08 01:46:43",
            "media_subtypes": null,
            "intended_audience": null,
            "audited": false,
            "audit_level": "site",
            "default_calculation_type": "gross",
            "publisher_name": "Test Publisher 1",
            "site_name": "[Test Publisher 1] - ROS",
            "site_audit_status": "unaudited",
            "demand_filter_action": "default",
            "is_resizable": false,
            "pixel_url_secure": null,
            "floor_application_target": "all",
            "pop_values": null,
            "inventory_attributes": null,
            "supported_media_types": null,
            "supported_media_subtypes": [
                {
                    "id": 3,
                    "name": "In-Banner Video",
                    "media_type": {
                        "id": 1
                    }
                }
            ],
            "content_categories": null,
            "segments": null,
            "estimated_clear_prices": [
                {
                    "clear_price": 1,
                    "average_price": 0.5,
                    "width": 0,
                    "height": 0,
                    "verified": true
                }
            ],
            "filtered_advertisers": null,
            "filtered_line_items": null,
            "filtered_campaigns": null,
            "default_creatives": null
        }
    }
}
```

### Adding a placement that allows only creatives with the `"Popup"` media subtype

```
$ cat placement

{
    "placement": {
        "name": "Placement for Popups",
        "publisher_id": 88888,
        "supported_media_subtypes": [
            {
                "id": 2
            }
        ],
        "pop_values":{
            "pop_is_prepop":false,
            "pop_freq_times":4,
            "pop_freq_duration":1440,
            "pop_max_width":500,
            "pop_max_height":100
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @placement 'https://api.appnexus.com/placement?publisher_id=88888'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 605076,
        "start_element": 0,
        "num_elements": 100,
        "placement": {
            "id": 605076,
            "name": "Placement for Popups",
            "code": null,
            "code2": null,
            "code3": null,
            "state": "active",
            "cost_cpm": null,
            "publisher_id": 88888,
            "site_id": 188040,
            "reserve_price": null,
            "width": null,
            "height": null,
            "default_position": "unknown",
            "default_creative_id": null,
            "ad_profile_id": null,
            "acb_code": null,
            "tag_data": null,
            "hide_referer": false,
            "inventory_source_id": null,
            "pixel_url": null,
            "pixel_type": "image",
            "last_modified": "2012-03-08 15:56:05",
            "media_subtypes": null,
            "intended_audience": null,
            "audited": false,
            "audit_level": "site",
            "default_calculation_type": "gross",
            "publisher_name": "National Public Radio",
            "site_name": "[National Public Radio] - ROS",
            "site_audit_status": "unaudited",
            "demand_filter_action": "default",
            "is_resizable": false,
            "pixel_url_secure": null,
            "floor_application_target": "all",
            "pop_values": {
                "pop_freq_times": 4,
                "pop_freq_duration": 1440,
                "pop_is_prepop": false,
                "pop_max_width": 500,
                "pop_max_height": 100
            },
            "inventory_attributes": null,
            "supported_media_types": null,
            "supported_media_subtypes": [
                {
                    "id": 2,
                    "name": "Popup",
                    "media_type": {
                        "id": 2
                    }
                }
            ],
            "content_categories": null,
            "segments": null,
            "estimated_clear_prices": [
                {
                    "clear_price": 1,
                    "average_price": 0.5,
                    "width": 0,
                    "height": 0,
                    "verified": true
                }
            ],
            "filtered_advertisers": null,
            "filtered_line_items": null,
            "filtered_campaigns": null,
            "default_creatives": null
        }
    }
}
```

### Adding a placement that allows only creatives with the `"Video Standard VAST"` media subtype

```
$ cat placement
{
    "placement": {
        "name": "Placement for Standard VAST Video",
        "publisher_id": 585173,
        "supported_media_subtypes": [
            {
                "id": 64
            }
        ],
        "video": {
        "id": 5,
        "width": 750,
        "max_duration_secs": 30,
        "supports_skippable": true,
        "player_vast_version": "3.0",
        "context": "pre-roll",
        "playback_method": null,
        "frameworks": [
          "vpaid_1_0",
          "vpaid_2_0",
          "mraid_1",
          "ormma",
          "mraid_2"
          ]
      }
    }
}
 
$ curl -b cookies -c cookies -X POST -d @placement 'https://api.appnexus.com/placement?publisher_id=585173'
 
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 5078562,
    "start_element": 0,
    "num_elements": 100,
    "placement": {
      "id": 5078562,
      "name": "Placement for Standard VAST Video",
      "code": null,
      "code2": null,
      "code3": null,
      "state": "active",
      "cost_cpm": null,
      "publisher_id": 585173,
      "content_retrieval_timeout_ms": 0,
      "enable_for_mediation": true,
      "is_prohibited": false,
      "site_id": 1275896,
      "default_referrer_url": null,
      "reserve_price": null,
      "width": 1,
      "height": 1,
      "default_position": "unknown",
      "default_creative_id": null,
      "ad_profile_id": null,
      "acb_code": null,
      "tag_data": null,
      "hide_referer": false,
      "inventory_source_id": null,
      "pixel_url": null,
      "pixel_type": "image",
      "last_modified": "2015-07-07 20:44:42",
      "media_subtypes": null,
      "intended_audience": null,
      "audited": false,
      "audit_level": "site",
      "default_calculation_type": "gross",
      "publisher_name": "National Public Radio",
      "site_name": "[National Public Radio] - ROS",
      "site_audit_status": "unaudited",
      "member_id": 958,
      "demand_filter_action": "default",
      "visibility_profile_id": null,
      "is_resizable": false,
      "pixel_url_secure": null,
      "floor_application_target": "all",
      "client_js_tracking_pct": 0,
      "use_detected_domain": true,
      "pop_values": null,
      "toolbar": null,
      "inventory_attributes": null,
      "supported_media_types": null,
      "supported_media_subtypes": [
        {
          "id": 64,
          "name": "Standard VAST",
          "media_type": {
            "id": 4
          }
        }
      ],
      "content_categories": null,
      "segments": null,
      "estimated_clear_prices": [
        {
          "clear_price": 1,
          "average_price": 0.5,
          "width": 0,
          "height": 0,
          "verified": true
        }
      ],
      "filtered_advertisers": null,
      "filtered_line_items": null,
      "filtered_campaigns": null,
      "default_creatives": null,
      "private_sizes": null,
      "video": {
        "id": 9,
        "width": 750,
        "max_duration_secs": 30,
        "supports_skippable": true,
        "context": "pre-roll",
        "playback_method": null,
        "frameworks": [
          "vpaid_1_0",
          "vpaid_2_0",
          "mraid_1",
          "ormma",
          "mraid_2"
        ]
      }
    }
  }
}
```

### Adding an ad pod placement that allows an intro bumper

```
$ cat placement
{
    "placement": {
        "video": {
            "supports_skippable": false,
            "player_vast_version": "3.0",
            "playback_method": null,
            "max_duration_sec": 200,
            "maximum_number_ads": 20,
            "context": "mid-roll",
            "start_delay_secs": 30,
            "frameworks": [
                "vpaid_2_0"
            ],
            "video_bumpers": [
                {
                    "video_bumper_type": "outro",
                    "max_duration_secs": 30
                }
            ]
        }
    }
}
 
$ curl -b cookies -c cookies -X POST -d @placement 'https://api.appnexus.com/placement?publisher_id=626425'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "11323022",
        "start_element": 0,
        "num_elements": 100,
        "placement": {
            "id": 11323022,
            "name": "Ad Pod Placement",
            "code": null,
            "code2": null,
            "code3": null,
            "state": "active",
            "cost_cpm": null,
            "publisher_id": 626425,
            "content_retrieval_timeout_ms": 0,
            "enable_for_mediation": true,
            "is_prohibited": false,
            "site_id": 1433875,
            "default_referrer_url": null,
            "reserve_price": null,
            "width": 1,
            "height": 1,
            "default_position": "unknown",
            "default_creative_id": null,
            "ad_profile_id": null,
            "acb_code": null,
            "tag_data": null,
            "hide_referer": false,
            "exclusive": false,
            "pixel_url": null,
            "pixel_type": "image",
            "last_modified": "2017-05-23 15:27:18",
            "media_subtypes": null,
            "intended_audience": null,
            "audited": false,
            "audit_level": "site",
            "default_calculation_type": "gross",
            "publisher_name": "New_Publisher",
            "site_name": "[New_Publisher] - ROS",
            "site_audit_status": "unaudited",
            "member_id": 958,
            "demand_filter_action": "default",
            "visibility_profile_id": null,
            "is_resizable": false,
            "pixel_url_secure": null,
            "floor_application_target": "all",
            "client_js_tracking_pct": 0,
            "use_detected_domain": true,
            "auction_timeout_ms": null,
            "pop_values": null,
            "toolbar": null,
            "inventory_attributes": null,
            "supported_media_types": null,
            "supported_media_subtypes": [
                {
                    "id": 64,
                    "is_private": false,
                    "name": "Standard VAST",
                    "media_type": {
                        "id": 4
                    }
                }
            ],
            "content_categories": null,
            "segments": null,
            "estimated_clear_prices": [
                {
                    "clear_price": 1,
                    "average_price": 0.5,
                    "width": 0,
                    "height": 0,
                    "verified": true,
                    "geo_country": ""
                }
            ],
            "filtered_advertisers": null,
            "filtered_line_items": null,
            "filtered_campaigns": null,
            "default_creatives": null,
            "private_sizes": null,
            "video": {
                "id": 282568,
                "width": null,
                "max_duration_secs": null,
                "supports_skippable": false,
                "context": "mid-roll",
                "playback_method": null,
                "maximum_number_ads": 20,
                "maximum_ad_duration_secs": null,
                "start_delay_secs": 30,
                "frameworks": [
                    "vpaid_2_0"
                ],
                "video_bumpers": [
                    {
                        "video_bumper_type": "outro",
                        "max_duration_secs": 30
                    }
                ]
            },
            "ad_types": null
        }
    }
}
```

### Adding a placement with the skipoffset feature enabled

```
{
        "placement": {
            "id": 11633087,
            ...
            "video": {
                "id": 336328,
                "width": null,
                "max_duration_secs": 60,
                "supports_skippable": true,
                "player_vast_version": "3.0",
                "context": "pre-roll",
                "playback_method": null,
                "maximum_number_ads": 3,
                "maximum_ad_duration_secs": null,
                "start_delay_secs": null,
                "use_server_side_trackers": false,
                "frameworks": null,
                "video_bumpers": [
                    {
                        "video_bumper_type": "outro",
                        "max_duration_secs": 15
                    }
                ],
                "skipoffset_seconds": 10
            }
        }
}
```
