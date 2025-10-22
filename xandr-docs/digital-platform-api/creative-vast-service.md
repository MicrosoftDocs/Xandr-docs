---
title: Creative VAST Service
description: In this article, learn about the Creative VAST service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Creative VAST service

You can use the Creative Vast Service to add **video** or **audio** creatives to Xandr. All creatives must be attached to an advertiser or publisher.

- You can view your advertiser ID by calling the [Advertiser Service](advertiser-service.md).
- You can view your publisher ID by calling the [Publisher Service](publisher-service.md).
- You can attach a creative to a publisher for use as a default creative for a placement. You would then attach the creative to a placement via its ID using the [Placement Service](placement-service.md).

> [!NOTE]
> `video_attribute` is always required on the `creative-vast`endpoint.

## Auditing

Xandr works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. For quality assurance, all creatives that serve on third-party inventory must be pre-registered using the Creative Service.

- Creatives are identified by their media_url (either a third-party adserver URL or a Content Delivery Network URL for a Flash or video file).
- Xandr checks media_urls on a regular basis. If a file disappears, the creative will be treated as unaudited.
- Once a creative has passed Xandr audit, certain changes to the creative cause it to be resubmitted for audit. For more details, see [Changes That Cause Re-Audit](#changes-that-cause-re-audit) below.
- For more details on auditing, see [Creative Standards and Auditing](../bidders/creative-standards-and-auditing.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/creative-vast?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-vast?advertiser_id=ADVERTISER_ID)<br> (creative JSON) | Add a new hosted video or audio creative to one of your advertisers. |
| `POST` | [https://api.appnexus.com/creative-vast?publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative-vast?publisher_id=PUBLISHER_ID)<br> (creative JSON) | Add a new hosted video or audio creative to one of your publishers. |
| `PUT` |  - [https://api.appnexus.com/creative-vast?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-vast?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/creative-vast?id=CREATIVE_ID&publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative-vast?id=CREATIVE_ID&publisher_id=PUBLISHER_ID)<br> (creative JSON) | Modify an existing hosted video or audio creative. |
| `GET` | [https://api.appnexus.com/creative-vast](https://api.appnexus.com/creative-vast) | View all hosted video or audio creatives. |
| `GET` |  - [https://api.appnexus.com/creative-vast?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-vast?advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/creative-vast?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/creative-vast?advertiser_code=ADVERTISER_CODE)<br> - [https://api.appnexus.com/creative-vast?publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative-vast?publisher_id=PUBLISHER_ID)<br> - [https://api.appnexus.com/creative-vast?publisher_code=PUBLISHER_CODE](https://api.appnexus.com/creative-vast?publisher_code=PUBLISHER_CODE) | View all hosted video or audio creatives for an advertiser or publisher. |
| `GET` |  - [https://api.appnexus.com/creative-vast?id=CREATIVE_ID](https://api.appnexus.com/creative-vast?id=CREATIVE_ID)<br> - [https://api.appnexus.com/creative-vast?code=CREATIVE_CODE](https://api.appnexus.com/creative-vast?code=CREATIVE_CODE) | View a specific creative. |
| `GET` | [https://api.appnexus.com/creative-vast?id=1,2,3](https://api.appnexus.com/creative-vast?id=1,2,3) | View multiple creatives by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/creative-vast?audit_stats=true](https://api.appnexus.com/creative-vast?audit_stats=true) | View creative audit stats. |
| `DELETE` |  - [https://api.appnexus.com/creative-vast?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-vast?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID)<br> - [https://api.appnexus.com/creative-vast?id=CREATIVE_ID&publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative-vast?id=CREATIVE_ID&publisher_id=PUBLISHER_ID) | Delete a creative. |

> [!NOTE]
> You can filter for creatives based on when they first and last served. This is particularly useful when you are approaching your [object limit](object-limit-service.md) and need to identify creatives that can be deleted from the system. For more details, see [First Run/Last Run](#first-runlast-run) below.
> [!TIP]
> The response tells you the number of creatives with each Xandr, Microsoft, and Google audit status. For the response format, see the [Examples](#examples) below.
>
> You cannot delete a creative that is used as the default creative for a member or placement. Default creatives can be deleted once they are disassociated from a placement.

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The internal ID associated with the creative.<br> - **Default:** Auto-generated number.<br> - **Required On:** `PUT`, in query string. |
| `code` | string (100) | The custom code for the creative. |
| `code2` | string (100) | The additional custom code for the creative. |
| `name` | string (100) | The name of the creative. |
| `type` | enum | The type of creative. Possible values:<br> - `"standard"`<br> - `"html"`<br> - `"video"`<br><br>**Note:** **Alpha-Beta Notice** <br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.<br>**Read Only.** |
| `advertiser_id` | int | The ID of the advertiser to which the creative is attached.<br>**Required On:** `POST`/`PUT`, in query string, if the creative is attached to an advertiser. |
| `publisher_id` | int | The ID of the publisher/media buy to which the creative is attached.<br>**Required On:** `POST`/`PUT`, in query string, if the creative is attached to an advertiser. |
| `brand_id` | int | The ID of the brand of the company advertising the creative. If included, it will be verified by the Xandr auditing team. If not included, it will be assigned by the auditing team. To retrieve a full list of brands, see the [Brand Service](brand-service.md). |
| `state` | enum | The state of the creative. Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `status` | object | The status of the creative describing if the creative is ready to serve. For more details, see [Status](#status) below. |
| `click_track_result` | enum | The result of the click track test, a feature only available in the Console user interface. <br>Possible values: `"not_tested"`, `"passed"`, or `"failed"`.<br>**Required On:** `POST`/`PUT`, in query string, if the creative is attached to a publisher. |
| `campaigns` | array of objects | The list of campaigns to which the creative is associated. For more details, see [Campaigns](#campaigns) below.<br><br>**Tip:** This field will only be returned if an `advertiser_id` is specified in the querystring. |
| `template` | object | The creative template (Example: `template_id` 6439) for the creative's format and media type. The template includes code to control how the creative renders on web pages.<br>Possible values:<br> - Video creatives: **6439**<br> - Audio creatives: **38745**<br>**Required On:** `POST` |
| `media_url` | string (1000) | The URL of the creative - can be flash, HTML, javascript (see format). URL must exist and should point to a CDN hosted VAST XML file.<br>*This field only applies to third party creatives.*<br>**Default:** `"not_tested"` |
| `media_url_secure` | string (1000) | The URL of the secure (HTTPS) creative - can be flash, HTML, javascript (see format) to be served on a secure ad call. URL must exist and should point to a CDN hosted VAST XML file.<br>*This field only applies to third party creatives.* |
| `click_url` | string (2000) | The (optional) landing page URL for non-3rd party image and flash creatives.<br><br>**Note:** This value must begin with "http://" or "https://"<br>**Required On:** `POST`, if not using content. |
| `file_name` | string (1000) | *This field does not apply to hosted video creatives.* |
| `audit_status` | enum | The audit status of the creative. Possible values: `"no_audit"`, `"pending"`, `"rejected"`, or `"audited"`.<br><br>**Note:**<br> - If `allow_audit` is `false`, this field must be `"no_audit"`.<br> - If a creative is expired, you can reanimate it by changing this field. Setting it to `"pending"` will resubmit it for auditing. For changes that automatically resubmit the creative for auditing, see [Changes That Cause Re-Audit](#changes-that-cause-re-audit) below.<br>**Required On:** `POST`, if template is for the `"image"` format. |
| `audit_feedback` | string | The creative auditing team can pass messages about a creative in this field.<br>**Read Only.** |
| `allow_audit` | Boolean | If `true`, the creative will be submitted for auditing. If `false`, the creative will not be submitted. Unaudited creatives can only run on a network's managed inventory.<br><br>**Note:**<br> - If `audit_status` is `"no_audit"`, this field must be `"false"`.<br> - If your member is not yet active, you can add creatives, but they will not be submitted for audit (`allow_audit` will be false). Once your member has been activated, if you want these creatives to be audited, you must update the creatives and set `allow_audit` to `true`.<br>**Default:** `"pending"` |
| `ssl_status` | enum | The ssl (HTTPS) status of the creative. Only creatives with ssl_status = approved will be eligible to serve on secure inventory.<br><br>**Note:**<br>If a creative fails the ssl Sherlock audit, you can submit it for a retest (once you've fixed the downstream non-secure content) by changing this field to `"pending"`. Allowed values:<br> - `"disabled"`<br> - `"pending"`<br> - `"approved"`<br> - `"failed"`<br>**Default:** `"disabled"` |
| `allow_ssl_audit` | Boolean | If `true`, the creative will be submitted for secure (HTTPS) auditing. If `false`, the creative will not be submitted. If `true`, either `media_url_secure` or `content_secure` is required as well.<br>**Default:** `"disabled"` |
| `google_audit_status` | enum | **Deprecated.** See `adx_audit` instead. |
| `google_audit_feedback` | string | **Deprecated.** See `adx_audit` instead. |
| `msft_audit_status` | enum | **Deprecated.** |
| `msft_audit_feedback` | string | **Deprecated.** |
| `is_self_audited` | Boolean | If `true`, the creative is self-audited and thus will not go through platform (Xandr) audit. The creative can only serve on inventory that accepts your self-classified creative or on inventory that accepts unaudited creatives.<br>**Default:** `false` |
| `is_expired` | Boolean | If your creative (1) has not run and (2) has not been modified in 45 days, then it will be automatically marked expired and will not serve on any inventory.<br> - Expired creatives must be reaudited to run on third-party inventory. To unexpire a creative for third-party inventory, set `audit_status` to `"pending"`.<br> - Expired creatives do not need to be reaudited to run on direct inventory. To unexpire a creative for direct inventory, set `audit_status` to `"no_audit"`.<br>**Default:** `false`<br>**Read Only.** |
| `is_prohibited` | Boolean | If Sherlock flags the creative for having malware or loading blocked domains, this is set to true to prevent the creative from serving.<br>**Default:** `false`<br>**Read Only.** |
| `is_hosted` | Boolean | If `true`, the creative is hosted by Xandr.<br>**Read Only.** |
| `lifetime_budget` | double | The lifetime budget in dollars.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `false` |
| `lifetime_budget_imps` | int | The lifetime limit for number of impressions.<br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `daily_budget` | double | The daily budget in dollars.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `daily_budget_imps` | int | The daily limit for number of impressions.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `enable_pacing` | Boolean | If `true`, daily budgeted spend is spread evenly throughout a day.<br><br>**Note:** To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `allow_safety_pacing` | Boolean | If `true`, spend per minute is limited to a maximum of 1% of the lifetime budget and 5% of the daily budget.<br>**Admin Only.** |
| `profile_id` | int | You can attach targeting such as gender and geography to a creative by creating a profile and associating it here. |
| `folder` | object | To arrange your creatives in folders for convenience (usually in the UI) you will create a folder using the [Creative Folder Service](creative-folder-service.md) and then associate it here via folder ID or in the Creative Folder service via creative ID. Output is `{"id": "41", "name": "MyFolder"}`. |
| `line_items` | array of objects | The line items that are associated with the creative. For more details, see [Line Items](#line-items) below. |
| `is_control` | Boolean | This is a flag used to mark this creative as part of a control/test group in A/B testing. For more information, see [Test and Control Targeting](../monetize/test-and-control-targeting.md).<br>**Default:** `true` |
| `segments` | array | A list of segments that a user will be added to upon viewing or clicking on this creative. For more information, see [Segments](#segments) and the [example](#segments-example) below. |
| `created_on` | timestamp | The date and time when this creative was created. If it was created before January 2010, this will be zero.<br>**Read Only.** |
| `last_modified` | timestamp | The date and time when the creative was last modified.<br>**Read Only.** |
| `creative_upload_status` | enum | **Deprecated.** |
| `categories` | array of objects | The categories that describe the creative and offer type.<br><br>**Note:**<br>To include categories in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of categories, see the [Category Service](category-service.md) and the [example](#categories-example) below. |
| `adservers` | array of objects | The ad servers that deliver the creative or are called for data collection purposes during the delivery the creative. <br><br>**Note:**<br> To include adservers in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of ad servers, see the [Ad Server Service](ad-server-service.md) and the [example](#adservers-example) below.<br>**Read Only.** |
| `technical_attributes` | array of objects | The attributes that describe technical characteristics of the creative, such as `"Expandable"` or `"Video"`.<br><br>**Note:**<br>To include technical attributes in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of technical attributes, see the [Technical Attribute Service](technical-attribute-service.md) and the [example](#technical_attributes-example) below. |
| `language` | object | The language of the creative. To retrieve a full list of languages, see the [Language Service](language-service.md) and the [example](#language-example) below. |
| `brand` | object | The brand of the company advertising the creative and the category associated with the brand. For more details, see [Brand](#brand) below.<br>**Read Only.** |
| `sla` | int | Creatives set to `0` will be submitted for audit with a standard SLA.<br><br>**Caution:** Creatives submitted with any number other than 0 will result in a priority audit (when enabled) and resulting fees.<br>If you have a supplemental services agreement with Xandr for priority audits, you can submit a creative for priority audit (auditing within 2 hours during business hours) by setting this field to `2`. For more details about priority auditing, see [Creative Standards and Auditing](../bidders/creative-standards-and-auditing.md). |
| `sla_eta` | timestamp | The estimate time of completion for a priority audit.<br>**Read Only.** |
| `currency` | string | The code that defines the advertiser's primary currency (for example, **USD**). For more details about the currency types available, see [Currency Service](currency-service.md).<br> **Default:** Member's default currency.<br>**Read Only.** |
| `first_run` | timestamp | The date and time when the creative first served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter creatives based on when they first served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `last_run` | timestamp | The date and time when the creative last served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to creatives based on when they last served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `video_attribute` | object | Attributes for third-party in-stream (VAST) and hosted video and audio creatives. For more details, see [Video Attribute](#video-attribute) below.<br> **Default:** Member's default currency.<br> **Required On:** `POST`, if template is for "Standard VAST" media subtype. |
| `competitive_brands` | array of objects | Creatives associated with the brands in this array will not serve together in `/mtj` auctions. The classic example of competing brands is Coke vs. Pepsi. See [Competitive Brands](#competitive-brands) below. For more information about the brands in our system, see the [Brand Service](brand-service.md).<br>**Default:** **N/A** |
| `competitive_categories` | array of objects | Creatives associated with the categories in this array will not serve together in `/mtj` auctions, e.g., "Dating" and "Education". See [Competitive Categories](#competitive-categories) below. For more information about the categories we apply to creatives (and brands), see the [Category Service](category-service.md).<br>**Default:** **N/A** |
| `adx_audit` | object | This object contains information about the status and feedback related to the Google AdExchange audit of the creative. Information about whether or not a creative has been approved is returned in the `audit_status` field.<br>**Read Only.** |
| `member_id` | int | The ID of the member that owns the creative. |
| `media_assets` | array of objects | Used to associate Xandr hosted files to your creative. This field will be auto-populate when uploading files via the API.<br>See [example](#media_assets-example).<br><br>**Note:**<br>`creative_field` should always be null for a VAST creative. |
| `ad_type` | string | **Tip:**<br>This field only applies when you are associating creatives to [augmented line items](line-item-service---ali.md).<br>The type of creative used. Possible values:<br> - `"banner"`<br> - `"video"` (includes audio creatives)<br> - `"native"`<br><br>This value determines how auction items are tracked for the line item's buying strategy, paying strategy, optimization options, creative association, and targeting options.<br><br>**Note:**<br> All creatives associated to a line item must have the same ad type, which should match the `ad_type` selected in the [Line Item Service - ALI](line-item-service---ali.md). |

### `segments` example

```
"segments":[
{"id":11111,
"action":"add_on_view"
},
{"id":22222,
"action":"add_on_click"
}
]
```

### `categories` example

```
"categories":[{"id":"13","name":"Online Games"}]
```

### `adservers` example

```
"adservers":[{"id":"1","use_type":"adserver","name":"24/7 Real Media"}]
```

### `technical_attributes` example

```
"technical_attributes":[{"id":"1","name":"Image"}]
```

### `language` example

```
"language":{"id":"1","name":"English"}
```

### `media_assets` example

```
"media_assets":[
{
"media_asset_id":22,
"creative_field":null
}
]
```

### Audio

| Field | Type | Description |
|:---|:---|:---|
| `click_target` | string | The target of the click_action, which is the action that the device should take when the creative is clicked. Enter a URL that our audit team can use to verify the brand and attributes of your audio creative. Ensure that the site the URL points to is in the same language as the audio. This URL is used only for auditing purposes.<br><br>**Caution:**<br>You must provide an auditable URL in order for your creative to pass auditing. |

### Line items

Each object in the `line_items` array includes the following fields. To obtain information for `"id"` or `"code"` fields, you can use the [Line Item Service - ALI](line-item-service---ali.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `name` | string | The name of the line item.<br>**Read Only.** |
| `state` | enum | The state of the creative. Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `id` | int | The ID of the line item. Either `"id"` or `"code"` is required when updating line item association.<br>**Required On:** `PUT` |
| `code` | string | The custom code for the line item. Either `"id"` or `"code"` is required when updating line item association.<br>**Required On:** `PUT` |

### Campaigns

Each object in the `campaigns` array includes the following fields. To obtain information for `"id"` or `"code"` fields, you can use the [Campaign Service](campaign-service.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `id` | int | The ID of the campaign. Either `"id"` or `"code"` is required when updating campaign association.<br>**Required On:** `PUT` |
| `campaign_id` | int | The ID of the campaign. |
| `creative_id` | int | The ID of the creative. |
| `name` | string | The name of the campaign.<br>**Read Only.** |
| `state` | enum | The state of the campaign. Possible values: `"active"`, `"inactive"`, or `"parent_inactive"`.<br>**Read Only.** |
| `code` | string | The custom code for the campaign. Either `"id"` or `"code"` is required when updating line item association.<br>**Required On:** `PUT` |

### Status

| Name | Type | Description |
|:---|:---|:---|
| `user_ready` | boolean | The status of the creative set by the user describing if the creative is ready to serve or not. Possible values: `"true"` or `"false"`.<br>**Default:** `true` |
| `hosted_assets_association_complete` | boolean/null | Status of the creative uploaded by Xandr's internal systems. Possible values: `"true"` or `"false"` for hosted creatives and "null" for third-party creatives.<br>**Read Only.** |

### Competitive brands

> [!TIP]
> For more information about brands, see the [Brand Service](brand-service.md).

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand.<br>**Default:** N/A<br>**Required On:** N/A |
| `name` | string | The name of the brand.<br>**Default:** N/A<br>**Required On:** N/A |

### Media-asset

`media-asset` object includes the following fields:

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | ID of the media asset.<br>**Required On:** `POST` |
| `parent_media_asset_id` | int | ID of the parent media asset. |
| `size_in_bytes` | int | Size in bytes. |
| `cdn_uploaded_on` | int | Date on which it was uploaded to CDN. |
| `cdn_url` | string | Non-secure CDN URL to the media-asset. |
| `cdn_secure_url` | string | Secure CDN URL to the media-asset. |
| `deleted` | boolean | Boolean indicator that determines if the media-asset was deleted or not. |
| `mime_type` | enum | The type of asset. |
| `asset_type` | enum | One of the following asset types:<br> - html5<br> - video<br> - audio<br> - image |
| `duration` | double | Duration of video asset in milliseconds. |

### Media_asset_status

`media_asset_status` object includes the following fields:

| Name | Type | Description |
|:---|:---|:---|
| `cdn_upload_attempt_count` | int | The number of attempts made while uploading to CDN. |
| `status` | enum | Indicates the stage of processing the asset is in. |

### Template

`template` object includes the following fields:

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of creative template. |
| `name` | string | The name of the creative template.<br>**Read Only.** |
| `media_subtype_id` | int | The ID of the media subtype assigned to the template. You can use the [Media Subtype Service](media-subtype-service.md) to view all supported media subtypes.<br>**Read Only.** |
| `format_id` | string | The name of the format assigned to the template. You can use the [Creative Format Service](creative-format-service.md) to view all supported formats.<br>**Read Only.** |

### Competitive categories

> [!TIP]
> For more information about categories, see the [Category Service](category-service.md).

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the category.<br>**Default:** N/A<br>**Required On:** N/A |
| `name` | string | The name of the category.<br>**Default:** N/A<br>**Required On:** N/A |

### Video Attribute

`video_attribute` is required for both audio and video creatives on the `creative-vast` endpoint. Template IDs are:

- 6439 - Video: Standard VAST
- 38745 - Audio: Standard VAST

The `video_attribute` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `is_skippable` | boolean | Deprecated. Xandr automatically adds a skip tracker to all trafficked VAST creatives. |
| `duration_ms` | double | The duration, in milliseconds, of the in-stream (VAST) video or audio creative. This must be greater than `0`.<br>**Required On:** `POST`, `PUT`. |
| `wrapper` | object | The VAST document wrapper that contains the `elements` array and the `trackers` array. For details, see [Video Attribute Wrapper](#video-attribute-wrapper) below.<br>**Required On:** Either the wrapper or inline object is required on `POST`, `PUT`. |
| `inline` | object | The inline VAST document. For details, see [Video Attribute Inline](#video-attribute-inline) below.<br>**Required On:** Either the wrapper or inline object is required on `POST`, `PUT`. |

> [!NOTE]
> Either the `wrapper` or `inline`object can be specified in the creative call. They are mutually exclusive.

## Video Attribute Wrapper

The `wrapper` object contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | URL of the VAST document.<br>**Required On:** `POST`, `PUT`. |
| `secure_url` | string | Secure URL of the VAST document. |
| `elements` | array | Elements of the VAST wrapper.<br>**Required On:** `POST`, `PUT`. |

## Video Attribute Wrapper Element

The `elements` array contains the following fields:

> [!NOTE]
> At least one element must be specified.

| Field | Type | Description |
|---|---|---|
| `vast_element_type_id` | int | VAST element ID. Possible value:<br>`1`: linear |
| `type` | string | Type of element. Possible value: `"linear"`<br>**Read Only.** |
| `trackers` | array | VAST event trackers. |
| `media_files` | array | Media files in the VAST wrapper. |

## Video Wrapper Event Tracker

You can drop pixels on every event that we track in reporting (see `vast_event_type_id` below). Add the pixel(s) as `trackers` on the creative. The `trackers` array contains the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The name of the event tracker. |
| `vast_event_type_id` | int | The ID of the VAST event. Possible values:<br> - `2`: start<br> - `3`: skip<br> - `4`: error<br> - `5`: first_quartile<br> - `6`: midpoint<br> - `7`: third_quartile<br> - `8`: completion<br> - `9`: impression<br> - `10`: click |
| `url` | string | The URL of the event tracker. |
| `secure_url` | string | The secure URL of the event tracker. |
| `event_type` | string | The type of event corresponding to `vast_event_type_id`.<br>**Read Only.** |

### Video Wrapper Media Files

| Field | Type | Description |
|:---|:---|:---|
| `maintain_aspect_ratio` | string | The ratio between a media file's sizes in dif­fer­ent dimen­sions.<br>**Read Only.** |
| `scalable` | string | Is the media file scalable.<br>**Read Only.** |
| `media_asset` | string | The values are derived from the video or audio upload app.<br>**Read Only.** |

### Video Attribute Inline

| Field | Type | Description |
|:---|:---|:---|
| `ad_title` | string | The title of the ad.<br>**Required On:** `POST`, `PUT`. |
| `ad_description` | string | **Optional.** The description of the ad. |
| `linear` | object | Ad that appears before, after or during a break in content. |
| `companion_ads` | array of objects | Companion banner ads that appear in banner placements in the same page as the accompanying video or audio (see [Inline Companion Ads Object](#inline-companion-ads-object) below). |

### Inline Linear object

| Field | Type | Description |
|:---|:---|:---|
| `trackers` | array | Inline linear trackers. |
| `media_files` | array | The inline linear media files. |
| `skipoffset_seconds` | int | The number of seconds that is allowed for the video to play, before it can be skipped. The default value is `null`.<br><br>**Note:**<br>This field can only be used if you are serving ads into a placement by the same member. |

### Inline Linear Trackers

| Field | Type | Description |
|:---|:---|:---|
| `vast_event_type` | string | The type of tracking event. Possible Values:<br> - `start`<br> - `skip`<br> - `error`<br> - `first_quartile`<br> - `completion`<br> - `impression`<br> - `click`<br>**Required On:** `POST`, `PUT`. |
| `name` | string | The name of the tracker. |
| `url` | string | The URL of the inline linear event tracker.<br>**Required On:** `POST`, `PUT`. |
| `secure_url` | string | The secure URL of the inline linear event tracker. |

### Inline Linear Media Files

| Field | Type | Description |
|:---|:---|:---|
| `maintain_aspect_ratio` | string | The ratio between a media file's sizes in dif­fer­ent dimen­sions.<br>**Read Only.** |
| `scalable` | string | Is the media file scalable.<br>**Read Only.** |
| `media_assets` | string | The values are derived from the video upload app.<br>**Read Only.** |

### Inline Companion Ads object

| Field | Type | Description |
|:---|:---|:---|
| `trackers` | array of objects | Inline companion ad trackers. |
| `companion_creative_id` | int | The ID of the the companion ad. |

### Segments

These fields will be included in the Segments array:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the segment.<br>**Required On:** `POST`, `PUT`. |
| `segment_id` | int | The ID of the segment. This field contains the same information as the `id` field. |
| `action` | enum | The action taken by users that will add them to the segment. Possible values: `"add on view"` or `"add on click"`.<br>**Required On:** `POST`, `PUT`. |
| `name` | string | The segment's name. |

### Brand

The `brand` object contains the following fields.

> [!TIP]
> This object is **read-only**. To set the brand for a creative, use the `brand_id` field outside of this object.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand of the company advertising the creative.<br>**Read Only.** |
| `name` | string | The name of the brand of the company advertising the creative.<br>**Read Only.** |
| `category_id` | int | The ID of the category associated with the brand.<br>**Read Only.** |
| `category_name` | string | The name of the category associated with the brand.<br><br>**Note:**<br>The `category_name` field is returned only when you pass `show_category_name=true` in the query string of your call. |

## First run/last run

To include the `first_run` and `last_run` fields in a `GET` response, pass `flight_info=true` in the query string. You can also filter for creatives based on when they first and last served, as follows:

### Retrieve only creatives that have never served

Pass `never_run=true` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&never_run=true'
```

> [!TIP]
> You can use `never_run=true` in combination with other filters, but note that it will always be an OR relationship. For example, if you pass both `never_run=true` and `min_first_run=2012-01-01 00:00:00` in the query string, you will be looking for creatives that have never served OR line items that first served on or after 2012-01-01.

### Retrieve only creatives that first served on or after a specific date

Pass `min_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00'
```

### Retrieve only creatives that first served on or before a specific date

Pass `max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&max_first_run=2012-08-01 00:00:00'
```

### Retrieve only creatives first served within a specific date range

Pass `min_first_run=YYYY-MM-DD HH:MM:SS&max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00&max_first_run=2012-08-01 00:00:00'
```

### Retrieve only creatives that last served on or after a specific date

Pass `min_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00'
```

### Retrieve only creatives that last served on or before a specific date

Pass `max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&max_last_run=2012-08-01 00:00:00'
```

### Retrieve only creatives that last served within a specific date range

Pass `min_last_run=YYYY-MM-DD HH:MM:SS&max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative-vast?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00&max_last_run=2012-08-01 00:00:00'
```

## Changes that cause re-audit

Once a creative has passed Xandr audit (`audit_status` is `"audited"`), changing any of the following fields causes the creative to be resubmitted for audit (`allow_audit` is set to `"pending"`).

- `media_url`
- `click_url`
- `language`
- `categories`
- `technical_attributes`
- `brand_id`
- `pixel_url`
- `video_attribute`
- `media_assets`

Also, if the `audit_status` is `"no_audit"`, changing `allow_audit` from `"false"` to `"true"` causes the creative to be resubmitted for Xandr audit.

## Examples

### Upload a video or audio creative

When uploading a creative for hosting with Xandr:

**Step 1: Upload the asset to the [creative upload service](creative-upload-service---file-format.md).**

```
curl -X POST -H "Authorization: hbapi:139072:5761726637ada:nym2" --form "type=video" --form "file=@./Xandr_30_1280_720_2500k.mp4" "https://api.appnexus.com/creative-upload?member_id=123"
```

The **media_asset_id** is returned.

```
{
    "response": 
        "status": "OK",
        "count": 0,
        "start_element": 0,
        "num_elements": 0,
        "media-asset": [
            {
                "id": 54621,
                "parent_media_asset_id": null,
                "member_id": 123,
                "advertiser_id": null,
                "publisher_id": null,
                "file_name": "Xandr_30_1280_720_2500k.mp4",
                "size_in_bytes": 8358845,
                "cdn_uploaded_on": null,
                "cdn_url": null,
                "cdn_secure_url": null,
                "created_on": "2016-06-15 15:33:17",
                "last_modified": "2016-06-15 15:33:17",
                "deleted": false,
                "media_asset_status": [
                    {
                        "id": 54621,
                        "media_asset_id": 54621,
                        "error_message": null,
                        "local_path": "03/36/2e/66/03362e66-674a-41b3-9477-fcd979cdbf0b/03362e66-674a-41b3-9477-fcd979cdbf0b.mp4",
                        "cdn_upload_attempt_count": 0,
                        "created_on": "2016-06-15 15:33:17",
                        "last_modified": "2016-06-15 15:33:17",
                        "deleted": false,
                        "status": "on_shared_storage"
                    }
                ],
                "media_asset_video": null,
                "media_asset_html5": null,
                "asset_type": "video",
                "mime_type": "video/mp4",
                "duration": "32000"
            }
        ]
    }
```

**Step 2:** **Use the** **`media_asset_id`** **to upload the creative.**

```
$ cat creative_video

{
    "creative-vast": {
        "name": "upload hosted video",
        "media_assets": [
            {
               "media_asset_id": 54621
            }
        ],
        "click_url": "https://appnexus.com",
        "video_attribute": {
            "inline": {
                "ad_title": "hosting test",
                "linear": {
                    "trackers": []
                }
            },
            "is_skippable": true,
            "duration_ms": "57000"
        },
        "template": {
            "id": 6439
        },
        "advertiser_id": 164979,
        "segments": null,
        "allow_audit": true,
        "is_self_audited": false,
        "sla": 0
    }
}

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 12345678,
        "start_element": 0,
        "num_elements": 100,
        "creative-vast": {
            "name": "hosted creative video",
            "brand_id": 1,
            "media_url": "http://appnexus.com",
            "id": 12345678,
            ...
            "track_clicks": true,
            "audit_status": "pending",
            ...
            "media_url_secure": "https://appnexus.com",
            ...
            "is_hosted": true,
            ...
            "language": {
                "id": 1,
                "name": "English"
            },
            ...
            },
            "template": {
                "id": 6439,
                "name": "Standard",
                "media_subtype_id": 64,
                "format_id": 10
            },
            ...
            "video_attribute": {
               "is_skippable": true,
                "duration_ms": 57000,
                "inline": {
                    "ad_title": "hosted video creative",
                    "ad_description": null,
                    "linear": {
                        "trackers": null,
                        "media_files": null
                    }
                },
                "video_frameworks": null
            },
            "media_assets": [
                {
                    "media_asset_id": 54621
                }
            ],
            ...
            "currency": "USD",
            "type": "video"
        },
        ...
    }
}
```

**A `video_attribute` object with wrapper example**

```
{
    "creative-vast": {
        "id": 145,
        ...
        "template_id": 6439,
        "video_attribute": {
            "is_skippable": true,
            "duration_ms": 21000,
            "wrapper": {
                "url": "http://www.doubleclick.net/...",
                "secure_url": "https://www.doubleclick.net/...",
                "elements": [
                    {
                        "vast_element_type_id": 1,
                        "name": "linear",
                        "trackers": [
                            {
                                "name": "startTracker",
                                "vast_event_type": "impression",
                                "url": "http://tracker.com/...",
                                "secure_url": "https://tracker.com/...",
                            }
                            {
                                "name": "completionTracker",
                                "vast_event_type_id": 8,
                                "url": "http://tracker.com/...",
                                "secure_url": "https://tracker.com/...",
                                "event_type": "completion"
                            }
                        ]
                    }
                ]
            }
        }
    }
    }
```

**A `video_attribute` object with inline VAST example**

```
{
    "creative-vast": {
        "name": "John-Doe test",
        "member_id": 1111,
        "advertiser_id": 2474202,
        "template": {
            "id": 6439
        },
        "video_attribute": {
            "duration_ms": 10000,
            "inline": {
                "ad_title": "John-Doe test",
                "linear": {
                    "trackers": []
                }
            }
        },
        "media_assets": [
            {
                "media_asset_id": 5375731,
                "creative_field": null
            }
        ]
    }
    }
```

## Related topics

- [Creative Upload Service - File Format](creative-upload-service---file-format.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
