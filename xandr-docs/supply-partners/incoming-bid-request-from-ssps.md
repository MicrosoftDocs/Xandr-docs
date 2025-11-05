---
title: Incoming Bid Request from SSPs
description: This article provides information on the incoming bid request from SSPs.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Incoming bid request from SSPs

> [!NOTE]
> This describes Xandr's integration with the [OpenRTB 2.4 protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).
>
> This Bid Request is sent by SSPs and contains information on which advertisers and creatives are allowed to win an auction. Xandr will produce a [Bid Response](./outgoing-bid-response-to-ssps.md) that contains a bid price and a creative to serve.

## Implementation

### Endpoints

You will receive one or more endpoints that you can use to `POST` bid requests. Contact your Xandr representative to receive your endpoints. Endpoints will generally look like the following:

```
https://seller-region.adnxs.com/openrtb2?member_id=YOUR_MEMBER_ID
```

- `member_id` is required; this is your member ID on the Xandr platform. This ID will be provided by Xandr during integration.
- You will receive one endpoint for each region in which you operate. Possible regions include: `us-east`, `us-west`, `emea`, and `apac`.

Any other query string value will be ignored.

### Bid request object

> [!NOTE]
> The `tmax` field is not supported. Speak with your Integrations Consultant to configure auction timeout limits. **Multi-format impressions** are not supported. The format's precedence if we receive multi-format impression is as following:
>
> - video
> - audio
> - banner
> - native

Xandr supports the following fields in the top-level bid request object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) Used to pass back the seller's auction ID in the bid response. |
| `imp` | array of objects | (Required) The impressions offered in this bid request. See [Impression Object](#impression-object) below. |
| `site` | object | Specifies information about the website or subset of inventory (placement group) for the impressions. Applicable for website impressions. See [Site Object](#site-object) below. |
| `app` | object | Specifies information about the app for the impressions. Applicable for app impressions. See [App Object](#app-object) below. |
| `device` | object | Specifies information about the user's device to which these impressions will be delivered. See [Device Object](#device-object) below. |
| `user` | object | Specifies information about the person to whom the impressions will be delivered. See [User Object](#user-object) below. |
| `test` | integer | Indicates that this auction is in test mode and is not billable. If not present, default is used.<br>`0`: live mode; billable (default)<br>`1`: test mode; not billable |
| `wseat` | array of strings | Specifies an array representing a allowlist of buyer seats allowed to bid on this impression. If omitted, there are no seat restrictions for this impression. |
| `cur` | array of strings | Specifies an array of allowed currencies for bids on this impression. USD is assumed by default.<br><br>**Note**: By default, this field is NOT supported. Speak with your Integrations Consultant if you would like to be enabled for bids non-USD currencies. |
| `bcat` | array of strings | Specifies a list of blocked content categories. Can include both IAB categories (listed in section 5.1 of the specification) and Xandr category ID values. Xandr categories are in this format `APN-ID` where ID is the Xandr category ID; for example, `APN-13`. |
| `badv` | array of strings | Specifies a list of blocked top-level advertiser domains that correspond to brand URLs in the Xandr system. For example, `["company1.com", "company2.com"]`. For more information, see the [Brand Service](../bidders/brand-service.md). |
| `regs` | object | Specifies information about an industry, legal, or governmental regulation in force for this request. See [Regs Object below](#regs-object). |
| `ext` | object | Used for identifying Xandr-specific extensions to the OpenRTB bid request. See [Bid Request Extension Object](#bid-request-extension-object) below. |

### Bid request extension object

Xandr supports the follow objects in the `ext` object to support Xandr-specific extensions as well as supply-chain signals:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the Xandr-specific extensions to the OpenRTB bid request. |
| `schain` | object | Specifies the SupplyChain fields included in the OpenRTB bid request for supply path transparency. See [Schain Object](#schain-object) below. |

### Xandr object

Xandr supports the following fields in the `appnexus` extension object:

| Field | Type | Description |
|:---|:---|:---|
| `anid` | integer | Specifies the Xandr User ID. If a value is set here, it overrides the `buyeruid` in the [User Object](#user-object). |
| `markup_delivery` | enum | Specifies how ad markup will be received. This applies only to banner, video, and audio objects.<br>`0: ADM`: markup will be delivered in the `adm` field of the bid response (default)<br>`1: nurl`: markup will be delivered in the winning bid notification |

### Schain object

Xandr supports the following fields in the `schain` (Supply Chain) object:

| Field | Type | Description |
|:---|:---|:---|
| `ver` | string | Version of the supply chain specification in use, in the format of `“major.minor”`. Currently using version 1.0 of the spec. |
| `complete` | enum | Flag indicating whether the chain contains all nodes involved in the transaction leading back to the owner of the site, app or other medium of the inventory, where `0` = no, `1` = yes. |
| `nodes` | object | Array of `SupplyChainNode` objects in the order of the chain. In a complete supply chain, the first node represents the initial advertising system and seller ID involved in the transaction, i.e. the owner of the site, app, or other medium. In an incomplete supply chain, it represents the first known node. The last node represents the entity sending this bid request, which will be the Xandr node. Xandr supports the following fields in the nodes object. <br><br> **Note**: In order for a node to be considered complete, the following fields must be included in the node object.<br><br>- **asi** (mandatory string): The canonical domain name of the SSP, Exchange, Header Wrapper, etc system that bidders connect to. This should be the same value as used to identify sellers in an ads.txt file if one exists.<br>- **sid** (mandatory string): The identifier associated with the seller or reseller account within the advertising system.<br> - **rid** (optional string): The OpenRTB RequestId of the request as issued by the seller.<br>- **hp** (mandatory integer): Indicates whether this node will be involved in the flow of payment for the inventory. For version 1.0 of SupplyChain, this property should always be `1`. |

### Impression object

Xandr supports the following fields in the `imp` object, which describe the impression being auctioned. A single bid request may contain an array with multiple `imp` objects.

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) Specifies a unique identifier for this impression within the context of the bid request. |
| `banner` | object | Required if this impression is offered as a banner ad. See [Banner Object](#banner-object) below. |
| `video` | object | Required if this impression is offered as a video ad. See [Video Object](#video-object) below. |
| `audio` | object | Required if this impression is offered as an audio ad. See [Audio Object](#audio-object) below. |
| `native` | object | Required if this impression is offered as a native ad. See [Native Object](#native-object) below. |
| `displaymanagerver` | string | Specifies the version of ad mediation partner, SDK technology, or player responsible for rendering the ad (typically video or mobile). |
| `instl` | integer | Indicates whether the impression is interstitial or full screen.<br>`0`: the impression is not interstitial or full screen (default)<br>`1`: the impression is interstitial or full screen |
| `tagid` | string | Specifies an identifier for the specific ad placement or ad tag that was used to initiate the auction. If set, this is the Xandr placement code. Omitted when sending to buyers if seller visibility settings prohibit sharing. |
| `secure` | integer | Indicates whether the impression requires secure HTTPS URL creative assets and markup. If omitted, the secure state is unknown but non-secure HTTP support can be assumed.<br>`0`: the impression is not secure<br>`1`: the impression is secure |
| `bidfloor` | float | Minimum bid for this impression expressed in CPM.<br><br>**Note**: The `bidfloor` field should be the publisher's net CPM floor price on incoming ad requests. This floor price must be greater than the existing hard floor, set on the platform, in order to override it for the given auction. |
| `bidfloorcur` | string | Specifies the currency for this bid using ISO-4217 alphabetic codes. Defaults to `USD` if not specified. |
| `pmp` | object | Specifies information about a private marketplace deal that is in effect for this impression. See [Private Marketplace Object](#private-marketplace-object) below.|
| `ext` | object | Used for identifying Xandr-specific extensions to the impression object. See [Impression Extension Object](#impression-extension-object) below.|

### Impression extension object

Xandr supports a single object in the `impression` object's `ext` object to support Xandr-specific extensions:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the Xandr-specific extensions to the impression object. |

### Skadn object
Xandr supports the following field in the appnexus extension object:

| Field | Type | Description |
|:---|:---|:---|
| `skadn` | object array | Array representing the details for Apple’s SKAdNetwork |

### Impression extension appnexus skadn object
| Field | Type | Description |
|:---|:---|:---|
| `versions` | array of strings | Array of strings containing the supported skadnetwork versions. Always "2.0" or higher. Dependent on both the OS version and the SDK version. |
| `sourceapp` | string | ID of publisher app in Apple’s App Store. Should match app.bundle in OpenRTB 2.x and app.storeid in AdCOM 1.x. |
| `skadnetids` | array of strings | A subset of SKAdNetworkItem entries in the publisher app’s Info.plist, expressed as lowercase strings, that are relevant to the bid request. Recommended that this list not exceed 10 |


### Xandr object

Xandr supports the following field in the `appnexus` extension object:

| Field | Type | Description |
|:---|:---|:---|
| `predicted_view_rate` | double | Specifies the probability that the impression will be viewable by the user, based on historical data. |

### Banner object

For banner impressions, Xandr supports the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `w` | integer | (Recommended) Specifies the exact width of the banner in pixels. Must be set if the placement object in Xandr does not have a width set. |
| `h` | integer | (Recommended) Specifies the exact height of the banner in pixels. Must be set if the placement object in Xandr does not have a height set. |
| `btype` | array of integers | Specifies the banner creative types to block. Refer to section 5.2 of the IAB specification for a list of types. |
| `battr` | array of integers | Specifies the banner creative attributes to block. Refer to section 5.3 of the IAB specification for a list of attributes. |
| `pos` | integer | Specifies the video ad position on screen. <br> - `0`: Unknown (default).<br> - `1`: Above The Fold.<br> - `2`: Locked (i.e., fixed postion) <br> - `3`: Below The Fold <br> - `4`: Header <br> - `5`: Footer <br> - `6`: Sidebar <br> - `7`: Fullscreen |
| `api` | array of integers | Specifies the supported API frameworks for this impression. Parsed, but not used. If an API is not explicitly listed, vpaid support is deduced from mime types sent:  VPAID 1 and 2 would be allowed for javascript and flash mimes. Refer to section 5.6 of the IAB specification for a list of API frameworks. |
| `format` | object array | Array of format objects representing the banner sizes permitted. If none are specified, then use of the `h` and `w` attributes is highly recommended. |

### Format object

> [!NOTE]
> The `banner.w` and `banner.h` fields are still required when using the `format` object, which should be used to specify additional sizes.

Xandr supports the following field in the `format` object of the `banner` object:

| Field | Type | Description |
|:---|:---|:---|
| `w` | integer | Specifies the width of the creative, in pixels.|
| `h` | integer | Specifies the height of the creative, in pixels.|

### Video object

For video impressions, Xandr supports the following fields:

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | (Required) Specifies the video content MIME types supported; for example, `video/x-ms-wmv` and `video/x-flv`. If not specified, any MIME type is allowed.<br><br>**Note**: `application/x-shockwave-flash` and `application/javascript` are VPAID formats. You should select these MIME types only if your placement supports VPAID. |
| `minduration` | integer | (Recommended) Specifies the minimum video ad duration, in seconds. |
| `maxduration` | integer | (Recommended) Specifies the maximum video ad duration, in seconds. |
| `w` | integer | (Recommended) Specifies the width of the video player, in pixels. |
| `h` | integer | (Recommended) Specifies the height of the video player, in pixels. |
| `startdelay` | integer | (Recommended) Specifies the start delay of the video:<br>`> 0`: For values greater than zero, the delay before video start, in seconds.<br>`0`: Pre-roll<br>`-1`: Generic mid-roll<br>`-2`: Generic post-roll |
| `battr` | array of integers | Specifies the video creative attributes to block. Refer to section 5.3 of the IAB specification for a list of attributes. |
| `minbitrate` | integer | Specifies the minimum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. |
| `maxbitrate` | integer | Specifies the maximum bit rate, in kilobytes per second. If specified, only return creatives having at least one media file within the appropriate bit range. |
| `playbackmethod` | array of integers | Specifies the allowed playback methods. If not specified, all are assumed to be allowed. Currently supported values are:<br>`1`: Autoplay, sound on<br>`2`: Autoplay, sound off<br>`3`: Click to play<br>`4`: Mouse over to play |
| `pos` | integer | Specifies the video ad position on screen. <br> - `0`: Unknown (default).<br> - `1`: Above The Fold.<br> - `2`: Locked (i.e., fixed postion) <br> - `3`: Below The Fold <br> - `4`: Header <br> - `5`: Footer <br> - `6`: Sidebar <br> - `7`: Fullscreen |
| `companionad` | array of objects | Specifies an array of banner objects if companion ads are available. See [Banner Object](#banner-object) above. |
| `api` | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>`1`: VPAID 1.0<br>`2`: VPAID 2.0<br>`3`: MRAID-1<br>`4`: ORMMA<br>`5`: MRAID-2<br>`6`: MRAID-3<br>`7`: OMID-1 |
| `companiontype` | array of integers | Specifies the VAST companion ad types. Recommended if one or more companionad objects are included. Currently supported values are:<br>`1`: Static resource<br>`2`: HTML resource<br>`3`: iframe resource |
| `protocols` | array of integers | Array of supported video protocols of the creative types that are eligible. Following are the currently supported values:<br>`1`: VAST 1.0<br>`2`: VAST 2.0<br>`3`: VAST 3.0<br>`4`: VAST 1.0 Wrap    per<br>`5`: VAST 2.0 Wrapper<br>`6`: VAST 3.0 Wrapper<br>`7`: VAST 4.0<br>`8`: DAAST 1.0<br><br>**Warning**: As Xandr does not verify DAAST compliance in creatives, requests that exclusively support DAAST values in `protocols` will not result in any bids. |
| `ext` | object | Used for identifying Xandr-specific extensions to the video object. See [Video Extension Object](#video-extension-object) below. |

### Video extension object

Xandr supports a single object in the `video` object's `ext` object to support Xandr-specific extensions:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the Xandr-specific extensions to the video object. |

### Xandr object

Xandr supports the following field in the `appnexus` extension object:

| Field | Type | Description |
|:---|:---|:---|
| `context` | integer | Specifies the video context:<br>`0`: Unknown<br>`1`: Pre-roll<br>`2`: Mid-roll<br>`3`: Post-roll<br>`4`: Outstream |

### Audio object

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | (Required) Specifies the audio content MIME types supported; for example, `audio/vnd.wav`, `audio/mpeg`, `audio/mp4`, `audio/ogg`, or `audio/mp2`. |
| `minduration` | integer | (Recommended) Specifies the minimum audio ad duration, in seconds. |
| `maxduration` | integer | (Recommended) Specifies the maximum audio ad duration, in seconds. |
| `startdelay` | integer | (Recommended) Specifies the start delay of the audio ad:<br>`> 0`: For values greater than zero, the delay before audio start, in seconds.<br>`0`: Pre-roll<br>`-1`: Generic mid-roll (delay unknown)<br>`-2`: Generic post-roll |
| `battr` | array of integers | Specifies the audio creative attributes to block. Xandr supports:<br>`11`: Surveys<br>`16`: Ad Provides Skip Button |
| `minbitrate` | integer | The minimum bit rate, in kilobytes per second. |
| `maxbitrate` | integer | The maximum bit rate, in kilobytes per second. |
| `companionad` | array of objects | Specifies an array of banner objects if companion ads are available. See [Banner Object](#banner-object) above. |
| `api` | array of integers | Specifies the supported API frameworks for this impression. If an API is not explicitly listed, it is assumed not to be supported. Currently supported values are:<br>`1`: VPAID 1.0<br>`2`: VPAID 2.0<br>`3`: MRAID-1<br>`4`: ORMMA<br>5: MRAID-2 |
| `companiontype` | array of integers | Specifies the DAAST companion ad types. Recommended if one or more companion ad banner objects are included. Currently supported values are:<br>`1`: Static resource<br>`2`: HTML resource<br>`3`: iframe resource |
| `protocols` | array of integers | Array of supported audio protocols. Currently supported values are:<br>`1`: VAST 1.0<br>`2`: VAST 2.0<br>`3`: VAST 3.0<br>`4`: VAST 1.0 Wrapper<br>`5`: VAST 2.0 Wrapper<br>`6`: VAST 3.0 Wrapper<br>`7`: VAST 4.0<br>`8`: DAAST 1.0<br><br>**Warning**: As Xandr does not verify DAAST compliance in creatives, requests that exclusively support DAAST values in protocols will not result in any bids. |

### Native object

For native impressions, Xandr supports the following fields:

#### `request`

**Type**: String
<br>**Description**: The rendered creative markup to be delivered; native creatives can be returned in this field as a JSON-encoded string.

**Native 1.0 Example**:

```
"native": {
        "request": "{\"native\":{\"ver\":\"1.0\",\"assets\":[{\"id\":3}}]}"
}
```

**Native 1.1 Example**:

> [!NOTE]
> The main difference of the two versions is the removal of "native" in the request object.

```
"native": {
        "request": "{\"ver\":\"1.1\",\"assets\":[{\"id\":3}}]}"
}
```

**Native 1.2 Example**:

```
"native": {
        "request": "{\"ver\":\"1.2\",\"assets\":[{\"id\":3}}]}"
}
```

#### `ver`

**Type**: String
<br> **Description**: Version of the Native Markup version in use.
Xandr currently supports the following native versions:

- `1.0`
- `1.1`
- `1.2`

> [!NOTE]
> - Required if using `1.1` or `1.2`. If no version is submitted, then we will default to `1.0`.
>
> - For more information on different OpenRTB Native Ad specifications, go to [OpenRTB Dynamic Native Ads](https://iabtechlab.com/standards/openrtb-native/) and refer to specs for v1.0, v1.1 and v1.2.
>
> - Follow the above specifications and pass the necessary **required** fields in the mentioned objects such as asset ID (`id`) in the [Asset Object](#asset-object) described below.

### Request object

Xandr supports the following fields in the `request` object in the `native` object:

| Field | Type | Description |
|:---|:---|:---|
| `ver` | string | Version of the Native Markup version in use.<br>Xandr currently supports the following native version:<br>`1.0`<br>`1.1`<br>`1.2`<br><br>**Note**: If no version is submitted, then we will default to `1.0`. |
| `plcmttype` | integer | The design/format/layout of the ad unit being offered. Xandr supports the following:<br>`0`: none<br>`1`: In the feed of content<br>`4`: Recommendation widget<br><br>**Note**: This field is only for Native version `1.1` and `1.2`. |
| `privacy` | boolean | Flag to indicate if the seller supports a buyer-specific privacy notice.<br>`0 or absent`: The native ad doesn't support custom privacy links.<br>`1`: The native ad supports buyer-specific privacy notice.<br><br>**Note**: If privacy is `0 or absent`, then Xandr will not return a privacy link regardless of whether the buyer sent it. If privacy is 1, then Xandr will only send the privacy link if the buyer provides it. |
| `assets` | array of objects | An array of Asset Objects. |

### Asset object

Xandr supports the following fields to define one or more `asset` objects in the `native` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Specifies a unique identifier for the asset in this bid request. Â Typically, the first asset in the array is `1` and subsequent assets increment from there. |
| `required` | integer | Specifies if the asset is required:<br>`0`: Asset is optional<br>`1`: Asset is required |
| `title` | object | Specifies information about the title of the asset. See [Title Object](#title-object) below. |
| `img` | object | Specifies information about the image for the asset. See [Image Object](#image-object) below. |
| `data` | object | Specifies information about data for the asset. See [Assets Data Object](#assets-data-object) below. |
| `video` | object | Specifies information about the video asset. See [Video Object](#video-object-assetsobject) below. |

### Title object

Xandr supports the following fields in the `title` object in the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `len` | integer | Maximum length of the text in the title.|

### Image object

Xandr supports the following fields in the `img` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `type` | integer | Specifies the type ID of the image element requested by the publisher. Supported values are:<br>`1`: Icon image for use on smaller screen sizes (`icon_img_url`)<br>`3`: Large image preview of the ad for use on larger screen sizes (`main_media`) |
| `w` | integer | Specifies the exact width of the image, in pixels. Either `w` or `wmin` must be included. |
| `wmin` | integer | Specifies the minimum requested width of the image, in pixels. If included, this value should be used for any rescaling of images by the client. Either `w` or `wmin` must be included. If both are included, we will first try to find a creative that matches the exact width. If no creative matches the exact width, we will then use the minimum width. |
| `h` | integer | Specifies the height of the image, in pixels. Either `h` or `hmin` must be included. |
| `hmin` | integer | Specifies the minimum requested height of the image, in pixels. If included, this value should be used for any rescaling of images by the client. Either `h` or `hmin` must be included. If both are included, we will first try to find a creative that matches the exact height. If no creative matches the exact height, we will then use the minimum height. |
| `mimes` | array of strings | Specifies the image content MIME types supported. Should be empty, as all image types are supported.|

Image aspect ratios are determined by the minimum width and height specified (e.g., wmin:600 hmin:600 implies a 1:1 ratio). For common aspect ratios like 1.91:1 (landscape), users should specify sizes like 1200x627. Aspect ratio is not a separate attribute—it's implied by the dimensions. Larger images are generally preferred, as they scale down better than scaling up.
 
The requested aspect ratio **influences image demand**. A wmin:600 hmin:600 request yields images that are 1:1 or can be resized to 1:1, with both sides at least 600 pixels. A wmin:1200 hmin:627 request yields images that are 1.91:1 or resizable to that ratio, with a minimum height of 627 pixels. This applies similarly for other aspect ratios.

### Assets data object

Xandr supports the following fields in the `data` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `type` | integer | Specifies the type ID of the element supported by the publisher. The publisher can display this information in an appropriate format. Supported values are:<br>`1: sponsored` - "Sponsored By" message, where the the response contains the brand name of the sponsor<br>`2: desc` - Descriptive text associated with the product or service being advertised<br>`3: rating` - Rating of the product being offered to the user. For example, an app's rating in an app store from 0 to 5.<br>`12: ctatext` - Descriptive text for a "call to action" button for the destination URL |
| `len` | integer | Maximum length of the text in the element's response. |

### Video object (assets object)

Xandr supports the following fields in the `video` object of the `assets` object:

| Field | Type | Description |
|:---|:---|:---|
| `mimes` | array of strings | Content MIME types supported. If mimes are not specified in the bid request, then we will default to `“video/mp4”` for regular video and `“video/x-flv”` for mobile. |
| `minduration` | integer | Minimum video ad duration in seconds. |
| `maxduration` | integer | Maximum video ad duration in seconds. |
| `protocols` | array of integers | An array of video protocols the publisher can accept in the bid response.<br>Currently supported values are:<br>`1`: VAST 1.0<br>`2`: VAST 2.0<br>`3`: VAST 3.0<br>`4`: VAST 1.0 Wrapper<br>`5`: VAST 2.0 Wrapper<br>`6`: VAST 3.0 Wrapper<br>`7`: VAST 4.0<br>`8`: DAAST 1.0 |

### Private marketplace object

Xandr supports the following fields in the `pmp` object of the `imp` object to support private marketplaces (deals) between buyers and sellers that may apply to this impression:

| Field | Type | Description |
|:---|:---|:---|
| `private_auction` | integer | Indicates the auction eligibility for seats named in the deals object.<br>`0`: All bids are accepted<br>`1`: Only bids for specified deals are accepted |
| `deals` | array of objects | Specifies information about the deals for this bid. See [Deal Object](#deal-object) below. |

### Deal object

Xandr supports the following fields in the `deal` object of the `pmp` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Required) Specifies a unique identifier for the deal.<br><br>**Note**: The `id` must match the `deal.code` you registered using the Deal Service. See [Selling Deals](./selling-deals-on-xandr.md) for more details. The inclusion of a deal ID on the bid request implies that the buyer permitted to buy that deal is permitted to bid in the auction, even if that buyer is not included the bidrequest.wseat field. |
| `bidfloor` | float | Specifies the minimum bid price for the deal, in CPM using the default currency (`USD`). This field is only respected if the Deal object has configured with a `floor_price` and `use_deal_floor` is true. If so, this overrides `imp.bidfloor` for deal bids. |
| `bidfloorcur` | string | Specifies the currency for this bid using ISO-4217 alphabetic codes. Defaults to `USD` if not specified. |

### Site object

> [!NOTE]
> The `bid` object must not include both a `site` object and an `app` object. Only one is allowed, not both.

Xandr supports the following fields in the `site` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | (Recommended) The seller's site ID. If set, this should equal the Xandr placement code. |
| `domain` | string | Specifies the domain of the site (for example, [publishersite.com](https://publishersite.com/) ) where the impression will be shown. Set as the referrer domain on the impression if available, or extracted from the `page` field. |
| `cat` | array of strings | Specifies a list of IAB content categories (listed in section 5.1 of the specification) and Xandr category ID values. Xandr categories are in this format `APN-ID` where ID is the Xandr category ID; for example, `APN-13`. |
| `page` | string | Specifies the full URL of the page where the impression will be shown (for example, page.publishersite.com/path/to/page). This should be the referrer URL and is preferred over the `domain` field. |
| `publisher` | object | Specifies information about the publisher. See [Publisher Object](#publisher-object) below. |
| `keywords` | string | Comma separated list of keywords about the site. Keywords are global to the request and apply to all imp objects.<br>Example:<br>`"keywords":"car_make=ford,my_other_value"`<br><br>In this example, we look for<br>- a querystring mapping segment for `car_make` and set the value to ford (based on the segment's settings).<br>- a querystring key/value segment for `car_make=ford`.<br>- a querystring mapping segment with `my_other_value` as the key and set no value.<br><br>**Note**: The keywords feature is not available by default. Contact your Xandr representative to enable this feature. |
| `content` | object | Details about the Content within the site. See [Content Object](#content-object) below. |

### App object

> [!NOTE]
> Only one of `site` and `app` objects are allowed in an `imp` object.

Xandr supports the following fields in the `app` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the seller's app ID, used to look up an Xandr tinytag ID by tinytag code. |
| `bundle` | string | Specifies the application bundle or package name (e.g., `com.foo.mygame`). This is intended to be a unique ID across multiple exchanges. |
| `domain` | string | Specifies the domain of the app (for example, `mygame.publishersite.com`) where the impression will be shown. Set as the referrer domain on the impression if available. |
| `cat` | array of strings | Specifies a list of IAB content categories (listed in section 5.1 of the specification) and Xandr category ID values. Xandr categories are in this format `APN-ID` where ID is the Xandr category ID; for example, `APN-13`. |
| `publisher` | object | Specifies information about the publisher. See [Publisher Object](#publisher-object) below. |
| `name` | string | The full name of the app (i.e. Angry Birds). (This value may be aliased at the publisher's request.) |
| `keywords` | string | Comma separated list of keywords about the app. Keywords are global to the request and apply to all imp objects.<br>Example:<br>`"keywords":"car_make=ford,my_other_value"`<br><br>In this example, we look for<br> - a querystring mapping segment for `car_make` and set the value to ford (based on the segment's settings).<br>- a querystring key/value segment for `car_make=ford`.<br>- a querystring mapping segment with `my_other_value` as the key and set no value.<br><br> **Note**: The keywords feature is not available by default. Contact your Xandr representative to enable this feature. |
| `content` | object | Details about the Content within the site. See [Content Object](#content-object) below. |

### Publisher object

Xandr supports the following field in the `publisher` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | Specifies the seller's publisher ID. If set, this should equal the Xandr publisher code. Used to set a default placement ID in the auction if `tagid`, `site.id`, or `app.id` are not provided. |

### Content object

Xandr supports the following fields in the Content object:

| Field | Type | Description |
|:---|:---|:---|
| `genre` | string | Genre that best describes the content (e.g., rock, pop, etc). |
| `id` | string | ID uniquely identifying the content. |
| `language` | string | Content language using ISO-639-1-alpha-2. |
| `ext` | object | Placeholder for exchange-specific extensions to OpenRTB. |
| `episode` | integer | Episode number. |
| `title` | string | Content title.<br><br>Video Examples: "Search Committee" (television), "A New Hope" (movie), or "Endgame" (made for web).<br><br>Non-Video Example: "Why an Antarctic Glacier is Melting So Quickly" (Time magazine article). |
| `series` | string | Video Examples: "The Office" (television), "Star Wars" (movie), or "Arby 'N' The Chief" (made for web).<br><br>Non-Video Example: "Ecocentric" (Time Magazine blog). |
| `season` | string | Content season (e.g., "Season 3"). |
| `artist` | string | Artist credited with the content. |
| `album` | string | Album to which the content belongs; typically for audio. |
| `isrc` | string | International Standard Recording Code conforming to ISO-3901. |
| `producer`  | object | Details about the content `Producer`. Refer to section 3.2.12 in the IAB specification. |
| `url`  | string | URL of the content, for buy-side contextualization or review. |
| `cat`  | string array | Array of IAB content categories that describe the content producer. Refer to list 5.1 in the IAB specification. |
| `prodq`  | integer | Production quality. Refer to List 5.11 in the IAB specification. |
| `videoquality` | integer; DEPRECATED | Deprecated in favor of prodq. Video quality. Refer to List 5.11 in the IAB specification. |
| `context` | integer | Type of content (game, video, text, etc.). Refer to List 5.16  in the IAB specification. |
| `contentrating` | string | Content rating (e.g., MPAA). |
| `userrating`  | string  | User rating of the content (e.g., number of stars, likes, etc.). |
| `qagmediarating`  | integer | Media rating per IQG guidelines. Refer to List 5.17 in the IAB specification. |
| `keywords`  | string  | Comma separated list of keywords describing the content. |
| `livestream`  | integer | `0` = not live <br> `1` = content is live (e.g., stream, live blog). |
| `sourcerelationship`  | integer | `0` = indirect <br> `1` = direct. |
| `len` | integer | Length of content in seconds; appropriate for video or audio. |
| `data`  | object array  | Additional content data. Each Data object represents a different data source. Refer to Section 3.2.16 in the IAB specification. |

### Content extension object

Xandr supports the following fields in the `ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `network` | String | The top-level parent company or, where relevant, a sub-brand which owns multiple TV-like channels, d2c content brands, or digital properties on which the content is being viewed |
| `channel` | String | Name of channel the content is airing on |
| `appnexus` | object | Specifies the Xandr-specific extensions to the OpenRTB bid request. |

Xandr supports the following fields in the appnexus extension object of the content object

| Field | Type | Description |
|:---|:---|:---|
| `airtime` | String | Original airtime, for time-shifted content |
| `program_type` | String | Type of program (e.g. movie, event, episode, etc.) |

### Device object

Xandr supports the following fields in the `device` object. Note that the device IDs in this object should override
any device IDs in the [Bid Request Extension Object](#bid-request-extension-object).

| Field | Type | Description |
|:---|:---|:---|
| `ua` | string | (Recommended) Specifies the user agent string from the browser. User agent often identifies such information as the application, operating system, and software vendor acting on behalf of the user, e.g., `"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4"`. |
| `geo` | object | Specifies the location of the device, as derived from the device's location services (such as cell tower triangulation or GPS) or IP address. See [Geo Object](#geo-object) for details. |
| `dnt` | integer | Specifies the Do Not Track setting:<br>`0`: Do Not Track is set to false in browser (tracking is allowed)<br>`1`: Do Not Track is set to true in browser (user has opted out of tracking) |
| `ip` | string | Specifies the IPv4 address closest to the device. Omitted when sent to buyers if seller visibility settings prohibit sharing. |
| `ipv6` | string | Specifies the IPv6 address closest to the device. Used only for geolocation for buyer targeting. |
| `devicetype` | integer | Specifies the type of device, using IAB values:<br>`1`: Mobile/Tablet<br>`2`: Personal Computer<br>`3`: Connected TV<br>`4`: Phone<br>`5`: Tablet<br>`6`: Connected Device<br>`7`: Set Top Box<br>Only used if not supported via the `ua` field |
| `make` | string | Specifies the make of the device. Only used if not supported via the `ua` field. |
| `model` | string | Specifies the model of the device. Only used if not supported via the `ua` field. |
| `os` | string | This is the code field that you obtain from operating system code. |
| `carrier` | string | Specifies carrier for the device. Only used if not supported via the `ua` field. |
| `language` | string | Specifies the browser language; use ISO 639-1 or ISO 3166 alpha-2. |
| `device.ext.ifa_type` | string | Identifies the source of the IFA, whether it is device-generated (used across apps), publisher-provided, or temporary/session-based. Supports a broader range of devices, including CTV platforms such as Roku and Amazon Fire TV. Must be passed inside `device.ext` for compatibility with OpenRTB. An incorrect or missing value may impact bid eligibility, especially for CTV campaigns. (e.g., `dpid`, `ppid`, `sspid`, `sessionid`, `idfa`, `aaid`, `rida`, `afai`, `tifa`, `vida`, `lgudid`) |
| `ifa` | string | The "identifier for advertising" is an unhashed device ID sanctioned for advertiser use. This will be the IDFA on iOS or AAID on Android.<br>Example: `"ifa": "AA000DFE74168477C70D291f574D344790E0BB12"`. |
| `didsha1` | string | Specifies the SHA1-encrypted unique identifier for the mobile device. |
| `didmd5` | string | Specifies the MD5-encrypted unique identifier for the mobile device. |
| `dpidsha1` | string | Specifies the SHA1-encrypted, platform-specific (e.g., `ANDROID_ID` or `UDID` for iOS) unique identifier for the mobile device. |
| `dpidmd5` | string | Specifies the MD5-encrypted, platform-specific (e.g., `ANDROID_ID` or `UDID` for iOS) unique identifier for the mobile device. |
| `lmt` | integer | "Limit Ad Tracking" signal commercially endorsed (e.g., iOS, Android), where `0`=tracking is unrestricted, `1`=tracking must be limited per commercial guidelines. |

### User Object

Xandr supports the following fields in the `user` object:

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | The seller's unique ID for this user.  |
| `buyeruid` | string | The Xandr unique ID of this user. If set, this value will overwrite the `customdata` value. |
| `yob` | integer | Specifies the year of birth as a 4-digit integer. Omitted when sent to buyers if unknown or value set to `0`. |
| `gender` | string | Specifies the gender. Set to `null` if unknown. Omitted when sent to buyers if unknown.<br>`M`: male<br>`F`: female<br>`O`: other |
| `customdata` | string | A properly encoded string that can contain an Xandr user ID. Will be ignored if `buyeruid` is set. |
| `keywords` | string | Comma separated list of keywords about the user. Keywords are global to the request and apply to all imp objects.<br>Example:<br>`"keywords":"car_make=ford,my_other_value"`<br><br>In this example, we look for<br>- a querystring mapping segment for `car_make` and set the value to ford (based on the segment's settings).<br>- a querystring key/value segment for `car_make=ford`.<br>- a querystring mapping segment with `my_other_value` as the key and set no value.<br><br>**Note**: The keywords feature is not available by default. Contact your Xandr representative to enable this feature. |
| `geo` | object | Location of the user’s home base defined by a Geo object. This is not necessarily their current location.<br><br>**Note**: By default, this field is not supported. Contact support or your account representative for more information. |
| `ext` | object | Used for identifying Xandr-specific extensions to OpenRTB for the `user` object. |

### eid object

| Field | Type | Description |
|:---|:---|:---|
| `source` | string | Source of technology provider responsible for the set of included IDs.  |
| `uids` | object array; | Array of extended ID UID objects from the given source. |
| `ext` | object | Placeholder for vendor specific extensions to this object. |

### Geo object

Xandr supports the following fields in the `geo` object:

| Field | Type | Description |
|:---|:---:|:---|
| `lat` | float | Specifies the latitude of the device, as derived from the device's location services (such as cell tower triangulation or GPS) or IP address. This can range from `-90` to `90`. South is negative. |
| `lon` | float | Specifies the longitude of the device, as derived from the device's location services (such as cell tower triangulation or GPS) or IP address. This can range from `-180` to `180`. West is negative. |
| `country` | string | Country code using ISO-3166-1-alpha-3.<br><br>**Note**: By default, this field is not supported. Your account can be enabled to add support for this field, in which case country + zip will be used to determine location information. Contact support or your account representative for more information. |
| `zip` | string | Zip or postal code.<br><br>**Note**: By default, this field is not supported. Your account can be enabled to add support for this field, in which case country + zip will be used to determine location information. Contact support or your account representative for more information.|

### User extension object

Xandr supports the following field in the `user.ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `consent` | string | Optional. Contains the data structure developed by the General Data Protection Regulation (GDPR) Consent Working Group under the auspices of [IAB Europe](https://iabeurope.eu/).<br><br>**Note**: The field is not enforced until May 25, 2018.|
| `eids` | object array | This object can contain one or more UIDs from a single source or a technology provider. Extended Identifiers support in OpenRTB allows buyers to use audience data in real time bidding. For more information, see [eid Object](#eid-object).|

### Regs object

Xandr supports the following fields in the regs object:

| Field | Type | Description |
|:---|:---|:---|
| `coppa` | integer | Indicates if this request is subject to the United States Children's Online Privacy Protection Act (COPPA).<br>`0`: Not subject to COPPA. Treat as a normal auction.<br>`1`: Subject to COPPA. Limit what is allowed for targeting and logging as required. |
| `ext` | object | Used for identifying Xandr-specific extensions to OpenRTB for the reg object. |
| `gpp` |  | Indicates the actual IAB GPP consent string. It implies which vendors are permitted to process personal data and under which conditions.<br>Example:<br>```{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [5]} } }``` |
| `gpp_sid` |  | Optional: indicates which regulations or GPP logics are to be applied, or whether a user is located in a country (EEA country) with a framework that is part of the GPP.<br>Example: <br> `{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [5]} } }`|

### Regs extension object

Xandr supports the following field in the `regs.ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `gdpr` | integer | Optional. Indicates whether the request is subject to General Data Protection Regulation (GDPR) regulations. Possible values:<br>`0`: No, the request is not subject to GDPR regulations.<br>`1`: Yes, the request is subject to GDPR regulations.<br><br>No value indicates Unknown. |
| `us_privacy` | string | Optional. Indicates whether the request complies with the California Consumer Privacy Act (CCPA) regulations. This field complies with the [IAB US Privacy specification](https://github.com/InteractiveAdvertisingBureau). Refer to the IAB's string specifications for possible values; for example:<br>```{ "Regs": {    "ext":        {       "us_privacy": "1YNN"       }   } }```|
| `gpp` |  | Indicates the actual IAB GPP consent string. It implies which vendors are permitted to process personal data and under which conditions.<br>Example:<br>```{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [5]} } }``` |
| `gpp_sid` |  | Optional: indicates which regulations or GPP logics are to be applied, or whether a user is located in a country (EEA country) with a framework that is part of the GPP.<br>Example:<br>```{ "Regs": { "ext": { "gpp": "DBACNYA~CPXxRfAPXxRfAAfKABENB-CgAAAAAAAAAAYgAAAAAAAA~1YNN", "gpp_sid": [5]} } }``` |
| `dsa` |  |```{ dsarequired: 1, pubrender: 0, transparency: [ { domain: 'request.tomato.com', dsaparams: [ 1 ] },{ domain: 'request2.tomato.com', dsaparams: [ 1, 2, 3 ] }],datatopub: 1 }``` |

## Example bid requests

### Banner bid request

```
{
    "id": "3456789098765432",
    "imp": [{
        "banner": {
            "h": 200,
            "w": 750
        },
        "bidfloor": 0.0779016539,
        "bidfloorcur": "USD",
        "id": "a5974205-4a2d-43e1-b346-693b0dad1372",
        "pmp": {
            "deals": [{
                "bidfloor": 1.03868878,
                "bidfloorcur": "USD",
                "id": "123456789"
            }],
            "private_auction": 1
        }
    }, {
        "banner": {
            "h": 300,
            "w": 750
        },
        "bidfloor": 0.0779016539,
        "bidfloorcur": "USD",
        "id": "5a123e7a-e72e-4503-912e-03fdad931da4",
        "pmp": {
            "deals": [{
                "bidfloor": 1.03868878,
                "bidfloorcur": "USD",
                "id": "654321234"
                ]
            }],
            "private_auction": 1
        }
    }, {
        "banner": {
            "h": 60,
            "w": 468
        },
        "bidfloor": 0.0779016539,
        "bidfloorcur": "USD",
        "id": "912308dd-6643-4bfd-8ff6-4b14f8799dad",
        "pmp": {
            "deals": [{
                "bidfloor": 1.03868878,
                "bidfloorcur": "USD",
                "id": "432123456"
            }],
            "private_auction": 1
        }
    }, {
        "banner": {
            "h": 250,
            "w": 970
        },
        "bidfloor": 0.0779016539,
        "bidfloorcur": "USD",
        "id": "1123c57b-464e-4b6d-87ce-89f501dadfb9",
        "pmp": {
            "deals": [{
                "bidfloor": 1.03868878,
                "bidfloorcur": "USD",
                "id": "543234567"
            }],
            "private_auction": 1
        }
    }],
    "site": {
        "domain": "https://example.com",
        "id": "456789",
        "name": "example.com",
        "page": "https://example.com/example",
        "publisher": {
            "id": "123",
            "name": "mypublisher"
        }
    },
    "user": {
        "id": "6543212345654"
    },
    "bcat": [
        "IAB24",
        "IAB26"
    ],
    "cur": [
        "USD"
    ],
    "device": {
        "devicetype": 2,
        "ext": {
            "is_app": 0
        },
        "ip": "198.51.100.1",
        "language": "pl",
        "ua": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:41.0) Gecko/20100101 Firefox/41.0"
    }
}
```

### Video bid request

```
{
    "id": "951_1470171234556050-40",
    "imp": [{
        "bidfloor": 13.768,
        "bidfloorcur": "USD",
        "displaymanager": "DisplayManager",
        "displaymanagerver": "1.0",
        "id": "1",
        "pmp": {
            "deals": [{
                "bidfloor": 4.3506,
                "bidfloorcur": "USD",
                "id": "STI-VER-00004"
            }],
            "private_auction": 0
        },
        "secure": 0,
        "video": {
            "api": [
                1,
                2
            ],
            "ext": {
                "sticky_viewability_score": 10
            },
            "h": 250,
            "maxduration": 3600,
            "mimes": [
                "video/mp4",
                "video/x-flv",
                "application/x-shockwave-flash",
                "application/javascript"
            ],
            "minduration": 0,
            "playbackmethod": [
                1
            ],
            "protocol": 2,
            "protocols": [
                2,
                5
            ],
            "startdelay": 0,
            "w": 300
        }
    }],
    "badv": [
        "example.com",
        "example2.com"
    ],
    "cur": [
        "EUR",
        "JPY",
        "USD",
        "AUD",
        "GBP"
    ],
    "device": {
        "devicetype": 2,
        "ip": "198.51.100.10",
        "ipv6": "::ffff:198.51.100.10",
        "language": "en",
        "os": "windows",
        "ua": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36"
    },
    "site": {
        "cat": [
            "IAB1"
        ],
        "domain": "example.com",
        "id": "456789",
        "page": "https://www.example.com/example-page",
        "publisher": {
            "id": "123"
        }
    },
    "user": {
        "buyeruid": "87654332122234",
        "id": "5123dab34d2fe47f225b2fd8dad97ec"
    }
}
```

### Native 1.1 bid request

```
{
    "id": "333a8888abcd47e98cb69de19999egad",
    "imp": [{
        "id": "1",
        "native": {
            "request": "{\"ver\":\"1.1\",\"context\":1,\"contextsubtype\":10,\"plcmttype\":11,\"plcmtcnt\":1,\"assets\":[{\"id\":1,\"required\":1,\"video\":{\"minduration\":10,\"maxduration\":60,\"protocols\": [2],\"mimes\":[\"video/mp4\"]}},{\"id\":2,\"required\":0,\"title\":{\"len\":140}},{\"id\":3,\"required\":1,\"img\":{\"w\":428,\"h\":240,\"type\":3}}]}",
            "ver": "1.1"
        },
        "tagid": "PC1111IAG0.0000011ABC"
    }],
    "app": {
        "domain": "dashboard.example.com",
        "bundle": "bundle1.example.dashboard"
    },
    "device": {
        "ua": "XBoxSAS/1",
        "ip": "126.149.60.85",
        "language": "us"
    },
    "user": {
        "id": "1234567899B74ABCDEFB783E2BE0987653DF70D0"
    },
    "ext": {
        "appnexus": {
            "ext_inv_code": "100"
        }
    }
}
```

### Mobile bid request

```
{
    "id": "05FD4E3A-BFCB-4E5E-8D63-14DB77250C32",
    "imp": [
        {
            "id": "1",
            "tagid": "987654",
            "banner": {
                "w": 300,
                "h": 250,
                "pos": 3,
                "topframe": 1,
                "battr": [
                    12,
                    44
                ]
            }
        }
    ],
    "app": {
        "id": "2490165635",
        "name": "GO Keyboard - Emoji, Wallpaper",
        "bundle": "com.jb.gokeyboard",
        "domain": "https://play.google.com",
        "cat": [
            "IAB3"
        ],
        "publisher": {
            "id": "123456"
        }
    },
    "device": {
        "ip": "27.55.84.146",
        "lmt": 0,
        "ua": "Mozilla/5.0 (Linux; Android 4.4.2; Z520 Build/KOT49H) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/30.0.0.0 Mobile Safari/537.36",
        "carrier": "Truemove",
        "language": "th",
        "make": "Acer",
        "model": "Z520",
        "os": "Android",
        "osv": "4.4",
        "js": 1,
        "devicetype": 1,
        "ifa": "528b4158-67d6-475d-b29f-6d62c8adbbce"
    },
    "user": {
        "id": "389FB549-4D41-456D-AA3C-5AF980683652"
    },
    "bcat": [
        "IAB7-45",
        "IAB7-31",
        "IAB26",
        "IAB7-30",
        "IAB25",
        "IAB23",
        "IAB7-39"
    ]
}
```

### Outstream bid request

```
{
    "site": {
        "domain": "https://example.com",
        "page": "https://www.example.com/movies",
        "id": "ChTqkJcUbhNNTW4RPYdWYALE",
        "publisher": {
            "id": "654321"
        },
        "content": {
            "language": "en"
        },
        "cat": [
            "IAB1",
            "IAB24"
        ]
    },
    "id": "6fb5623c-f88e-462f-b679-a902db6deff4",
    "imp": [
        {
            "native": {
                "plcmtcnt": 1,
                "request": "{\"native\":{\"plcmtcnt\":1,\"assets\":[{\"id\":4,\"required\":0,\"img\":{\"hmin\":315,\"wmin\":600,\"type\":3}},{\"id\":3,\"required\":0,\"img\":{\"hmin\":48,\"wmin\":48,\"type\":2}},{\"id\":11,\"required\":0,\"data\":{\"len\":2000,\"type\":501}},{\"id\":12,\"required\":0,\"data\":{\"len\":2000,\"type\":502}},{\"id\":1,\"required\":1,\"title\":{\"len\":90}},{\"id\":2,\"required\":1,\"img\":{\"hmin\":0,\"wmin\":0,\"type\":1}},{\"id\":5,\"required\":1,\"data\":{\"len\":140,\"type\":1}},{\"id\":6,\"required\":1,\"data\":{\"len\":200,\"type\":2}}],\"adunit\":2,\"ver\":\"1.0\",\"layout\":3}}",
                "adunit": 2,
                "ver": "1.0",
                "layout": 3
            },
            "id": "1",
            "bidfloor": 1.01,
            "video": {
                "protocols": [
                    2,
                    3,
                    7
                ],
                "playbackmethod": [
                    2
                ],
                "minduration": 3,
                "ext": {
                    "appnexus": {
                        "context": 4
                    }
                },
                "maxduration": 300,
                "h": 250,
                "w": 300,
                "mimes": [
                    "video/mp4"
                ]
            },
            "secure": 0
        }
    ],
    "user": {
        "buyeruid": "2905333698551584116"
    },
    "device": {
        "connectiontype": 0,
        "devicetype": 4,
        "ip": "101.177.51.245",
        "model": "SM-G920I",
        "ua": "Mozilla/5.0 (Linux; Android 6.0.1; SM-G920I Build/MMB29K; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/57.0.2987.132 Mobile Safari/537.36 [FB_IAB/FB4A;FBAV/116.0.0.17.69;]",
        "os": "Android",
        "osv": "4",
        "language": "en",
        "make": "Samsung",
        "js": 1,
        "dnt": 0
    }
}
```
