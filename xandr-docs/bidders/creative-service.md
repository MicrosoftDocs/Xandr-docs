---
title : Bidders - Creative Service
description : Learn how Creative Service can be used for quality assurance of all creatives that pass through our system. The page covers different stages that a creative goes through so that it's accepted.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Bidders - Creative service

Xandr works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. For quality assurance, all creatives that serve on third-party inventory must be pre-registered using the Creative Service.

- Creatives are identified by their media_url (either a third-party adserver URL or a Content Delivery Network URL for a flash/GIF file).
- We will check media_urls on a regular basis. If a file disappears, the creative will be treated as unaudited.
- An audit notify request will be sent to the audit_notify_uri handler for each creative whose audit status has changed.
- Uploading malware or deceptive creatives or purposely mislabeling creatives is absolutely prohibited.
- It is highly recommended to configure your member (see the [Member Service](member-service.md)) to receive emails
  when:
  - The creative is audited (by configuring the audit_notify_email field in the [Member Service](member-service.md).)
  - The creative has been scanned by [Sherlock](sherlock-creative-quality-control.md) (by configuring the sherlock_notify_email in the [Member Service](member-service.md).)

> [!NOTE]
> Expired Creative Policy
>
> When a creative (1) has not run and (2) has not been modified for 15 consecutive days, then it will be automatically marked expired ("is_expired": true) and will not serve on any inventory. Creatives will be automatically reactivated if your bidder resumes bidding with the creative.

**Permissions:**

- Only admin can change `audit_status` field.
- Creatives that are modified after they've been audited will return to an `pending` audit status.

> [!NOTE]
> Effective September 2025: Declare whether your ad is political and intended to be served in the EU via the `is_political_and_eu_targeted` and `is_political_and_non_eu_targeted` fields. 

## REST API

| HTTP method | End point | Description |
|--|--|--|
| DELETE | [https://api.adnxs.com/creative/MEMBER_ID?id=CREATIVE_ID](https://api.adnxs.com/creative/MEMBER_ID?id=CREATIVE_ID) | Delete a creative. |
| GET | [https://api.adnxs.com/creative/MEMBER_ID](https://api.adnxs.com/creative/MEMBER_ID)<br>[https://api.adnxs.com/creative/MEMBER_ID?num_elements=X&start_element=Y&min_last_activity=Z&sort=id.asc](https://api.adnxs.com/creative/MEMBER_ID?num_elements=X&start_element=Y&min_last_activity=Z&sort=id.asc) | View all of a member's creatives. <br>**Note**: If you have more than 100 creatives for a member, please use the num_elements and start_element parameters discussed below. <br><br> To see a specific number and range of creatives for a member. X is the number of elements to be returned. This should be 100 or lower. Y is the first element of the X elements to be returned. The first element is 0. If you use num_elements, you must also specify the start_element. To retrieve unique paginated results use the parameter `&sort=id.asc` as shown below. You may also specify `min_last_activity=Z` as a filter. Z must be in the form `YYYY-MM-DD`. |
| GET | [https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID https://api.adnxs.com/creative?member_id=MEMBER_ID&id=CREATIVE_ID1,CREATIVE_ID2,CREATIVE_ID3](https://api.adnxs.com/creative?member_id=MEMBER_ID&id=CREATIVE_ID1,CREATIVE_ID2,CREATIVE_ID3) [https://api.adnxs.com/creative?member_id=MEMBER_ID&code=CODE](https://api.adnxs.com/creative?member_id=MEMBER_ID&code=CODE) | View a specific creative. |
| POST | [https://api.adnxs.com/creative/MEMBER_ID](https://api.adnxs.com/creative/MEMBER_ID) (creative JSON) | Add a new creative. |
| PUT | [https://api.adnxs.com/creative-macro-check?include_tests=1](https://api.adnxs.com/creative-macro-check?include_tests=1) (replace_pattern_in_content_url JSON) | Modify an existing creative. |
| PUT | [https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID](https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID) (creative JSON) [https://api.adnxs.com/creative/MEMBER_ID?code=CODE](https://api.adnxs.com/creative/MEMBER_ID?code=CODE) |  |

## JSON structure

| Field | Set By | Required | Type | Description |
|--|--|--|--|--|
| `active` | internal | no | Boolean | **Read-only**. The current state of the creative. |
| `added_by_bidder` | internal | no | int | The ID of the bidder that added this creative. |
| `adservers` | internal | no | array of objects | **Read-only**. The ad servers that deliver the creative or are called for data collection purposes during the delivery of the creative. |
| `adx_audit` | internal | no | object | **Read only**. This object contains information about the status and feedback related to the Google Ad Exchange audit of the creative. Information about whether or not a creative has been approved is returned in the `audit_status` field. |
| `allow_audit` | client | no | Boolean | Set to true if you would like to opt the creative into the audit process. |
| `allow_ssl_audit` | client | no | Boolean | If true, the creative will be submitted for secure (https) auditing. If false, the creative will not be submitted. If true, either media_url_secure or content_secure is required as well. <br> **Default**: false |
| `audit_feedback` | internal | no | string | If the creative has failed the creative audit for Xandr, this includes the audit team's reasoning. |
| `audit_status` | audit team and client | no | enum ('no_audit','pending','rejected','unauditable', 'audited') | The status of the audit. This field is set by the Xandr creative auditing team. A creative that does not have audit_status "audited" may be resubmitted for audit by setting the audit_status of the creative to "pending." |
| `backup_upload_status` |  |  |  | **Deprecated**. |
| `brand` | client | no | object | Contains the id of the brand of the company advertising the creative, the name, and the category_id. Will be audited. <br> **Tip**: To return `category_name` as well, pass `show_category_name=true` in the query string of your call. |
| `brand_id` | client | no | int | The id of the brand of the company advertising the creative. |
| `campaign` | client | no | string(50) | The (optional) name of the campaign for this creative - used for reporting/management purposes. |
| `categories` | audit team (Except for political attestation set by client) | no | List[Object] | ID and names of categories associated with the creative - see [Category Service](category-service.md). For GET, these are only returned if you use the flag attributes=true in the request URL. |
| `click_action` | no | no | string | The action that the device should take when the creative is clicked. Currently, this field will be set to the only supported click action, "click-to-web" <br> **Default**: click-to-web |
| `click_target` | no | no | string | The target of the click_action. For click-to-web, this is the `click_url` of the creative.  `click_url` will eventually be deprecated in favor of this field. |
| `click_trackers` |  |  |  | **Deprecated**. |
| `click_url` | client | yes (When creative.format is image) | string(1000) | Does not work for Bidder clients. |
| `code` | client | no | string (100) | The member code of the creative; used for external ID mapping purposes only (see [Incoming Bid Response from Bidders](incoming-bid-response-from-bidders.md)). |
| `content` | client | no (if media_url exists) | text | The raw javascript or html content of the creative used instead of a media_url. |
| `content_secure` | client | no (if media_url_secure exists) | text | Javascript or HTML content when "format" is "raw-js" or "iframe-html" served on a secure ad call. |
| `created_on` | internal | no | timestamp | The timestamp when the creative was originally uploaded to Xandr |
| `creative_upload_status` |  |  |  | **Deprecated**. |
| `description` |  | no | string (400) | Optional description associated with the creative. |
| `filter` |  |  |  | **Deprecated**. |
| `flash_backup_url` |  | no | string | Backup for flash format creatives, which will be served if the user's browser doesn't support flash. |
| `flash_click_variable` | client | no | string | For flash creatives only. Attempting to `POST` or `PUT` to this field for non-flash creatives is not enabled. This is the name of the Flash clickTAG variable into which Xandr will insert a click tracking URL (if click tracking is enabled) that will be followed when the user clicks on the creative. See [Adobe's designer's guide](https://www.adobe.com/resources/richmedia/tracking/designers_guide/) on how to set up a Flash file to use the clickTAG variable. |
| `format` |  |  |  | **Deprecated**. |
| `height` | client | yes | int | The height of the creative in pixels. |
| `id` | internal | yes (on update) | int | The ID of the creative; used for internal matching purposes only. |
| `impression_trackers` |  |  |  | **Deprecated**. |
| `is_expired` | internal | no | boolean | Indicates whether the creative has been served or modified in the past 15 days. |
| `is_prohibited` | internal | no | boolean | True if the Xandr internal auditing system has detected malicious behavior while analyzing the creative. If True, this creative will not be eligible to serve. |
| `is_suspicious` | internal | no | boolean | True if the Xandr internal auditing system has detected suspect behavior while analyzing the creative. If True, this creative will not be eligible to serve. |
| `is_political_and_eu_targeted` | client | No | Boolean | Set to true if the creative contains political content and you intend to run it in the EU. Assumed default is false if the field is not sent. <br> **NOTE**: Political advertising is not supported in the EU. |
| `is_political_and_non_eu_targeted` | client | No | Boolean | Set to true if the creative contains political content and you do not intend to run it in the EU. Assumed default is false if the field is not sent. <br> **NOTE**: Political advertising is supported in non-EU countries, only for Microsoft Monetize Adserver clients.  |
| `language_id` | audit team | no | int | ID of the creative's language - see [Language service](language-service.md) |
| `last_activity` | internal | no | timestamp | The date and time when the creative was last modified. Timezone is UTC. **Read Only**. |
| `last_checked` | internal | no | timestamp | The timestamp that the URL was last checked for existence. |
| `media_subtypes` |  |  |  | **Deprecated**. |
| `media_url` | client | no (if content exists) | string(1000) | The URL of the creative - can be image, flash, html, javascript. URL must exist and should be on a CDN or equivalent. |
| `media_url_secure` | client | no (if content_secure exists) | string(1000) | The URL of the secure (https) creative - can be image, flash, HTML, javascript to be served on a secure ad call. URL must exist and should be on a CDN or equivalent. |
| `member_id` | client | no | int | The ID of the member this creative belongs to. This is specified in the URI of the API call and does not need to also be in the JSON. |
| `mobile` | client | no | object | Information needed for mobile creatives to pass the creative audit. See [Mobile](#mobile) below. |
| `native` |  |  |  | **Deprecated**. |
| `native_attribute` | client | yes (required for native ads with template 39461) | object | This is the native object that contains elements required for native ads. For more information, see the description of the [Native Attribute](#native-attribute) object below. |
| `no_iframes` |  |  |  | **Deprecated**. |
| `no_iframes` |  |  |  | **Deprecated**. |
| `not_found` | internal | no | boolean | How many times the URL has failed to load. After a certain number of checks, the creative will deactivate. |
| `original_content` | internal | no | string | This field is for reference only. When a tag with third party content is uploaded to Xandr, the original content uploaded with the creative will be stored in this field. <br> **Default**: <br> **Required on**: POST when submitting as type  `raw-html`. |
| `original_content_secure` | internal | no | string | See original_content. This is the secure version of this content. |
| `passed_sherlock_audit` | internal | no | boolean | Indicates whether the creative has been recently checked by the Xandr automated creative auditing system ("Sherlock"). |
| `pixel_type` |  |  |  | **Deprecated**. Please use the `pixels` field instead. |
| `pixel_url` |  |  |  | **Deprecated**. Please use the `pixels` field instead. |
| `pixel_url_secure` |  |  |  | **Deprecated**. Please use the `pixels` field instead. |
| `pixels` | client | no | array of objects | The pixels to serve with the creative. They can be for external impression tracking, external click tracking, or other purposes, such as adding the AdChoices icon to a creative. See [Pixels](#pixels) below for more details. |
| `placement` | client | no | string(50) | The (optional) name of the placement for this creative - used for reporting/management purposes. |
| `pop_values` |  |  |  | **Deprecated**. |
| `segments` | client | no | array | A list of segments that a user will be added to upon viewing or clicking on this creative. For more information, see [Segments](#segments) below.  Example: `"segments": [ { "id": 11111, "action": "add_on_view" }, { "id": 22222, "action": "add_on_click" } ]` |
| `size_in_bytes` | internal | no | int | The size of the media file in bytes. |
| `sla` | client | no | integer | The target timeframe when requesting a platform audit.  A value of 0 is standard, 2 is priority/rush.  Default is 0. <br> **Note**: When requesting a standard audit, the api will populate this field with a value of null. |
| `ssl_status` | audit team | no | enum('disabled','pending','approved','failed') | Only creatives with ssl_status = approved will be eligible to serve on secure inventory.  **Note**: If a creative fails the ssl Sherlock audit, you can submit it for a retest (once you've fixed the downstream non-secure content) by changing this field to "pending". <br> **Default**: 'disabled' |
| `state` | internal | no | enum | The state of the creative. Possible values are "active" or "inactive" |
| `status` | client | no | object | The status of the creative describing if the creative is ready to serve. See [Status](#status) below for details. |
| `technical_attributes` | audit team | no | List of ints | IDs of technical attributes associated with the creative - see [Technical Attribute Service](technical-attribute-service.md). For GET, these are only returned if you use the flag attributes=true in the request URL. |
| `template` | client | yes | object | The creative template (ex.:  `template_id 6` ) for the creative's format and media type (i.e., flash and expandable). The template includes code to control how the creative renders on web pages. For more details, see [Creative Template](#creative-template) below. <br> **Warning**: When using a template for the "raw-html" format (HTML that will not be served in an iFrame), everything in the `content` field must be `escaped` (quotes, slashes, etc.,) and wrapped in a `document.write()`; statement. This is necessary to deliver the content to the page **Default**: `POST` |
| `text_description` | client | yes, only if format is text | string up to 70 characters | The lower line of text displayed in a text creative |
| `text_display_url` | client | yes, only if format is text | string up to 35 characters | The readable URL displayed in a text creative |
| `text_title` | client | yes, only if format is text | string up to 25 characters | The top line of text displayed in a text creative |
| `track_clicks` |  |  |  | **Deprecated**. |
| `track_clicks` |  |  |  | **Deprecated**. |
| `video_attribute` | client | no | object | Attributes for third-party in-stream (VAST) video creatives. See [Video Attribute](#video-attribute) below for more details. |
| `width` | client | yes | int | The width of the creative in pixels. |

## Mobile

| Field | Type | Description |
|--|--|--|
| `alternative_landing_page_url` | string | An alternative landing page URL that can be viewed in a desktop browser for creatives that have a landing page targeted to a specific device, operating system, or carrier. <br> **Warning**: You must provide an auditable URL in order for your creative to pass auditing. |

## Audio

| Field | Type | Description |
|--|--|--|
| `click_target` | string | The target of the click_action, which is the action that the device should take when the creative is clicked. Enter a URL that our audit team can use to verify the brand and attributes of your audio creative. Ensure that the site the URL points to is in the same language as the audio. This URL is used only for auditing purposes.  <br>**Warning**: You must provide an auditable URL in order for your creative to pass auditing. |

## Video attribute

The template id for `video_attribute` is 6439 - Video: Standard VAST
(also accepts VPAID), and the object includes the following fields:

> [!NOTE]
> Audio The video attribute object is also used to create audio creatives. The template id for audio is 38745 - Xandr Audio Template (VAST). Both XML-urls and audio file urls are accepted.
>
> VAST check.
> When adding a third party VAST or VPAID video creative, a series of checks are performed on the XML. There are different outputs you may see and corrective action that can be taken. See [VAST Check](vast-check.md) for details. 

| Field | Type | Description |
|--|--|--|
| `duration_ms` | double | The duration, in milliseconds, of the in-stream (VAST) video creative. This must be greater than `0`. |
| `is_skippable` | boolean | If `true`, the in-stream (VAST) video creative is skippable. Only third-party skippable VAST video creatives are supported; therefore, when `is_skippable` is `true`, `is_hosted` must be `false`. |
| `wrapper` | object | The VAST document wrapper that contains the `elements` array and the `trackers` array. |

## Video attribute wrapper

The `wrapper` object contains the following fields:

| Field | Type | Description |
|--|--|--|
| `elements` | array | Elements of the VAST wrapper. |
| `secure_url` | string | Secure URL of the VAST document. |
| `url` | string | URL of the VAST document. |

**Video attribute wrapper element**

The `elements` array contains the following fields:

At least one element must be specified.

| Field | Type | Description |
|--|--|--|
| `trackers` | array | VAST event trackers. |
| `type` | string | Read only. Type of element. Possible value: "linear" |
| `vast_element_type_id` | int | VAST element ID. Possible value: `1`: linear |

**Video attribute event trackers**

You can drop pixels on every event that we track in reporting (see
vast_event_type_id below). Add the pixel(s) as `trackers` on the
creative. The `trackers` array contains the following fields:

| Field | Type | Description |
|--|--|--|
| `event_type` | string | Read only. The type of event corresponding to `vast_event_type_id`. |
| `is_segment_pixel` | boolean | Defines the pixel as a segment pixel, and ensures the userid for that event is added to segment regardless of device type. Default value = **false**. Where this is set to **true**, the url must be configured in the standard format: [https://ib.adnxs.com/seg?add=segmentID](https://ib.adnxs.com/sbounce?%2Fseg%3Fadd%3D137401), otherwise you will receive an error. |
| `name` | string | The name of the event tracker. |
| `secure_url` | string | The secure URL of the event tracker. |
| `url` | string | The URL of the event tracker. |
| `vast_event_type_id` | int | The ID of the VAST event. Possible values: <br> -  1: service <br> - 2: start <br> - 3: skip <br> - 4: error <br> - 5: first_quartile <br> - 6: midpoint <br> - 7 : third_quartile <br> - 8: completion <br> - 9: impression <br> - 10: click |

## Creative template  

You can use the [Creative Template Service](creative-template-service.md) to view all rendering templates that can be assigned to creatives.

| Field | Type | Description |
|--|--|--|
| `id` | int | The ID of the creative template. |

Here are standard template ids for the most common creative formats.

| ID | Format | Name |
|--|--|--|
| `1` | url-html | Standard Banner |
| `2` | url-js | Standard Banner |
| `3` | flash | Standard Banner |
| `4` | image | Standard Banner |
| `5` | raw-js | Standard Banner |
| `6` | raw-html | Standard Banner |
| `7` | iframe-html | Standard Banner |
| `8` | url-xml | In-Banner Video |
| `9` | url-html | Popup |
| `10` | url-js | Popup |
| `11` | flash | Popup |
| `12` | image | Popup |
| `13` | raw-js | Popup |
| `14` | raw-html | Popup |
| `15` | iframe-html | Popup |
| `6439` | VAST, VPAID | Standard VAST |

For Expandable creatives, please see the [Expandables and Rich Media](expandables-and-rich-media.md) page for more details.

## Status

| Name | Type | Description |
|--|--|--|
| `user_ready` | boolean | The status of the creative set by the user describing if the creative is ready to serve or not. Possible values: "true" or "false" <br> **Default**: true |
| `hosted_assets_association_complete` | boolean / null | **Read-only**. Status of the creative uploaded by Xandr's internal systems. Possible values: "true" or "false" for hosted creatives and "null" for third-party creatives. |

## Native attribute

The `native_attribute` object contains the following fields. For more information, see **Adding a native creative** in the Examples .

| Field | Type | Description |
|--|--|--|
| `data_assets` | array of objects | Attributes of the native creative. See [Data Assets](#data-assets) below for more details. |
| `image_assets` | array of objects | Attributes of each individual image. See [Image Assets](#image-assets) for more details. |
| `image_trackers` | array of objects | A list of third-party impression tracking URLs intended to be used with native creatives. For more information, see [Image Trackers](#image-trackers) below. |
| `javascript_trackers` | array of objects | A list of third-party impression tracking URLs. For more information, see [Javascript Trackers](#javascript-trackers) below. All OpenRTB and Xandr macros are supported for this field except for ${AUCTION_PRICE} and ${PRICE_PAID}. |
| `link` | object | URLs associated with the native creative. See [Link](#link) below for details. |
| `privacy_url` | string | If support was indicated in the request, URL of a page informing the user about the buyer’s targeting activity. Xandr does not provide a default privacy link. |
| `video_assets` | array of objects | Attributes of the video assets. See Video Assets for more details. |

> [!NOTE]
> Please use image_trackers for impression trackers and link.trackers for click trackers.

## Link

The `link` object contains the landing page URL, fallback URL and Trackers associated with the native creative. The `link` object is required for native attribute.

The `link` object includes the following fields:

| Field | Type | Description |
|--|--|--|
| `fallback_url` | string | A backup url if the main deeplink url is not supported. |
| `trackers` | array of objects | A list of third-party tracking URLs intended to be used with native creatives. This should be an array of click trackers. See [Trackers](#trackers) below for more details. |
| `url` | string | The landing page of the native creative. <br> **Required On** : `POST`,`PUT` |

> [!NOTE]
> All native creatives are submitted for secure auditing by default.
>
> - If the secure url has not been specified for any tracker (image trackers, javascript trackers, and creative image asset trackers), secure audit is disabled for that creative.
>
> - If the secure URL has not been specified, but URL is prefixed wit \`https\`, the creative will be submitted for secure audit.

## Trackers

| Name | Type | Description |
|--|--|--|
| `url` | string | A third-party impression tracking URL. This should contain your impression tracker. |
| `url_secure` | string | A third-party impression tracking URL (that uses SSL). This should contain your impression tracker. |

## Image trackers

| Name | Type | Description |
|--|--|--|
| `url` | string | A third-party impression tracking URL. This should contain your impression tracker. |
| `url_secure` | string | A third-party impression tracking URL (that uses SSL). This should contain your impression tracker. |

## Javascript trackers

| Name | Type | Description |
|--|--|--|
| `url` | string | A third-party javascript tracking URL. |
| `url_secure` | string | A third-party javascript tracking URL (that uses SSL) |

## Data assets

The `data_assets` object includes the following fields:

| Field | Type | Description |
|--|--|--|
| `data_type` | string | The asset type for the native creative. Possible values: <br> - sponsored_by <br> - title <br> - description <br> - rating <br> - call_to_action <br> - display_url <br> - likes <br> - downloads <br> - price <br> - sale_price <br> - phone <br> - address <br> - additional_description |
| `value` | string | The description of the `data_type asset` that you have specified. <br> - "sponsored_by" - brand name of the sponsor <br> - "title" - title of the creative <br> - "description" - description of the product or service being advertised <br> - "rating" - rating of the product being offered <br> - "call_to_action" - suggested action for next step  <br> - "display_url" - the URL you would like displayed <br> - "likes" - social media likes <br> - "downloads" - number downloads/installs of this product <br> - "price" - Price for product / app / in-app purchase <br> - "sale_price" - sale price that can be used together with price to indicate a discounted price <br> - "phone" - phone number "address" - address <br> - "additional_description" - the longer version of your ad's description |

## Image assets

The image`_assets` object includes the following fields:

| Field | Type | Description |
|--|--|--|
| `creative_asset_image` | object | The object containing details of the creative asset. Required for third-party native creatives. See details in [Creative Asset Image](#creative-asset-image) below. |
| `image_type` | string | The format of the image. Possible values include: <br> - icon_image <br> - main_image |

## Creative asset image

| Field | Type | Description |
|--|--|--|
| `height` | int | The height of the image. Value must be > 0 |
| `url` | string | The url of the image. |
| `url_secure` | string | The secure url of the image. |
| `width` | int | The width of the image. Value must be > 0 |

**Video assets**

The video_assets object includes the following fields:

| Field | Type | Description |
|--|--|--|
| `video_creative_id` | int | The Xandr creative id of the video asset associated with the native creative. **Note**: A separate video creative must be registered first before registering a native video creative. |

## Pixels

You use this array to add up to five Xandr-approved and custom pixels to a creative.

**Xandr-approved pixels** are from trusted, commonly-used providers. Most of them do not cause the creative to be resubmitted for audit. To add a Xandr-approved
pixel to a creative, you need to pass only the pixel_template_id and the number of params that the pixel requires. See the "Adding a Xandr-approved pixel to a creative" example below for further guidance. Note that you can use the [Pixel Template Service](pixel-template-service.md) to get information about these pixels, including whether or not they trigger re-audit.

Custom pixels are defined by you and do cause the creative to be resubmitted for audit. To add a custom pixel, you need to pass only the format and, depending on the format, the content or url. See the [Adding a custom pixel to a creative](#adding-a-custom-pixel-to-a-creative) example below for further guidance.

| Field | Type | Description |
|--|--|--|
| `content` | string (255) | If the pixel format is "raw-js", the HTML or JavaScript content to serve with the creative. |
| `format` | enum | The format of the pixel. Possible values: "raw-js", "url-html", "url-js", or "url-image". |
| `id` | int | **Read-only**. The ID of the pixel. |
| `param_1` | string | For Xandr-approved pixel: The value for the first parameter in the pixel content or URL. To find out how many parameters are required for a Xandr-approved pixel, use the [Pixel Template Service](pixel-template-service    .md). |
| `param_2` | string | For Xandr-approved pixel: The value for the second parameter in the pixel content or URL. |
| `param_3` | string | For Xandr-approved pixel: The value for the third parameter in the pixel content or URL. |
| `param_4` | string | For Xandr-approved pixel: The value for the fourth parameter in the pixel content or URL. |
| `param_5` | string | For Xandr-approved pixel: The value for the fifth parameter in the pixel content or URL. |
| `pixel_template_id` | int | The ID of the Xandr-approved pixel. You can use the [Pixel Template Service](pixel-template-service.md) to get this ID. |
| `url` | string (255) | If the pixel format is "url-html", "url-js", "url-image", or "raw-url", the URL of the HTML, JavaScript, or Image pixel to serve with the creative. |

## Segments

These fields will be included in the Segments array:

| Field | Type | Description |
|--|--|--|
| `action` | enum | The action taken by users that will add them to the segment. Possible values: 'add on view' or 'add on click'. <br> **Required On**: POST, PUT |
| `id` | int | The ID of the segment. <br> **Required On**: POST, PUT |
| `name` | string | The segment's name. |
| `segment_id` | int | The ID of the segment. This field contains the same information as the id field. |

| Field | Type | Description |
|--|--|--|
| `landing_page_url` | string | The landing page URL entered by the Xandr administrator during the audit process. <br> **Default**: `null` |
| `thirdparty_campaign_id` | int | **Read-only**. If the campaign has been synced with a third-party, this is the ID in the third-party system. <br> **Default**: `null` |
| `thirdparty_creative_id` | int | **Read-only**. If the creative has been synced with a third-party such as Yahoo Ad Exchange, this is the ID in the third-party system.If an issue arises with the sync, you can reset `thirdparty_creative_id` to null with the following PUT call: `$ curl -b cookies -c cookies -X PUT -d '{"creative":{}}' 'https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID&reset_thirdparty_creative_id'` **Default**: `null` |

## Changes that cause Re-Audit

Once a creative has passed Xandr audit (audit_status is "audited"), changing any of the following fields causes the creative to be resubmitted for audit (allow_audit is set to "pending"):

- width
- height
- content
- media_url
- click_url
- template
- custom_macros
- media_subtypes
- language
- categories
- technical_attributes
- brand_id
- pixel_url
- pixels (if adding or removing a custom pixel or a
  Xandr-approved pixel)
- text_title (if text creative)
- text_description (if text creative)
- text_display_url (if text creative)
- pop_window_maximize (if pop creative)
- pop_is_tag_initiated (if pop creative and changing from false to true)
- video_attribute
- media_assets

Also, if the audit_status is "no_audit", changing allow_audit from "false" to "true" causes the creative to be resubmitted for Xandr audit.

## Examples

**Adding a creative**

``` 
$ cat creative
{
 "creative":
  {     "width" : 300,
        "height" : 250,
        "media_url" : "https://ad.doubleclick.net/adi/ABC.Advertising.com/DEF.40;sz=300x250;click0=",
        "template":{
           "id": 1
        },
       "is_political_and_eu_targeted": false,
       "is_political_and_non_eu_targeted": false
  }
}
```

``` 
$ curl -b cookies -c cookies -X POST -d @creative.json "https://api.adnxs.com/creative/5"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": 703355,
    "creative": {
      "id": 703355,
      "active": true,
      "member_id": 5,
      "description": null,
      "code": null,
      "code2": null,
      "media_url": "https:\/\/ad.doubleclick.net\/adi\/ABC.Advertising.com\/DEF.40;sz=300x250;click0=",
      "audit_status": "pending",
      "allow_audit": true,
      "size_in_bytes": 0,
      "last_checked": null,
      "not_found": 0,
      "added_by_bidder": null,
      "campaign": null,
      "placement": null,
      "format": null,
      "width": 300,
      "height": 250,
      "click_url": null,
      "landing_page_url": null,
      "flash_click_variable": null,
      "no_iframes": false,
      "content": null,
      "original_content": null,
      "track_clicks": true,
      "audit_feedback": null,
      "created_on": "2013-10-31 21:17:17",
      "flash_backup_url": null,
      "is_self_audited": false,
      "file_name": null,
      "is_prohibited": false,
      "last_activity": "2013-10-31 21:17:17",
      "passed_sherlock_audit": true,
      "is_expired": false,
      "creative_upload_status": null,
      "backup_upload_status": null,
      "filter": null,
      "is_suspicious": false,
      "suspicious_activity_timestamp": null,
      "media_subtypes": [
        "banner"
      ],
      "no_adservers": false,
      "is_blanking": false,
      "is_rotating": false,
      "text_title": null,
      "text_description": null,
      "text_display_url": null,
      "click_action": "click-to-web",
      "click_target": null,
      "ssl_status": "disabled",
      "allow_ssl_audit": false,
      "media_url_secure": null,
      "content_secure": null,
      "original_content_secure": null,
      "flash_backup_url_secure": null,
      "is_hosted": false,
      "content_source": "standard",
      "thirdparty_creative_id": null,
      "thirdparty_campaign_id": null,
      "custom_request_template": null,
      "categories": 
     [
        {
        "id": 37,
        "name": "Politics",
        "self declared": true,
        }
     ],
      "brand": {
       "id": 1,
       "name": "Unknown",
       "category_id": 8
      },
      "language": {
        "id": 1,
        "name": "English"
      },
      "template": {
        "id": 1
      },
      "segments": null,
      "pixels": null,
      "mobile": null,
      "brand_id": 1,
      "sla": "0",
      "sla_eta": "2013-11-01 11:18:17"
    }
  }
}
```

**View the creative that was added**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative/5/6'
{
   "response":{
        "status":"OK",
        "creative":{
                "id": 6,
                "active": true,
                "member_id": 5,
                "description": null,
                "code": null,
                "brand_id": 43,
                "media_url": "https:\/\/ad.doubleclick.net\/adi\/ABC.Advertising.com\/DEF.40;sz=300x250;click0=",
                "audit_status": "pending",
                "allow_audit": true,
                "size_in_bytes": 18467,
                "last_checked": null,
                "not_found": false,
                "added_by_bidder": 14,
                "campaign": null,
                "placement": null,
                "format": "url-html",
                "width": 300,
                "height": 250,
                "click_url": "",
                "flash_click_variable": null,
                "pixel_url": "",
                "no_iframes": false,
                "content": null,
                "original_content": null,
                "track_clicks": true,
                "pixel_type": "image",
                "audit_feedback": null,
                "created_on": "0000-00-00 00:00:00",
                "flash_backup_url": null,
                                "is_self_audited": false,
                "last_activity": "2008-08-26 05:41:04",
                                "passed_sherlock_audit": true,
                                "is_expired": false,
                                "creative_upload_status": null,
                                "backup_upload_status": null,
                        "filter": null,
                        "is_suspicious": false,
                        "suspicious_activity_timestamp": null,
                        "media_subtypes": [
                                "banner"
                        ],
                        "no_adservers": false,
                        "is_blanking": false,
                        "is_rotating": false,
                        "text_title": null,
                        "text_description": null,
                        "text_display_url": null,
                        "click_action": "click-to-web",
                        "click_target": null,
                        "ssl_status": "disabled",
                        "allow_ssl_audit": false,
                        "media_url_secure": null,
                        "content_secure": null,
                        "original_content_secure": null,
                        "flash_backup_url_secure": null,
                        "is_hosted": false,
                        "content_source": "standard",
                        "thirdparty_creative_id": null,
                        "thirdparty_campaign_id": null,
                        "custom_request_template": null,
                        "brand": {
                                "id": 5,
                                "name": "Adobe",
                                "category_id": 27
                        },
                        "language": {
                                "id": 16,
                                "name": "Norwegian"
                        },
                        "template": {
                                "id": 1
                                },
                        "segments": null,
                        "pixels": null,
                        "mobile": null,
                        "brand_id": 5,
                        "sla": null,
                        "sla_eta": null
                        }
  }
}
```

**Modifying a creative**

If you then decide to add a campaign name "Triple Play - October 2008" to the creative for reporting purposes:

``` 
$ cat creative_mod
{"creative" : {
        "campaign":"Triple Play - October 2008"
        }
}
$ curl -b cookies -c cookies -X PUT --data-binary @creative_mod 'https://api.adnxs.com/creative/5/6'
{
   "response":{
        "status":"OK",
        "id":6
}}
```

And then to view the change:

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative/5/6'
{
    "response": {
        "creatives": [
            {
                "id": 6,
                "active": true,
                "member_id": 5,
                "description": null,
                "code": null,
                "brand_id": 43,
                "media_url": "https:\/\/ad.doubleclick.net\/adi\/ABC.Advertising.com\/DEF.40;sz=300x250;click0=",
                "audit_status": "pending",
                "allow_audit": true,
                "size_in_bytes": 18467,
                "last_checked": null,
                "not_found": 0,
                "added_by_bidder": 14,
                "campaign": "Triple Play - October 2008",
                "placement": null,
                "format": "url-html",
                "width": 300,
                "height": 250,
                "click_url": "",
                "flash_click_variable": null,
                "pixel_url": "",
                "no_iframes": false,
                "content": null,
                "original_content": null,
                "track_clicks": true,
                "pixel_type": "image",
                "audit_feedback": null,
                "created_on": "2008-08-26 05:41:04",
                "flash_backup_url": null,
                "last_activity": "2008-09-14 06:20:04"
            }
        ],
        "status": "OK"
    }
}
```

**Submit a creative for audit**

If you would like to request an audit for a creative it must be active and have the `allow_audit` field set to true:

``` 
$ cat creative_mod
{"creative" : {
        "audit_status": "pending",
                "allow_audit" : true
        }
}
$ curl -b cookies -c cookies -X PUT --data-binary @creative_mod 'https://api.adnxs.com/creative/5/6'
{
   "response":{
        "status":"OK",
        "id":6
}}
```

**Unexpire a creative and resubmit for audit**

If a creative has expired, you can update it with these settings to set the status to "pending" and resubmit the creative for audit. Note that as of November 2017, creatives that have been expired for over one year will be permanently deleted. See "Expired Creative Policy" at the top of this page for more information.

``` 
$ cat unexpire_creative
{
    "creative": {
    "audit_status": "pending",
    "allow_audit": true,
    "status": {
        "user_ready": true
        }
    }
}
```

**Submit a mobile creative for audit**

This example uses the new `mobile` object:

``` 
$ cat mobile_creative
{
    "creative" : {
        "audit_status": "pending",
        "allow_audit" : true,
        "mobile" : {
                 "alternative_landing_page_url" : "https://..."
        }
    }
}
$ curl -b cookies -c cookies -X PUT --data-binary @creative_mod 'https://api.adnxs.com/creative/5/6'
{
   "response":{
        "status":"OK",
        "id":6
   }
}
```

**Submit a creative for priority audit**

If you would like to submit for a priority audit. Set "sla" to 2 (a value of 1 is not currently used). You will be charged a priority audit fee per your contract.

``` 
$ cat creative_mod
{"creative" : {
        "audit_status": "pending",
        "sla": 2
        }
}
$ curl -b cookies -c cookies -X PUT --data-binary @creative_mod 'https://api.adnxs.com/creative/5/6'
{
   "response":{
        "status":"OK",
        "id":6
}}
```

**View the estimated audit time for your creative ('sla_eta')**

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/creative/5/6'
{
    "response": {
        "creatives": [
            {
                "id": 6,
                ...
                "audit_status": "pending",
                "sla": 0,
                "sla_eta": "2011-05-21 05:33:06"
            }
        ],
        "status": "OK"
    }
}
```

**Adding a creative (third-party HTML tag)**

``` 
$ cat creative
{
 "creative":
  { "width" : 300,
    "height" : 250,
    "media_url" : "https://ad.doubleclick.net/adi/ABC.Advertising.com/DEF.40;sz=300x250;click0=",
    "template":{
       "id": 1
    }
  }
}                       
$ curl -b cookies -c cookies -X POST -d @creative.json 'https://api.sand-08.adnxs.net/creative?member_id=1282'   
  
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "id":816447,
        "creative":{
            "id":816447,
            "active":true,
            "member_id":1282,
            "description":null,
            "code":null,
            "code2":null,
            "media_url":"https:\/\/ad.dblclick.net\/adi\/ABC.Advertising.com\/DEF.40;sz=300x250;click0=",
            "audit_status":"pending",
            "allow_audit":true,
            "size_in_bytes":0,
            "last_checked":null,
            "not_found":0,
            "added_by_bidder":null,
            "campaign":null,
            "placement":null,
            "format":null,
            "width":300,
            "height":250,
            "click_url":null,
            "landing_page_url":null,
            "flash_click_variable":null,
            "no_iframes":false,
            "content":null,
            "original_content":null,
            "track_clicks":true,
            "audit_feedback":null,
            "created_on":"2014-01-24 16:02:31",
            "flash_backup_url":null,
            "is_self_audited":false,
            "file_name":null,
            "is_prohibited":false,
            "last_activity":"2014-01-24 16:02:31",
            "passed_sherlock_audit":true,
            "is_expired":false,
            "creative_upload_status":null,
            "backup_upload_status":null,
            "filter":null,
            "is_suspicious":false,
            "suspicious_activity_timestamp":null,
            "media_subtypes":[
                "banner"
            ],
            "no_adservers":false,
            "is_blanking":false,
            "is_rotating":false,
            "text_title":null,
            "text_description":null,
            "text_display_url":null,
            "click_action":"click-to-web",
            "click_target":null,
            "ssl_status":"disabled",
            "allow_ssl_audit":false,
            "media_url_secure":null,
            "content_secure":null,
            "original_content_secure":null,
            "flash_backup_url_secure":null,
            "is_hosted":false,
            "content_source":"standard",
            "thirdparty_creative_id":null,
            "thirdparty_campaign_id":null,
            "custom_request_template":null,
            "brand":{
                "id":1,
                "name":"Unknown",
                "category_id":8
            },
            "language":{
                "id":1,
                "name":"English"
            },
            "template":{
                "id":1
            },
            "segments":null,
            "pixels":null,
            "mobile":null,
            "brand_id":1,
            "sla":"0",
            "sla_eta":"2014-01-27 00:03:31"
        }
```

**Adding an iframe-html creative**

The creative service allows for a number of different types of creatives to be created. For example, to create a creative using the format "iframe-html", you would upload the raw html that will be embedded in an iframe in the page serving the ad.

``` 
$ cat iframe-html-creative
{
   "creative" : {
        "content":"<script type=\"text/javascript\" language=\"javascript\">
                   var sample_var = 350;
                   </script>
                   <script type=\"text/javascript\" language=\"javascript\" src=\"https://sample_source.com/sample_id?ord=${CACHEBUSTER}\"</script>",
        "width":"300",
        "height":"250",
        "format":"iframe-html",
        "brand_id" : 43
        }
}
$ curl -b cookies -c cookies --data-binary @iframe-html-creative 'https://api.adnxs.com/creative/5'
{
   "response":{
        "status":"OK",
        "id":7
}}
```

**Adding a Xandr-approved pixel to a creative**

This example walks you through the process of adding the Xandr-approved Evidon AdChoices Icon pixel to a creative.

First, you need to find out the pixel_template_id and the number of parameters you must define for the pixel. You use the [Pixel Template Service](pixel-template-service.md) to get this information.

``` 
$ curl -b cookies -c cookies 'https://api.adnxs.com/pixel-template'
{
    "response": {
        "status": "OK",
        "count": 3,
        "start_element": 0,
        "num_elements": 100,
        "pixel-templates": [
            {
                "id": 1,
                "name": "Evidon AdChoices Icon",
                "format": "raw-js",
                "content": "(function() {document.write('<sc'+'ript type=\"text/javascript\"' + ((\"https:\"
                 == document.location.protocol) ? \"https://c.betrad.com\" : \"https://c.betrad.com\") +
                 '/surly.js?;ad_wxh=${CREATIVE_SIZE};coid=${P1};nid=${P2};${P3}\"></scr'+'ipt>');}());",
                "num_required_params": 2,
                "require_reaudit": false
            },
            {
                "id": 2,
                "name": "Brilig Impression Tracker",
                "format": "url-image",
                "num_required_params": 1,
                "require_reaudit": false,
                "url": "https://p.brilig.com/contact/bct?pid=${P1}&_ct=pixel&adid=${CP_ID}&action=1"
            },
            ...
        ],
        "dbg_info": {
            ...
        }
    }
}
```

The Evidon AdChoices Icon pixel is the first in the response. You note that id is 1. You also note that num_required_params is 2. This means that, when adding the pixel to your creative, you must provide values for {P1} and {P2} in the pixel content.

Then you create the JSON-formatted file for adding the pixel to the creative. In the file, you set pixel_template_id to 2, and you set param_1 and param_2 to the values for {P1} and {P2} in the pixel content.

> [!NOTE]
> The pixels array will be completely overwritten with the information in this file. Therefore, if the creative already includes any pixels, be sure to specify them in the file as well.


``` 
$ cat creative_update
{
    "creative": {
        "pixels": [
            {
                "pixel_template_id": 1,
                "param_1":"12",
                "param_2":"34"
            }
        ]
    }
}
```

Finally, you make a PUT call to update the creative. The pixels array in the response then shows that the pixel has been added. The two parameters are defined and have been populated in the pixel content. Note that, because the Evidon AdChoices Icon pixel does **not** cause the creative to require re-auditing, audit_status has not be reverted to "pending".

``` 
$ curl -b cookies -c cookies -X PUT -d @creative_update 'https://api.adnxs.com/creative/3/503577'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "503577",
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https://creative.com/300x250",
            "id": 503577,
            "code": null,
            "code2": null,
            "state": "active",
            "click_track_result": "not_tested",
            "member_id": 3,
            ...
            "audit_status": "audited",
            ...
            "pixels": [
                {
                    "id": 163,
                    "pixel_template_id": 1,
                    "param_1": "12",
                    "param_2": "34",
                    "param_3": null,
                    "param_4": null,
                    "param_5": null,
                    "format": "url-image",
                    "content": "(function() {document.write('<sc'+'ript type=\"text/javascript\"' +
                     ((\"https:\" == document.location.protocol) ? \"https://c.betrad.com\" :
                     \"https://c.betrad.com\") + '/surly.js?;ad_wxh=${CREATIVE_SIZE};coid=12;nid=34;
                     \"></scr'+'ipt>');}());"
                }
            ],
            ...
        },
        "dbg_info": {
            ...
        }
    }
}
```

## Adding a custom pixel to a creative

In this example, the PUT request adds a custom url-js pixel to creative 503577. In the JSON-formatted file, the format is set to "url-js", and the url is set to the location of the JavaScript that you want to serve with the creative. Note in the response that audit_status is "pending"; this is because adding a custom pixel to a creative causes the creative to be resubmitted for audit.

> [!NOTE]
> The pixels array will be completely overwritten with the information in this file. Therefore, if the creative already includes any pixels, be sure to specify them in the file as well.


``` 
$ cat creative_update
{
    "creative": {
        "pixels": [
            {
                "format": "url-js",
                "url":"https://50.16.221.228/render_js?cb=${CACHEBUSTER}&uid=${USER_ID}&ref=${REFERER_URL}
                 &campaign_id=147"
            }
        ]
    }
}
$ curl -b cookies -c cookies -X PUT -d @creative_update 'https://api.adnxs.com/creative/3/503577'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "503577",
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https://creative.com/300x250",
            "id": 503577,
            "code": null,
            "code2": null,
            "state": "active",
            "click_track_result": "not_tested",
            "member_id": 3,
            ...
            "audit_status": "pending",
            ...
            "pixels": [
                {
                    "id": 196,
                    "pixel_template_id": null,
                    "param_1": null,
                    "param_2": null,
                    "param_3": null,
                    "param_4": null,
                    "param_5": null,
                    "format": "url-js",
                    "url": "https://50.16.221.228/render_js?cb=${CACHEBUSTER}&uid=${USER_ID}
                     &ref=${REFERER_URL}&campaign_id=147"
                }
            ],
            ...
        },
        "dbg_info": {
            ...
        }
    }
}
```

**Add a video creative with video attribute object and wrapper**

``` 
{
    "creative": {
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
                                "vast_event_type_id": 2,
                                "url": "http://tracker.com/...",
                                "secure_url": "https://tracker.com/...",
                                                                "event_type": "start"
                            },
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

**Adding a native creative**

When adding a native creative, use template ID 39461.

``` 
cat native
{
        "creative": {
                "description": "native_test",
                "brand_id": 1,
                "media_url": "https://mediaurl.com",
                "code": "test",
                "code2": null,
                "member_id": 4,
                "state": "active",
                "template": {
                        "id": 39461
                },
                "native_attribute": {
                        "link": {
                                "url": "https://url.com",
                                "fallback_url": "https://fallback.com",
                                "trackers": [{
                                        "url": "http://url.com",
                                        "url_secure": "https://secureurl.com"
                                }]
                        },
                        "data_assets": [{
                                "data_type": "sponsored_by",
                                "value": "a value"
                        }, {
                                "data_type": "rating",
                                "value": "8"
                        }],
                        "image_assets": [{
                                "image_type": "icon_image",
                                "creative_asset_image": {
                                        "url": "http://url.com",
                                        "url_secure": "https://secureurl.com",
                                        "height": 1,
                                        "width": 1
                                }
                        }],
                        "image_trackers": [{
                                "url": "http://url.com",
                                "url_secure": "https://secureurl.com"
                        }],
                        "javascript_trackers": [{
                                "url": "http://url.com",
                                "url_secure": "https://secureurl.com"
                        }]
                },
                "thirdparty_viewability_providers": null,
                "status": {
                        "user_ready": true
                },
                "sla_eta": null
        }
}
$ curl -b cookies -c cookies -X POST -s @native 'https://api.adnxs.com/creative/4'
{
        "response": {
                "status": "OK",
                "count": 1,
                "id": 411,
                "start_element": 0,
                "num_elements": 100,
                "dbg_info": {
                        ...
                },
                "creative": {
                        "description": "native_test",
                        "brand_id": 1,
                        "media_url": "https://mediaurl.com",
                        "id": 411,
                        "code": "test",
                        "code2": null,
                        "member_id": 4,
                        "state": "active",
                        "click_track_result": "not_tested",
                        "format": "url-file",
                        "width": null,
                        "height": null,
                        "click_url": null,
                        "flash_click_variable": null,
                        "no_iframes": false,
                        "content": null,
                        "original_content": null,
                        "file_name": null,
                        "track_clicks": true,
                        "audit_status": "pending",
                        "macros": null,
                        "profile_id": null,
                        "audit_feedback": null,
                        "is_prohibited": false,
                        "is_suspicious": false,
                        "created_on": "2017-03-09 21:54:11",
                        "flash_backup_url": null,
                        "last_modified": "2017-03-09 21:54:11",
                        "is_control": false,
                        "allow_audit": true,
                        "is_expired": false,
                        "creative_upload_status": null,
                        "backup_upload_status": null,
                        "use_dynamic_click_url": false,
                        "media_subtypes": [
                                "popunder",
                                "popup",
                                "banner"
                        ],
                        "size_in_bytes": 0,
                        "is_self_audited": false,
                        "no_adservers": false,
                        "text_title": null,
                        "text_description": null,
                        "text_display_url": null,
                        "click_action": "click-to-web",
                        "click_target": null,
                        "ssl_status": "pending",
                        "allow_ssl_audit": true,
                        "media_url_secure": "https://MEDIAURL.appnexus.com",
                        "content_secure": "document.write(\\\"\\\")",
                        "original_content_secure": null,
                        "flash_backup_url_secure": null,
                        "is_hosted": false,
                        "content_source": "standard",
                        "lifetime_budget": null,
                        "lifetime_budget_imps": null,
                        "daily_budget": null,
                        "daily_budget_imps": null,
                        "enable_pacing": null,
                        "allow_safety_pacing": null,
                        "landing_page_url": null,
                        "thirdparty_creative_id": null,
                        "thirdparty_campaign_id": null,
                        "facebook_audit_status": null,
                        "facebook_audit_feedback": null,
                        "custom_request_template": null,
                        "language": {
                                "id": 1,
                                "name": "English"
                        },
                        "brand": {
                                "id": 1,
                                "name": "Unknown",
                                "category_id": null
                        },
                        "template": {
                                "id": 329,
                                "name": "native ad",
                                "media_subtype_id": 17,
                                "format_id": 11
                        },
                        "ios_ssl_audit": null,
                        "adx_audit": null,
                        "custom_macros": null,
                        "segments": null,
                        "folder": null,
                        "campaigns": null,
                        "line_items": null,
                        "competitive_brands": null,
                        "competitive_categories": null,
                        "pixels": null,
                        "mobile": null,
                        "video_attribute": null,
                        "media_assets": null,
                        "sla": null,
                        "thirdparty_pixels": null,
                        "native": null,
                        "native_attribute": {
                                "link": {
                                        "url": "https://url.com",
                                        "fallback_url": "https://fallback.com",
                                        "trackers": [{
                                                "url": "http://url.com",
                                                "url_secure": "https://secureurl.com"
                                        }]
                                },
                                "data_assets": [{
                                        "data_type": "sponsored_by",
                                        "value": "a value"
                                }, {
                                        "data_type": "rating",
                                        "value": "8"
                                }],
                                "image_assets": [{
                                        "image_type": "icon_image",
                                        "creative_asset_image": {
                                                "url": "https://vcdn.adnxs.com/sand/creative-image/ea/f5/30/28/eaf53028-e6c6-4ac0-bcbb-ce8fe14b73ab.png",
                                                "url_secure": "https://secureurl.com",
                                                "height": 12,
                                                "width": 34
                                        }
                                }],
                                "image_trackers": [{
                                        "url": "http://url.com",
                                        "url_secure": "https://secureurl.com"
                                }],
                                "javascript_trackers": [{
                                        "url": "http://url.com",
                                        "url_secure": "https://secureurl.com"
                                }]
                        },
                        "thirdparty_viewability_providers": null,
                        "status": {
                                "user_ready": true,
                        },
                        "sla_eta": null,
                        "currency": "USD",
                        "type": "standard"
                }
        }
}
```

**Determining the Technical Atttributes assigned to your creative**

Although technical attributes isn't something that can be added to the automated reports today, this can be retrieved through the Creative service in the bidder API. For more information please refer to the [Technical Attribute Service](technical-attribute-service.md)

This can be accessed by adding the query string parameter "?attributes=true" as: "[adnxs.com/creative/MEMBER_ID/CREATIVE_ID?attributes=true](https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID?attributes=true)"

``` 
"technical_attributes": [
{
 "id": 2,
 "name": "Flash"
},
{
 "id": 9,
"name": "Initial Load > 40kb"
},
 {
  "id": 13,
  "name": "Banner has AdChoices Icon"
 },
 {
  "id": 15,
  "name": "Animated: 15 seconds or less"
 }
 ]
```

The [Meta Service](https://api.adnxs.com/creative/MEMBER_ID/CREATIVE_ID?attributes=true) provides the most up to date information about interfacing with objects in our API.

**Creative Macros**

The impression bus supports two types of creative macros replaced in real time: pre-defined **Xandrcreative macros** and **custom macros** that can be defined by the bidder. The main difference between the two is the perspective. For example, the impression bus has no knowledge of a Campaign or an Insertion Order when a real time bid is placed, so any objects supported with a bidder's internal object model and required in a macro should be supported using custom macros.

> [!WARNING]
> Macro Restrictions
>
> - Only pre-defined Xandr macros and custom macros are supported when registering creatives.
>
> - DO NOT use OpenRTB macros when registering creatives. OpenRTB macros are for use only in the [bid response](incoming-bid-response-from-bidders.md).
> - Do not give a custom macro a name that matches the name of an OpenRTB macro.

**Xandr creative macros**

See [Xandr Macros](xandr-macros.md) for a complete list of the available creative macros.

**Click Tracking Example**:

``` 
"media_url": "https://ad.doubleclick.net/adi/N5364.Ivillage.com/B2965815.5;sz=728x90;click0=${CLICK_URL};ord=${CACHEBUSTER}?"
```

**Custom Macros**

Using custom_macro functionality in the [Bid Response](incoming-bid-response-from-bidders.md), you can dynamically pass into the pre-registered creatives. For instance, if you wanted to always return a particular campaign and reporting code, you could set up your creative as follows:

``` 
{
   "creative":{
       "media_url":"https://adserver.com/imp?z=300x250;camp=${CAMPAIGN_ID};int=${INT_CODE}",
       "format":"url-html",
       "width":"300",
       "height":"250"
}}
```

Then, when your bidder responds to an auction, the bid response can
specify the name and value of the macros to replace, by including, for
example:

``` 
"custom_macros":[
{
   "name":"CAMPAIGN_ID",
   "value":"452346"
},
{
   "name":"INT_CODE",
   "value":"a352-45we-sdr3"
}]
```

> [!NOTE]
> Even if the value is an integer, it must be placed within quotation marks (for example,  `"42"`).

``` 
<iframe src="https://adserver.com/sz=300x250;camp=452346;int=a352-45we-sdr3" width=300 height=250/>
```