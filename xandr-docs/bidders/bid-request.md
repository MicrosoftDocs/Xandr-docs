---
title: Bidders - Bid Request
description: In this article, learn about the different types of bid requests and their implementation with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Bid request

> [!IMPORTANT]
>
> - **Not Supported**: The AppNexus Bidding Protocol is no longer supported; this documentation is for legacy purposes only. We will deprecate this protocol on December 1, 2018.
> - If you're a new bidder integrating with AppNexus, please see the [OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

A Bid Request is sent to bidders whenever an ad call reaches the Impression Bus. It contains all the necessary information for a bidder to produce a bid price and a creative to serve.

The Bid Request includes information from sellers that specifies which advertisers and creatives are allowed to win an auction and run on a page. This information is stored into an ad approval profile, which bidders can use to make sure that their bids are accepted.

## Throttling bid requests

You may not wish to receive all bid requests that pass through the AppNexus platform. You can either throttle requests by some percentage, or filter requests by preset criteria such as geography.

## Multi-tag bid requests

We sometimes send "multi-tag bid requests" where one Bid Request may include multiple tag IDs with potentially different sizes, ad quality standards, reserve prices, etc. For now, these requests should be handled with individual responses for each tag as if they were independent requests. However, in the near future, these multi-tag requests will be the foundation for takeovers, full page buyouts, and many other premium inventory features.

Each individual tag in a multi-tag request has a unique auction ID.

## Implementation

### Request headers

| Field | Scope | Type | Description |
|---|---|---|---|
| `Connection` | all | string | Always set to "keep-alive" to ensure persistent TCP connections. |
| `Content-Length` | all | int | Length of the body of the HTTP request (which includes all fields described below). |
| `Host` | all | string | IP address to which the bid request has been sent. |
| `X-Debug` | some | int | If set to 1, the ad call included the debug=1 flag, and no ad will be served. |
| `X-DMA` | some | int | Code for the designated market area of the user based on IP address, if it can be determined. |
| `X-Exclusive` | some | int | Indicates whether or not the auction is exclusive by default. An exclusive auction is one in which only the placement owner can serve an ad. The exclusive default may be overridden by the owner during the owner phase of the auction. |
| `X-Segment` | some | string | A comma-separated list of segments that the user is in. Segments available include those owned by your members and those owned by 3rd party data providers (to whom AppNexus has granted your bidder access). |
| `X-Venue` | all | int | This header is not currently used. |

### Auction info

#### General data

| Field | Scope | Type | Description |
|---|---|---|---|
| `member_ad_profile_id` | some | int | The member-level ad approval profile ID that applies for the impression. |
| `timestamp` | all | timestamp | Time the request was sent. |
| `bidder_timeout_ms` | all | int | Number of milliseconds the bidder has from the time the request is sent by the Imp Bus to the time the response is received by the Imp Bus before timeout. This number will vary according to the supply partner. |
| `bid_info` | all | object | Details about the user and the bid request in general. See [Bid_Info](#bid_info) below for more information. |
| `members` | all | array of objects | An array of members that are eligible to bid on this call. A member is an entity that has a financial buying or selling relationship with AppNexus and is associated with a bidder. Some bidders may have multiple members; if you are building a bidder for your own exclusive use, you will be the only member. The member object has the id of the member. See [Members](#members) below for more information. <br><br> **Note**: This is not an array of numbers, it is an array of objects. The exact syntax is given in the [example](#example) below. |
| `tags` | all | array of objects | An array of the tags that are being auctioned in this call. An auction will have at least one, but may have several tags. See [Tags](#tags) below for more information. |

#### Owner-specific data

| Field | Scope | Type | Description |
|---|---|---|---|
| `allow_exclusive` | some | Boolean | If the bidding member owns the inventory (i.e. member_id of tag = member ID of the bidder) then the member can serve into it without allowing other bidders to participate. |

#### Debug data

| Field | Scope | Type | Description |
|---|---|---|---|
| `debug_requested` | some | Boolean | If *true*, the ad call included the `debug=1` flag, and no ad will be served. This will only be included in the bid request if the correct dongle is used. |
| `debug_member_id` | some | int | This field will contain the value of the "debug_member" parameter, if the parameter is passed in the querystring and the "dongle" parameter passed in the querystring matches the member's dongle (set on the [Member Service](member-service.md)). Your bidder can use the debug_member_id to produce debug output that is limited to a particular member. |
| `test` | some | Boolean | If *true*, the ad tag is running as a test and no ad will be served. If not present, test is false. |

#### Other data

| Field | Scope | Type | Description |
|---|---|---|---|
| `excluded_adservers` | some | array of integers | The IDs of adservers that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Ad Server Service](ad-server-service.md) to look up ad servers. |
| `excluded_brands` | some | array of integers | The IDs of brands that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Brand Service](brand-service.md) to look up brands. |
| `excluded_languages` | some | array of integers | The IDs of languages that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Language Service](language-service.md) to look up languages. |
| `excluded_categories` | some | array of integers | The IDs of categories that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Category Service](category-service.md) to look up categories. |
| `excluded_creatives` | some | array of integers | The IDs of creatives that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Creative Service](creative-service.md) to look up creatives. |
| `excluded_technical_attributes` | some | array of integers | The IDs of technical attributes that are not eligible for the impression, as defined by the seller's ad quality settings. You can use the [Technical Attribute Service](technical-attribute-service.md) to look up technical attributes. |
| `single_phase` | some | Boolean | This field is not currently used for bidders. |

### Members

| Field | Scope | Type | Description |
|---|---|---|---|
| `id` | all | int | The member's id. |

### Tags

Information associated with the ad tag.

#### Auction data

| Field | Scope | Type | Description |
|---|---|---|---|
| `auction_id_64` | all | int | The ID of the auction. This is useful for reconciliation and discrepancies, so we recommend that you add it to your logs. This is not guaranteed to be unique. |

#### Inventory hierarchy data

| Field | Scope | Type | Description |
|---|---|---|---|
| `id` | some | int | The ID of the TinyTag. A a tag is a subset of inventory within a site. Bidders cannot lookup what tag the ID corresponds to, but these IDs can be used as anonymous, optimizeable chunks of inventory. |
| `site_id` | some | int | The ID of the site. Sites are the second-largest groupings of inventory for members that sell their inventory through AppNexus. A site is a subset of inventory for a publisher. Bidders cannot lookup what site the ID corresponds to, but these IDs can be used as anonymous, optimizeable chunks of inventory. |

#### General data

| Field | Scope | Type | Description |
|---|---|---|---|
| `size` | all | string | A size (widthxheight; e.g. 300x160) for this impression. |
| `sizes` | all | array of strings | Allowable creative sizes for this impression, given in "widthxheight" format. |
| `position` | all | enum("below","above","unknown") | Position of the ad on the page above or below the fold; taken from the tag, if available. |
| `tag_format` | some | enum("iframe", "js", "wp7", "vast", "json", "xml") | For "iframe" tags, the impression bus will return HTML to display the winning creative on the publisher's page (if necessary, the HTML will contain an IFrame tag.) For "js" tags, the impression bus will return javascript to be executed on the publisher's page. (The javascript returned will typically contain document.write commands to generate the HTML for displaying the creative.) This distinction is only relevant to bidders in the case where a creative will not display properly in one or more tag formats. |
| `allowed_media_types` | some | array of integers | Valid media types. Use the [Media Type Service](../digital-platform-api/media-type-service.md) for a list of IDs. |
| `allowed_media_subtypes` | some | array of integers | Valid media subtype IDs. Use the [Media Subtype Service](../digital-platform-api/media-subtype-service.md) for a list of IDs. |
| `media_subtypes` | some | array of strings | Valid media subtypes for a creative, in string format. |
| `inventory_audits` | some | array | Seller self-classification data about the content of the site. |
| `venue_id` | some | int | This field is not currently used for bidders. |
| `ad_profile_id` | some | int | The tag-level ad approval profile ID that applies for the impression for the particular tag. |
| `predicted_view_rate` | all | double | The probability that the impression will be viewable by the user, based on historical data. |

#### Pricing data

| Field | Scope | Type | Description |
|---|---|---|---|
| `reserve_price` | some | float | When provided, this is the minimum bid necessary to win the auction. If the bidding member owns the inventory (allow_exclusive = true), this is ignored. |
| `estimated_clear_price` | some | double | The ECP is the estimated price needed to win the inventory. The ECP is larger than 95% of all winning bids for this tag submitted through AppNexus.<br><br> **Note**: Significant % of winning bids for any tag may not be submitted through AppNexus. <br><br> See [Price Reduction Mechanics](price-reduction-mechanics.md) for details. |
| `estimated_average_price` | some | double | The EAP is similar to the ECP, except that the EAP is larger than 70% of all winning bids for this tag submitted through AppNexus. |
| `estimated_price_verified` | some | Boolean | This field indicates whether the EAP and ECP have been verified by data observed by AppNexus. |

#### Owner-specific data

| Field | Scope | Type | Description |
|---|---|---|---|
| `tag_data` | owned only | string | If available, the other information associated with this TinyTag ID. The TinyTag's owner may add this information to the TinyTag in advance of an auction. |
| `exclusive_default` | owned only | Boolean | Indicates whether or not the auction is exclusive by default. An exclusive auction is one in which only the placement owner can serve an ad. The exclusive default may be overridden by the owner during the owner phase of the auction. |
| `default_creative_id` | owned only | int | The default creative ID for this TinyTag. |

#### Mobile-specific fields

| Field | Scope | Type | Description |
|---|---|---|---|
| `supply_type` | some | Always sent for "mobile_app" (not sent for "web") | Distinguishes whether this inventory is Web, Mobile Browser, or Mobile App. To determine if a web impression is being viewed on a mobile device, use the operating system in the bid request. |
| `creative_formats` | some | One or more of "text", "image", "html-url", "js-url", "flash", "js-raw", "html-raw", "html-iframe", "url-vast", "xml-url", "file-url", unknown" | List of AppNexus creative formats that can be used to bid on the impression. Other formats may be added to this list as they become supported. |
| `creative_actions` | some | One or more of "click-to-web", "click-to-call" | List of allowable click actions of creatives that can be used to bid on this impression. Today, click-to-call is not available but will be available soon. Other actions may be added to this list as they become supported. |
| `smaller_sizes_allowed` | some | Boolean | True if creatives of a smaller size and text creatives may also be used to bid for the impression. |

#### Deal data

| Field | Scope | Type | Description |
|---|---|---|---|
| `deals` | some | array of objects | An array of deals that apply to the impression. See [Deals](#deals) for more information. |

### Deals

Each object in the `deals` array contains the following fields.

| Field | Type | Description |
|---|---|---|
| `ad_quality_override` | int | Specifies how the deal handles creatives: <br> - `1`: Creatives use existing ad quality settings. (Default) <br> - `2`: Creatives in "pending" audit status will serve. Once these creatives are audited, the existing ad quality settings are used. <br> - `3`: No ad profile restrictions will be applied to this deal. (Maximum trust) |
| `allowed_media_subtypes` | array of integers. | Specifies the IDs of the media subtypes that are allowed on this deal. Use the [Media Subtype Service](../digital-platform-api/media-subtype-service.md) to view a list of media subtypes. If there are no unique media subtypes for this deal as compared to the main bid request object, this field will be an empty array. This does NOT mean the deal does not allow any media subtypes, instead it just means that the media subtypes on the main bid object should be used when bidding on this deal. |
| `allowed_media_types` | array of integers. | Specifies the IDs of the media types that are allowed on this deal. Use the [Media Type Service](../digital-platform-api/media-type-service.md) to view a list of media types. If there are no unique media types for this deal as compared to the main bid request object, this field will be an empty array. This does NOT mean the deal does not allow any media types, instead it just means that the media types on the main bid object should be used when bidding on this deal. |
| `floor_cpm` | double | The price the seller has set for the deal. Use this amount plus any applicable fees as your minimum bid in order to compete for this inventory. Note that bidding this amount plus any applicable fees will help ensure that you are eligible for the deal but will not guarantee that your bid wins. <br> This amount will always be in US dollars. Ask prices entered in another currency will be converted to dollars. |
| `id` |  int | The ID of the deal that applies to the impression. You can use the [Deal Buyer Access Service](deal-buyer-access-service.md) to view the deal's details including deal name, description, start and end date, and associated inventory. |
| `member_id` | int | The ID of the buyer member for whom the deal was created. |
| `sizes` | array of strings. | Allowable creative sizes for this deal, given in "widthxheight" format. If there are no unique sizes for this deal as compared to the main bid request object, this field will be an empty array. This does NOT mean the deal does not allow any sizes, instead it just means that the sizes on the main bid object should be used when bidding on this deal. |

### Bid_Info

Information on the user and the overall bid request.

#### User

| Field | Scope | Type | Description |
|---|---|---|---|
| `user_id_64` | all | int | The unique 64-bit ID for the user. It will be the same for all requests from this user until cookies are cleared. <br><br> **Note**: This value is only populated when the field `no_cookies` is `false`. <br><br> This field is `0` when AppNexus does not have a match for this user or the user's browser doesn't accept cookies. It will be `-1` for opt-out users. |
| `user_agent` | some | string | The "User-Agent" header from the browser. (In other words the type of browser.) |
| `operating_system` | some | int | The ID of the user's operating system. You can use the [Operating System Service](operating-system-service.md) to map operating system IDs to names. |
| `browser` | some | int | The ID of the user's browser. You can use the [Browser Service](browser-service.md) to map browser IDs to names. |
| `accepted_languages` | some  | string | The "Accept-Language" header from the browser (using ISO-639 language and ISO-3166 country codes). |
| `language` | some | int | The ID of the language as parsed from the accepted_languages string. You can use the [Language Service](language-service.md) to map languages to names. |
| `no_flash` | all | boolean | Informs the bidder if we have detected that the user's browser does not have flash installed. |
| `no_cookies` | all | boolean | If the `no_cookies` field is set to `false`<br> - AppNexus is able to track the user via a user id that is placed in a cookie in the user's browser. <br> - The user id will be contained in the `user_id_64` field on the bid request. <br><br> If the `no_cookies` field is set to `true` AND the `user_id_64` field is set to `0` <br> - AppNexus is not able to track the user since the user's browser does not accept cookies. <br> - You should not bid for such an auction on behalf of campaigns that require user data (e.g. frequency capping, recency capping). <br><br> If the `no_cookies` field is set to `true` AND the `user_id_64` field is **nonzero** <br> - AppNexus is able to track the user via cookies, and the user_id_64 field contains the user id. <br> - However, a problem occurred while looking up user information in the AppNexus server-side user data store. <br> - As a result, the bid request will not include user data, nor can AppNexus reliably update user data based on commands sent in the bid response. <br> - You should not bid for such an auction on behalf of campaigns that require user data (e.g. frequency capping, recency capping). |
| `gender` | some  | enum | "male" or "female" - This data may be supplied by the publisher at auction time. |
| `age` | some | int | This data may be supplied by the publisher at auction time. |
| `segments` | all | array of objects. | An array of the segments the user is in. Segments available include those owned by your members and those owned by 3rd party data providers (to whom AppNexus has granted your bidder access). Described in more detail below. |
| `session_freq` | all | int | The number of impressions AppNexus has served this user for the duration of the browsing session. For these purposes, a browsing session is defined as the lifetime of the user's AppNexus cookie. |
| `pub_session_freq` | all | int | The number of impressions AppNexus has served this user, on this publisher, for the duration of the browsing session. For these purposes, a browsing session is defined as the lifetime of the user's AppNexus cookie. |

#### Geographical data

| Field | Scope | Type | Description |
|---|---|---|---|
| `ip_address` | all | string | The IP address of the user. |
| `country` | some | string | The country or region of the user based on IP address, if it can be determined. |
| `region` | some | string | The region (state/province) of the user based on IP address, if it can be determined. |
| `city` | some | string | The city of the user based on IP address. |
| `postal_code_id` | some | int | The ID of the postal code of the user, based on IP address. |
| `dma` | some | int | Code for the designated market area of the user based on IP address, if it can be determined. |
| `time_zone` | some | string | The time zone of the user based on IP address, if it can be determined. |

#### Userdata from server-side cookie store

| Field | Scope | Type | Description |
|---|---|---|---|
| `userdata_json` | some |  | The userdata attached to the user's cookie stored by the bidder receiving the request. |
| `total_clicks` | some | int | **This field has been deprecated.** |

#### Inventory (page) information

| Field | Scope | Type | Description |
|---|---|---|---|
| `selling_member_id` | all | int | The ID of the member selling the inventory. See [Platform Member Service](platform-member-service.md) to find the corresponding member names. |
| `url` | some | string | The referral URL (contains the ad / launches the ad request). This is always provided if available, unless the publisher has chosen to restrict its use. A publisher may also opt to configure a default referrer url in AppNexus that will be passed on the bid request in the event that the referrer is not available or the publisher has chosen to restrict its use. Contact your AppNexus technical representative for more information. |
| `domain` | some | string | The domain of the referral URL. |
| `inventory_audits` | some | array | AppNexus audit data about the content of the site. Audits on bid_info pertain to all tags in the auction. This info often comes from a domain-level audit. Described in more detail below. |
| `within_iframe` | all | boolean | If the tag sits on the page with no enclosing iframes, this is `'true'`. Note that if AppNexus is unable to determine whether the tag is wrapped, this will be `'false'`. |
| `publisher_id` | some | int | The ID of the publisher. Publishers are used as the largest groupings of inventory for members that sell their inventory through AppNexus. Bidders cannot lookup what publisher the ID corresponds to, but these IDs can be used as anonymous, optimizeable chunks of inventory. |
| `is_secure` | some | boolean | If the page is secure, this is true. <br><br> **Note**: All connections to secure inventory must be secure. This includes pixels, creatives and 3rd party calls. (i.e. for a creative: `https://mysecure.content.com/ad/ABC.123.com/DEF.40;sz=300x250) \\`) |
| `certified_supply` | some | boolean | **Deprecated**. |

#### Mobile-specific fields

| Field | Scope | Type | Description |
|---|---|---|---|
| `app_id` | some | string | Global App Id for Android and iOS devices (For example, for Angry Birds app: "app_id": "com.rovio.angrybirds" for an Android device, "app_id" : "343200656" or "com.clickgamer.AngryBirds" for an iOS device). |
| `loc` | some | string | Location of the user, provided in terms of latitude and longitude. Expressed in the format "snnn.ddd,snnn.ddd", for example +123.456 or -456.123. South and west are represented as negative. There can be a maximum of 5 decimal places of precision. |
| `carrier` | some | int | Identifier for the carrier. A mapping of IDs to carrier names and countries or regions will be available from the carrier read-only service. A special carrier "WIFI" will exist for users connecting via WiFi. |
| `device_make` | some | int | The ID of the device make on which the ad will be shown. You can use this to manufacturer of the device on which the ad will be shown. For more information see the [Device Make Service](../digital-platform-api/device-make-service.md). |
| `device_model` | some | int | The ID of the device model on which the ad will be shown. For more information, see the [Device Model Service](../digital-platform-api/device-model-service.md). |
| `device_type` | some | int | The ID of the type of device on which the ad will be shown. This is represented by an integer, and can be looked up using the [Device Model Service](../digital-platform-api/device-model-service.md). Allowed values, and their meanings:<br> - `1` = "pc" <br> - `2` = "phone" <br> - `3` = "tablet" |
| `device_ids` | some | object | A JSON object containing information about the device IDs associated with the impression up for bid. For more information, see [Device IDs](#device-ids). |

### Device IDs

| Field | Scope | Type | Description |
|---|---|---|---|
| `aaid` | some | string | The Google advertising identifier for Android devices as retrieved from Google Play services. |
| `idfa` | some | string | The Apple advertising identifier for iOS devices running iOS 6+. |
| `md5udid` | some | string | The MD5 hash of the `ANDROID_ID`. This should only be sent for Android devices. It should be URL encoded. |
| `openudid` | some | string | The [OpenUDID](https://github.com/ylechelle/OpenUDID) of the device. This should only be sent for iOS versions 5 and below. |
| `sha1mac` | some | string | [ODIN](https://code.google.com/archive/p/odinmobile/). This should only be sent for iOS versions 5 and below. This should be URL encoded |
| `sha1udid` | some | string | The SHA1 hash of the `ANDROID_ID`. This should only be sent for Android devices. It should be URL encoded. |

### Segments

An array of the segments the user is in. Segments available include those owned by your members and those owned by 3rd party data providers (to whom AppNexus has granted your bidder access).

| Field | Scope | Type | Description |
|---|---|---|---|
| `code` | some | string | See [Pixel Services](../digital-platform-api/third-party-pixel-service.md) for details. |
| `id` | all | int | Segment ID. |
| `last_seen_min` | all | int | The number of minutes since this user was last tagged with this segment. Given in Posix time (represented in minutes). Multiply this value by 60 to get the number of seconds since the epoch when this segment was updated. |
| `member_id`  | all | int | ID of the member associated with this Segment.  |
| `other` | some | int | The value of the segment, if the segment contains a value. |

### Inventory audits

| Field | Scope | Type | Description |
|---|---|---|---|
| `auditor_member_id` | all | int | ID of the member who provided this audit. If this field is null, the audit was performed by the Platform Operations team. |
| `content_categories` | some | array of integers. | IDs of content categories of the site. To get the meaningful names of specific content categories or for the full list, see [Content Category Service](content-category-service.md). <br><br> **Note**: You may see ids in this list that are not visible to you in the content-category service. |
| `intended_audience` | some | enum | general, children, young_adult, or mature. Indicates the target maturity level of readers of this website. |
| `inventory_attributes` | some | array of integers. | IDs of sensitive attributes of the site that some advertisers may opt not to run on. To get the meaningful names of specific attributes or for the full list, see [Inventory Attribute Service](inventory-attribute-service.md). The presence of an empty array in this field indicates that the site has been audited and found to have **no** sensitive attributes. |

## Example

### Single tag request

```
{
    "bid_request": {
        "timestamp": "2015-06-07 14:39:35",
        "bidder_timeout_ms": 100,
        "members": [
            {
                "id": 6
            },
            {
                "id": 12
            }
        ],
        "allow_exclusive": false,
        "debug_requested": false,
        "tags": [
            {
                "id": 13,
                "sizes": [
                    "728x90"
                ],
                "position": "unknown",
                "inventory_source_id": 476,
                "auction_id_64": 8984480746668973000,
                "tag_format": "iframe",
                "reserve_price": 1,
                "ad_profile_id": 382,
                "predicted_view_rate": 0.654321,
                "inventory_audits": [
                    {
                        "auditor_member_id": 3,
                        "inventory_attributes": [
                            1431,
                            1432,
                            1887
                        ],
                        "content_categories": [
                            171
                        ]
                    }
                ]
            }
        ],
        "bid_info": {
            "user_id_64": 2987961585469200400,
            "no_flash": false,
            "no_cookies": false,
            "ip_address": "96.246.152.18",
            "inventory_audits": [
                {
                    "auditor_member_id": null,
                    "intended_audience": "young_adult",
                    "inventory_attributes": [
                        2,
                        3,
                        6,
                        7
                    ],
                    "content_categories": [
                        39
                    ]
                }
            ],
            "user_agent": "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US;rv:1.9.0.3) Gecko/2008092414 Firefox/3.0.3",
            "accepted_languages": "en-US,en;q=0.8",
            "country": "US",
            "region": "NY",
            "city": "New York",
            "postal_code_id": "10014",
            "dma": 501,
            "time_zone": "America/New_York",
            "url": "https://www.foodandwine.com/recipes/",
            "domain": "foodandwine.com",
            "selling_member_id": 3,
            "inventory_source_id": 123,
            "inventory_class": "class_2",
            "within_iframe": false,
            "total_clicks": 0,
            "segments": [
                {
                    "id": 103,
                    "member_id": 6,
                    "code": "PotentialCarBuyer",
                    "last_seen_min": 21108407
                }
            ]
        }
    }
}
```

### Multi tag request

```
{
    "bid_request": {
        "timestamp": "2015-09-17 20:32:00",
        "bidder_timeout_ms": 200,
        "members": [
            {
                "id": 1513
            }
        ],
        "member_ad_profile_id": 11138,
        "tags": [
            {
                "auction_id_64": 1704399148337927200,
                "size": "120x600",
                "sizes": [
                    "120x600"
                ],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "js",
                "site_id": 188164,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "url-vast"
                ],
                "ad_profile_id": 201859,
                "ad_profiles": [
                    201859
                ],
                "visibility_profile_id": 132,
                "venue_id": 12043,
                "predicted_view_rate": 0.675,
                "allowed_media_types": [
                    1
                ],
                "allowed_media_subtypes": [],
                "ecp": 1.43206,
                "eap": 0.5,
                "id": 624139,
                "inventory_audits": [
                    {
                        "auditor_member_id": null,
                        "intended_audience": "general",
                        "inventory_attributes": [],
                        "content_categories": []
                    }
                ]
            },
            {
                "auction_id_64": 3898100382999990000,
                "size": "5x6",
                "sizes": [
                    "5x6"
                ],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "js",
                "site_id": 188164,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "url-vast"
                ],
                "ad_profile_id": 201859,
                "ad_profiles": [
                    201859
                ],
                "visibility_profile_id": 132,
                "venue_id": 12043,
                "predicted_view_rate": 0.7131,
                "allowed_media_types": [
                    1
                ],
                "allowed_media_subtypes": [],
                "ecp": 2.07576,
                "eap": 0.5,
                "id": 624139,
                "inventory_audits": [
                    {
                        "auditor_member_id": null,
                        "intended_audience": "general",
                        "inventory_attributes": [
                            14
                        ],
                        "content_categories": []
                    }
                ]
            }
        ],
        "bid_info": {
            "user_id_64": 488125638053592500,
            "no_cookies": false,
            "payment_rule_id": 91411,
            "selling_member_id": 681,
            "no_flash": false,
            "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.89 Safari/537.1",
            "browser": 8,
            "operating_system": 11,
            "language": 1,
            "accepted_languages": "en-US,en;q=0.8",
            "session_freq": 75,
            "pub_session_freq": 15,
            "ip_address": "207.27.32.2",
            "country": "US",
            "region": "NY",
            "city": "New York",
            "dma": 501,
            "time_zone": "America/New_York",
            "inventory_class": "unaudited",
            "within_iframe": false,
            "publisher_id": 89400,
            "url": "https://www.foodandwine.com/recipes/",
            "domain": "www.foodandwine.com",
            "inventory_audits": [
                {
                    "auditor_member_id": null,
                    "inventory_attributes": [],
                    "content_categories": []
                }
            ],
            "userdata_json": "{}",
            "segments": []
        }
    }
    }
```

### Mobile request (debugging mode)

```
{
    "bid_request": {
        "timestamp": "2015-08-23 14:27:08",
        "bidder_timeout_ms": 2000,
        "members": [
            {
                "id": 307
            },
            {
                "id": 308
            }
        ],
        "single_phase": true,
        "member_ad_profile_id": 8610,
        "tags": [
            {
                "auction_id_64": 5638094169507807000,
                "size": "728x90",
                "sizes": [
                    "728x90"
                ],
                "smaller_sizes_allowed": true,
                "position": "unknown",
                "tag_format": "wp7",
                "site_id": 173564,
                "supply_type": "mobile_app",
                "creative_formats_map": "0000100001",
                "creative_formats": [
                    "image",
                    "text"
                ],
                "visibility_profile_id": 129,
                "venue_id": 663,
                "predicted_view_rate": 0.6891,
                "inventory_source_id": 926,
                "allowed_media_subtypes": [
                    1
                ],
                "estimated_clear_price": 1.24481,
                "estimated_average_price": 0.167,
                "estimated_price_verified": true,
                "id": 583751
            }
        ],
        "bid_info": {
            "user_id_64": 5725700387444723000,
            "no_cookies": false,
            "payment_rule_id": 84497,
            "selling_member_id": 618,
            "no_flash": true,
            "user_agent": "Mozilla%2f5.0+(compatible%3b+MSIE+9.0%3b+Windows+NT+6.1%3b+Trident%2f5.0)",
            "operating_system": 13,
            "language": 1,
            "accepted_languages": "en-us,en;q=0.5",
            "app_id": "2ac11907-8e3b-4b9b-b803-2ac834fa559a",
            "ip_address": "131.107.0.83",
            "country": "US",
            "postal_code_id": "10016",
            "loc": "38.7875232696533,-77.2614831924438",
            "inventory_class": "class_1",
            "within_iframe": false,
            "publisher_id": 81242,
            "gender": "male",
            "age": 27,
            "userdata_json": "{\"frequency\":[[\"r\",101,1,1,1,1303349386],[\"r\",102,1,1,1,1303349386]],\"last_imp_time\":1303349386,\"version\":4,\"pixel\":[],\"impserved\":45}",
            "segments": []
        }
    }
}
```

### Expandable request

```
{
    "bid_request": {
        "timestamp": "2015-04-20 20:00:14",
        "bidder_timeout_ms": 2000,
        "members": [
            {
                "id": 123
            }
        ],
        "test": true,
        "member_ad_profile_id": 11138,
        "tags": [
            {
                "auction_id_64": "7310650419817444682",
                "size": "300x250",
                "sizes": [
                    "300x250"
                ],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "js",
                "site_id": 188163,
                "creative_formats_map": "1111111111",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "url-vast",
                    "text"
                ],
                "ad_profile_id": 201859,
                "predicted_view_rate": 0.675,
                "visibility_profile_id": 132,
                "venue_id": 12043,
                "allowed_media_types": [
                    6
                ],
                "allowed_media_subtypes": [
                    10,
                    11,
                    12,
                    13,
                    14,
                    15,
                    16,
                    17,
                    18,
                    19,
                    20,
                    24
                ],
                "estimated_clear_price": 1,
                "estimated_average_price": 0.5
            }
        ],
        "bid_info": {
            "user_id_64": 7994340253645703000,
            "no_cookies": false,
            "payment_rule_id": 91411,
            "selling_member_id": 681,
            "no_flash": false,
            "is_secure": false,
            "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.163 Safari/535.19",
            "browser": 8,
            "operating_system": 11,
            "language": 1,
            "accepted_languages": "en-US,en;q=0.8",
            "session_freq": 1,
            "pub_session_freq": 1,
            "ip_address": "68.67.167.12",
            "country": "US",
            "region": "NY",
            "city": "New York",
            "postal_code_id": "10003",
            "dma": 501,
            "time_zone": "America/New_York",
            "inventory_class": "unaudited",
            "within_iframe": false,
            "url": "https://www.foodandwine.com/recipes/",
            "domain": "foodandwine.com",
            "inventory_audits": [
                {
                    "auditor_member_id": null,
                    "inventory_attributes": []
                }
            ],
            "userdata_json": "{}",
            "segments": []
        }
    }
}
```

### Deal-related request

```
{
    "bid_request": {
        "timestamp": "2015-04-18 17:00:57",
        "bidder_timeout_ms": 2000,
        "members": [
            {
                "id": 1417
            }
        ],
        "test": true,
        "member_ad_profile_id": 555216,
        "excluded_technical_attributes": [
            2033
        ],
        "tags": [
            {
                "auction_id_64": 5555508250840351000,
                "size": "300x250",
                "sizes": [
                    "300x250"
                ],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "iframe",
                "site_id": 555526,
                "creative_formats_map": "111111111011",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "url-vast",
                    "unknown",
                    "unknown"
                ],
                "ad_profile_id": 555180,
                "visibility_profile_id": 5553,
                "venue_id": 407258,
                "predicted_view_rate": 0.675,
                "pop_max_width": 300,
                "pop_max_height": 250,
                "pop_is_prepop": false,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 0.913,
                "estimated_average_price": 0.456,
                "id": 5555354,
                "deals": [
                    {
                        "id": 555664,
                        "member_id": 5555,
                        "floor_cpm": 0.5,
                        "ad_quality_override": 2,
                        "allowed_media_types": [
                            1,
                            5
                        ],
                        "allowed_media_subtypes": [
                            10,
                            11,
                            23,
                            50
                        ],
                        "sizes": [
                            "300x250",
                            "300x600"
                        ]
                    }
                ]
            }
        ],
        "bid_info": {
            "user_id_64": 5555037017052493000,
            "no_cookies": false,
            "payment_rule_id": 555018,
            "selling_member_id": 55578,
            "no_flash": false,
            "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36",
            "browser": 8,
            "operating_system": 11,
            "operating_system_extended": 81,
            "operating_system_family": 4,
            "carrier": 1,
            "device_type": 1,
            "language": 1,
            "accepted_languages": "en-US",
            "session_freq": 1,
            "pub_session_freq": 1,
            "ip_address": "555.1.12.54",
            "country": "US",
            "inventory_class": "unaudited",
            "within_iframe": false,
            "device_ids": {
                "sha1udid": "d55555c2314f3789198685914c01425034b5d502",
                "md5udid": "caf55557c5b39fb4ad68dabc9808bda1"
            },
            "publisher_id": 555547,
            "userdata_json": "{}",
            "segments": [
                {
                    "id": 1,
                    "member_id": 0,
                    "code": "cookie_birthday",
                    "provider": "",
                    "last_seen_min": 23274134
                }
            ]
        }
    }
}
```
