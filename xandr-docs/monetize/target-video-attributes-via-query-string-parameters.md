---
title: Target Video Attributes via Query String Parameters
description: Streamline video targeting with versatile VAST XML tags for diverse devices. Achieve precision using the user-friendly solution for various formats. 
ms.date: 10/28/2023
---

# Target video attributes via query string parameters

If you use a tag solution for in-stream video, effectively targeting demand requires knowledge and careful implementation of the range of possible tag parameters.

Microsoft Advertising provides clients with a simple-to-use tag to source video demand from a client or server environment. Requests are fulfilled via industry standard VAST XML where the VAST can contain VAST (media files only), VPAID1 (Flash) or VPAID2 (Flash or JavaScript). The `ptv` and `vmap` tags can be used on the client side, and the `ssptv` and `ssvmap` tags can be used on the server side. These tags are used across multiple use cases, sourcing demand to different device contexts such as desktop web, mobile web, mobile app (iOS and Android), OTT, IPTV, game consoles, and more.

When used for desktop web video, cookies can be used; for mobile apps, device identifiers such as IDFA and AAID can be used. For OTT or IPTV IP, other identifiers may be used for user and device identification. The `ptv` and `ssptv` tags can be used with OpenRTB protocols (2.2 and higher).

This page describes available query string parameters and what they target. Each attribute can be added to a`/ptv` or`/ssptv` tag using a query string parameter. These attributes are distinct from the creative attributes. Here's an example of a query string parameter:

```
https://ib.adnxs.com/ptv?id=5523324&vmaxduration=30&vskippable=0&vplaybackmethod=5&vwidth=480&vcontext=1&vframeworks=1,2&schain=<blahblah>
```

The following targetable attributes of the video placement and player are compliant with the OpenRTB 2.2 and OpenRTB 2.3 specifications. (For more information, see [Incoming Bid Requests from SSPs](../supply-partners/incoming-bid-request-from-ssps.md)) The ad call accepts the query string parameters shown below. The Compatible Handlers column notes which tag type(s) work with each parameter.

The following parameters are especially important for success:

- For web and mobile web inventory, always include the `referrer` parameter on your video request. For example, include `"referrer=`*`abcd.com&`*`"` where `abcd.com` is the appropriate URL for your inventory.
- Mobile app and CTV inventory require the `appid` parameter instead of `referrer`. For example, include `"appid=com.xandr"` where `com.xandr` is the app ID for your inventory.
- To receive exchange demand, you must pass in the either the `referrer` or `appid` parameter on all ad requests for video inventory. Not doing so will significantly limit demand for your inventory, and prevent you from monetizing effectively.

> [!NOTE]
> Device ID fields are casesensitive.

## Basic targetable attributes

| Parameter | Type | Required? | Compatible Handlers | Description |
|---|---|---|---|---|
| `gdpr` | boolean | Yes, on all GET calls in the EU | `ptv`, `ssptv`, `vmap`, `ssvmap` | A boolean value that shows GDPR status for the call. <br> - `0` = no = GDPR does not apply <br> - `1` = yes = GDPR applies |
| `gdpr_consent` | string | Yes, on all GET calls in the EU | `ptv`, `ssptv`, `vmap`, `ssvmap` | A string containing GDPR consent data. This field is comparable to `getConsentData` as discussed in IAB Europe's [Consent String and Vendor List Format: Transparency & Consent Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/a32574941ce201708e30e78702278efe1ce6cd59/Consent%20string%20and%20vendor%20list%20formats%20v1.1%20Final.md) as well as [advertisingconsent.eu](https://advertisingconsent.eu/). |
| `vmax_slot_duration` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Maximum video duration per slot in an ad pod in seconds. Any creative with a duration longer than this value will be excluded from the pod.<br><br>**Note**: This value only overrides the slot maximum duration defined on the placement video settings if the placement and request (i.e. vmaxduration) does not have a pod maximum duration value specified. |
| `vmax_num_ads` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Maximum number of ads per ad pod. This is the number of requests that will be sent for a given pod. |
| `vmaxduration` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | For single requests, this is the maximum video placement duration in seconds. Any creative with a duration longer than this value will be excluded from the auction. For podded inventory, this is the length of the full pod. |
| `vskippable` | int | No | `ptv`, `ssptv` | Denotes whether the placement is skippable. Possible values:<br> - `1` - the ad slot is skippable<br> - `0` - the ad slot is not skippable |
| `vplaybackmethod` | int | No | `ptv`, `ssptv` | Designates the playback method of the placement:<br> - `1` - Auto-play, sound-on<br> - `2` - Auto-play, sound-off<br> - `3` - Click-to-play<br> - `4` - Mouse-over<br> - `5` - Auto-play, sound unknown |
| `vwidth` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Player width (in pixels). While not required, this parameter is recommended in order to ensure video bidders receive both width and height on bid requests. |
| `vheight` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Player height (in pixels). While not required, this parameter is recommended in order to ensure video bidders receive both width and height on bid requests. |
| `vcontext` | int | Required to monetize inventory | `ptv`, `ssptv` | Position of the video placement. Possible Values:<br> - `1` - Linear Pre-roll<br> - `2` - Linear Mid-roll<br> - `3` - Linear Post-roll<br> - `4` - Outstream |
| `vframeworks` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Frameworks supported by the player. Possible values:<br> - `1` - VPAID 1.0<br> - `2` - VPAID 2.0<br> - `3` - MRAID-1<br> - `4` - MRAID-2<br> - `5` - ORMMA<br> - `6` - OMID-1<br><br>**Note**: `vframeworks` supports single as well as a list of comma-separated integer values. For example,<br>`vframeworks=1,2,3`<br>or<br>`vframeworks=1`. |
| `referrer` | string | Yes, for web traffic | `ptv`, `ssptv`, `vmap`, `ssvmap` | The URL where the ad will be rendered. |
| `appid` | int | Yes, for mobile app/CTV traffic | `ptv`, `ssptv`, `vmap`, `ssvmap` | The bundle ID of the mobile/CTV application. A platform-specific application identifier intended to be unique to the app and independent of the exchange. This string is used to identify an app running on Android or Apple iOS mobile devices as well as on Connected TV devices, such as Android TV, Apple TV, Roku, etc. For more details/examples see, [IAB Tech Lab OTT/CTV Store Assigned App Identification Guidelines](https://iabtechlab.com/wp-content/uploads/2020/08/IAB-Tech-Lab-OTT-store-assigned-App-Identification-Guidelines-2020.pdf).<br><br> - On Android (mobile & CTV), this is the app’s alphanumeric package name defined by the developer in the Google Play Store. It’s formatted as follows: `com.example.helloworld`, wherein this bundle ID appears at the end of the URL of the app store’s detail page<br> - On iOS (mobile) and tvOS (CTV), this is the app’s numeric iOS store ID, auto-generated by the Apple App Store. It’s formatted as follows: `123456789`, wherein this bundle ID appears at the end of the URL of the app store’s detail page.<br> - On Roku (CTV), this is the numeric ID autogenerated by Roku. It’s formatted as follows: `123456`,wherein this bundle ID is available in the HTML meta-tags in the Roku Channel Store page source following IABTL app-ads.txt guidelines.<br> <br>Many buyers set campaign targeting and reporting based on appid. Failing to supply a correct appid will make your inventory unattractive to these buyers. Therefore, passing this field is strongly recommended when supply_type is set to mobile_app. Note that this is what our Mobile SDKs do when they request an ad. To find the app ID for a particular app, inspect the app’s detail page, which you can find using a web search. For example, here are the detail pages for the “Tubi” app (with appid bundles available as per above descriptions):<br><br> - Google Play (Android): https://play.google.com/store/apps/details?id=com.tubitv<br> - Apple (iOS / tvOS): https://apps.apple.com/us/app/tubi-watch-movies-tv-shows/id886445756<br> - Roku: https://channelstore.roku.com/details/7c34d32446def64db7eb2cc359749fe5/tubi-free-movies-and-tv |
| `vv` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The VAST version supported by the player:<br> - `2` - VAST 2.0<br> - `3` - VAST 3.0<br> - `4` - VAST 4.0<br> - `5` - VAST 4.1<br> - `6` - VAST 4.2 |
| `schain` | string | Required for requests on resold inventory | `ptv`, `ssptv` | Advertising systems should support a parameter in their ad tags or VAST URLs to accept a string-serialized SupplyChain. It is recommended that this parameter be `schain`. For more information about `schain` string parameters and their corresponding JSON objects, see: [SupplyChain for Non-OpenRTB Requests](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/master/supplychainobject.md#supplychain-for-non-openrtb-requests)<br><br>`1.0,1!exchange1.com,1234,1,bid-request-1,publisher,publisher.com!exchange2.com,abcd,1,bid-request2,intermediary,intermediary.com` |
| `eids` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | An external ID (eid) is passed by a publisher when an auction is initiated. Each eid has 3 comma separated fields, where the source and id are the required fields.<br> - **source**: The identity solution source, representing the origin of the ID. For example, you can specify liveramp.com or a custom string for publisher provided ID solutions.<br> - **id**: The user ID provided by identity solution.<br> - **rti_partner**: The third party identity solution name.<br>The following example shows two external IDs, each with their respective fields. To pass multiple IDs, separate the eids with a pipe character:<br> &nbsp;&nbsp;&nbsp; - External ID1: `source=adserver.org,id=987654,rti_partner=TDID`<br> &nbsp;&nbsp;&nbsp; - External ID2: `source=criteo.com,id=1234567,rti_partner=(none)`<br><br> The two external IDs are then passed into an endpoint, in the following way:<br><br>`...&eids=adserver.org,987654,TDID\|criteo.com,1234567&...` |

## Additional settings

| Parameter | Type | Required? | Compatible Handlers | Description |
|---|---|---|---|---|
| `id` | int | Yes | `ptv`, `ssptv`, `vmap`, `ssvmap`| The unique ID of the placement where the ad will serve. If you'd rather not pass the raw placement ID, you can pass in a combination of `member` and `inv_code` parameters. For more information, see the documentation for those parameters. |
| `member` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | (Optional) The member ID of the member on whose placement the ad will serve. Instead of passing the placement ID, you can pass a combination of this field and `inv_code` to uniquely identify a specific placement. |
| `carrier` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Name of the mobile carrier. This is optional because our system can usually deduce the carrier from the device's IP address. For Example: `AT&T - US`. For more information on allowed values for this field, see [Carrier Service](../digital-platform-api/carrier-service.md). |
| `connection_type` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The type of network used by the device. Allowed values are "`wifi`" or "`wan`". |
| `content_len` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The content duration in seconds. |
| `content_livestream` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Whether the content is live or video on demand (VOD). 0: VOD, 1: Live |
| `content_genre` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The genre that best describes the content. |
| `content_program_type` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The type of program (For example: movie, event, episode, etc). |
| `content_contentrating` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The content rating (For example: PG-13). |
| `content_album` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Album to which the content belongs; typically for audio. |
| `content_artist` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Artist credited with the content. |
| `content_cat` | string array | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Array of IAB content categories that describe the content producer. Refer to [list 5.1](https://iabtechlab.com/standards/content-taxonomy/). |
| `content_context` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Type of content (game, video, text, etc.). |
| `content_data_id` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Exchange-specific ID for the data provider. |
| `content_data_name` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Exchange-specific name for the data provider. |
| `content_data_segment` | object array | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Array of Segment objects that contain the actual data values. |
| `content_embeddable` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Indicator of whether or not the content is embeddable (Example: An embeddable video player), where 0 = no, 1 = yes. |
| `content_episode` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Episode number. |
| `content_isrc` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | International Standard Recording Code conforming to ISO-3901. |
| `content_keywords` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Comma separated list of keywords describing the content. |
| `content_prodq` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Production quality. |
| `content_producer_id` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Content producer or originator ID. Useful if content is syndicated and may be posted on a site using embed tags. |
| `content_producer_cat` | string array | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Array of IAB content categories that describe the content producer. Refer to [list 5.1](https://iabtechlab.com/standards/content-taxonomy/). |
| `content_producer_name` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Content producer or originator name (e.g., “Warner Bros”). |
| `content_producer_domain` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Highest level domain of the content producer (Example: “[producer.com](https://producer.com/)”). |
| `content_qagmediarating` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Media rating per IQG guidelines. Refer to [List 5.19](https://iabtechlab.com/standards/content-taxonomy/). |
| `content_season` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Content season (Example: “Season 3”). |
| `content_series` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Content series. Video Examples: “The Office” (television), “Star Wars” (movie), or “Arby ‘N’ The Chief” (made for web). Non-Video Example: “Ecocentric” (Time Magazine blog). |
| `content_sourcerelationship` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | 0 = indirect, 1 = direct. |
| `content_title` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Content title. Video Examples: “Search Committee” (television), “A New Hope” (movie), or “Endgame” (made for web). Non-Video Example: “Why an Antarctic Glacier Is Melting So Quickly” (Time magazine article). |
| `content_url` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | URL of the content, for buy-side contextualization or review. |
| `content_userrating` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | User rating of the content (Example: Number of stars, likes, etc.). |
| `content_network` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The top-level parent company or, where relevant, a sub-brand which owns multiple TV-like channels, d2c content brands, or digital properties on which the content is being viewed |
| `content_language` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The language of the video content. Specify the language using the two-letter ISO-639-1-alpha-2 code. |
| `channel_name` | string | No | `ptv`, `ssptv` | The name of channel the content is airing on. |
| `airtime` | string | No | `ptv`, `ssptv` | The original airtime. It only applies to time-shifted content. |
| `content_id` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The unique alphanumeric content identifier. |
| `devmake` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The manufacturer of the device requesting the ad. Typically, this value is parsed from the UA string parameter (for server-side implementations) or included automatically in the request headers (for client-side integrations). Otherwise, you can use this parameter to pass the information in the query string directly. For Example: `da-4G Systems`. For more information on allowed values for this field, see the name values from the [Device Make Service](../digital-platform-api/device-make-service.md) and prefix them with `"da-"`. |
| `devtype` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The type of the device requesting the ad. Typically, this value is parsed from the UA string parameter (for server-side implementations) or included automatically in the request headers (for client-side integrations). Otherwise, you can use this parameter to pass the information in the query string directly. Allowed values are `da-Tablet`, `da-Mobile Phone`, `da-Game Console`, `da-TV`, `da-Set Top Box`, `da-Media Player`. For more information on how the values in this field get mapped into targeting/reporting, see the [Device Type Targets section of Profile Service](../digital-platform-api/delivery-type-service.md). |
| `devmodel` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The specific name or number of the device requesting the ad. Typically, this value is parsed from the UA string parameter (for server-side implementations ) or included automatically in the request headers (for client-side integrations). Otherwise, you can use this parameter to pass the information in the query string directly. For Example: `da-3499464`. For more information on allowed values for this field, see the code values with `“da-”` prefix from the [Device Model Service](../digital-platform-api/device-model-service.md). |
| `dnt` | boolean | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | **This field is deprecated, and may be removed in the future**. Use the `LimitAdTrackingEnabled` flag instead.<br>If `true`, the user has set the system-level preference to not receive behaviorally targeted ads. Allowed values: `true`, `false`, `1`, or `0`. |
| `devtime` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The time on the device, measured in seconds since the epoch, or UNIX Time.|
| `devtz` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The device's timezone. |
| `external_uid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | A string that corresponds to an external user ID for this user. |
| `ifa` | string | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | The unique device identifier using the UUID standard (8-4-4-4-12) |
| `ifa_type` | string | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Possible values are `aaid` (Android), `idfa` (AppleTV), `afai` (Amazon Fire), msai (Microsoft), `rida` (Roku), `ppid`, `tif`a (Tizen (Samsung)), `vida` (Vizio), `lgudid` (LG).<br><br>**Note**: If you can't dynamically pass in device or platform IDs, you should use:<br> - `ifa_type=openudid` for CTV ad requests if you have authentication data and can pass persistent IDs<br> - `&ifa_type=sessionid` if you don't have authentication data with persistent IDs |
| `LimitAdTrackingEnabled` | boolean | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | If `true`, the user has set the system-level preference to not receive behaviorally targeted ads. Allowed values: `true`, `false`, `1`, or `0`.<br>For more information about the system-level ads preferences on iOS, see [Opt out of interest-based ads from iAd](https://support.apple.com/en-us/HT202074).<br>For more information about the system-level ads preferences on Android, see [Advertising ID](https://developer.android.com/google/play-services/id.html). |
| `md5udid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The MD5 hash of the `ANDROID_ID`. This should only be sent for Android devices. This should be URL-encoded. |
| `sha1udid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The SHA1 hash of the `ANDROID_ID`. This should only be sent for Android devices. This should be URL encoded.. |
| `rida` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The device ID for a Roku device.<br><br>**Note**: This parameter isn't needed if `ifa` and `ifa_type` are passed. |
| `idfa` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The Apple advertising identifier for iOS devices running iOS 6+.<br><br>**Note**: This parameter isn't needed if `ifa` and `ifa_type` are passed. |
| `aaid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The Google advertising identifier for Android devices as retrieved from Google Play services. |
| `adid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The Windows advertising identifier for Windows devices.<br>**Note**: This parameter isn't needed if `ifa` and `ifa_type` are passed. |
| `ip` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | IP address of the device making the ad request, e.g., `207.237.150.246`.<br> - If `ip` is not specified for `/ptv` calls, the IP passed via HTTP headers will be used for geo detection instead.<br> - If `ip` is not specified for `/ssptv` calls, Microsoft Advertising will not be able to detect geographic location, and buyers will therefore not be able to target by geolocation. |
| `language` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The device's language, specified with an [ISO Language Code](https://www.iso.org/iso/home/standards/language_codes.htm). |
| `loc` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The user's location expressed in latitude and longitude, in the format: `snnn.ddddddddddddd`,`snnn.ddddddddddddd`. Up to 13 decimal places of precision are allowed. |
| `loc_age` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Age of the location data in milliseconds. |
| `loc_prec` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Precision of the location data in meters. |
| `mcc` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The Mobile Country Code as specified by the [ITU](https://www.itu.int/en/publications/ITU-T/Pages/publications.aspx?parent=T-SP&view=T-SP1). |
| `mnc` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The Mobile Network Code as specified by the [ITU](https://www.itu.int/en/publications/ITU-T/Pages/publications.aspx?parent=T-SP&view=T-SP1). |
| `openudid` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The [OpenUDID](https://github.com/ylechelle/OpenUDID) of the device. This should only be sent for iOS versions 5 and below. |
| `orientation` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Device screen orientation during the ad request. Allowed values are `"v"` or `"h"`. |
| `os` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The operating system and the version number of the device requesting the ad. Typically, this value is parsed from the UA string parameter (for server-side implementations) or included automatically in the request headers (for client-side integrations). Otherwise, you can use this parameter to pass the information in the query string directly. For Example: `iPhone - iOS (other versions)`. For more information on allowed values for this field, see [Operating System Service](../digital-platform-api/operating-system-service.md). |
| `pcode` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The postal code of the user requesting an ad. If not specified, postal code will be determined from the IP address. |
| `redirenc` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The redirect URL that should be used in the case where there is no valid creative to serve. The url should be encoded. |
| `reserve` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The reserve price for this inventory, which is the minimum net amount the placement will accept for placing a creative. This parameter will override a preset price and will set the hard floor (and soft floor where relevant) if Yield Management is not being used or if the reserve price is greater in value than the YM Floor wherein the Floor Rule has the override setting on. |
| `sha1mac` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The SHA1 hash of the [ODIN](https://code.google.com/p/odinmobile/). This should only be sent for iOS versions 5 and below. This should be URL encoded. |
| `st` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The supply type of the inventory, which indicates the environment in which an ad will be shown. Allowed values: `"mobile_app"`, `"mobile_web"`, or `"web"`. Defaults to `"mobile_app"`. |
| `size` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | **Deprecated**. Use `vwidth` and `vheight` instead. The requested banner size, for example, `"320x50"`, or the screen size for Interstitial ads. |
| `tmpl_id` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The supply template identifier. |
| `traffic_source_code` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | A traffic source code provides the ability to check the third-party traffic source of a particular impression. If the traffic source code is pre-registered with Microsoft Advertising, and is passed via the query string using the `trafficSourceCode` property, then it would let you know the sources for the third-party traffic occurred for an impression.<br>This `traffic_source_code` is included in the [Standard Feed](../log-level-data/standard-feed.md) and can be used to pass publisher key-value information to the feed. |
| `ua` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The user agent string associated with the device requesting an ad. If specified, this value will be used rather than the standard user agent sent via HTTP header. This should be URL encoded. The user agent identifies information such as the device’s operating system as well as the device’s make and model, along with the information about the application, and the software vendor acting on behalf of the user. Many buyers target their audiences based on these parameters and not including them will restrict demand. |
| `us_privacy` | string | No | `ptv`, `ssptv` | The IAB Tech Lab's US Privacy String communicates signals regarding consumer privacy and choice under US privacy regulation. [CCPA Client Overview](https://microsoftapc.sharepoint.com/teams/PrivacyRegulations/SitePages/CCPA-Client-Overview.aspx) (Login required)<br>For more information, see: [CCPA Publisher Controls](https://microsoftapc.sharepoint.com/teams/PrivacyRegulations/SitePages/CCPA-Publisher-Controls-Provided-by-Microsoft Advertising.aspx) (Login required) |
| `placement_set` | string | No | `vmap`, `ssvmap` | The placement set to be associated with the tag. To learn more, see [Placement Set Service](../digital-platform-api/placement-set-service.md). |
| `vmin_ad_duration*`| int | No | `ptv`, `ssptv` | The minimum ad duration, in seconds. |
| `mimes*` | string | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | Video mimes accepted, expressed as a comma-separated list of IDs. You can find the IDs in the [Placement Service documentation](../digital-platform-api/placement-service.md) under "Supported Mime Types." |
| `minbitrate*` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The minimum bitrate accepted |
| `mf_min_height*` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The minimum media file height, in pixels |
| `mf_min_width*` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The minimum media file width, in pixels |
| `mf_aspect_ratio*` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | The media file aspect ratio |
| `an_user_id` | int | No | `ssptv` | The Microsoft Advertising user ID |
| `gpp` | string | Yes, on all GET calls in applicable US states | `ptv`, `ssptv`, `vmap`, `ssvmap` | Indicates the actual IAB GPP consent string. It implies which vendors are permitted to process personal data and under which conditions. This field is discussed as part of the IAB Tech Lab's [Global Privacy Platform](https://iabtechlab.com/gpp) (GPP). |
| `gpp_sid` | string array | Yes, on all GET calls in applicable US states | `ptv`, `ssptv`, `vmap`, `ssvmap` | A boolean value that shows which [sections of the GPP](https://github.com/InteractiveAdvertisingBureau/Global-Privacy-Platform/blob/main/Sections/Section%20Information.md#section-ids) apply for the call. |
| `ext_inv_code` |  |  |  | A predefined value passed on the query string that can be used in reporting. The value must be entered into the system before it is logged. For more information, see External Inventory Code Service. Example: `ext_inv_code=10039` |

## Related topics

- [Create a Placement](create-a-placement.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
- [Export Video Placement Tags](export-video-placement-tags.md)
- [Onboarding Video Supply](onboarding-video-supply.md)
