---
title: Creative Service
description: In this article, learn about the Digital Platform API's Creative service, their JSON fields, and REST API with thorough examples.
ms.date: 07/08/2025
ms.custom: digital-platform-api
---

# Digital Platform API - Creative service

You can use the Creative Service to add creatives to our system. All creatives must be attached to an advertiser or publisher.

- You can view your advertiser ID by calling the [Advertiser Service](advertiser-service.md).
- You can view your publisher ID by calling the [Publisher Service](publisher-service.md).
- You can attach a creative to a publisher for use as a default creative for a placement. You would then attach the creative to a placement via its ID using the [Placement Service](placement-service.md).

> [!NOTE]
> Effective September 1, 2025: Declare whether your ad is political and intended to be served in the EU via the `is_political_and_eu_targeted` and `is_political_and_non_eu_targeted` fields. To learn more, please refer to the upcoming updates to [Monetize Creative Standards regarding political ad](../monetize/creative-standards).


## Auditing

Xandr works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. For quality assurance, all creatives that serve on third-party inventory must be pre-registered using the Creative Service.

- Creatives are identified by their media_url (either a third-party adserver URL or a Content Delivery Network URL for a Flash, image, or video file).
- Xandr checks media_urls on a regular basis. If a file disappears, the creative will be treated as unaudited.
- Once a creative has passed Xandr's audit, certain changes to the creative cause it to be resubmitted for audit. For more details, see [Changes That Cause Re-Audit](#changes-that-cause-re-audit) below.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/creative?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative?advertiser_id=ADVERTISER_ID)<br>(creative JSON) | Add a new creative to one of your advertisers. |
| `POST` | [https://api.appnexus.com/creative?publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative?publisher_id=PUBLISHER_ID)<br>(creative JSON) | Add a new creative to one of your publishers. |
| `PUT` | - [https://api.appnexus.com/creative?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/creative?id=CREATIVE_ID&publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative?id=CREATIVE_ID&publisher_id=PUBLISHER_ID)<br>(creative JSON) | Modify an existing creative. |
| `GET` | [https://api.appnexus.com/creative](https://api.appnexus.com/creative) | View all creatives. |
| `GET` | - [https://api.appnexus.com/creative?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative?advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/creative?advertiser_code=ADVERTISER_CODE](https://api.appnexus.com/creative?advertiser_code=ADVERTISER_CODE)<br>- [https://api.appnexus.com/creative?publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative?publisher_id=PUBLISHER_ID)<br>- [https://api.appnexus.com/creative?publisher_code=PUBLISHER_CODE](https://api.appnexus.com/creative?publisher_code=PUBLISHER_CODE) | View all creatives for an advertiser or publisher.<br><br>**Note:**<br>You can filter for creatives based on when they first and last served. This is particularly useful when you are approaching your [object limit](object-limit-service.md) and need to identify creatives that can be deleted from the system. For more details, see [First Run/Last Run](#first-runlast-run) below. |
| `GET` | - [https://api.appnexus.com/creative?id=CREATIVE_ID](https://api.appnexus.com/creative?id=CREATIVE_ID)<br> - [https://api.appnexus.com/creative?code=CREATIVE_CODE](https://api.appnexus.com/creative?code=CREATIVE_CODE) | View a specific creative. |
| `GET` | [https://api.appnexus.com/creative?id=1,2,3](https://api.appnexus.com/creative?id=1,2,3) | View multiple creatives by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/creative?audit_stats=true](https://api.appnexus.com/creative?audit_stats=true) | View creative audit stats.<br><br>**Note:**<br>The response tells you the number of creatives with each Xandr, Microsoft, and Google audit status. For the response format, see the [Examples](#examples) below. |
| `DELETE` | - [https://api.appnexus.com/creative?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID)<br>- [https://api.appnexus.com/creative?id=CREATIVE_ID&publisher_id=PUBLISHER_ID](https://api.appnexus.com/creative?id=CREATIVE_ID&publisher_id=PUBLISHER_ID) | Delete a creative.<br><br>**Note:** You cannot delete a creative that is used as the default creative for a member or placement. Default creatives can be deleted once they are disassociated from a placement. |
| `GET` | [https://api.appnexus.com/creative/meta](https://api.appnexus.com/creative/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The internal ID associated with the creative.<br>**Default:** Auto-generated number.<br>**Required On:** `PUT`, in query string. |
| `code` | string (100) | The custom code for the creative. **Note**: It is important for this code to be unique. |
| `code2` | string (100) | The additional custom code for the creative. **Note**: It is important for this code to be unique.|
| `name` | string (400) | The name for the creative. |
| `type` | enum | The type of creative. Possible values:<br> - `"standard"`<br>`"html"`<br> - `"video"`<br><br>**Note:**<br>**Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.<br><br>**Read Only.** |
| `advertiser_id` | int | The ID of the advertiser to which the creative is attached.<br>**Required On:** `POST`/`PUT`, in query string, if the creative is attached to an advertiser. |
| `political` | object |**Read only.** If this creative is "political" and will serve in the US, this object is populated with the elements required for US political creatives. For more information, see the description of the [Political object](#political) below.<br>**Default:** `null` |
| `publisher_id` | int | The ID of the publisher/media buy to which the creative is attached.<br>**Required On:** `POST`/`PUT`, in query string, if the creative is attached to a publisher. |
| `brand_id` | int | The ID of the brand of the company advertising the creative. If included, it will be verified by the Xandr auditing team. If not included, it will be assigned by the auditing team. To retrieve a full list of brands, see the [Brand Service](brand-service.md). |
| `state` | enum | The state of the creative. Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `status` | object | The status of the creative describing if the creative is ready to serve. For more details, see [Status](#status) below. |
| `click_track_result` | enum | The result of the click track test, a feature only available in the user interface. Possible values: `"not_tested"`, `"passed"`, or `"failed"`.<br>**Default:** `"not_tested"` |
| `campaigns` | array of objects | The list of campaigns to which the creative is associated. For more details, see [Campaigns](#campaigns) below.<br><br>**Note:** This field will only be returned if an `advertiser_id` is specified in the query string. |
| `format` | enum | **Deprecated.** |
| `template` | object | The creative template (ex.: `template_id` `6`) for the creative's format and media type (i.e., flash and expandable). The template includes code to control how the creative renders on web pages. For more details, see [Creative Template](#creative-template) below.<br><br>**Note:** When using a template for the `"raw-html"` format (HTML that will not be served in an iFrame), everything in the `content` field must be `escaped` (quotes, slashes, etc.,) and wrapped in a `document.write();` statement. This is necessary to deliver the content to the page.<br>**Required On:** `POST` |
| `thirdparty_page` | object | **Note:** This field is no longer in use. |
| `custom_macros` | array of objects | The values for custom macros used in the creative template. For more details, see [Custom Macros](#custom-macros) below.<br>**Required On:** `POST`, if template includes required custom macros. |
| `width` | Int | The width of the creative; the string should contain an int.<br>**Required On:** `POST`, if template is for the `"Banner"` or `"Expandable"` media type. |
| `height` | Int | **Required On:** `POST`, if template is for the `"Banner"` or `"Expandable"` media type.<br>The height of the creative; the string should contain an int. If the creative's template has a Pop media type, then either the creative's `height` must be set OR `pop_window_maximize` (in the `pop_values` field) must be `true` (but not both).<br><br>**Note:** You can only submit pop creatives of accepted sizes for Xandr audit. If `media_subtype_id` within the `template` array is 4 (popunder) and `audit_status` is `"pending"`, `height` must be set to 300 and `width` to 720. If `media_subtype_id` within the `template` array is 2 (popup) and `audit_status` is `"pending"`, `width` and `height` must be one of the following: 250x250, 300x250, 550x480.<br>**Required On:** `POST`, if template is for the `"Banner"` or `"Expandable"` media type. |
| `media_url` | string (1000) | The URL of the creative - can be image, flash, HTML, javascript (see format). URL must exist and should be on a CDN or equivalent.<br>**Required On:** `POST`, if not using content. |
| `media_url_secure` | string (1000) | The URL of the secure (HTTPS) creative - can be image, flash, HTML, javascript (see format) to be served on a secure ad call. URL must exist and should be on a CDN or equivalent. |
| `click_url` | string (2000) | `click_url` is being deprecated in favor of `click_target`.<br><br>**Note:**<br>This value must begin with "http://" or "https://"<br>**Required On:** `POST`, if template is for the "image" format. |
| `file_name` | string (1000) | The file name and extension for a hosted creative. Allowed file types: jpg, gif, png, swf, flv, mp4, wmv, f4v, avi, m4v, mov, and mpg.<br>**Required On:** `POST`, if adding a hosted creative. |
| `flash_click_variable` | string (255) | The ClickTag variable in a Flash creative. Xandr can execute and track user clicks on a Flash creative only if you provide the exact variable in the file (clickTAG, ClickTag, Clicktag, etc). You can use the ClickTags Service to identify this variable. If you need to specify more than one ClickTag variable for a single creative, contact support.<br><br>**Note:** This field may only be updated (via `POST` or `PUT`) for Flash creatives. |
| `content` | string | Javascript or HTML content when `"format"` is `"raw-js"` or `"iframe-html"`. For a hosted creative, the content of the file must be base64-encoded and submitted as a string within the content field.<br><br>**Tip:** When using a template (example: `template_id` `6`) for the `"raw-html"` format (HTML that will not be served in an iFrame), everything in the `content` field must be `escaped` (quotes, slashes, etc.,) and wrapped in a `document.write();` statement. This is necessary to deliver the content to the page.<br><br>**Tip:** There is a maximum length in the content field of 65535 characters.<br>**Required On:** `POST`, if not using `media_url`.<br>**Default:** 3rd party tag holder. |
| `content_secure` | string | Javascript or HTML content when `"format"` is `"raw-js"` or `"iframe-html"` served on a secure ad call. |
| `original_content` | string | The value you pass into the `"content"` field through the UI will be returned in this field unchanged. The `"content"` field will contain the content modified by Xandr to properly serve. This field can also be uploaded directly through the API. In this case, the value uploaded to this field will be referenced in the content section of the UI (Creative Content > Tag field).<br>**Required On:** `POST` when submitting as type `raw-html`. |
| `original_content_secure` | string | See `original_content`. This is the secure version of this content. |
| `macros` | string | The API pulls out macros and puts them in this field so that the bidder knows which macros to expect.<br>**Read Only.** |
| `audit_status` | enum | The audit status of the creative. Possible values: `"no_audit"`, `"pending"`, `"rejected"`, or `"audited"`.<br><br>**Note:**<br> - If `allow_audit` is `false`, this field must be `"no_audit"`.<br> - If a creative is expired, you can reanimate it by changing this field. Setting it to `"pending"` will resubmit it for auditing. The **user_ready** field also needs to set to true in order to reactivate a expired creative. For changes that automatically resubmit the creative for auditing, see [Changes That Cause Re-Audit](#changes-that-cause-re-audit) below.<br> - You can only submit pop creatives of accepted sizes for Xandr audit. If `media_subtype_id` within the `template` array is 4 (popunder), `audit_status` can not be set to `"pending"` unless `width` is 720 and `height` is 300. If `media_subtype_id` within the `template` array is 2 (popup), `audit_status` can not be set to pending unless `width` and `height` are one of the following: 250x250, 300x250, 550x480.<br><br>**Default:** `"pending"` |
| `audit_feedback` | string | The creative auditing team can pass messages about a creative in this field.<br>**Read Only.** |
| `allow_audit` | Boolean | If `true`, the creative will be submitted for auditing. If `false`, the creative will not be submitted. Unaudited creatives can only run on a network's managed inventory.<br><br>**Note:**<br> - If `audit_status` is `"no_audit"`, this field must be `"false"`.<br> - If your member is not yet active, you can add creatives, but they will not be submitted for audit (`allow_audit` will be `false`). Once your member has been activated, if you want these creatives to be audited, you must update the creatives and set `allow_audit` to `true`.<br> - You can only submit pop creatives of accepted sizes for Xandr audit. If `media_subtype_id` within the `template` array is 4 (popunder), `allow_audit` can not be set to 1 unless `width` is 720 and `height` is 300. If `media_subtype_id` within the `template` array is 2 (popup), `allow_audit` can not be set to 1 unless `width` and `height` are one of the following: 250x250, 300x250, 550x480.<br><br>**Default:** `true` |
| `ssl_status` | enum | The ssl (HTTPS) status of the creative. Only creatives with ssl_status = approved will be eligible to serve on secure inventory.<br><br>**Note:**<br>If a creative fails the ssl Sherlock audit, you can submit it for a retest (once you've fixed the downstream non-secure content) by changing this field to `"pending"`. Allowed values:<br> - `"disabled"`<br> - `"pending"`<br> - `"approved"`<br> - `"failed"`<br><br>**Default:** `"disabled"` |
| `allow_ssl_audit` | Boolean | If `true`, the creative will be submitted for secure (HTTPS) auditing. If `false`, the creative will not be submitted. If `true`, either `media_url_secure` or `content_secure` is required as well.<br>**Default:** `true`, if `media_url_secure` or `content_secure` is provided. Otherwise, `false` will be the default. |
| `msft_audit_status` | enum | **Deprecated.** |
| `msft_audit_feedback` | string | **Deprecated.** |
| `facebook_audit_status` | enum | **Note:** This field is no longer in use. |
| `facebook_audit_feedback` | string | **Note:** This field is no longer in use. |
| `is_self_audited` | Boolean | If `true`, the creative is self-audited and thus will not go through Xandr platform audit. The creative can only serve on inventory that accepts your self-classified creative or on inventory that accepts unaudited creatives.<br>**Default:** `false` |
| `is_expired` | Boolean | If your creative (1) has not run and (2) has not been modified in 45 days, then it will be automatically marked expired and will not serve on any inventory.<br> - Expired creatives must be reaudited to run on third-party inventory. To unexpire a creative for third-party inventory, set `audit_status` to `"pending"`.<br> - Expired creatives do not need to be reaudited to run on direct inventory. To unexpire a creative for direct inventory, set `audit_status` to `"no_audit"`.<br>**Default:** `false`<br>**Read Only.** |
| `is_prohibited` | Boolean | If Sherlock flags the creative for having malware or loading blocked domains, this is set to true to prevent the creative from serving.<br>**Default:** `false`<br>**Read Only.** |
| `is_hosted` | Boolean | If `true`, the creative is hosted by Xandr.<br>**Read Only.** |
| `lifetime_budget` | double | The lifetime budget in dollars.<br><br>**Note:** To include this field in a `GET` response, pass `attributes=1` in the query string.<br><br>**Default:** `unlimited` |
| `lifetime_budget_imps` | int | The lifetime limit for number of impressions.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `daily_budget` | double | The daily budget in dollars.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `daily_budget_imps` | int | The daily limit for number of impressions.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `unlimited` |
| `enable_pacing` | Boolean | If `true`, daily budgeted spend is spread evenly throughout a day.<br><br>**Note:**<br>To include this field in a `GET` response, pass `attributes=1` in the query string.<br>**Default:** `true` |
| `allow_safety_pacing` | Boolean | **Admin-only.** If `true`, spend per minute is limited to a maximum of 1% of the lifetime budget and 5% of the daily budget. |
| `profile_id` | int | You can attach targeting such as gender and geography to a creative by creating a [profile](profile-service.md) and associating it here. |
| `folder` | object | To arrange your creatives in folders for convenience (usually in the UI) you will create a folder using the [Creative Folder Service](creative-folder-service.md) and then associate it here via folder ID or in the Creative Folder service via creative ID. Output is: <br> `{"id": "41", "name": "MyFolder"}` |
| `line_items` | array of objects | The line items that are associated with the creative. For more details, see [Line Items](#line-items) below. |
| `pixels` | array of objects | The pixels to serve with the creative. They can be for external impression tracking, external click tracking, or other purposes, such as adding the AdChoices icon to a creative. For more details, see [Pixels](#pixels) below. |
| `pixel_url` | string (100) | **Deprecated.** Use the pixels array instead. The URL of an impression pixel to serve with the media URL or content. |
| `pixel_url_secure` | string (100) | **Deprecated.** Use the pixels array instead. The URL of a secure (HTTPS) impression pixel to serve with the media URL content on a secure ad call. |
| `pixel_type` | enum | **Deprecated.** Use the pixels array instead. The type of impression pixel. This field must be set if pixel_url is used. Possible values: `"javascript"` or `"image"`. |
| `no_iframes` | Boolean | **Deprecated.** If `true`, the bidder will not serve this creative when an iframe is detected in the ad call.<br>**Default:** `false` |
| `track_clicks` | Boolean | **Deprecated.**<br>**Default:** `true` |
| `flash_backup_content` | string | For a flash creative, this is the content of the backup creative that will be served if a user's browser does not support flash. For an in-banner video creative, this is the content of the poster image that will display before users click play and after the video has finished playing. This field must be used in combination with `flash_backup_file_name`.<br>Once the backup creative has been uploaded, the content will be stored on the CDN, and the location will be set in the flash_backup_url field. Neither flash_backup_content nor `flash_backup_file_name` can be retrieved on `GET`.<br>**Required On:** `POST`/`PUT`, if using `flash_backup_file_name`.<br>**Write Only.** |
| `flash_backup_file_name` | string | This field must be used in combination with `flash_backup_content`. This is the file name and extension of the backup creative.<br>**Required On:** `POST`/`PUT`, if using `flash_backup_content`.<br>**Write Only.** |
| `flash_backup_url` | string (100) | For a flash creative, this is the URL of a 3rd-party creative that will be served if the user's browser does not support flash. For an in-banner video creative, this is the URL of the poster image that will display before users click play and after the video has finished playing. |
| `is_control` | Boolean | This is a flag used to mark this creative as part of a control/test group in A/B testing.<br>**Default:** `false` |
| `segments` | array | A list of segments that a user will be added to upon viewing or clicking on this creative. For more information, see [Segments](#segments) below. |
| `created_on` | timestamp | The date and time when this creative was created. If it was created before January 2010, this will be zero.<br>**Read Only**. |
| `last_activity` | timestamp | The date and time when the creative was last modified. Timezone is UTC.<br>**Read Only.** |
| `media_subtypes` | array of strings | **Deprecated.** |
| `creative_upload_status` | enum | **Deprecated.** |
| `backup_upload_status` | enum | **Deprecated.** |
| `use_dynamic_click_url` | Boolean | If `true`, the (optional) landing page URL for non-3rd party image and flash creatives is set at the campaign or line item level.<br>**Default:** `false` |
| `size_in_bytes` | int | The size of an uploaded creative (in bytes).<br>**Read Only.** |
| `text_title` | string (25) | The top line of text displayed in a text creative.<br>**Required On:** `POST`, if template is for the `"text"` format. |
| `text_description` | string (70) | The lower line of text displayed in a text creative.<br>**Required On:** `POST`, if template is for the `"text"` format. |
| `text_display_url` | string (35) | The readable URL displayed in a text creative.<br>**Required On:** `POST`, if template is for the `"text"` format. |
| `click_action` | enum | The action that the device should take when the creative is clicked. Currently, this field will be set to the only supported click action, `"click-to-web"`.<br>**Default:** `"click-to-web"` |
| `click_target` | string (2000) | The target of the `click_action`. For click-to-web, this is the `click_url` of the creative.<br>`click_url` will eventually be deprecated in favor of this field. In the meantime, setting `click_url` or `click_target` will have the same effect. |
| `categories` | array of objects | The categories that describe the creative and offer type.<br>**Note:**<br>To include categories in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of categories, see the [Category Service](category-service.md). |
| `adservers` | array of objects | The ad servers that deliver the creative or are called for data collection purposes during the delivery of the creative.<br><br>**Note:** To include adservers in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of ad servers, see the [Ad Server Service](ad-server-service.md).<br>**Read Only.** |
| `technical_attributes` | array of objects | The attributes that describe technical characteristics of the creative, such as `"Expandable"` or `"Video"`.<br><br>**Note:**<br>To include technical attributes in a `GET` response, pass `attributes=1` in the query string. To retrieve a full list of technical attributes, see the [Technical Attribute Service](technical-attribute-service.md). |
| `language` | object | The language of the creative. To retrieve a full list of languages, see the [Language Service](language-service.md). |
| `brand` | object | The brand of the company advertising the creative and the category associated with the brand. For more details, see [Brand](#brand) below.<br>**Read Only.** |
| `pop_values` | array | **Deprecated.** |
| `sla` | int | Creatives set to `0` will be submitted for audit with a standard SLA.<br><br>**Caution:** Creatives submitted with any number other than `0` will result in a priority audit (when enabled) and resulting fees.<br>If you have a supplemental services agreement with Xandr for priority audits, you can submit a creative for priority audit (auditing within 2 hours during business hours) by setting this field to `2`. |
| `sla_eta` | timestamp | The estimate time of completion for a priority audit.<br>**Read Only.** |
| `currency` | string | Read-only. The code that defines the advertiser's primary currency (for example, USD). For more details about the currency types available, see [Currency Service](currency-service.md).<br>**Default:** Member's default currency. |
| `first_run` | timestamp | The date and time when the creative first served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to filter creatives based on when they first served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `last_run` | timestamp | The date and time when the creative last served, refreshed on an hourly basis. This value reflects the UTC time zone. To include this information in a `GET` response, pass `flight_info=true` in the query string. For details about how to creatives based on when they last served, see [First Run/Last Run](#first-runlast-run) below.<br>**Read Only.** |
| `mobile` | object | Information needed for mobile creatives to pass the creative audit. See [Mobile](#mobile) below. |
| `video_attribute` | object | Attributes for third-party in-stream (VAST) and hosted video creatives.<br><br>**Note:**<br>To add & update vast creatives, use the `/creative-vast` service. For detailst, see [Creative Vast Service](creative-vast-service.md).<br>**Default:** `null` |
| `stats` | object | The `stats` object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `content_source` | string | The source of this creative's content.<br>**Default:** `"standard"`<br>Allowed values:<br> - `"standard"`: This creative consists of content hosted on an ad server, that will generally be retrieved with a single HTTP request.<br> - `"mediation"`: This creative is a container that is used to fetch content from another ad server for the purposes of mediation. Due to the way mediation is performed, this can involve making multiple HTTP requests in sequence. For more information, see the [Creative Custom Request Template Service](creative-custom-request-template-service.md).<br><br>**Note:** If this field is set to `"mediation"`, the following actions will occur:<br> - A `"mediation"` technical attribute will be added to the creative's `technical_attributes` array.<br>In addition, the following validations will be performed:<br> - `"audit_status"` cannot be set to `"pending"`; instead it will always be set to `"no_audit"`.<br> - `allow_audit` cannot be set to `true`; instead it will always be set to `false`.<br> - The `custom_request_template` multi-object must be defined for the creative.<br> - The `custom_macros` array must be populated with macros defined by the template parameters associated with the [Custom Request Template](#custom-request-template).<br>The following fields will no longer be required:<br> - `content`<br> - `media_url`<br> - `template` |
| `custom_request_template` | multi-object | If the value of this creative's `content_source` field is set to `"mediation"`, this object describes the association between this creative and a custom request template which is used to populate the creative with content. For more information, see [Custom Request Template](#custom-request-template).<br>**Default:** `null`<br>**Required On:** `PUT`, if `content_source` is set to `"mediation"`. |
| `competitive_brands` | array of objects | Creatives associated with the brands in this array will not serve together in `/mtj` auctions. The classic example of competing brands is Coke vs. Pepsi. See [Competitive Brands](#competitive-brands) below. For more information about the brands in our system, see the [Brand Service](brand-service.md). |
| `competitive_categories` | array of objects | Creatives associated with the categories in this array will not serve together in `/mtj` auctions, e.g., "Dating" and "Education". See [Competitive Categories](#competitive-categories) below. For more information about the categories we apply to creatives (and brands), see the [Category Service](category-service.md). |
| `thirdparty_pixels` | array of objects | An array of third-party pixels associated with the creative. You can automatically attach these pixels to all creatives owned by an advertiser or member using the [Third-party Pixel service](third-party-pixel-service.md) or attach them individually at the creative level using the Creative Service.<br>**Default:** `null`<br>**Required On:** `PUT` |
| `native` | object | Deprecated. If this creative is a native ad, this object is populated with the elements required for native ads. For more information, see the description of the [Native](#native) object below.<br>**Default:** `null`<br>**Required On:** `POST` and `PUT` for native ads. Technically, native ads are identified by our system as those creatives that have a `template` with a `creative_format_id` of `12` that identifies them as `native`. |
| `native_attribute` | object | This is the new native object which contains elements required for native ads. For more information, see the description of the [Native Attribute](#native-attribute) object below.<br>**Default:** `null`<br>**Required On:** Required for native ad with template 39461. |
| `click_trackers` | array of objects | A list of third-party click tracking URLs intended to be used with native creatives. For more information, see [Click Trackers](#click-trackers) below. |
| `impression_trackers` | array of objects | A list of third-party impression tracking URLs intended to be used with native creatives. For more information, see [Impression Trackers](#impression-trackers) below. |
| `adx_audit` | object | This object contains information about the status and feedback related to the Google AdExchange audit of the creative. Information about whether or not a creative has been approved is returned in the `audit_status` field.<br>**Read Only.** |
| `flash_backup_url_secure` | string | This is the secure version of `flash_backup_url`, which is served on a secure ad call. |
| `msft_external_audit_feedback` | string | **Deprecated.** |
| `msft_external_audit_status` | enum | **Deprecated.** |
| `member_id` | int | The ID of the member that owns the creative. |
| `media_assets` | array of objects | The asset id of the original file and a field describing what the asset must be used for. It is used to associate Xandr hosted files to your creative. This array will auto-populate when uploading files via the API. For more information, see [Media Assets](#media-assets) below. |
| `ad_type` | string | **Tip:** This field only applies when you are associating creatives to [augmented line items](line-item-service---ali.md).<br>The type of creative used. Possible values:<br> - `banner`<br> - `video` (includes audio types)<br> - `native`<br>This value determines how auction items are tracked for the line item's buying strategy, paying strategy, optimization options, creative association, and targeting options.<br><br>**Note:** All creatives associated to a line item must have the same ad type, which should match the `ad_type` selected in the [Line Item Service - ALI](line-item-service---ali.md). |
| `is_political_and_eu_targeted` | Boolean | Set to true if the creative contans political content and you intend to run it in the EU. Assumed default is false if the field is not sent. <br> **NOTE**: Political advertising is not supported in the EU. |
| `is_political_and_non_eu_targeted` | Boolean | Set to true if the creative contans political content and you do not intend to run it in the EU. Assumed default is false if the field is not sent. <br> **NOTE**: Political advertising is supported in non-EU countries, only for Microsoft Monetize Adserver clients.  |

### Brand

The `brand` object contains the following fields.

> [!NOTE]
> This object is read-only. To set the brand for a creative, use the `brand_id` field outside of this object.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand of the company advertising the creative.<br>**Read Only.** |
| `name` | string | The name of the brand of the company advertising the creative.<br>**Read Only.** |
| `category_id` | int | The ID of the category associated with the brand.<br>**Read Only.** |
| `category_name` | string | The name of the category associated with the brand.<br><br>**Note:**<br>The category_name field is returned only when you pass `show_category_name=true` in the query string of your call.<br>**Read Only.** |

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

### Competitive brands

> [!NOTE]
> For more information about brands, see the [Brand Service](brand-service.md).

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the brand. |
| `name` | string | The name of the brand. |

### Competitive categories

> [!NOTE]
> For more information about categories, see the [Category Service](category-service.md).

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the category. |
| `name` | string | The name of the category. |

### Creative template

You can use the [Creative Template Service](creative-template-service.md) to view all rendering templates that can be assigned to creatives.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of creative template. |
| `name` | string | The name of the creative template.<br>**Read Only.** |
| `media_subtype_id` | int | The ID of the media subtype assigned to the template. You can use the [Media Subtype Service](media-subtype-service.md) to view all supported media subtypes.<br>**Read Only.** |
| `format_id` | string | The name of the format assigned to the template. You can use the [Creative Format Service](creative-format-service.md) to view all supported formats.<br>**Read Only.** |

## Frequently used creative templates

For more information, see [Selecting the Correct Template for Your Creative](selecting-the-correct-template-for-your-creative.md).

| Template ID | Creative Type | Requirements |
|:---|:---|:---|
| `1` | Single URL that points to a piece of html code. | You will need to pass the URL in the `media_url` field and set an id of 1 in the template object. |
| `2` | Single URL that points to a piece of Javascript code. | You will need to pass the URL in the `media_url` field and set an id of 2 in the template object. |
| `5` | Creative that starts and ends with Javascript components, even if the Javascript code writes HTML. | You will need to pass the Javascript code in the `content` field and set an id of 5 in the template object. |
| `6` | Creative that starts and ends with HTML components, even if these HTML components are `<script>` tags. | You will need to pass the html code in the `content` field and set an id of 6 in the template object. |

### Custom macros

If the creative template provides default values for a macro, passing the codes and values here is optional. If the template defines a custom macro as required, however, you must pass the code and value for the macro.

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | The exact name of the macro, as it is used in the code of the creative template, for example, `"BORDER_COLOR"`. |
| `value` | string | The value for the macro. <br>**Note:** This value must match the type of the macro, as defined in the template.<br> For example, if a macro is of the type "integer", the value must be an integer. The possible macro types are `"true/false"`, `"string"`, `"url"`, `"integer"`, `"decimal"`, and `"select_from_list"`. |

For further insight, see the *Adding a creative that uses a custom rendering template* example in the [Examples](#examples) below.

### Custom request template

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The creative custom request template associated with this creative, if its `content_source` is set to `"mediation"`. For more information, see the [Creative Custom Request Template Service](creative-custom-request-template-service.md). |
| `timeout_ms` | int | If this is a "mediation" creative, it will make at least one HTTP request to an external ad server, which may in turn make one or more additional requests. This is the time beyond which we will not wait any longer for this creative to be populated with content. For more information, see the [Creative Custom Request Template Service](creative-custom-request-template-service.md). |
| `last_activity` | timestamp | The date and time when the creative was last modified. Timezone is UTC. **Read Only.** |

### Line items

Each object in the `line_items` array includes the following fields. To obtain information for `"id"` or `"code"` fields, you can use the [Line Item Service](line-item-service.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `name` | string | The name of the line item.<br>**Read Only.** |
| `state` | enum | The state of the creative. Possible values: `"active"` or `"inactive"`.<br>**Read Only.** |
| `id` | int | The ID of the line item. Either `"id"` or `"code"` is required when updating line item association.<br>**Required On:** `PUT` |
| `code` | string | The custom code for the line item. Either `"id"` or `"code"` is required when updating line item association.<br>**Required On:** `PUT` |

### Media assets

The `media_assets` array of objects contain the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `media_asset_id` | int | The unique ID of the creative asset. |
| `creative_field` | string | This field denotes what that particular creative asset must be used for. Possible valid values are:<br> - `null` (if asset is VAST or HTML5)<br> - `media_url`<br> - `flash_backup_url`<br> - `native_icon_img_url`<br> - `native_main_media`<br> - `macro_CODE_FOR_MACRO`: This is dynamically generated based on the macros for the selected template. |

For each `media_assets` array, the following rules apply:

- Each field value can only be used once per creative. For example, you cannot have two 'flash_backup_url' assets.
- The value must be one of the valid values.
- VAST/HTML5 creatives must have one, and only one, asset.
- All other creatives can have 0 or more media assets.

#### Media assets: Example

```
"media_assets": [
    {
        "media_asset_id": 22,
        "creative_field": "media_url"
    }, 
    {
        "media_asset_id": 23,
        "creative_field": "flash_backup_url"
    }
]
```

### Mobile

| Field | Type | Description |
|:---|:---|:---|
| `alternative_landing_page_url` | string | An alternative landing page URL that can be viewed in a desktop browser for creatives that have a landing page targeted to a specific device, operating system, or carrier. You must provide an auditable URL in order for your creative to pass auditing. |

### Native attribute

The native_attribute object contains the following fields. For more information, see Adding a native creative in the [Examples](#examples) below.

| Field | Type | Description |
|:---|:---|:---|
| `link` | object | URLs associated with the native creative. For details, see [Link](#link) below. |
| `image_trackers` | array of objects | A list of third-party impression tracking URLs intended to be used with native creatives. |
| `javascript_trackers` | array of objects | A list of third-party impression tracking URLs. |
| `data_assets` | array of objects | Attributes of the native creative. For more details, see [Data Asset](#data-asset) below. |
| `image_assets` | array of objects | Attributes of each individual image. For more details, see [Image Asset](#image-asset) below. |
| `privacy_url` | string | If support was indicated in the request, URL of a page informing the user about the buyer's targeting activity. Xandr does not provide a default privacy link. |
| `video_assets` | array of objects | A list of video_asset objects. For more details, see [Video Assets](#video-asset) below. |

### Link

The `link` object contains the landing page URL, fallback URL and Trackers associated with the native creative. The `link` object is required for native attribute.

The `link` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | The landing page of the native creative.<br>**Required On:** `PUT`, `POST` |
| `fallback_url` | string | A backup url if the main deeplink url is not supported. |
| `trackers` | array of objects | A list of third-party tracking URLs intended to be used with native creatives. |

All native creatives are submitted for secureauditing by default.

- If the secure url has not been specified for any tracker (image trackers, javascript trackers, and creative image asset trackers), secure audit is disabled for that creative.
- If the secure URL has not been specified, but URL is prefixed with `https`, the creative will be submitted for secure audit.

### Link tracker

The `link_tracker` object includes the following fields:

| Field | Type | Description |
|---|---|---|
| `url` | string | A third-party tracking URL. |
| `url_secure` | string | (optional) A secure third-party tracking URL. |

### Image tracker

The `image_tracker` object includes the following fields:

| Name | Type | Description |
|:---|:---|:---|
| `url` | string | A third-party impression tracking URL. |
| `url_secure` | string | A third-party impression tracking URL (that uses SSL). |

### Javascript tracker

The `javascript_tracker` object includes the following fields:

| Name | Type | Description |
|:---|:---|:---|
| `url` | string | A third-party javascript tracking URL. |
| `url_secure` | string | A third-party javascript tracking URL (that uses SSL). |

### Data asset

Each `data_asset` represents a text component of the native creative. The `data_assets` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `data_type` | string | The asset type for the native creative. Possible values:<br> - `title`<br> - `description`<br> - `sponsored_by`<br> - `call_to_action`<br> - `display_url`<br> - `price`<br> - `sale_price`<br> - `rating`<br> - `likes`<br> - `downloads`<br> - `phone`<br> - `address`<br> - `additional_description`<br> - `custom_title_1` - `custom_title_5`<br> - `custom_body_1` - `custom_body_5`<br> - `custom_call_to_action_1` - `custom_call_to_action_5`<br> - `custom_social_url_1` - `custom_social_url_5`<br> - `custom_display_url_1` - `custom_display_url_5`<br><br>The `data_type` string should have double quotation marks around it. |
| `value` | string | The content of the `data_type` asset that you have specified. Possible values include:<br> - `title`: Title of the creative.<br> - `description`: Description of the product or service being advertised.<br> - `sponsored_by`: Brand name of the sponsor.<br> - `call_to_action`: Suggested action for next step.<br> - `display_url`: The URL you would like displayed.<br> - `price`: Price for product/app/in-app purchase.<br> - `sale_price`: Sale price that can be used together with price to indicate a discounted price.<br> - `rating`: Rating of the product being offered.<br> - `likes`: Social media likes.<br> - `downloads`: Number downloads/installs of this product.<br> - `phone`: Phone number.<br> - `address`: Address.<br> - `additional_description`: The longer version of your ad's description.<br> - `custom_title_1` - `custom_title_5`: Additional titles that will appear on the native creative.<br> - `custom_body_1` - `custom_body_5`: Additional body text that will appear on the native creative.<br> - `custom_call_to_action_1` - `custom_call_to_action_5`: Additional calls-to-action that will encourage the user to take the necessary action after viewing the native creative (e.g., signing for the mailing list).<br> - `custom_social_url_1` - `custom_social_url_5`: Social URLs that will take the user to the corresponding social media platforms.<br> - `custom_display_url_1` - `custom_display_url_5`: Additional public URLs that may be visible and/or automatically redirect the user to a web page that is connected to the landing page's domain.<br><br>The `value` string should have double quotation marks around it. |

### Image asset

Each `image_asset` represents an image component of the native creative. The `image_asset` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `image_type` | string | The format of the image. Possible values include:<br> - `main_image`: Primary image that will appear when the native creative is rendered.<br> - `icon_image`: Primary icon that will appear when the native creative is rendered.<br> - `custom_image_1` - `custom_image_5`: Additional images that will appear when the native creative is rendered.<br> - `custom_icon_1` - `custom_Icon_5`: Additional icons that will appear when the native creative is rendered.<br> - `custom_social_icon_1` - `custom_social_icon_5`: Corresponding social media icons that will appear when native creative is rendered. |
| `media_asset_id` | int | The ID of the media asset. Required for hosted native creatives.<br>If `media_asset_id` can be retrieved, the `creative_asset_image` object will be populated automatically. |
| `creative_asset_image` | object | The object containing details of the creative asset. Required for third-party native creatives. For more details, see [Creative Asset Image](#creative-asset-image) below. |
| `image_resize_setting` | object | The object containing the image resize settings. For more details, see [Image Resize Setting](#image-resize-setting) below. |

### Creative asset image

The `creative_asset_image` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | The landing page URL of the image. |
| `url_secure` | string | The secure landing page URL of the image. |
| `width` | int | The width of the image. Value must be > 0. |
| `height` | int | The height of the image. Value must be > 0. |

### Image resize setting

The `image_resize_setting` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `resize_enabled` | boolean | Indicates whether the creative should be resized. Possible values include:<br> - `True`<br> - `False` |
| `crop_enabled` | boolean | Indicates whether the creative should be cropped to fill placement. Possible values include:<br> - `True`<br> - `False` |
| `aspect_ratio_upper_bound` | double | The maximum aspect ratio allowed for the creative. |
| `aspect_ratio_lower_bound` | double | The minimum aspect ratio allowed for the creative. |
| `max_scale_factor` | double | The maximum value that the creative's width and height can be scaled. |

### Video asset

Each `video_asset` represents a video component of the native creative. The `video_asset` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `media_asset_id` | int | The id of the hosted video media asset.<br>**Required On:** `PUT`, `POST` |
| `vast_url` | string | URL to a VAST document. Must be secure.<br>**Required On:** `PUT`, `POST` |
| `trackers` | array | Optional VAST event trackers. |
| `media_files` | array | Array of available media files. See Media File for more details.<br>**Read Only.** |
| `duration` | int | Duration (in milliseconds) of the video extracted from video media asset or VAST document.<br>**Read Only.** |
| `minimum_vast_version` | string | The minimum VAST version required to play the video. Possible Values:<br> - `2.0`<br> - `3.0`<br> - `4.0`<br>**Read Only.** |

Only one of `{ media_asset_id , vast_url }` should be populated per request.

### Vast tracker

The `vast_tracker` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `vast_event_type` | string | The type of tracking event. Possible values include:<br> - `service`<br> - `start`<br> - `skip`<br> - `error`<br> - `first_quartile`<br> - `completion`<br> - `impression`<br> - `click` |
| `url` | string | URL to a VAST document. Must be secure. |

### Media file

The `media_file` object includes the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `bitrate_kbps` | int | Bitrate of the media file. |
| `mime_type` | string | MIME type of the media file. |
| `width` | int | Width of the media file. |
| `height` | int | Height of the media file. |

### Native

The `native` object used to contain the following fields, which have all been deprecated.

| Field | Type | Description |
|:---|:---|:---|
| `title` | text | **Deprecated.** |
| `description` | text | **Deprecated.** |
| `full_text` | text | **Deprecated.** |
| `context` | string | **Deprecated.** |
| `icon_img_url` | string | **Deprecated.** |
| `main_media` | array of objects | **Deprecated.** |
| `sponsored` | string | **Deprecated.** |
| `cta` | string | **Deprecated.** |
| `rating` | object | **Deprecated.** |
| `click_url` | string | **Deprecated.** |
| `click_fallback_url` | string | **Deprecated.** |
| `custom_key_values` | array of objects | **Deprecated.** |

### Main media

| Name | Type | Description |
|:---|:---|:---|
| `width` | int | **Deprecated.** |
| `height` | int | **Deprecated.** |
| `media_url` | string | **Deprecated.** |
| `media_url_secure` | string | **Deprecated.** |

> [!NOTE]
> There can only be one `main_media` object associated with a native creative.

### Custom key values

| Name | Type | Description |
|:---|:---|:---|
| `custom_key` | string | **Deprecated.** |
| `custom_value` | string | **Deprecated.** |

### Click trackers

| Name | Type | Description |
|---|---|---|
| `click_tracker_url` | string | **Deprecated.** |

### Impression trackers

| Name | Type | Description |
|---|---|---|
| `impression_tracker_url` | string | **Deprecated.** |
| `impression_tracker_url_secure` | string | **Deprecated.** |

### Pixels

You use this array to add Xandr-approved and custom pixels to a creative. You can add up to five pixels for a creative.

Xandr-approved pixels are from trusted, commonly-used providers. Most of them do not cause the creative to be resubmitted for audit. To add a Xandr-approved pixel to a creative, you need to pass only the pixel_template_id and the number of params that the pixel requires. For further guidance, see the *Adding a Xandr-approved pixel to a creative* example in [Examples](#examples) below.

> [!NOTE]
> You can use the [Pixel Template Service](pixel-template-service.md) to get information about these pixels, including whether or not they trigger re-audit.

Custom pixels are defined by you and do cause the creative to be resubmitted for audit. To add a custom pixel, you need to pass only the format and, depending on the format, the content or url. For further guidance, see the *Adding a custom pixel to a creative* example in the [Examples](#examples) below.

> [!CAUTION]
> When you make a `PUT` call to update the pixels array, the array is completely overwritten with the information in the JSON-formatted file. Therefore, if the array already includes pixels, be sure to include those pixels in the JSON-formatted file as well.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The Xandr-assigned ID of the pixel array. You will associate pixels via the `pixel_template_id`, `content`, or `URL` fields listed below.<br>**Read Only.** |
| `pixel_template_id` | int | The ID of the Xandr-approved pixel. You can use the [Pixel Template Service](pixel-template-service.md) to get this ID. |
| `param_1` | string | For Xandr-approved pixel: The value for the first parameter in the pixel content or URL. To find out how many parameters are required for a Xandr-approved pixel, use the [Pixel Template Service](pixel-template-service.md). |
| `param_2` | string | For Xandr-approved pixel: The value for the second parameter in the pixel content or URL. |
| `param_3` | string | For Xandr-approved pixel: The value for the third parameter in the pixel content or URL. |
| `param_4` | string | For Xandr-approved pixel: The value for the fourth parameter in the pixel content or URL. |
| `param_5` | string | For Xandr-approved pixel: The value for the fifth parameter in the pixel content or URL. |
| `format` | enum | The format of the pixel. Possible values: `"raw-js"`, `"url-html"`, `"url-js"`, or `"url-image"`. |
| `content` | string (255) | If the pixel format is `"raw-js"`, the HTML or JavaScript content to serve with the creative. |
| `secure_content` | string (255) | If the pixel format is `"raw-js"`, the HTML or JavaScript content to serve with the creative on a secure (HTTPS) ad call. |
| `url` | string (255) | If the pixel format is `"url-html"`, `"url-js"`, `"url-image"`, or `"raw-url"`, the URL of the HTML, JavaScript, or Image pixel to serve with the creative. |
| `secure_url` | string (255) | If the pixel format is `"url-html"`, `"url-js"`, `"url-image"`, or `"raw-url"`, the URL of the HTML, JavaScript, or Image pixel to serve with the creative on a secure (HTTPS) call. |

### Political

The `"political"` object used to contain the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `in_scope` | boolean | Determines if the US political creative is in scope to be regulated. If yes, then all required political buyer information must be provided at the insertion level. For additional information, see the Create an Insertion Order documentation via our UI (login is required). |

### Pop values

> [!NOTE]
> The `pop_values` fields are deprecated and ignored/not used by our systems.

These fields should be included in a `"pop_values"` array within the creative JSON. See below for an example.

| Field | Type (Length) | Description |
|:---|:---|:---|
| `pop_window_maximize` | Boolean | If `true`, the publisher's tag should maximize the window. Only relevant for creatives with format `"url-html"` and `"url-js"`. If `pop_window_maximize` is set to `true`, then neither `"height"` nor `"width"` should be set on the creative.<br>**Default:** `false` |
| `pop_is_tag_initiated` | Boolean | If `true`, the creative's tag will initiate the pop. If `false`, then the impression bus will initiate the pop.<br>**Default:** `false` |
| `pop_window_title` | string (255) | The title of the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `Network name` |
| `pop_statusbar` | Boolean | If `true`, a status bar is shown in the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |
| `pop_menubar` | Boolean | If `true`, a menu bar is shown in the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |
| `pop_resizable` | Boolean | If `true`, the popped window is resizable. Only applies to pops with `pop_is_tag_initiated` set to false. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |
| `pop_scrollbars` | Boolean | If `true`, scroll bars are shown in the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |
| `pop_toolbar` | Boolean | If `true`, a toolbar is shown in the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |
| `pop_addressbar` | Boolean | If `true`, an address bar is shown in the popped window. Only applies to pops with `pop_is_tag_initiated` set to `false`. Not guaranteed to be supported in all browsers.<br>**Default:** `true` |

### Segments

These fields will be included in the Segments array:

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the segment.<br>**Required On:** `POST`, `PUT` |
| `segment_id` | int | The ID of the segment. This field contains the same information as the `id` field. |
| `action` | enum | The action taken by users that will add them to the segment. Possible values: `"add on view"` or `"add on click"`.<br>**Required On:** `POST`, `PUT` |
| `name` | string | The segment's name. |

### Status

| Name | Type | Description |
|:---|:---|:---|
| `user_ready` | boolean | The status of the creative set by the user describing if the creative is ready to serve or not. Possible values: `"true"` or `"false"`. The value of **user_ready** needs to be **true** in order to reactivate an expired creative along with its audit_status.<br>**Default:** `true` |
| `hosted_assets_association_complete` | boolean/null | Status of the creative uploaded by Xandr's internal systems. Possible values: `"true"` or `"false"` for hosted creatives and "null" for third-party creatives.<br>**Read Only.** |

### Third-party pixels

The `thirdparty_pixels` array contains the fields in the table below. These fields, except for `id`, are read-only. Use this service to update the `id` of a third-party pixel or attach third-party pixels to individual creatives.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The pixel's ID.<br>**Required On:** `PUT` |
| `name` | string | The full name of the pixel.<br>**Read Only.** |
| `active` | Boolean | The current status of the pixel (true = active).<br>**Read Only.** |
| `audit_status` | string | Audit status of the pixel.<br>**Read Only.** |

> [!NOTE]
> To update or create a third-party pixel and/or attach third-party pixels to all creatives owned by the advertiser or network member, use the [Third-party Pixel service](third-party-pixel-service.md).

### First run/last run

To include the `first_run` and `last_run` fields in a `GET` response, pass `flight_info=true` in the query string. You can also filter for creatives based on when they first and last served, as follows:

### Retrieve only creatives that have never served

Pass `never_run=true` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&never_run=true'
```

> [!NOTE]
> You can use `never_run=true` in combination with other filters, but note that it will always be an OR relationship. For example, if you pass both `never_run=true`and `min_first_run=2012-01-01 00:00:00` in the query string, you will be looking for creatives that have never served OR line items that first served on or after 2012-01-01.

### Retrieve only creatives that first served on or after a specific date

Pass `min_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00'
```

### Retrieve only creatives that first served on or before a specific date

Pass `max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&max_first_run=2012-08-01 00:00:00'
```

### Retrieve only creatives first served within a specific date range

Pass `min_first_run=YYYY-MM-DD HH:MM:SS&max_first_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&min_first_run=2012-01-01 00:00:00&max_first_run=2012-08-01 00:00:00'
```

### Retrieve only creatives that last served on or after a specific date

Pass `min_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00'
```

### Retrieve only creatives that last served on or before a specific date

Pass `max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&max_last_run=2012-08-01 00:00:00'
```

### Retrieve only creatives that last served within a specific date range

Pass `min_last_run=YYYY-MM-DD HH:MM:SS&max_last_run=YYYY-MM-DD HH:MM:SS` in the query string.

```
curl -b cookies -c cookies 'https://api.appnexus.com/creative?advertiser_id=100&flight_info=true&min_last_run=2012-01-01 00:00:00&max_last_run=2012-08-01 00:00:00'
```

### Stats

> [!NOTE]
> The `stats`object has been deprecated (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead.

## Changes that cause re-audit

Once a creative has passed Xandr audit (`audit_status` is `"audited"`), changing any of the following fields causes the creative to be resubmitted for audit (`audit_status` is set to `"pending"`):

- `width`
- `height`
- `content`
- `media_url`
- `click_url`
- `template`
- `custom_macros`
- `media_subtypes`
- `language`
- `categories`
- `technical_attributes`
- `brand_id`
- `pixel_url`
- `pixels` (if adding or removing a custom pixel or a Xandr-approved pixel)
- `text_title` (if text creative)
- `text_description` (if text creative)
- `text_display_url` (if text creative)
- `pop_window_maximize` (if pop creative)
- `pop_is_tag_initiated` (if pop creative and changing from false to true)
- `video_attribute`
- `media_assets`
- `brand_url` (not applicable to API users)
- `alternative_landing_page_url`
- `native_attribute`

Also, if the `audit_status` is `"no_audit"`, changing `allow_audit` from `"false"` to `"true"` causes the creative to be resubmitted for Xandr audit.

## Creative macros

Xandr has predefined some macros that can be used within the creative's `media_url`, `content`, `click_url`, and `pixel_url` fields.

### Click tracking example

```
"media_url": "https://ad.doubleclick.net/adi/N5364.Ivillage.com/B2965815.5;sz=728x90;click0=$
{CLICK_URL};ord=${CACHEBUSTER}?"
        
```

## Examples

> [!CAUTION]
> Exclude `audit_status` and `no_audit` in **`PUT`** calls to avoid errors.

### Add a banner image creative (hosted)

When uploading a standard banner image creative for hosting with Xandr:

Once the creative has been registered, the content will be stored on the CDN, and the creative will be given a `media_url` such as `https://cdn.adnxs.com/p/29/23/21/a0/292321a0bea05427598914c8bb626032.jpg`.

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat creative

{
   "creative": {
      "template": {"id":4},
      "width": 300,
      "height": 250,
      "click_url": "https://www.gothere.com",
      "click_target": "https://www.gothere.com",
      "file_name": "gothere.png",
      "content": "/9j/4AAQSkZJRgABAgAAZABkAAD/7AARRHVja3kAAQAEAAAAPAAA/+4ADkFkb2JlAGTAAAAAAf/b
                 AIQABgQEBAUEBgUFBgkGBQYJCwgGBggLDAoKCwoKDBAMDAwMDAwQDA4PEA8ODBMTFBQTExwbGxsc
                 Hx8fHx8fHx8fHwEHBwcNDA0YEBAYGhURFRofHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8f
                 ...
                 nwj3HrP+oer6/wDPa/tKsOz/AEf8CnxP82z3fTu9VDboP//Z",
       "is_political_and_eu_targeted": false,
       "is_political_and_non_eu_targeted": false
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=2'

{
   "response": {
      "status": "OK",
      "id": 10,
      ...
      "template": {
          "id": 4,
          "name": "Standard",
          "media_subtype_id": 1,
          "format_id": 4
      },
      "width": 300,
      "height": 250,
      ...
      "click_url": "https://www.gothere.com",
      "click_target": "https://www.gothere.com",
      "media_url": "https://cdn.adnxs.com/p/29/23/21/a0/gothere.png"
      ...
      "audit_status": "pending",
      ...
     "categories":  [
           {
                 "id": 37,
                 "name": "Politics",
                 "self_declared": true
          }],
   }
}
```

### Add a mobile banner image creative (hosted)

In order for mobile creatives to pass Xandr platform audit, you need to pass the `mobile` object with an alternative URL that will display correctly in a desktop browser when the creative is clicked.

```
$ cat creative
 
{
    "creative": {
        "content": "\/9j\/4AAQSkZJRgABAQEASABIAAD\/7QCEUGhvdG9zaG9wIDMuMAA4QklNBAQAAAAAAGccAVoAAxsl...",
        "mobile": {
            "alternative_landing_page_url": "https:\/\/example.com"
        },
        "file_name": "SWEET.png",
        "click_url": "https:\/\/example.com",
        "click_target": "https:\/\/example.com",
        "height": 250,
        "width": 300,
        "template": {
            "id": 4
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=3141'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 700864,
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https:\/\/cdn.sand-08.adnxs.net\/s\/d3\/d6\/1c\/61\/d3d61c611fd6f98becc8ad6d45c43875.png",
            "id": 700864,
            "code": null,
            "code2": null,
            "member_id": 1309,
            "state": "inactive",
            "click_track_result": "not_tested",
            "advertiser_id": 41798,
            "publisher_id": null,
            "format": null,
            "width": 300,
            "height": 250,
            "click_url": "https:\/\/example.com",
            "click_target": "https:\/\/example.com",
            "flash_click_variable": null,
            "no_iframes": false,
            "content": null,
            "original_content": null,
            "file_name": "OH_YEAH.png",
            "track_clicks": true,
            "audit_status": "pending",
            "macros": null,
            "profile_id": null,
            "audit_feedback": null,
            "is_prohibited": false,
            "is_suspicious": false,
            "created_on": "2013-10-18 15:57:03",
            "flash_backup_url": null,
            "last_modified": "2013-10-18 15:57:03",
            "is_control": false,
            "allow_audit": true,
            "is_expired": false,
            "creative_upload_status": "pending",
            "backup_upload_status": null,
            "use_dynamic_click_url": false,
            "media_subtypes": [
                "banner"
            ],
            "size_in_bytes": 15171,
            "msft_audit_status": "pending",
            "msft_audit_feedback": null,
            "msft_external_audit_status": "pending",
            "msft_external_audit_feedback": null,
            "is_self_audited": false,
            "no_adservers": false,
            "text_title": null,
            "text_description": null,
            "text_display_url": null,
            "click_action": "click-to-web",
            "ssl_status": "disabled",
            "allow_ssl_audit": false,
            "media_url_secure":"https:\/\/a248.e.akamai.net\/appnexus.download.akamai.com\/89298\/sandbox\/s\/d3\/d6\/1c\/61\/d3d61c611fd6f98becc8ad6d45c43875.png",
            "content_secure": null,
            "original_content_secure": null,
            "flash_backup_url_secure": null,
            "is_hosted": true,
            "content_source": "standard",
            "lifetime_budget_imps": null,
            "daily_budget_imps": null,
            "enable_pacing": null,
            "allow_safety_pacing": null,
            "lifetime_budget": null,
            "daily_budget": null,
            "landing_page_url": null,
            "thirdparty_creative_id": null,
            "thirdparty_campaign_id": null,
            "custom_request_template": null,
            "language": {
                "id": 1,
                "name": "English"
            },
            "pop_values": null,
            "brand": {
                "id": 1,
                "name": "Unknown",
                "category_id": 8
            },
            "template": {
                "id": 4,
                "name": "Standard",
                "media_subtype_id": 1,
                "format_id": 4
            },
            "thirdparty_page": null,
            "custom_macros": null,
            "segments": null,
            "folder": null,
            "campaigns": null,
            "competitive_brands": null,
            "competitive_categories": null,
            "pixels": null,
            "mobile": {
                "alternative_landing_page_url":"https:\/\/example.com"
            },
            "sla": null,
            "sla_eta": null,
            "currency": "USD"
        },
        "dbg_info": {
            ...
        }
    }
}
```

### Add a banner flash creative (hosted)

When uploading a standard banner flash creative for hosting with Xandr:

Once the creative has been registered, the content will be stored on the CDN, and the creative will be given a `media_url` such as `https://cdn.adnxs.com/p/29/23/21/a0/292321a0bea05427598914c8bb626032.jpg`.

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat creative

{
   "creative": {
      "template": {"id":3},
      "width": 300,
      "height": 250,
      "click_url": "https://www.gothere.com",
      "click_target": "htpps://www.gothere.com",
      "file_name": "gothere.swf",
      "flash_click_variable": "ClickTag",
      "content": "/9j/4AAQSkZJRgABAgAAZABkAAD/7AARRHVja3kAAQAEAAAAPAAA/+4ADkFkb2JlAGTAAAAAAf/b
                 AIQABgQEBAUEBgUFBgkGBQYJCwgGBggLDAoKCwoKDBAMDAwMDAwQDA4PEA8ODBMTFBQTExwbGxsc
                 Hx8fHx8fHx8fHwEHBwcNDA0YEBAYGhURFRofHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8f
                 ...
                 nwj3HrP+oer6/wDPa/tKsOz/AEf8CnxP82z3fTu9VDboP//Z",
      "flash_backup_content": "AcndgAAZABkAAD/7AARRHVja3kAAQAEAAAAPAAA/+4ADkFkb2JlAGTAAAAAAf/b
                 AIQABgQEBAUEBgUFBgkGBQYJCwgGcdkDCADBdcdDDBAMDAwMDAwQDA4PEA8ODBMTFBQTExwbGxsc
                 Hx8fHx8fHx8fHwEHBwcNDA0YEBAYGhURFRofHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx6smd34
                 ...
                 nwj3HrP+oer6/wDPa/tKsOz/AEf8Cnnd30cddaxcio244adc",
      "flash_backup_file_name": "flash_backup.png"
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=2'

{
   "response": {
      "status": "OK",
      "id": 11,
      ...
      "template": {
          "id": 3,
          "name": "Standard",
          "media_subtype_id": 1,
          "format_id": 3
      },
      "width": 300,
      "height": 250,
      ...
      "click_url": "https://www.gothere.com",
      "click_target": "https://www.gothere.com",
      "media_url": "https://cdn.adnxs.com/p/29/23/21/a0/gothere.swf"
      "flash_backup_url": "https://cdn.adnxs.com/c/54/f2/d1/v3/flash_backup.png"
      ...
      "audit_status": "pending",
      ...
   }
}
```

### Add a banner flash creative (third-party URL)

When adding a third-party URL for a banner flash creative:

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat creative

{
   "creative": {
      "media_url": "https://creative.com/300x250",
      "flash_backup_url": "https://creative.com/backupimage/300x250",
      "template": {"id":2},
      "width": 300,
      "height": 250,
      "campaigns": [
         {"id":58990},
         {"id":58991}
      ]
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=35'

{
   "response": {
      "status": "OK",
      "id":12,
      ...
      "media_url": "https://creative.com/300x250",
      "flash_backup_url": "https://creative.com/backupimage/300x250",
      ...
      "template": {
          "id": 2,
          "name": "Standard",
          "media_subtype_id": 1,
          "format_id": 2
      },
      ...
      "audit_status": "pending",
      ...
   }
}
```

### Add a MediaMind expandable creative (third-party URL)

In this example, note that the `media_url` field provides the third-party URL for the expandable creative, and the template array specifies template 108, which is the Xandr standard template for creatives of the `"MediaMind Expandable"` media subtype and the `"url-js"` format.

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat creative

{
   "creative": {
      "media_url": "https://bs.serving-sys.com/BurstingPipe/adServer.bs?ncu=$$${CLICK_URL_ENC}$$&cn=rsb&c=28&
          pli=2980019&PluID=0&w=300&h=250&ord=${CACHEBUSTER}&ucm=true",
      "template": {"id":108},
      "width": 300,
      "height": 250,
      "campaigns":[
          {"id": 58990},
          {"id": 58991}
      ]
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=35'

{
   "response":{
      "status":"OK",
      "id":12,
      ...
      "media_url":"https://bs.serving-sys.com/BurstingPipe/adServer.bs?ncu=$$${CLICK_URL_ENC}$$&cn=rsb&c=28&
          pli=2980019&PluID=0&w=300&h=250&ord=${CACHEBUSTER}&ucm=true",
      ...
      "template": {
          "id": 108,
          "name": "Standard",
          "media_subtype_id": 11,
          "format_id": 2
      },
      ...
      "audit_status": "pending",
      ...
   }
}
```

### Add a Pointroll expandable creative (third-party HTML tag)

In this example, note that the content field provides the JavaScript tag for the expandable creative, and the template array specifies template 159, which is the Xandr standard template for creatives of the `"Pointroll Expandable"` media subtype and the `"raw-html"` format.

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat creative

{
   "creative": {
      "content":<script type=\"text/javascript\">function pr_swfver(){var osf,osfd,i,axo=1,v=0,nv=navigator;
       if(nv.plugins&&nv.mimeTypes.length){osf=nv.plugins[\"ShockwaveFlash\"];if(osf&&osf.description)
       {osfd=osf.description;v=parseInt(osfd.substring(osfd.indexOf(\".\")-2))}}else{try{for(i=5;axo!=null;i++)
       {axo=new ActiveXObject(\"ShockwaveFlash.ShockwaveFlash.\"+i);v=i}}catch(e){}}return v;}var pr_d=new Date
       ();pr_d=pr_d.getDay()+\"|\"+pr_d.getHours()+\": \"+pr_d.getMinutes()+\"|\"+-pr_d.getTimezoneOffset()/60;
       var pr_postal=\"\";var pr_data=\"\";var pr_redir=\"$CTURL$\";var pr_nua=navigator.userAgent.toLowerCase();
       </script>,
      "template": {"id":159},
      "width": 300,
      "height": 250,
      "campaigns": [
         {"id": 58990},
         {"id": 58991}
      ]
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=35'

{
   "response": {
      "status": "OK",
      "id": 12
      ...
      "content":"var click = '${CLICK_URL}'; var t = (new Date()).getTime(); var s = document.createElement('script');
                s.setAttribute('src', 'https://pointroll.adserver.org/showad?size=300x250;click=' + click + ';ord=' + t);
                document.getElementsByTagName('body').appendChild(s);https://creative.com/300x250",
      ...
      "template": {
         "id": 159,
         "name": "Standard",
         "media_subtype_id": 12,
         "format_id": 6
      },
      ...
      "audit_status":"pending",
      ...
   }
}
```

### Add a popup image creative (third-party URL)

In this example, note that the `media_url` field provides the third-party URL for the popup image creative, and the template array specifies template 10, which is the standard Xandr rendering template for the `"Popup"` media subtype and the `"url-js"` format. If you don't specify a template in the request, you must pass format as `"image"` and `media_subtype` as `"popup"`.

```
{
   "creative":
   {
     "media_url": "https://dummyimage.com/728x90",
     "click_url": "https://www.google.com",
     "click_target": "https://www.google.com",
     "template": {"id":10},
     "pop_values": {
       "pop_is_tag_initiated": false,
       "pop_window_maximize": false,
       "pop_window_title": null,
       "pop_statusbar": false,
       "pop_resizable": false,
       "pop_scrollbars": false,
       "pop_toolbar": false,
       "pop_addressbar": false
       },
      "width": 728,
      "height": 90
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=2'

{
   "response": {
      "status": "OK",
      "id": 14,
      ...
      "template": {
          "id": 10,
          "name": "Standard",
          "media_subtype_id": 2,
          "format_id": 2
      },
      "width": 728,
      "height": 90,
      ...
      "audit_status": "pending",
      ...
   }
}
```

### Add a popunder image creative (third-party URL)

In this example, note that the `media_url` field provides the third-party URL for the popunder image creative, and the template array specifies template 17, which is the standard Xandr rendering template for the `"Popunder"` media subtype and the `"url-js"` format. If you don't include a template in the request, you must pass format as `"image"` and `media_subtype` as `"popunder"`.

```
{
   "creative" :
   {
     "media_url": "https://dummyimage.com/728x90",
     "click_url": "https://www.google.com",
     "click_target": "https://www.google.com",
     "template": {"id":17},
     "pop_values": {
       "pop_is_tag_initiated": false,
       "pop_window_maximize": false,
       "pop_window_title": null,
       "pop_statusbar": false,
       "pop_resizable": false,
       "pop_scrollbars": false,
       "pop_toolbar": false,
       "pop_addressbar": false
       },
      "width": 728,
      "height": 90
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=2'

{
   "response": {
      "status": "OK",
      "id":14,
      ...
      "template": {
          "id": 17,
          "name": "Standard",
          "media_subtype_id": 2,
          "format_id": 2
      },
      "width": 728,
      "height": 90,
      ...
      "audit_status": "pending",
      ...
   }
}
```

### Add an in-banner video (third-party video file)

When adding a third-party in-banner video file:

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

``` pre
$ cat inbanner

{
   "creative": {
      "media_url": "https://example.com/inbanner.flv",
      "template": {"id":219},
      "click_url": "https://www.example.com",
      "click_target": "https://www.example.com",
      "width": 300,
      "height": 250,
      "flash_backup_url": "https://www.example.com/poster_image.png"
      "custom_macros": [
          {
              "code": "FLV_URL",
              "value": "https:www.example.com/inbanner.flv"
          },
          {
              "code": "MP4_URL",
              "value": "https:www.example.com/inbanner.mp4"
          },
          {
              "code": "WEBM_URL",
              "value": "https:www.example.com/inbanner.webm"
          }
      ],
   }
}


$ curl -b cookies -c cookies -X POST -d @inbanner 'https://api.appnexus.com/creative?advertiser_id=2'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 510242,
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https://example.com/inbanner.flv",
            "id": 510244,
            "code": null,
            "code2": null,
            "state": "inactive",
            "click_track_result": "not_tested",
            "advertiser_id": 2,
            "publisher_id": null,
            "format": null,
            "width": 300,
            "height": 250,
            "click_url": "https://www.example.com",
            "flash_click_variable": null,
            "pixel_url": null,
            "pixel_type": "image",
            "no_iframes": false,
            "content": null,
            "original_content": null,
            "file_name": "inbanner.flv",
            "track_clicks": true,
            "audit_status": "pending",
            "macros": null,
            "profile_id": null,
            "audit_feedback": null,
            "is_prohibited": false,
            "created_on": "2012-04-13 14:47:46",
            "flash_backup_url": "https://example.com/poster_image.png",
            "last_modified": "2012-04-13 14:47:46",
            "is_control": false,
            "allow_audit": true,
            "is_expired": false,
            "creative_upload_status": "pending",
            "backup_upload_status": null,
            "use_dynamic_click_url": false,
            "media_subtypes": [
                "banner"
            ],
            "size_in_bytes": 0,
            "msft_audit_status": "pending",
            "msft_audit_feedback": null,
            "msft_external_audit_status": "pending",
            "msft_external_audit_feedback": null,
            "is_self_audited": false,
            "no_adservers": false,
            "text_title": null,
            "text_description": null,
            "text_display_url": null,
            "click_action": "click-to-web",
            "click_target": "https://www.example.com",
            "ssl_status": "disabled",
            "allow_ssl_audit": false,
            "media_url_secure": "https://example.com/inbanner.flv",
            "content_secure": null,
            "original_content_secure": null,
            "pixel_url_secure": null,
            "flash_backup_url_secure": null,
            "is_hosted": true,
            "lifetime_budget_imps": null,
            "daily_budget_imps": null,
            "enable_pacing": null,
            "lifetime_budget": null,
            "daily_budget": null,
            "language": {
                "id": 1,
                "name": "English"
            },
            "pop_values": null,
            "brand": {
                "id": 1,
                "name": "Unknown",
                "category_id": 8
            },
            "template": {
                "id": 219,
                "name": "Standard",
                "media_subtype_id": 3,
                "format_id": 11
            },
            "custom_macros": [
                {
                    "code": "AUTOPLAY",
                    "value": "0"
                },
                {
                    "code": "CONTROLS",
                    "value": "1"
                },
               {
                    "code": "FLV_URL",
                    "value": "https:www.example.com/inbanner.flv"
                },
                {
                    "code": "MP4_URL",
                    "value": "https:www.example.com/inbanner.mp4"
                },
                {
                    "code": "WEBM_URL",
                    "value": "https:www.example.com/inbanner.webm"
                }
            ],
            "segments": null,
            "folder": null,
            "campaigns": null,
            "competitive_brands": null,
            "competitive_categories": null,
            "pixels": null,
            "sla": null,
            "sla_eta": null,
            "currency": "USD"
        },
        "dbg_info": {
            ... 
        }
    }
}
```

### Add an in-banner video (third-party XML file)

When adding a third-party in-banner XML file:

Auditing: By default, the creative will be submitted for auditing by Xandr. If you don't want the creative to be audited, you must include `allow_audit` and set it to `false`. Alternately, if you want to audit the creative yourself, you must include `is_self_audited` and set it to `true`.

```
$ cat inbanner

{
   "creative": {
      "media_url": "https://example.com/inbanner.xml",
      "template": {"id":8},
      "click_url": "https://www.example.com",
      "click_target": "https://www.example.com",
      "width": 300,
      "height": 250,
      "flash_backup_url": "https://example.com/poster_image.png"
   }
}


$ curl -b cookies -c cookies -X POST -d @inbanner 'https://api.appnexus.com/creative?advertiser_id=2'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 510242,
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https://example.com/inbanner.xml",
            "id": 510245,
            "code": null,
            "code2": null,
            "state": "inactive",
            "click_track_result": "not_tested",
            "advertiser_id": 2,
            "publisher_id": null,
            "format": null,
            "width": 300,
            "height": 250,
            "click_url": "https://www.example.com",
            "flash_click_variable": null,
            "pixel_url": null,
            "pixel_type": "image",
            "no_iframes": false,
            "content": null,
            "original_content": null,
            "file_name": "inbanner.xml",
            "track_clicks": true,
            "audit_status": "pending",
            "macros": null,
            "profile_id": null,
            "audit_feedback": null,
            "is_prohibited": false,
            "created_on": "2012-04-13 14:47:46",
            "flash_backup_url": "https://example.com/poster_image.png",
            "last_modified": "2012-04-13 14:47:46",
            "is_control": false,
            "allow_audit": true,
            "is_expired": false,
            "creative_upload_status": "pending",
            "backup_upload_status": null,
            "use_dynamic_click_url": false,
            "media_subtypes": [
                "banner"
            ],
            "size_in_bytes": 0,
            "msft_audit_status": "pending",
            "msft_audit_feedback": null,
            "msft_external_audit_status": "pending",
            "msft_external_audit_feedback": null,
            "is_self_audited": false,
            "no_adservers": false,
            "text_title": null,
            "text_description": null,
            "text_display_url": null,
            "click_action": "click-to-web",
            "click_target": "https://www.example.com",
            "ssl_status": "disabled",
            "allow_ssl_audit": false,
            "media_url_secure": "https://example.com/inbanner.xml",
            "content_secure": null,
            "original_content_secure": null,
            "pixel_url_secure": null,
            "flash_backup_url_secure": null,
            "is_hosted": true,
            "lifetime_budget_imps": null,
            "daily_budget_imps": null,
            "enable_pacing": null,
            "lifetime_budget": null,
            "daily_budget": null,
            "language": {
                "id": 1,
                "name": "English"
            },
            "pop_values": null,
            "brand": {
                "id": 1,
                "name": "Unknown",
                "category_id": 8
            },
            "template": {
                "id": 8,
                "name": "Standard",
                "media_subtype_id": 3,
                "format_id": 10
            },
            "custom_macros": null,
            "segments": null,
            "folder": null,
            "campaigns": null,
            "competitive_brands": null,
            "competitive_categories": null,
            "pixels": null,
            "sla": null,
            "sla_eta": null,
            "currency": "USD"
        },
        "dbg_info": {
           ...
        }
    }
}
```

### Add a creative that uses a custom rendering template

In this example, the `POST` request adds a hosted flash banner creative to Xandr. The creative uses a custom creative template, which is designed to render the creative with a border when it is served. Custom macros in the template allow the trafficker to specify the HTML color code and size (in pixels) or the border.

```
$ cat creative

{
   "creative": {
      "template": {"id":252},
      "width": 300,
      "height": 250,
      "custom_macros": [
         {
            "code": "BORDER_COLOR",
            "value": "#000000"
         },
         {
            "code": "BORDER_SIZE",
            "value": 1
         }
      ],
      "click_url": "https://www.gothere.com",
      "click_target": "https://www.gothere.com",
      "file_name": "gothere.swf",
      "flash_click_variable": "ClickTag",
      "content": "/9j/4AAQSkZJRgABAgAAZABkAAD/7AARRHVja3kAAQAEAAAAPAAA/+4ADkFkb2JlAGTAAAAAAf/b
                 AIQABgQEBAUEBgUFBgkGBQYJCwgGBggLDAoKCwoKDBAMDAwMDAwQDA4PEA8ODBMTFBQTExwbGxsc
                 Hx8fHx8fHx8fHwEHBwcNDA0YEBAYGhURFRofHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8f
                 ...
                 nwj3HrP+oer6/wDPa/tKsOz/AEf8CnxP82z3fTu9VDboP//Z",
      "flash_backup_content": "AcndgAAZABkAAD/7AARRHVja3kAAQAEAAAAPAAA/+4ADkFkb2JlAGTAAAAAAf/b
                 AIQABgQEBAUEBgUFBgkGBQYJCwgGcdkDCADBdcdDDBAMDAwMDAwQDA4PEA8ODBMTFBQTExwbGxsc
                 Hx8fHx8fHx8fHwEHBwcNDA0YEBAYGhURFRofHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx8fHx6smd34
                 ...
                 nwj3HrP+oer6/wDPa/tKsOz/AEf8Cnnd30cddaxcio244adc",
      "flash_backup_file_name": "flash_backup.png"
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=2'

{
   "response": {
      "status": "OK",
      "id": 11,
      ...
      "template": {
          "id": 252,
          "name": "Flash Banner with Border",
          "media_subtype_id": 1,
          "format_id": 3
      },
      "width": 300,
      "height": 250,
      ...
      "click_url": "https://www.gothere.com",
      "click_target": "https://www.gothere.com",
      "media_url": "https://cdn.adnxs.com/p/29/23/21/a0/gothere.swf"
      "flash_backup_url": "https://cdn.adnxs.com/c/54/f2/d1/v3/flash_backup.png"
      ...
      "audit_status": "pending",
      ...
      "custom_macros": [
         {
            "code": "BORDER_COLOR",
            "value": "#000000"
         },
         {
            "code": "BORDER_SIZE",
            "value": 1
         }
      ],
      ...
   }
}
```

### Add a secure creative

When uploading a non-secure creative, you can also upload a version to serve on SSL inventory as follows:

> [!NOTE]
> You can check the ssl audit status of a creative by making a simple `GET` request. The `ssl_status` field in the response tells you the audit status. The creative will be eligible to serve on secure inventory only once it passes the audit and the `ssl_status` is `"approved"`. A third-party creative will pass our audit only if all calls in the ad chain go through secure servers. If the creative fails the ssl audit, you can resubmit it for ssl auditing by changing the `ssl_status` field to `"pending"`.

```
$ cat creative

{
   "creative": {
      "media_url": "https://creative.com/123",
      "media_url_secure": "https://creative.com/123",
      "template": {"id":2},
      "allow_ssl_audit": true
      "format": "image",
      "width": 300,
      "height": 250,
      "campaigns": [
         {"id":58990},
         {"id":58991}
      ]
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=35'

{
   "response": {
      "status":"OK",
      "id":13
      ...
      "audit_status":"pending",
      ...
      "ssl_status":"pending",
      ...
   }
}
```

### Submit a creative for priority audit

If you have a supplemental services agreement with Xandr for priority audits, you can submit a creative for priority audit (auditing within 2 hours during business hours) by setting the `sla` field to 2. The `sla_eta` field in the response will provide an estimated finish time for the audit.

```
$ cat creative

{
   "creative": {
      "media_url": "https://creative.com/456",
      "template": {"id":2},
      "width": 300,
      "height": 250,
      "campaigns": [
         {"id":58990},
         {"id":58991}
      ],
      "sla": 2
   }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=35'

{
   "response": {
      "status": "OK",
      "id": 469340,
      ...
      "audit_status": "pending",
      ...
      "sla": "2",
      "sla_eta": "2012-01-13 22:43:33",
      ...
   }
}
```

### Cancel a creative audit

If you have submitted a creative for Xandr audit, and the `audit_status` is `"pending"`, you can cancel the audit and not be charged the auditing fee by making a `PUT` request with `allow_audit` set to `false`. The `audit_status` field will be `"no_audit"` in the response.

```
$ cat creative

{
   "creative": {
      "allow_audit":false
   }
}

$ curl -b cookies -c cookies -X PUT -d @creative 'https://api.appnexus.com/creative?id=469340&advertiser_id=35'

{
   "response": {
      "status": "OK",
      "id": 469340,
      ...
      "audit_status":"no_audit",
      ...
   }
}
```

### View audit stats for all creatives

In this example, `"audit_stats=true"` is passed in the query string of the `GET` call. This returns the number of creatives with each Xandr, Microsoft, and Google audit status.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative?audit_stats=true'

{
    "response": {
        "status": "OK",
        "count": 30,
        "start_element": 0,
        "num_elements": 100,
        "creatives": [
            {
                "total": 30,
                "appnexus_audit": {
                    "no_audit": 10,
                    "pending": 18,
                    "approved": 0,
                    "rejected": 1
                },
                "microsoft_audit": {
                    "no_audit": 10,
                    "pending": 18,
                    "approved": 1,
                    "rejected": 1
                }
            }
        ],
        "dbg_info": {
            ...
        }
    }
}
```

### Add a Xandr-approved pixel to a creative

This example walks you through the process of adding the Xandr-approved Evidon AdChoices Icon pixel to a creative.

1. First, you need to find out the `pixel_template_id` and the number of parameters you must define for the pixel. You use the [Pixel Template Service](pixel-template-service.md) to get this information.

    ```
    $ curl -b cookies -c cookies 'https://api.appnexus.com/pixel-template'
    
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

1. The Evidon AdChoices Icon pixel is the first in the response. You note that id is 1. You also note that `num_required_params` is `2`. This means that, when adding the pixel to your creative, you must provide values for `{P1}` and `{P2}` in the pixel content.
1. You create the JSON-formatted file for adding the pixel to the creative. In the file, you set `pixel_template_id` to `2`, and you set
`param_1` and `param_2` to the values for `{P1}` and `{P2}` in the pixel content.

    > [!CAUTION]
    > The pixels array will be completely overwritten with your JSON. Therefore, if the pixels array on the creative already includes any pixels, be sure to specify them in your JSON array as well. For more details, see [Creative Service](creative-service.md).

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

1. Finally, you make a `PUT` call to update the creative. The pixels array in the response then shows that the pixel has been added. The two parameters are defined and have been populated in the pixel content.

    > [!NOTE]
    > The Evidon AdChoices Icon pixel does not cause the creative to require re-auditing, `audit_status` has not be reverted to `"pending"`.

    ```
    $ curl -b cookies -c cookies -X PUT -d @creative_update 'https://api.appnexus.com/creative?id=503577&advertiser_id=35081'
    
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
                "advertiser_id": 35081,
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

### Add a custom pixel to a creative

In this example, the `PUT` request adds a custom url-js pixel to creative 503577. In the JSON-formatted file, the format is set to `"url-js"`, and the url is set to the location of the JavaScript that you want to serve with the creative.

> [!NOTE]
> In the response that `audit_status` is `"pending"`; this is because adding a custom pixel to a creative causes the creative to be resubmitted for audit.
> [!CAUTION]
> The pixels array will be completely overwritten with the information in this file. Therefore, if the creative already includes any pixels, be sure to specify them in the file as well.

```
$ cat creative_update

{
    "creative": {
        "pixels": [
            {
                "format": "url-js",
                "url": "https://50.16.221.228/render_js?cb=${CACHEBUSTER}&uid=${USER_ID}&ref=${REFERER_URL}
                 &campaign_id=147"
            }
        ]
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @creative_update 'https://api.appnexus.com/creative?id=503577&advertiser_id=35081'

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
            "advertiser_id": 35081,
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

### Add a third-party pixel to a creative

In this example, the `PUT` request adds 2 third-party pixels to creative "503577".

> [!NOTE]
> In the response that `audit_status` is `"pending"`; this is because adding a third party pixel to a creative causes the creative to be resubmitted for audit.

```
$ cat creative_update

{
    "creative": {
        "thirdparty_pixels": [
          {
            "id": 145
          },
          {
            "id": 314
          }
        ]
    }
}
```

```
$ curl -b cookies -c cookies -X PUT -d @creative_update 'https://api.appnexus.com/creative?id=503577&advertiser_id=35081'

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
            "advertiser_id": 35081,
            ...
            "audit_status": "pending",  ??remove this, confirm with UTSAV
            ...
            "thirdparty_pixels": [

                {
                  "id": 145,
                  "name": "sample pixel",
                  "audit_status": "pending",
                  "active": true
                },
                {
                  "id": 314,
                  "name": "another sample pixel",
                  "audit_status": "pending",
                  "active": true
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

### Add a creative (third-party HTML tag)

When the format field is set to `"raw-html"`, content from the `content` field must be wrapped in `document.write()` and also `escaped`.

```
$ cat creative 
{
    "creative": {
        "adservers": [
            {
                "id": 79,
                "use_type": "adserver"
            }
        ],
        "name": "Test Creative",
        "original_content": "<script language=\"javascript\"src=\"https://track.adform.net/adfscript/?bn=2342059;click=${CLICK_URL}\"></script><noscript><a href=\"{CLICK_URL}https://track.adform.net/C/?bn=2342059;C=0\"  target=\"_blank\"><img  src=\"https://track.adform.net/adfserve/?bn=2342059;srctype=4;ord=${CACHEBUSTER}\"  border=\"0\"  width=\"300\"  height=\"250\"  alt=\"\"/></a></noscript>",
        "track_clicks": "true",
        "width": 300,
        "height": 250,
        "is_self_audited": "false",
        "content": "document.write('<scr' + 'ipt language=\\\"javascript\\\"src=\\\"https://track.adform.net/adfscript/?bn=2342059;click=${CLICK_URL}\\\"></scr' + 'ipt><noscript><a href=\\\"{CLICK_URL}https://track.adform.net/C/?bn=2342059;C=0\\\"  target=\\\"_blank\\\"><img  src=\\\"https://track.adform.net/adfserve/?bn=2342059;srctype=4;ord=${CACHEBUSTER}\\\"  border=\\\"0\\\"  width=\\\"300\\\"  height=\\\"250\\\"  alt=\\\"\\\"/></a></noscript>');",
        "template": {
            "id": "6"
        }
    }
}

$ curl -b cookies -c cookies -X POST -d @creative 'https://api.appnexus.com/creative?advertiser_id=1'

{
   "response": {
      "status": "OK",
      "id": 20,
      ...
      "template": {
          "id": 6,
          "name": "Standard"
      },
      "width": 300,
      "height": 250,
      "audit_status": "pending",
   }
}
```

### Add a native creative

This is the new native attribute. When adding a native creative with the new attribute, use template ID 39461.

Step 1: Upload the asset to the [creative upload service](creative-upload-service---file-format.md).

```
curl -X POST -H 'Authorization:hbapi:21816:58f909dfa3405:nym2' --form "type=image" --form "file=@./NATIVE.JPG" 'https://api.appnexus.com/creative-upload?member_id=123'
```

The `media_asset_id` is returned.

```
{  
   "response": {  
      "status": "OK",
      "count": 0,
      "start_element": 0,
      "num_elements": 0,
      "dbg_info": {  
         "instance": "05.media-asset-pipeline.prod.nym2",
         "db":"",
         "warnings": [  
         ],
         "start_microtime": 1492716035.805,
         "time": 5,
         "version": "",
         "output_term": "media-asset"
      },
      "media-asset":[  
         {  
            "id": 1536691,
            "parent_media_asset_id": null,
            "member_id": 123,
            "advertiser_id": null,
            "publisher_id": null,
            "file_name": "NATIVE.JPG",
            "size_in_bytes": 79400,
            "cdn_uploaded_on": null,
            "cdn_url": "https://vcdn.adnxs.com/p/creative-image/1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
            "cdn_secure_url": "https://vcdn.adnxs.com/p/creative-image/1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
            "created_on": "2017-04-20 19:20:35",
            "last_modified": "2017-04-20 19:20:35",
            "deleted": false,
            "media_asset_status": [  
               {  
                  "id": 1536687,
                  "media_asset_id": 1536691,
                  "error_message": null,
                  "local_path": "1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
                  "cdn_upload_attempt_count": 0,
                  "created_on": "2017-04-20 19:20:35",
                  "last_modified": "2017-04-20 19:20:35",
                  "deleted": false,
                  "status": "on_shared_storage"
               }
            ],
            "media_asset_image": {  
               "id": 1005450,
               "media_asset_id": 1536691,
               "height": 480,
               "width": 640,
               "created_on": "2017-04-20 19:20:35",
               "last_activity": "2017-04-20 19:20:35",
               "deleted": false
-            },
            "media_asset_video": null,
            "media_asset_html5": null,
            "asset_type": "image",
            "mime_type": "image/jpeg"
         }
      ]
   }
}
```

Step 2: Use the `media_asset_id` to upload the creative.

```
cat native
{
    "creative": {
        "name": null,
        "brand_id": 1,
        "media_url": "https://mediaurl.com",
        "code": "test",
        "code2": null,
        "member_id": 4,
        "state": "active",
        "advertiser_id": 7,
        "publisher_id": null,
    "template": {
        "id": 39461
    },
        "native_attribute": {
            "link": {
                "url": "https://url.com",
                "fallback_url": "https://fallback.com",
                "trackers": [
                    {
                        "url": "http://url.com",
                        "url_secure": "https://secureurl.com"
                    }
                ]
            },
            "data_assets": [
                {
                    "data_type": "sponsored_by",
                    "value": "a value"
                },
                {
                    "data_type": "rating",
                    "value": "8"
                }
            ],
            "image_assets": [
                {
                    "image_type": "main_image",
                    "media_asset_id": 1536691,
                    "image_resize_setting": {
                        "resize_enabled": true,
                        "crop_enabled": true,
                        "aspect_ratio_upper_bound": 1.2,
                        "aspect_ratio_lower_bound": 0.8,
                        "max_scale_factor": 1.41
                    }
                }
            ],
            "image_trackers": [
                {
                    "url": "http://url.com",
                    "url_secure": "https://secureurl.com"
                }
            ],
            "javascript_trackers": [
                {
                    "url": "http://url.com",
                    "url_secure": "https://secureurl.com"
                }
            ]
        },
        "thirdparty_viewability_providers": null,
        "status": {
            "user_ready": true
        },
        "sla_eta": null,
        "currency": "USD",
        "type": "native"
    }
}
 
```

```
$ curl -b cookies -c cookies -X POST -d @native 'https://api.appnexus.com/creative/1751'
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
            "proxy": true
        },
        "creative": {
            "name": null,
            "brand_id": 1,
            "media_url": "https://mediaurl.com",
            "id": 411,
            "code": "test",
            "code2": null,
            "member_id": 4,
            "state": "active",
            "click_track_result": "not_tested",
            "advertiser_id": 3,
            "publisher_id": null,
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
            "pop_values": null,
            "brand": {
                "id": 1,
                "name": "Unknown",
                "category_id": null
            },
            "template": {
                "id": 39461,
                "name": "native ad",
                "media_subtype_id": 17,
                "format_id": 11
            },
            "ios_ssl_audit": null,
            "adx_audit": null,
            "thirdparty_page": null,
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
                    "trackers": [
                        {
                            "url": "http://url.com",
                            "url_secure": "https://secureurl.com"
                        }
                    ]
                },
                "data_assets": [
                    {
                        "data_type": "sponsored_by",
                        "value": "a value"
                    },
                    {
                        "data_type": "rating",
                        "value": "8"
                    }
                ],
                "image_assets": [
                    {
                        "image_type": "main_image",
                        "media_asset_id": 1536691,
                        "creative_asset_image": {
                            "url": "http://url.com",
                            "url_secure": "https://secureurl.com",
                            "height": 12,
                            "width": 34
                        }
                        "image_resize_setting": {
                            "resize_enabled": true,
                            "crop_enabled": true,
                            "aspect_ratio_upper_bound": 1.2,
                            "aspect_ratio_lower_bound": 0.8,
                            "max_scale_factor": 1.41
                        }
                    }
                ],
                "image_trackers": [
                    {
                        "url": "http://url.com",
                        "url_secure": "https://secureurl.com"
                    }
                ],
                "javascript_trackers": [
                    {
                        "url": "http://url.com",
                        "url_secure": "https://secureurl.com"
                    }
                ]
            },
            "thirdparty_viewability_providers": null,
            "status": {
                "user_ready": true
            },
            "sla_eta": null,
            "currency": "USD",
            "type": "standard"
        }
    }
    }
```

## Related topics

- [Creative Upload Service - File Format](creative-upload-service---file-format.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
