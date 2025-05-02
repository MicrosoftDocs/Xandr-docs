---
title: Outgoing Bid Request to Bidders
description: Learn about outgoing bid request to bidders that offers all the necessary information for a bidder to produce a bid price and a creative to serve.
ms.date: 10/28/2023
---

# Outgoing bid request to bidders

> [!NOTE]
> This describes the integration of the [OpenRTB 2.4 protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

This bid request is sent to bidders whenever an ad call reaches the impression bus. It contains all the necessary information for a bidder to produce a bid price and a creative to serve.

The bid request includes information from sellers that specifies which advertisers and creatives are allowed to win an auction and run on a page.

> [!NOTE]
> You may not wish to receive all bid requests that pass through our platform. You can either throttle requests by some percentage, or filter requests by preset criteria such as geography.

## Implementation

Refer to the tables to locate the implementation details such as objects and headers that you need more information on.

### Bid request headers

| Field | Type | Description |
|:---|:---|:---|
| `Content-Length` | int | Length of the body of the HTTP request (which includes all fields described below). |
| `Host` | string | IP address to which the bid request has been sent. |
| `Connection` | string | Always set to `"keep-alive"` to ensure persistent TCP connections. |
| `Content-Type` | string | The type of content passed in the request. Always set to `"application/json"`. |
| `x-openrtb-version` | string | The openrtb version supported in the bid request. Currently set to `2.4`. |

### Bid request object

Xandr supports the following fields in the top-level bid request object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) The unique identifier of the bid request. |
| `imp` | array of objects | (Required) The impressions offered in this bid request. See [Impression Object](#impression-object) below. |
| `site` | object | Specifies information about the website or subset of inventory (placement group) for the impressions. Applicable for website impressions. See [Site Object](#site-object) below. |
| `app` | object | Specifies information about the app for the impressions. Applicable for app impressions. See [App Object](#app-object) below. |
| `device` | object | Specifies information about the user's device to which these impressions will be delivered. See [Device Object](#device-object) below. |
| `user` | object | Specifies information about the person to whom the impressions will be delivered. See [User Object](#user-object) below. |
| `test` | integer | Indicates that this auction is in test mode and is not billable. If not present, default is used.<br> - `0`: Live mode; billable (default).<br> - `1`: Test mode; not billable. |
| `at` | integer | Specifies the auction type. If not present, default is used.<br> - `1`: First price.<br> - `2`: Second price plus one cent (default). |
| `wseat` | array of strings | Specifies an array representing a allowlist of buyer seats allowed to bid on this impression. |
| `tmax` | integer | Specifies the maximum time (in milliseconds) to submit a bid before timing out. |
| `cur` | array of strings | Specifies an array of allowed currencies for bids on this bid request using ISO-4217 alphabetic codes. Defaults to `USD`. |
| `bcat` | array of strings | Specifies a list of blocked content categories. Includes IAB categories (listed in section 5.1 of the specification). `Bcat` is not a required field and is only sent if there are blocked categories associated with the bid request. If no blocked categories are associated, then we don't send this field. |
| `badv` | array of strings | Specifies a list of blocked top-level advertiser domains that correspond to brand URLs in our system. For example, `["company1.com","company2.com"]`. <br>For more information, see the [Brand Service](brand-service.md). A max of 64 values is sent. |
| `regs` | object | Specifies information about an industry, legal, or governmental regulation in force for this request. See [Regs Object](#regs-object) below. |
| `source` | object | Provides data about the inventory source and which entity makes the final decision. See [Source Object](#source-object) below. |
| `ext` | object | Used for identifying platform-specific extensions to the OpenRTB bid request. See [Bid Request Extension Object](#bid-request-extension-object) below. |

### Bid request extension object

We support the follow objects in the `ext` object to support platform-specific extensions as well as supplychain signals:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the OpenRTB bid request. |
| `schain` | object | Specifies the SupplyChain fields included in the OpenRTB bid request for supply path transparency. See [Schain Object](#schain-object) below. |

### Schain object

We support the following fields in the `schain` (Supply Chain) object:

| Field | Type | Description |
|:---|:---|:---|
| `ver` | string | Version of the supply chain specification in use, in the format of “major.minor”. Currently using version 1.0 of the spec. |
| `complete` | enum | Flag indicating whether the chain contains all nodes involved in the transaction leading back to the owner of the site, app or other medium of the inventory, where 0 = no, 1 = yes. |
| `nodes` | object | Array of SupplyChainNode objects in the order of the chain. In a complete supply chain, the first node represents the initial advertising system and seller ID involved in the transaction, i.e. the owner of the site, app, or other medium. In an incomplete supply chain, it represents the first known node. The last node represents the entity sending this bid request, which is the Xandr node.<br>We support the following fields in the nodes object:<br> - **asi** (string): The canonical domain name of the SSP, Exchange, Header Wrapper, etc system that bidders connect to. This should be the same value as used to identify sellers in an ads.txt file if one exists. For the Xandr node that domain will be appnexus.com<br> - **sid** (string): The identifier associated with the seller or reseller account within the advertising system.<br> - **rid** (string): The OpenRTB RequestId of the request as issued by the seller.<br> - **hp** (integer): Indicates whether this node is involved in the flow of payment for the inventory. For version 1.0 of SupplyChain, this property should always be 1. |

### Bid request object

We support the following fields in the `appnexus` extension object for the bid request object:

| Field | Type | Description |
|:---|:---|:---|
| `seller_member_id` | integer | Specifies the ID of the member selling the inventory. See [Platform Member Service](platform-member-service.md) to find the corresponding member names. |
| `spend_protection` | Boolean | **Deprecated** (October 2018). |
| `publisher_integration` | object | Provides details about the publisher integration. |
| `ext_inv_code` | integer | A predefined value passed on the query string that can be used in reporting. The value must be entered into the system before it is logged. For more information, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md).<br>Example: `ext_inv_code=10039` |

### Publisher integration object

We support the following fields in the publisher_integration object:

| Field | Type | Description |
|:---|:---|:---|
| `is_header` | boolean | - `0`: This is not a header bidding integration.<br> - `1`: Integration into a wrapper. |
| `bid_shading_high` | double | **Deprecated** (October 2018). |
| `bid_shading_medium` | double | **Deprecated** (October 2018). |
| `bid_shading_low` | double | **Deprecated** (October 2018). |

### Impression object

We support the following fields in the `imp` object, which describe the impression being auctioned. A single bid request may contain an array with multiple `imp` objects.

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) Specifies a unique identifier for this impression within the context of the bid request. Set to the value of `auction_id_64`.  |
| `banner` | object | Required if this impression is offered as a banner ad. See [Banner Object](#banner-object) below. |
| `video` | object | Required if this impression is offered as a video ad. See [Video Object](#video-object) below. |
| `audio` | object | Required if this impression is offered as an audio ad. See [Audio Object](#audio-object) below. |
| `native` | object | Required if this impression is offered as a native ad. See [Native Object](#native-object) below |
| `instl` | integer | Indicates whether the impression is interstitial or full screen. <br> - `0`: The impression is not interstitial or full screen (default).<br> - `1`: The impression is interstitial or full screen. |
| `tagid` | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. This is our platform's placement ID. Omitted if seller visibility settings prohibit sharing. |
| `bidfloor` | float | Minimum bid for this impression expressed in CPM.<br>Xandr sends the publisher's gross open market floor price in the `bidfloor` field in outgoing bid requests to DSPs downstream. (This includes relevant Xandr seller and buyer fees). This is applicable when the `bidfloor` is set on the publisher's incoming ad request and/or when a publisher's placement reserve price is set. |
| `bidfloorcur` | string | Currency specified using ISO-4217 alpha codes. This may be different from bid currency returned by bidder if this is allowed by the exchange. |
| `secure` | integer | Indicates whether the impression requires secure HTTPS URL creative assets and markup. If omitted, the secure state is unknown but non-secure HTTP support can be assumed.<br> - `0`: The impression is not secure.<br> - `1`: The impression is secure. |
| `pmp` | object | Specifies information about a private marketplace deal that is in effect for this impression. See [Private Marketplace Object](#private-marketplace-object) below. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the impression object. See [Impression Extension Object](#impression-extension-object) below. |

### Banner object

For banner impressions, we support the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `w` | integer | (Recommended) Specifies the exact width of the banner in pixels. |
| `h` | integer | (Recommended) Specifies the exact height of the banner in pixels. |
| `id` | string | Specifies a unique identifier for the banner object. Useful for tracking multiple banner objects (such as with a companion banner array). Typically, the first banner in the array is `1` and subsequent objects increment from there. Currently hardcoded to `1`. |
| `btype` | array of integers | Specifies the banner creative types to block. Refer to section 5.2 of the IAB specification for a list of types. |
| `battr` | array of integers | Specifies the banner creative attributes to block. Refer to section 5.3 of the IAB specification for a list of attributes. |
| `pos` | integer | Specifies the position of the banner on the screen.<br> - `0`: Unknown (default)<br> - `1`: Above the fold<br> - `3`: Below the fold |
| `api` | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Refer to section 5.6 of the IAB specification for a list of API frameworks. |
| `format` | array of objects | The `format` objects that represent the banner sizes permitted. See [Format Object](#format-object) below. <br><br>**Note:** The banner sizes called out in the format object are not representative of allowed sizes via deals. |
| `ext` | object | Not supported. |

### Format object

We support the following field in the `format` object of the `banner` object:

| Field | Type | Description |
|:---|:---|:---|
| `w` | integer |  Specifies the width of the creative, in pixels. |
| `h` | integer |  Specifies the height of the creative, in pixels. |

### Video object

For video impressions, we support the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | (Required) Specifies the video content MIME types supported; for example, `video/x-ms-wmv` and `video/x-flv`. |
| `minduration` | integer | (Recommended) Specifies the minimum video ad duration, in seconds. |
| `maxduration` | integer | (Recommended) Specifies the maximum video ad duration, in seconds. |
| `w` | integer | (Recommended) Specifies the width of the video player, in pixels. |
| `h` | integer | (Recommended) Specifies the height of the video player, in pixels. |
| `startdelay` | integer | (Recommended) Specifies the start delay of the video ad:<br> - `> 0`: For values greater than zero, the delay before video start, in seconds.<br> - `0`: Pre-roll.<br> - `-1`: Generic mid-roll.<br> - `-2`: Generic post-roll. |
| `battr` | array of integers | Specifies the video creative attributes to block. Refer to section 5.3 of the IAB specification for a list of attributes. |
| `minbitrate` | integer | The minimum bit rate, in kilobytes per second. |
| `maxbitrate` | integer | The maximum bit rate, in kilobytes per second. |
| `playbackmethod` | array of integers | Specifies the allowed playback methods. If not specified, all are assumed to be allowed. Currently supported values are:<br>- `1`: Autoplay, sound on.<br> - `2`: Autoplay, sound off.<br> - `3`: Click to play.<br> - `4`: Mouse over to play. |
| `api` | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br> - `1`: VPAID 1.0<br> - `2`: VPAID 2.0<br> - `3`: MRAID-1<br> - `4`: ORMMA<br> - `5`: MRAID-2<br> - `6`: MRAID-3<br> - `7`: OMID-1 |
| `protocols` | array of integers | Array of supported video protocols. Currently supported values are:<br> - `1`: VAST 1.0<br> - `2`: VAST 2.0<br> - `3`: VAST 3.0<br> - `4`: VAST 1.0 Wrapper<br> - `5`: VAST 2.0 Wrapper<br> - `6`: VAST 3.0 Wrapper<br> - `7`: VAST 4.0<br> - `8`: DAAST 1.0 |
| `placement` | integer | Placement type for the impression. Possible options:<br> - `1`: In-Stream<br> - `2`: In-banner<br> - `3`: In-article<br> - `4`: In-feed<br> - `5`: Interstitial/Slider/Floating |
| `linearity` | integer | Indicates if the impression must be linear, nonlinear, etc. If none specified, assume all are allowed.<br> - `1`: Linear / In-Stream<br> - `2`: Non-Linear / Overlay |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the video object. See [Video Extension Object](#video-extension-object) below. |


### Video extension object

We support a single object in the `ext` object to support Xandr-specific extensions to the `video` object:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the video object. |

### Video AppNexus object

We support the following fields in the `appnexus` extension object of the `video` object:

| Field | Type | Description |
|:---|:---|:---|
| `context` | integer | Specifies the video context:<br> - `0`: Unknown<br> - `1`: Pre-roll<br> - `2`:  Mid-roll<br> - `3`:  Post-roll<br> - `4`: Outstream<br> - `5`: BannerStream<br> - `6`: In-feed<br> - `7`: Interstitial |
<!--
### Video placement object

We support the following field(s):

> [!NOTE]
> As of Monday, March 3rd, 2025, Microsoft Monetize supports both reading and sending the `video.plcmt` field in all OpenRTB bid requests, across all versions. This enhancement improves bid accuracy by providing richer contextual information about video ad placements. For bidders using OpenRTB versions earlier than 2.6, enablement is required to receive this field. Please contact your Microsoft account representative or submit a support ticket to request access.

| Field | Type | Description |
|:---|:---|:---|
| `plcmt` | integer | The video placement type for the impression references to the List: Plcmt Subtypes - Video in AdCOM 1.0. For further implementation guide, [Use Plcmt, Placement, and Context](integration-with-openrtb-2-6.md#use-plcmt-placement-and-context-fields-together) fields together. |
-->


### Audio object

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | (Required) Specifies the audio content MIME types supported; for example, `audio/vnd.wav`, `audio/mpeg`, `audio/mp4`, `audio/ogg`, or `audio/mp2`. |
| `minduration` | integer | (Recommended) Specifies the minimum audio ad duration, in seconds. |
| `maxduration` | integer | (Recommended) Specifies the maximum audio ad duration, in seconds. |
| `startdelay` | integer | (Recommended) Specifies the start delay of the audio ad:<br>- `> 0`: For values greater than zero, the delay before audio start, in seconds.<br> - `0`: Pre-roll.<br> - `-1`: Generic mid-roll (delay unknown).<br>- `-2`: Generic post-roll. |
| `battr` | array of integers | Specifies the audio creative attributes to block. We support:<br> - `11`: Surveys<br> - `16`: Ad Provides Skip Button |
| `minbitrate` | integer | The minimum bit rate, in kilobytes per second. |
| `maxbitrate` | integer | The maximum bit rate, in kilobytes per second. |
| `api` | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br> - `1`: VPAID 1.0<br> - `2`: VPAID 2.0<br> - `3`: MRAID-1<br> - `4`: ORMMA<br>- `5`: MRAID-2<br> - `6`: MRAID-3<br>- `7`: OMID-1 |

### Native object

For native impressions, we support the following field, which contains the creative markup:

|  Field | Type | Description |
|:---|:---|:---|
| `request` | string | The rendered creative markup to be delivered; native creatives can be returned in this field as a JSON-encoded string. The first value in the string must be `native`. For examples of native bid requests, see [Request Object](#request-object) below and [Example Bid Requests](#example-bid-requests). |

### Request object

For native impressions, the `request` object contains the creative object in the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `ver` | string | (Recommended) Specifies the version of the native ad specification currently in use. Currently versions **1.1** and **1.2** are supported. |
| `plcmtcnt` | integer | Specifies the number of identical placements available on the bid request. Usually `1`, but can be a different integer if the bid request is for a feed with multiple placements within it. |
| `plcmttype` | integer | The design/format/layout of the ad unit being offered. Xandr sends either value:<br> - `1`: In the feed of content.<br> - `4`: Recommendation widget. |
| `privacy` | boolean | Flag to indicate if the seller supports a buyer-specific privacy notice.<br> - `0` or absent: The native ad doesn't support custom privacy links.<br>- `1`: The native ad supports buyer-specific privacy notice. |
| `assets` | array of objects | Specifies a list of assets that are expected to be returned on the bid response. See [Assets Object](#assets-object) below. |

### Assets object

We support the following fields in the `assets` object in the `native` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Specifies a unique identifier for the asset in this bid request. Typically, the first asset in the array is `1` and subsequent assets increment from there. |
| `required` | integer | Specifies if the asset is required:<br>- `0`: Asset is optional.<br> - `1`: Asset is required. |
| `title` | object | Specifies information about the title of the asset. See [Title Object](#title-object) below. |
| `img` | object | Specifies information about the image for the asset. See [Image Object](#image-object) below. |
| `data` | object | Specifies information about data for the asset. See [Assets Data Object](#assets-data-object) below. |
| `video` | object | Specifies information about the video for the asset. See [Video object for the assets](#video-object-for-the-assets) below. |

### Title object

We support the following fields in the `title` object in the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `len` | integer | Maximum length of the text in the title. |

### Image object

We support the following fields in the `img` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `type` | integer | Specifies the type ID of the image element requested by the publisher. Supported values are:<br>- `1`: Icon image for use on smaller screen sizes (`icon_img_url`). <br> - `3`: Large image preview fo the ad for use on larger screen sizes (`main_media`). |
| `w` | integer | Specifies the exact width of the image, in pixels. |
| `wmin` | integer | Specifies the minimum requested width of the image, in pixels. If included, this value should be used for any rescaling of images by the client. If w or wmin are both included, use `w` as the exact width. |
| `h` | integer | Specifies the height of the image, in pixels. |
| `hmin` | integer | Specifies the minimum requested height of the image, in pixels. If included, this value should be used for any rescaling of images by the client. If both h and hmin are included, use h as the exact height. |
| `mimes` | array of strings | Specifies the image content MIME types supported. Should be empty, as all image types are supported. |

### Assets data object

We support the following fields in the `data` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `type` | integer | Specifies the type ID of the element supported by the publisher. The publisher can display this information in an appropriate format. Supported values are:<br>- `1`: `sponsored` - "Sponsored By" message, where the the response contains the brand name of the sponsor<br>- `2`: `desc` - Descriptive text associated with the product or service being advertised<br>- `3`: `rating` - Rating of the product being offered to the user. For example, an app's rating in an app store from 0–5.<br> - `12`: `ctatext` - Descriptive text for a "call to action" button for the destination URL |
| `len` | integer | Maximum length of the text in the element's response. |

### Event trackers request object

We support the following fields in the `event trackers request` object (Native 1.2 only):

| Field | Type | Description |
|:---|:---|:---|
| `event` | integer | Type of event available for tracking. Supported values are:<br> - `1`: `impression` - Impression<br> - `2`: `viewable-mrc50` - Viewable impression using MRC definition at 50% in view for 1 second.<br> - `3`: `viewable-mrc100` - Viewable impression using MRC definition at 100% in view for 1 second (ie GroupM standard).<br>- `4`: `viewable-video50` - Viewable impression for video using MRC definition at 50% in view for 2 seconds.<br> - `555`: `custom value to signify OMID`  |
| `methods` | array of integers | Array of the types of tracking available for the given event. <br>Supported values are:<br> - `1`: `img` - Img-pixel tracking - URL provided will be inserted as a 1x1 pixel at the time of the event.<br> - `2`: `js` - Javascript-based tracking - URL provided is inserted as a `js` tag at the time of the event. |

### Video object for the assets

We support the following fields in the `video` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | Content MIME types supported. If mimes are not specified in the bid request from supply side, then we will default to `“video/mp4”` for regular video and `“video/x-flv”` for mobile. |
| `minduration` | integer | Minimum video ad duration in seconds. |
| `maxduration` | integer | Maximum video ad duration in seconds. |
| `protocols` | array of integers | An array of video protocols the publisher can accept in the bid response.<br>Currently supported values are:<br> - `1`: VAST 1.0<br> - `2`: VAST 2.0<br> - `3`: VAST 3.0<br> - `4`: VAST 1.0 Wrapper<br> - `5`: VAST 2.0 Wrapper<br> - `6`: VAST 3.0 Wrapper<br> - `7`: VAST 4.0<br> - `8`: DAAST 1.0 |

### Private marketplace object

We support the following fields in the `pmp` object of the `imp` object to support private marketplaces (deals) between buyers and sellers that may apply to this impression:

| Field | Type | Description |
|:---|:---|:---|
| `private_auction` | integer | Indicates the auction eligibility for seats named in the `deals` object.<br> - `0`: All bids are accepted.<br>- `1`: Only bids for specified deals are accepted. |
| `deals` | array of objects | Specifies information about the deals for this bid. See [Deal Object](#deal-object) below. |

### Deal object

We support the following fields in the `deal` object of the `pmp` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) Specifies a unique identifier for the deal. |
| `bidfloor` | float | Specifies the minimum bid price for the deal, in CPM using the default currency (`USD`). If omitted, default is `0.00`. |
| `at` | integer | Optional override of the overall auction type of the bid request. If omitted, default is `2`.<br> - `1`: First price.<br> - `2`: Second price plus one cent (default).<br> - `3`: Bid floor is the agreed upon deal price (fixed price). |
| `wseat` | array of strings | Specifies a list of buyer seat IDs that are allowed to bid on this deal. If no seat is specified, all buyers are eligible. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the deal object. See [Deal Extension Object](#deal-extension-object) below. |

### Deal extension object

We support a single object in the `ext` object to support platform-specific extensions to the `deal` object:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the deal object. |

### Deal AppNexus object

We support the following fields in the `appnexus` extension object of the `deal` object:

| Field | Type | Description |
|:---|:---|:---|
| `ad_quality_override` | integer | Specifies how the deal handles creatives:<br><br> - `1`: Creatives use existing ad quality settings (default).<br> - `2`: Creatives in "pending" audit status will serve. Once these creatives are audited, the existing ad quality settings are used.<br> - `3`: No ad profile restrictions will be applied to this deal (Maximum trust). |
| `allowed_media_types` | array of integers | Specifies the IDs of the media types that are allowed on this deal. For a list of media types, see [Expandables and Rich Media](expandables-and-rich-media.md).<br> If there are no unique media types for this deal as compared to the main bid request object, this field will be an empty array. This does NOT mean the deal does not allow any media types, instead it just means that the media types on the main bid object (anything not specifically listed in the “battr” object) can be used when bidding on this deal. If this array is populated, it will contain a complete list of media types allowed on this deal. |
| `allowed_media_subtypes` | array of integers | Specifies the IDs of the media subtypes that are allowed on this deal. For a list of media subtypes, see [Expandables and Rich Media](expandables-and-rich-media.md).<br> If there are no unique media subtypes for this deal as compared to the main bid request object, this field will be an empty array. This does NOT mean the deal does not allow any media subtypes, instead it just means that the media subtypes on the main bid object (anything not specifically listed in the “battr” object) can be used when bidding on this deal. If this array is populated, it will contain a complete list of submedia types allowed on this deal. |
| `sizes` | array of objects | Specifies the allowed creative sizes for this deal. If this array is populated, it will contain a complete list of sizes allowed on this deal. Sizes allowed on the deal do not have to be a subset of what is allowed in the main bid request object. If the array is empty, that means that there are are no unique sizes for this deal, and the allowed sizes from the main bid object should be used instead. See [Sizes Object](#sizes-object) below. |
| `sc` | integer | Specifies whether the wseat field of the deal object is passing a buyer seat ID. This Field is only present for deals set up with a DSP's buyer seat ID and will pass a value of `"1"`. |
| `gtd` | integer | Specifies whether the deal is Programmatic Guaranteed. This Field is only present for deals set up as Programmatic Guaranteed and will pass a value of `"1"`. |

### Sizes object

We support the following fields in the `sizes` object of the deal `ext` object.

| Field | Type | Description |
|:---|:---|:---|
| `w` | integer | Specifies the width of the creative allowed for this deal, in pixels. |
| `h` | integer | Specifies the height of the creative allowed for this deal, in pixels. |

### Impression extension object

We support a single object in the `ext` object to support platform-specific extensions to the `imp` object:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the impression object. |

### Impression AppNexus object

We support the following fields in the `appnexus` extension object of the `imp` object:

| Field | Type | Description |
|:---|:---|:---|
| `estimated_clear_price` | double | Specifies the estimated clear price needed to win the impression.<br>Price is assumed to be in the publisher's currency. If not, you must specify the currency units. |
| `predicted_view_rate` | double | Specifies the probability that the impression will be viewable by the user as a percent of measured display impressions, based on historical data. |
| `predicted_view_rate_over_total` | double | Specifies the probability that the impression will be viewable by the user over all display impressions, based on historical data. |
| `predicted_video_view_rate_over_total` | double | Specifies the probability that the impression will be viewable by the user over all video impressions, based on historical data. |
| `predicted_video_view_rate` | double | Specifies the probability that the impression will be viewable by the user as a percent of measured video impressions, based on historical data. |
| `member_ad_profile_id` | integer | Specifies the seller's ad profile ID. |
| `allowed_payment_types` | array of objects | Specifies the allowable payments types for this impression. If this field is not present, then the only allowed payment type is `'impression'`.<br><br>**Note:** This object is not enabled for all clients. Reach out to your account representative for this feature. |
| `traffic_source_code` | string | Specifies the external source of the third party traffic for this impression. |
| `predicted_video_completion_rate` | double | Specifies the probability that the video impression will be viewed completely by a user, based on historical data. |
| `gpid` | string | Global placement-level identifier provided by the publisher to indicate a specific ad placement on page. |

### Allowed payment types object

We support the following fields in the `allowed_payment_types` object:

> [!NOTE]
> This object is not enabled for all clients. Reach out to your account representative for this feature.

| Field | Type | Description |
|:---|:---|:---|
| `payment_type` | integer | Specifies the payment type allowed for this impression. Currently supported values:<br> - `1`: Impression<br>- `2`: Views - Standard Display<br> - `6`: Views - Custom Display - 100pv1s<br> - `8`: Views - Standard Video<br> - `9`: Views - Custom Video - 100pv50pd |
| `conversion_rate` | double | Specifies the the rate that Xandr uses to convert a non-impression bid to an eCPM price for bid ranking in the auction. A Bidder may use this for internal bid ranking, budgeting/pacing, or potentially for others. |
| `imp_count_method` | int | Specifies how the impression is counted. Currently supported values:<br> - `0`: Not applicable<br> - `1`: Unknown<br> - `2`: Count on render<br> - `3`: Count on decision/serve |

For more information check the [Overview](guaranteed-outcomes.md) page.

### Site object

Sites (also known as placement groups) are a subset of inventory for a publisher. We support the following fields in the `site` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Recommended. Specifies the Xandr site ID. Omitted if seller visibility prohibits sharing. Bidders cannot lookup what site the ID corresponds to, but these IDs can be used as anonymous, optimizable chunks of inventory. |
| `domain` | string | Specifies the domain of the site (for example, `publishersite.com`). Omitted if seller visibility prohibits sharing. |
| `cat` | array of strings | Specifies a list of content categories. Includes IAB categories (listed in section 5.1 of the specification). Omitted if seller visibility settings prohibit sharing. |
| `page` | string | Specifies the full URL of the page where the impression is shown (for example, `page.publishersite.com/path/to/page`). Omitted if seller visibility settings prohibit sharing. Contains the domain instead of the full URL if only domain is exposed in the visibility profile. |
| `publisher` | object | Specifies information about the publisher. Omitted if seller visibility settings prohibit sharing. See [Publisher Object](#publisher-object) below. |
| `content` | object | Details about the Content within the site. See [Content Object](#content-object) below. |
| `ext` | object | Used for holding app extension fields. See [Site extension object](#site-extension-object) below.  |

### Site extension object

We support the following fields in the ext object of the site object.

| Field | Type | Description |
|:---|:---|:---|
| `inventorypartnerdomain` | object | The value passed in this field instructs the app-ads.txt enforcer to check the app’s app-ads.txt file for the directive inventorypartnerdomain=[value of this field]. |

### App object

We support the following fields in the `app` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the Xandr app ID. Omitted if seller visibility prohibits sharing. Bidders cannot lookup what site the ID corresponds to, but these IDs can be used as anonymous, optimizable chunks of inventory. |
| `bundle` | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. For iOS, this will be the iTunes app id (numerical ID). Omitted if seller visibility prohibits sharing. |
| `cat` | array of strings | Specifies a list of content categories. Includes IAB categories (listed in section 5.1 of the specification). Omitted if seller visibility settings prohibit sharing. |
| `publisher` | object | Specifies information about the publisher. Omitted if seller visibility settings prohibit sharing. See [Publisher Object](#publisher-object) below. |
| `name` | string | The full name of the app (i.e. Angry Birds). (This value may be aliased at the publisher's request.) |
| `content` | object | Details about the Content within the site. See [Content Object](#content-object) below. |
| `storeurl` | string | App store URL for an installed app. |
| `ext` | object | Used for holding app extension fields. See [App extension object](#app-extension-object) below.  |

### Publisher object

We support the following field in the `publisher` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the Xandr publisher ID. Omitted if seller visibility settings prohibit sharing. |

### Content object

Xandr supports the following fields in the Content object:

| Field | Type | Description |
|:---|:---|:---|
| `genre` | string | Genre that best describes the content (e.g., rock, pop, etc). |
| `id` | string | ID uniquely identifying the content. |
| `language` | string | Content language using ISO-639-1-alpha-2. |
| `ext` | object | Placeholder for exchange-specific extensions to OpenRTB. |
| `episode` | integer | Episode number. |
| `title` | string | Content title.<br>Video Examples: "Search Committee" (television), "A New Hope" (movie), or "Endgame" (made for web).<br>Non-Video Example: "Why an Antarctic Glacier is Melting So Quickly" (Time magazine article). |
| `series` | string | Video Examples: "The Office" (television), "Star Wars" (movie), or "Arby 'N' The Chief" (made for web).<br>Non-Video Example: "Ecocentric" (Time Magazine blog). |
| `season` | string | Content season (e.g., "Season 3"). |
| `artist` | string | Artist credited with the content. |
| `album` | string | Album to which the content belongs; typically for audio. |
| `isrc` | string | International Standard Recording Code conforming to ISO-3901. |
| `producer`  | object | Details about the content `Producer`. Refer to section 3.2.12 in the IAB specification. |
| `url`  | string | URL of the content, for buy-side contextualization or review. |
| `cat`  | string array | Array of IAB content categories that describe the content producer. Refer to list 5.1 in the IAB specification. |
| `prodq`  | integer | Production quality. Refer to List 5.11 in the IAB specification. |
| `videoquality` | integer | **Deprecated** in favor of prodq. Video quality. Refer to List 5.11 in the IAB specification. |
| `context` | integer | Type of content (game, video, text, etc.). Refer to List 5.16  in the IAB specification. |
| `contentrating` | string | Content rating (e.g., MPAA). |
| `userrating`  | string  | User rating of the content (e.g., number of stars, likes, etc.). |
| `qagmediarating`  | integer | Media rating per IQG guidelines. Refer to List 5.17 in the IAB specification. |
| `keywords`  | string  | Comma separated list of keywords describing the content. |
| `livestream`  | integer | `0` = not live, `1` = content is live (e.g., stream, live blog). |
| `sourcerelationship`  | integer | `0` = indirect, `1` = direct. |
| `len` | integer | Length of content in seconds; appropriate for video or audio. |
| `data`  | object array  | Additional content data. Each Data object represents a different data source. Refer to Section 3.2.16 in the IAB specification. |

### Content extension Object

Xandr supports the following field in the ext object:

| Field | Type | Description |
|:---|:---|:---|
| `network` | string | The top-level parent company or, where relevant, a sub-brand which owns multiple TV-like channels, d2c content brands, or digital properties on which the content is being viewed. |

### App extension object

We support the following fields in the ext object of the app object.

| Field | Type | Description |
|:---|:---|:---|
| `inventorypartnerdomain` | string | The value passed in this field instructs the app-ads.txt enforcer to check the app’s app-ads.txt file for the directive inventorypartnerdomain=[value of this field]. |

### Device object

We support the following fields in the `device` object.

| Field | Type | Description |
|:---|:---|:---|
| `ua` | string | (Recommended) Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. |
| `geo` | object | Specifies the location of the device, as derived from the device's location services (such as cell tower triangulation or GPS) or IP address. Also includes the timezone and a code for the designated market area. <br><br>**Note:** `geo` overrides IP. <br><br> For details, see [Geo Object](#geo-object). |
| `dnt` | integer | Specifies the Do Not Track setting:<br> - `0`: Do Not Track is set to false in browser (tracking is allowed).<br> - `1`: Do Not Track is set to true in browser (user has opted out of tracking). |
| `ip` | string | Specifies the IPv4 address closest to the device. Omitted if seller visibility settings prohibit sharing. |
| `ipv6` | string | IP address closest to device as IPv6. |
| `devicetype` | integer | Specifies the type of device, using IAB values:<br> - `1`: Mobile/Tablet<br> - `2`: Personal Computer<br> - `3`: Connected TV<br> - `4`: Phone<br> - `5`: Tablet<br> - `6`: Connected Device<br> - `7`: Set Top Box |
| `make` | string | Specifies the make of the device.  |
| `model` | string | Specifies the model of the device.  |
| `os` | string | Specifies operating system of the device. If passed, this overrides the operating system in the ua field. The following are the possible values in the os field:<br> - "Unknown"<br> - "Android"<br> - "Apple iOS"<br> - "Apple Mac"<br> - "Microsoft Windows"<br> - "Blackberry OS"<br> - "Microsoft Mobile"<br> - "Linux"<br> - "Symbian OS"<br> - "Chrome OS"<br> - "PlayStation 4 OS"<br> - "Firefox OS"<br> - "Roku OS" |
| `language` | string | Specifies the browser language; use ISO 639-1 or ISO 3166 alpha-2 codes. |
| `lmt` | integer | "Limit Ad Tracking" signal commercially endorsed (e.g., iOS, Android), where 0=tracking is unrestricted, 1=tracking must be limited per commercial guidelines. |
| `carrier` | string | Specifies carrier for the device.  |
| `connectiontype` | integer | Specifies the detected data connection type for the device using IAB values. We support the following values today:<br> - `0`: Unknown<br> - `3`: Cellular Network – Unknown Generation |
| `ifa` | string | Specifies the ID sanctioned for advertiser use in the clear. Set to iOS `idfa`, Android `aaid`, or Windows `adid` if available. Is also set for CTV impressions, using device-provided, publisher-provided, or other device ID types as applicable. For more information, see **ext.ifa_type**. Omitted if seller visibility settings prohibit sharing. |
| `dpidsha1` | string | Specifies the SHA1-encrypted, platform-specific (e.g., `ANDROID_ID` or `UDID` for iOS) unique identifier for the mobile device. Omitted if seller visibility settings prohibit sharing. |
| `dpidmd5` | string | Specifies the MD5-encrypted, platform-specific (e.g., `ANDROID_ID` or `UDID` for iOS) unique identifier for the mobile device.Omitted if seller visibility settings prohibit sharing. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the geo object. See [Geo Extension Object](#geo-extension-object) below. |

### Geo object

We support the following fields in the `geo` object:

| Field | Type | Description |
|:---|:---|:---|
| `lat` | float | Specifies the latitude of the device, as derived from the device's location services. This can range from `-90` to `90`. South is negative. |
| `lon` | float | Specifies the longitude of the device, as derived from the device's location services. This can range from -`180` to `180`. West is negative. |
| `country` | string | Specifies the country or region name, according to ISO-3166-1 Alpha-3. |
| `region` | string | Region code using ISO-3166-2; 2-letter state code if USA. |
| `city` | string | Specifies the city name. Omitted if seller visibility settings prohibit sharing. |
| `zip` | string | Specifies the ZIP or postal code where the device is located. Omitted if seller visibility settings prohibit sharing. |
| `metro` | string | Contains a code for the user's designated market area based on their IP address (if the IP address can be determined). |
| `utcoffset` | int | Indicates the local time as an offset from UTC. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the geo object. See [Geo Extension Object](#geo-extension-object) below. |

### Geo extension object

We support a single object in the `ext` object to support platform-specific extensions to the `geo` object:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the geo object. For a list of the extensions for this object, see [Geo AppNexus Object](#geo-appnexus-object) below. |

### Geo AppNexus object

We support the following field in the `appnexus` extension object of the `geo` object:

| Field | Type | Description |
|:---|:---|:---|
| `timezone` | string | Contains the timezone of the user based on IP address (if the IP address can be determined). |

### Device extension object

We support a single object in the `ext` object to support platform-specific extensions to the `device` object:

| Field | Type | Description |
|:---|:---|:---|
| `ifa_type` | string | Specifies the source of the IFA, whether that is device-generated (and therefore used across apps) or whether it is a publisher provided IFA, or a temporary/session IFA. Used primarily for CTV impressions.<br>The types of IFA are Device, Publisher (including apps), SSP and Session. The following are recommended values for the `ifa_type` parameter:<br> - "dpid" - the generic “device provided id”, but based on historical usage, common device type specific values can be used<br> - "rida" - Roku id<br> - "aaid" - Android id<br> - "idfa" - Apple id<br> - "afai" - Amazon Fire id<br> - "tifa" - Tizen Identifier for Advertising (Samsung Ad ID)<br> - "vida" - Vizio Advertising ID<br> - "lgudid" - LG Unique Device ID<br> - "msai" - Microsoft id<br> - "ppid" - publisher provided id<br> - "sspid" - SSP provided id<br> - "sessionid" - session id/synthetic id (described below) |

### User object

We support the following fields in the `user` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Either `id` or `buyeruid` is recommended) Specifies the Xandr unique ID for this user. Omitted if seller visibility settings prohibit sharing. The unique 64-bit ID for the user. It is the same for all requests from this user until cookies are cleared. This field is `0` when Xandr does not have a match for this user or the user's browser doesn't accept cookies. It is `-1` for opt-out users. |
| `buyeruid` | string | (Either `id` or `buyeruid` is recommended) The buyer's unique ID for this user, if known. Omitted if seller visibility settings prohibit sharing. |
| `yob` | integer | Specifies the year of birth as a 4-digit integer. Omitted if unknown, or if seller visibility settings prohibit sharing. |
| `gender` | string | Specifies the gender. Set to `null` if unknown. Omitted if unknown, or seller visibility settings prohibit sharing.<br> - `M`: Male<br> - `F`: Female<br> - `O`: Other |
| `data` | array of objects | Specifies information about data for the user. See [User Data Object](#user-data-object) below. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the user object. |

### User data object

We support the following fields in the `data` object of the `user` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the ID of the data provider. |
| `segment` | array of objects | **Deprecated** (April 2019). |

### User extension object

We support the following fields in the `ext` object to support platform-specific extensions to the `user` object:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the platform-specific extensions to the user object. See below for a list of the extensions for this object. |
| `consent` | string | Optional. Contains the data structure developed by the General Data Protection Regulation (GDPR) Consent Working Group under the auspices of [IAB Europe](https://www.iabeurope.eu/). |
| `eids` | object | Specifies the information relating to the extended user identifiers. This can be either third party identity solutions (Criteo, TDID, RampID, etc.) or Publisher-provided identifiers (PPIDs). |

### Object

> [!NOTE]
> `eids` is not available if privacy signals indicate personal information cannot be processed.

We support the following fields in the `eids` object:

| Field | Type | Description |
|:---|:---|:---|
| `source` | string | Specifies the domain of the organization that is the generator of the third party ID. |
| `uids` | Object | Specifies the identity information specific to the third party identity solution or publisher. Relevant fields include:<br>**id**<br>string<br>User id provided by third party identity solution or publisher.<br><br>**ext**<br>Object<br>Specifies specific additional information provided by third party identity solution or publisher.<br>Ext Fields include:<br>rtiPartner = third party identity solution name, used by TDID. |

### Segment object

> [!WARNING]
> This object is deprecated (2019).

We support the following fields in the `segment` object of the user `data` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the Xandr segment ID. |
| `value` | string | Specifies the value of the data segment. |

### Regs object

We support the following fields in the `regs` object:

| Field | Type | Description |
|:---|:---|:---|
| `coppa` | integer | Indicates if this request is subject to the United States Children's Online Privacy Protection Act (COPPA).<br> - `0`: Not subject to COPPA. Treat as a normal auction.<br> - `1`: Subject to COPPA. Limit what is allowed for targeting and logging as required. |
| `ext` | object | Used for identifying platform-specific extensions to OpenRTB for the reg object. |
| `gpp` |  | Indicates the actual IAB GPP consent string. It implies which vendors are permitted to process personal data and under which conditions.<br>Example:<br>`{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [2,6]} } }` |
| `gpp_sid` |  | Optional: indicates which regulations or GPP logics are to be applied, or whether a user is located in a country or region (EEA country or region) with a framework that is part of the GPP.<br>Example:<br>`{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [2,6]} } }` |

### Regs extension object

We support the following field in the `regs.ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `gdpr` | integer | Optional. Signals whether or not the request is subject to General Data Protection Regulation (GDPR) regulations. Possible values:<br> - `0`: No, the request is not subject to GDPR regulations.<br> - `1`: Yes, the request is subject to GDPR regulations.<br>No value indicates Unknown. |
| `us_privacy` | string | The U.S. Privacy String currently supports CCPA compliance by passing the follow information in the string: <br>**Specification Version**<br>Number (1 char in string)<br>The version of this string specification used to encode the string<br><br>**Explicit Notice/ Opportunity to Opt Out**<br>ENUM (`N` = No, `Y` = Yes, `-` = Not Applicable)<br>Has explicit notice been provided as required by 1798.115(d) of the CCPA and the opportunity to opt out of the sale of their data pursuant to 1798.120 and 1798.135 of the CCPA<br><br>**Opt-Out Sale**<br>ENUM (`N` = No, `Y` = Yes, `-` = Not Applicable)<br>Has user opted-out of the sale of his or personal information pursuant to 1798.120 and 1798.135<br><br>**LSPA**<br>ENUM (`N` = No, `Y` = Yes, `-` = Not Applicable)<br>Publisher is a signatory to the IAB Limites those terms are defined in the Agreement.  d Service Provider Agreement (LSPA) and the publisher declares that the transaction is covered as a “Covered Opt Out Transaction” or a “Non Opt Out Transaction” as those terms are defined in the Agreement.  s those terms are defined in the Agreement.   |
| `gpp` |  | Indicates the actual IAB GPP consent string. It implies which vendors are permitted to process personal data and under which conditions.<br>Example:<br>`{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [2,6]} } }` |
| `gpp_sid` |  | Optional: indicates which regulations or GPP logics are to be applied, or whether a user is located in a country or region (EEA country or region) with a framework that is part of the GPP.<br>Example:<br>`{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [2,6]} } }` |
| `dsa` |  | Indicates whether the request is subject to the Digital Services Act (DSA). For more details, see [here](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/main/extensions/community_extensions/dsa_transparency.md).<br><br>Example:<br>`{ dsarequired: 1, pubrender: 0, transparency: [ { domain: 'request.tomato.com', dsaparams: [ 1 ] },{ domain: 'request2.tomato.com', dsaparams: [ 1, 2, 3 ] }],datatopub: 1 }` |

### Source object

We support the following fields in the `source` object:

| Field | Type | Description |
|:---|:---|:---|
| `fd` | integer | Entity responsible for the final impression sale decision, where:<br> - `0`: exchange (default)<br> - `1`: upstream source |
| `tid` | string | Transaction ID that must be common across all participants in this bid request. Value will be passed in from the seller. If seller does not provide a transaction ID, we create one and share it. |

## Example bid requests

### Banner bid request

```
{
    "id": "8765482113786061111",
    "imp": [{
        "id": "7654319310942953333",
        "banner": {
            "w": 320,
            "h": 50,
            "id": "1",
            "battr": [1, 2, 15],
            "pos": 0,
            "format": [{
                "w": 320,
                "h": 50
            }]
        },
        "instl": 0,
        "tagid": "12347654",
        "secure": 1,
        "ext": {
            "appnexus": {
                "estimated_clear_price": 0.57,
                "predicted_view_rate": 0.073255,
                "member_ad_profile_id": 1111055,
                "predicted_video_completion_rate": 0.592172,
                "predicted_view_rate_over_total": 0.067229,
                "allowed_payment_types": [{
                    "payment_type": 1,
                    "imp_count_method": 2
                }]
            }
        }
    }],
    "site": {
        "id": "3232399",
        "domain": "example.com",
        "cat": ["IAB12-2", "IAB12", "IAB11-5"],
        "page": "https://example.com/somepage.md",
        "publisher": {
            "id": "1111999"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Linux; Android 6.0.1; HUAWEI Build/MMB28B) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.137 Mobile Safari/537.36",
        "geo": {
            "lat": 36.6203,
            "lon": -4.4998,
            "country": "ESP",
            "region": "MA",
            "metro": "1",
            "city": "UnaCuidad",
            "zip": "11111",
            "utcoffset": 60,
            "ext": {
                "appnexus": {
                    "timezone": "Africa/Ceuta"
                }
            }
        },
        "dnt": 0,
        "ip": "11.222.111.0",
        "devicetype": 4,
        "make": "Unknown",
        "model": "Generic Android Mobile",
        "os": "Android",
        "language": "es",
        "connectiontype": 0
    },
    "user": {
        "id": "7939999668795769876",
        "buyeruid": "CABBBBrbuQ9AA5DMJJJJlOL9ZOo",
        "gender": "O",
        "data": [{
            "id": "0",
            "segment": [{
                "id": "1",
                "value": "0"
            }]
        }, {
            "id": "1234",
            "segment": [{
                "id": "4444555",
                "value": "0"
            }]
        }],
        "ext": {
            "appnexus": {
                "userdata_json": "{\"uid\":\"CABBBBrbuQ9AA5DMJJJJlOL9ZOo\"}"
            }
        }
    },
    "test": 0,
    "at": 1,
    "tmax": 150,
    "wseat": ["1234",..., "9988"],
    "cur": ["USD"],
    "bcat": ["IAB23-7", "IAB23-5", "IAB23-10", "IAB23-9", "IAB23-1", "IAB7-44", "IAB9-9", "IAB8-18", "IAB8-5"],
    "badv": ["url1.com", "url2.com"],
    "ext": {
        "appnexus": {
            "seller_member_id": 123,
            "publisher_integration": {
                "is_header": 0
            }
        },
        "schain": {
            "complete": 1,
            "nodes": [{
                "asi": "appnexus.com",
                "sid": "123",
                "rid": "2dd111ff-7777-4abc-8558-86a123ab46d6",
                "hp": 1
            }],
            "ver": "1.0"
        }
    },
    "source": {
        "fd": 1,
        "tid": "2dd111ff-7777-4abc-8558-86a123ab46d6"
    }
}
```

### Native 1.1 bid request

```
{
    "id": "123456789",
    "imp": [{
        "id": "987654321",
        "native": {
            "request": "{\"ver\":\"1.1\",\"plcmttype\": 4,\"plcmtcnt\": 1,\"assets\":[{\"id\": 1,\"required\": 1,\"title\":{\"len\": 140}},{\"id\": 4,\"required\": 1,\"img\":{\"type\": 3,\"wmin\": 600,\"hmin\": 315}},{\"id\": 2,\"required\": 0,\"img\":{\"type\": 1,\"wmin\": 320,\"hmin\": 180}},{\"id\": 6,\"required\": 1,\"data\":{\"type\": 2,\"len\": 205}},{\"id\": 5,\"required\": 1,\"data\":{\"type\": 1,\"len\": 140}}]}}",
            "ver": "1.1"
        },
        "instl": 0,
        "secure": 0,
        "ext": {
            "appnexus": {
                "estimated_clear_price": 11.644000,
                "member_ad_profile_id": 667317,
                "predicted_view_rate_over_total": 0.000000
            }
        }
    }],
    "app": {
        "id": "1234",
        "bundle": "com.news.example"
    },
    "device": {
        "ua": "iPad; OS like Mac OS X; iOS 9.2; STR 2.2.4",
        "geo": {
            "country": "USA",
            "city": "Wilmington",
            "zip": "01887"
        },
        "dnt": 0,
        "ip": "198.51.100.2",
        "devicetype": 1,
        "make": "Apple",
        "model": "iPad",
        "os": "Apple iOS",
        "connectiontype": 0
    },
    "user": {
        "id": "2233445566",
        "data": [{
            "id": "0",
            "segment": [{
                "id": "1",
                "value": "0"
            }]
        }],
        "ext": {
            "appnexus": {
                "userdata_json": "{}"
            }
        }
    },
    "test": 0,
    "at": 2,
    "tmax": 2000,
    "wseat": [
        "1234"
    ],
    "cur": [
        "USD"
    ],
    "ext": {
        "appnexus": {
            "seller_member_id": 1234
        },
        "schain": {
            "complete": 1,
            "nodes": [{
                "asi": "appnexus.com",
                "sid": "1234",
                "rid": "25e2b11c-004f-4903-a912-5aef7732096b",
                "hp": 1
            }],
            "ver": "1.0"
        }
    }
}
```

### MultiMedia Bid Request

To ensure your bidder is configured to receive these requests, open a support case.

```
{
    "id": "914181541748747384",
    "imp": [{
        "id": "837746433617288491",
        "banner": {
            "w": 320,
            "h": 250,
            "id": "1",
            "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
            "pos": 0,
            "api": [3, 5],
            "format": [{
                "w": 320,
                "h": 250
            }, {
                "w": 1,
                "h": 1
            }, {
                "w": 1,
                "h": 1
            }]
        },
        "native": {
            "request": "{\"ver\":\"1.2\",\"plcmtcnt\":1,\"assets\":[{\"id\":7,\"required\":0,\"img\":{\"type\":3}},{\"id\":8,\"required\":0,\"img\":{\"type\":1}},{\"id\":1,\"required\":0,\"title\":{\"len\":100}},{\"id\":2,\"required\":0,\"data\":{\"type\":2,\"len\":300}},{\"id\":3,\"required\":0,\"data\":{\"type\":12,\"len\":20}},{\"id\":4,\"required\":0,\"data\":{\"type\":1}},{\"id\":5,\"required\":0,\"data\":{\"type\":3}}],\"plcmttype\":4,\"eventtrackers\":[{\"event\":1,\"methods\":[1]}]}",
            "ver": "1.2"
        },
        "instl": 0,
        "tagid": "12345678",
        "secure": 1,
        "pmp": {
            "private_auction": 0,
            "deals": [{
                "id": "345667",
                "bidfloor": 4,
                "bidfloorcur": "USD",
                "at": 2,
                "wseat": ["1234"],
                "ext": {
                    "appnexus": {
                        "sizes": [{
                            "w": 1,
                            "h": 1
                        }, {
                            "w": 320,
                            "h": 250
                        }]
                    }
                }
            }, {
                "id": "345678",
                "bidfloor": 3,
                "bidfloorcur": "USD",
                "at": 2,
                "wseat": ["1234"],
                "ext": {
                    "appnexus": {
                        "sizes": [{
                            "w": 1,
                            "h": 1
                        }, {
                            "w": 320,
                            "h": 250
                        }]
                    }
                }
            }]
        },
        "ext": {
            "appnexus": {
                "estimated_clear_price": 10.72,
                "predicted_view_rate": 0.784599,
                "member_ad_profile_id": 23456,
                "predicted_video_completion_rate": 0,
                "predicted_view_rate_over_total": 0.764223,
                "allowed_payment_types": [{
                    "payment_type": 1,
                    "imp_count_method": 2
                }]
            }
        }
    }],
    "app": {
        "id": "3840770",
        "name": "FunAPP",
        "bundle": "no.funapp.android",
        "publisher": {
            "id": "123567"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Linux; Android 9; SM-G965F Build/PPR1.180610.011; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/74.0.3729.157 Mobile Safari/537.36",
        "geo": {
            "country": "NOR",
            "region": "02",
            "metro": "2435",
            "city": "Hakadal",
            "zip": "1487",
            "utcoffset": 120,
            "ext": {
                "appnexus": {
                    "timezone": "Europe/Oslo"
                }
            }
        },
        "lmt": 0,
        "ip": "123.23.100.5",
        "devicetype": 4,
        "make": "Samsung",
        "model": "SM-G965F",
        "os": "Android",
        "connectiontype": 0,
        "ifa": "0b3979c6-9c84-4359-a5e6-ee6565048fde",
        "ext": {
            "ifa_type": "aaid"
        }
    },
    "user": {
        "id": "4038657820804547795",
        "buyeruid": "S5670DGCSRG"
    },
    "at": 2,
    "tmax": 100,
    "wseat": ["3456"],
    "cur": ["USD"],
    "bcat": ["IAB9-9", "IAB8-5", "IAB8-18"],
    "badv": ["some_advertiser_domain.com"],
    "regs": {
        "coppa": 0
    },
    "source": {
        "fd": 0,
        "tid": "5676d767-e8b8-43b1-b7bf-fd6056b65018"
    },
    "ext": {
        "appnexus": {
            "seller_member_id": 1234,
            "publisher_integration": {
                "is_header": 0
            }
        },
        "schain": {
                "complete": 1,
                "nodes": [{
                    "asi": "appnexus.com",
                    "sid": "1234",
                    "rid": "5676d767-e8b8-43b1-b7bf-fd6056b65018",
                    "hp": 1
                }],
                "ver": "1.0"
            }
    }
}
```

### MultiTag bid request

```
{
    "id": "5698201228871522665",
    "imp": [{
            "id": "13529449707735835",
            "banner": {
                "w": 300,
                "h": 250,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 300,
                    "h": 250
                }]
            },
            "instl": 0,
            "tagid": "123456",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 0.5,
                    "member_ad_profile_id": 1234,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        },
        {
            "id": "2460698130037038280",
            "banner": {
                "w": 580,
                "h": 400,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 580,
                    "h": 400
                }, {
                    "w": 580,
                    "h": 500
                }]
            },
            "instl": 0,
            "tagid": "123457",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 12.4,
                    "member_ad_profile_id": 1235,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }, {
            "id": "5610871170052394076",
            "banner": {
                "w": 580,
                "h": 400,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 580,
                    "h": 400
                }, {
                    "w": 580,
                    "h": 500
                }]
            },
            "instl": 0,
            "tagid": "123478",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 11.14,
                    "member_ad_profile_id": 8765,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }, {
            "id": "9057531734780521319",
            "banner": {
                "w": 580,
                "h": 400,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 580,
                    "h": 400
                }, {
                    "w": 580,
                    "h": 500
                }]
            },
            "instl": 0,
            "tagid": "677",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 11.31,
                    "member_ad_profile_id": 65987,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }, {
            "id": "7953238633763561522",
            "banner": {
                "w": 160,
                "h": 600,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 160,
                    "h": 600
                }]
            },
            "instl": 0,
            "tagid": "987345",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 18.91,
                    "member_ad_profile_id": 12345,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }, {
            "id": "6528429208551730965",
            "banner": {
                "w": 980,
                "h": 300,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 980,
                    "h": 300
                }, {
                    "w": 580,
                    "h": 400
                }, {
                    "w": 580,
                    "h": 500
                }]
            },
            "instl": 0,
            "tagid": "34546",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 8.58,
                    "member_ad_profile_id": 3456,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }, {
            "id": "8731177004555232453",
            "banner": {
                "w": 160,
                "h": 600,
                "id": "1",
                "battr": [1, 2, 3, 4, 5, 9, 10, 12, 14],
                "pos": 0,
                "format": [{
                    "w": 160,
                    "h": 600
                }, {
                    "w": 180,
                    "h": 500
                }, {
                    "w": 180,
                    "h": 700
                }]
            },
            "instl": 0,
            "tagid": "345637",
            "secure": 1,
            "ext": {
                "appnexus": {
                    "estimated_clear_price": 8.78,
                    "member_ad_profile_id": 34567,
                    "allowed_payment_types": [{
                        "payment_type": 1,
                        "imp_count_method": 2
                    }]
                }
            }
        }
    ],
    "site": {
        "id": "346789",
        "domain": "xandr.com",
        "cat": ["IAB12", "IAB12-2", "IAB11-5"],
        "page": "xandr.com",
        "publisher": {
            "id": "876543"
        }
    },
    "device": {
        "ua": "Mozilla/5.0 (Linux; Android 9; SAMSUNG SM-G950U) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/10.1 Chrome/71.0.3578.99 Mobile Safari/537.36",
        "geo": {
            "country": "USA",
            "region": "FL",
            "metro": "539",
            "city": "Tampa",
            "zip": "33617",
            "utcoffset": -240,
            "ext": {
                "appnexus": {
                    "timezone": "America/Indiana/Vevay"
                }
            }
        },
        "dnt": 0,
        "ip": "173.168.163.240",
        "devicetype": 2,
        "make": "Samsung",
        "model": "SM-G950U",
        "os": "Android",
        "language": "en",
        "connectiontype": 0,
        "ext": {}
    },
    "user": {
        "id": "6535227187230073444",
        "buyeruid": "a_dsp_user_id",
        "at": 1,
        "tmax": 100,
        "wseat": ["1417"],
        "cur": ["USD"],
        "regs": {
            "coppa": 0
        },
        "source": {
            "fd": 0,
            "tid": "0edd5bae-91e7-4723-9f6b-21e942b623ce"
        },
        "ext": {
            "appnexus": {
                "seller_member_id": 958,
                "publisher_integration": {
                    "is_header": 0
                }
            },
            "schain": {
                "complete": 1,
                "nodes": [{
                    "asi": "appnexus.com",
                    "sid": "958",
                    "rid": "0edd5eab-91e7-4723-9f6b-21e912b623ce",
                    "hp": 1
                }],
                "ver": "1.0"
            }
        }
    }
}
```
