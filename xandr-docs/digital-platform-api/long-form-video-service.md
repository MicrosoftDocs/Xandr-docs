---
title: Long Form Video Service
description: In this article, learn about the Long Form Video service, their request and response process, and parameters with an example.
ms.date: 09/25/2024
ms.custom: digital-platform-api
---

# Long Form Video Service

Direct Supply customers can integrate their app or web long-form ad pod video inventory with Prebid Server Premium (PSP) using the `/prebid/lfv` endpoint. Long-form video durations are at least 30 minutes with potential pre, mid, and post-roll positions.

Microsoft Monetize Ad Server customers do not need to change their current integration into Microsoft Monetize, can ignore the long-form video service, and can instead follow the [PSP Setup Steps](../monetize/integrate-with-psp.md).

## Request and response process

The following steps outline the long-form video request and response process:

1. Publishers submit a long-form video request to Microsoft Monetize's Impression Bus (ImpBus) via the `/prebid/lfv` endpoint. This request contains `POST` values for the ad pod such as ad duration, video width and height, and optional properties such as brand category for competitive separation.
1. ImpBus unpacks the request and determines the number of ad slots to fill within the ad pod.
1. The configurations from Monetize are retrieved and an OpenRTB request with the requested number of ad slots is created by ImpBus.
1. ImpBus submits the OpenRTB request to all Microsoft Monetize bidders, including PSP demand partners and Microsoft Invest
    1. The Prebid demand partners return bids, each with a unique IAB subcategory.
    1. Microsoft Invest and external bidders have a unique Microsoft Monetize brand category associated with every bid which are converted to an IAB subcategory.
1. ImpBus runs the auction for the Microsoft Monetize marketplace to determine the winning Microsoft Monetize bid.
1. Based on the publisher and ad server configuration retrieved in step three, ImpBus translates the IAB subcategories to the primary ad server categories (Freewheel or Google Ad Manager).
    1. For Microsoft Monetize bids, ImpBus will translate from the Microsoft Monetize category to the IAB subcategory and finally to the primary ad server category.
1. The bids are deduped based on the tuple values for price bucket, primary ad server category, and duration.
1. For each unique bid, ImpBus caches the unique VAST XML.
1. Key-value targeting pairs are generated for each bid for `hb_pb`, `hb_pb_cat_dur,` and `hb_cache_id`.
1. ImpBus returns a JSON response with Prebid targeting key-value pairs and the cache id.

:::image type="content" source="media/long-form-video-service-fig-a-edited.png" alt-text="Diagram that illustrates the request and response process.":::

## REST API

The following table list the required and optional parameters for submitting a long-form video bid request.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `app` | Required | Object | Container object describing the app that will display the ad pod(s). **If app is not included in the request then the site parameter must be.** |
| `auction_timeout_ms` | Optional | Integer | Maximum time in milliseconds to wait for the auction to complete. Defaults to zero if not given which uses the timeout setting from the member's [Prebid Server Premium Global Settings](../monetize/add-or-edit-psp-global-settings.md). |
| `bcat` | Optional | String Array | Blocked advertiser categories using the IAB content categories. |
| `badv` | Optional | String Array | Blocked list of advertisers by their domains (e.g., ["ford.com"](https://www.ford.com/)). |
| `cacheconfig` | Optional | Object | Optional controls to have Prebid Server cache information. |
| `content` | Optional | Object | Container object describing miscellaneous content metadata that can be used for targeting the `adPod(s)`. |
| `cur` | Optional | String | Default: USD. Allowed currency for targeting keys on this bid request using ISO-4217 alpha codes. |
| `device` | Optional | Object | Container object describing the device being used for video rendering. |
| `eids` | Optional | Object | The list of unified user IDs. |
| `gpid` | Optional | String | Global Placement ID. A unique identifier for the ad slot across platforms. For more information on the Prebid Ad Slot and GPID, see the [Prebid documentation](https://docs.prebid.org/features/pbAdSlot.html). |
| `includebrandcategory` | Optional | Object | Container object describing brand category inputs. |
| `memberid` | Optional (Required if using inventory codes) | Integer | The seller's member id. |
| `podconfig` | Required | Object | Container object for describing all the pod configurations. For more information on the `pod` object, see the [Pod Config](#pod-config) section below. |
| `pricegranularity` | Optional (recommended) | Object | For more information on the `pricegranualrity` object see the [Price Granularity](#price-granularity) section below. For a broader explanation on setting `pricegranularity`, see the [Prebid documentation](https://docs.prebid.org/adops/price-granularity.html#price-granularity-explained). |
| `site` | Required | Object | Container object describing the page submitting the `adpodrequest`. If `site` is not included then the `app` parameter must be. |
| `user` | Optional | Object | Container object describing the user of the device. |
| `video` | Optional | Object | Container object describing the video player. |
| `xdyn_params` | Optional | Object | This object holds bidder-specific parameters such that each key is a bidder name and the value is a JSON object containing parameters for that bidder. See [example](#xdyn_params-example). |

### `xdyn_params` example

```
{
  "xdyn_params": {
    "appnexus": {
      "keywords": "key1=val1,key2=val2"
    }
  }
}
```

### App

The `app` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `domain` | Required | String | The domain of the app. |
| `name` | Optional | String | The name of the app. |
| `bundle` | Optional | String | A platform-specific application identifier intended to be unique to the app and independent of the exchange. This should be a bundle or package name (e.g., com.foo.mygame). |
| `keywords` | Optional | String | Comma separated list of keywords. |
| `storeurl` | Optional | String | App store URL for an installed app. |

### Cache config

The `cache config` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `ttl` | Optional | Integer | Time to live for a cache entry specified in seconds. |
| `disablecache` | Optional | Boolean | The default setting is `false`. If this flag is set, the PBS cache is disabled and the responsibility of caching is on the publisher or publisher's vendor. |

### Content

The `content` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `album` | Optional | String | Album to which the content belongs; typically for audio. |
| `artist` | Optional | String | Artist credited with the content. |
| `airtime` | Optional | Integer | The date and time at which the content first aired. |
| `cat` | Optional | String Array | Array of IAB content categories that describe the content producer. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `channel` | Optional | String | Name of the channel the content is airing on. |
| `contentrating` | Optional | String | Content rating (e.g., MPAA). |
| `context` | Optional | Integer | Type of content (game, video, text, etc.). Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `data` | Optional | Object Array | Additional content data. Each Data object represents a different data source. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `embeddable` | Optional | Boolean | Indicator of whether or not the content is embeddable (e.g. an embeddable video player), where `false` = no, `true` = yes. |
| `episode` | Optional | Integer | Episode number. |
| `ext` | Optional | Object | Placeholder for exchange-specific extensions to OpenRTB. |
| `genre` | Optional | String | Genre that best describes the content (e.g., rock, pop, etc). |
| `id` | Optional | String | ID uniquely identifying the content. |
| `isrc` | Optional | String | International Standard Recording Code conforming to ISO-3901. |
| `keywords` | Optional | String | Comma separated list of keywords describing the content. |
| `language` | Optional | String | Content language using ISO-639-1-alpha-2. |
| `len` | Optional | Integer | Length of content in seconds; appropriate for video or audio. |
| `livestream` | Optional | Boolean | `true` = live, `false` = not live (e.g., stream, live log). |
| `network` | Optional | String | The top-level parent company or, where relevant, a sub-brand which owns multiple TV-like channels, d2c content brands, or digital properties on which the content is being viewed. |
| `prodq` | Optional | Integer | Production quality. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `producer` | Optional | Object | Details about the content `producer`. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `qagmediarating` | Optional | Integer | Media rating per IQG guidelines. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `season` | Optional | String | Content season (e.g., "Season 3"). |
| `series` | Optional | String | *Video Examples:* "The Office" (television), "Star Wars" (movie), or "Arby 'N' The Chief" (made for web).<br>*Non-Video Example:* "Ecocentric" (Time Magazine blog). |
| `sourcerelationship` | Optional | Integer | `0` = indirect, `1` = direct. |
| `title` | Optional | String | Content title.<br>*Video Examples:* "Search Committee" (television), "A New Hope" (movie), or "Endgame" (made for web).<br>*Non-Video Example:* "Why an Antarctic Glacier is Melting So Quickly" (Time magazine article). |
| `url` | Optional | String | URL of the content, for buy-side contextualization or review. |
| `userrating` | Optional | String | User rating of the content (e.g., number of stars, likes, etc.). |
| `videoquality` | Optional | integer; DEPRECATED | **Note:** **Deprecated** in favor of `prodq`. Video quality. Refer to [IAB specifications](https://iabtechlab.com/standards/content-taxonomy/). |
| `program_type` | Optional | String | Type of program. |

### Device

The `device` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `ua` | Optional | String | The browser user agent. |
| `dnt` | Optional | Integer | The standard “Do Not Track” flag as set in the header by the browser. Accepted values are:<br>- `0`. Tracking is unrestricted.<br>- `1`. Do not track. |
| `lmt` | Optional | Integer | The “Limit Ad Tracking” signal for mobile devices (e.g., iOS, Android). Accepted values are:<br>- `0`. Tracking is unrestricted.<br>- `1`. Tracking must be limited per commercial guidelines. |
| `ip` | Optional | String | The IP address of the device making the ad request. |
| `os` | Optional | String | The device operating system. Example `"iOS"`. |
| `h` | Optional | Integer | The physical height of the screen in pixels. |
| `w` | Optional | Integer | The physical width of the screen in pixels. |
| `devicetype` | Optional | Integer | The general type of device. Accepted values are:<br> - `Mobile/Tablet`<br> - `Personal Computer`<br> - `Connected TV`<br> - `Phone`<br> - `Tablet`<br> - `Connected Device`<br> - `Set Top Box` |
| `ifa` | Optional | String | The ID sanctioned for advertiser use in the clear (i.e., not hashed). |
| `didsha1` | Optional | String | The hardware device ID (e.g., IMEI); hashed via SHA1. |
| `didmd5` | Optional | String | The hardware device ID (e.g., IMEI); hashed via MD5. |
| `dpidsha1` | Optional | String | The platform device ID (e.g., Android ID); hashed via SHA1. |
| `dpidmd5` | Optional | String | The platform device ID (e.g., Android ID); hashed via MD5. |
| `macsha1` | Optional | String | The MAC address of the device; hashed via SHA1. |
| `macmd5` | Optional | String | The MAC address of the device; hashed via MD5. |

### Eids

The `eid` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `source` | Required | String | The source or technology provider. |
| `id` | Required | String | The unique user ID. |
| `rti_partner` | Required | String | The partner ID. |

### Include brand category

The `includebrandcategory` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `primaryadserver` | Optional | Integer | An integer whose value represents the ad server used by the publisher. Accepted values are:<br>- `Freewheel`<br>- `Google Ad Manager` |

### Site

The `site` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `page` | Required | String | A URL of the page where the impression will be displayed. |
| `keywords` | Optional | String | Comma separated list of keywords. |

### User

The `user` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `buyeruid` | Optional | Integer | The Microsoft Monetize user ID, if known. |
| `yob` | Optional | Integer | The user's year of birth as a four-digit integer. |
| `gender` | Optional | Integer | The user's gender. Accepted values are:<br>- `M`: male<br>- `F`: female<br>- `O`: Known to be other. |
| `keywords` | Optional | String | A list of keywords representing interests or intent. |
| `gdpr` | Optional | Object | Container object describing the user's GDPR settings. For more information see the [GDPR](#general-data-protection-regulation-gdpr) section below. |
| `privacy` | Optional | String | CCPA user privacy string. |

### Video

The `video` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `context` | Optional | Integer | Context in which the video ad will be shown.<br>- `0`: Unknown<br> - `1`: Preroll<br>- `2`: Midroll<br>- `3`: Postroll<br>- `4`: Outstream<br>- `5`: In Banner |
| `w` | Optional | Integer | The width of the video player in device independent pixels. |
| `h` | Optional | Integer | The height of the video player in device independent pixels. |
| `mimes` | Optional | String Array | An array of video player supported mime types. Example: `["video/mp4"]` |
| `protocols` | Optional | String Array | An array of video protocols supported by the video player. Accepted video protocols are:<br>- `VAST 1.0`<br>- `VAST 2.0`<br>- `VAST 3.0`<br>- `VAST 1.0 Wrapper`<br>- `VAST 2.0 Wrapper`<br>- `VAST 3.0 Wrapper`<br>- `VAST 4.0`<br>- `VAST 4.0 Wrapper`<br>- `DAAST 1.0`<br>- `DAAST 1.0 Wrapper` |

### Pods

The `pod` object supports the following request parameters.

| Parameeter | Scope | Type | Description |
|:---|:---|:---|:---|
| `podid` | Required | Integer | Unique id of the pod within a particular request. It is recommended these be ordered sequentially with an increment of one. |
| `adpoddurationsec` | Required | Integer | The duration of the `adPod`. |
| `placementid` | Required | Integer | Placement ID that a pod relates to. If `placementid` is omitted then `invcode` and `request.memberid` are required. |
| `invcode` | Optional | String | Inventory code that a pod relates to. If the `invcode` is passed in, then the seller must also pass in their member ID in `request.memberid`.<br>If `invcode` is omitted then `placementid` is required. |

### Pod config

The `pod config` object supports the following request parameters.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `adomaindedupe` | Optional | Boolean | Flag that indicates whether or not to deduplicate based on advertiser domain (`adomain` value in OpenRTB bid responses). When enabled, no two selected bids can have the same advertiser domain. |
| `perpodkeys` | Optional | Boolean | Flag indicating if key-values in response should be configured for per-pod competitive separation. Defaults to `false`. When this flag is enabled, a `_podX` identifier is added to the key names returned, where X starts at 1 and increase by 1 for each subsequent pod.<br>Each pod has a different `hb_cache_id` value that its bids are cached with, allowing for identical `hb_pb_cat_dur` values to be returned as long as they occur in different pods. Adds instance ids to the value to allow similar bids to be returned even in same pods. Instance ids on the values will be a postfix of `_pX` where X starts at 0 and increase by 1 for each subsequent identical bid. For Example, With `perpodkeys` flag enabled, a `hb_pb_cat_dur` key and value that would normally look like: `"hb_pb_cat_dur"`: `"15.00_airlines_30s"`<br>Will instead look like:<br>`"hb_pb_cat_dur_pod1"`: `"15.00_airlines_30s_p0"` |
| `pods` | Required | Object | Container object for describing the `adPod`(s) to be requested. |
| `durationrangesec` | Required | Integer | Range of ad durations allowed in the response. For more detail on duration range, see [Duration Range](#duration-range) section below. |
| `requireexactduration` | Optional | Boolean | Flag indicating if submitted ads must meet the exact duration requirement. The default setting is `false`. |

### Duration range

The `podconfig.durationrangesec` is an array of integers representing the ad slot durations within the ad pod:

```
podconfig.durationrangesec = [15, 30];
```

> [!NOTE]
> If `requireexactduration` is set to `false`, then the ad's duration will be rounded up to the closest value in the `durationrangesec` array. The minimum bid duration is zero. Using the setting above, a 10-second bid would be rounded to fifteen seconds and an 18-second bid rounded to thirty.
>
> If `requireexactduration` is set to `true`, then only the ads that are the exact duration match to the `durationrangesec` array will be allowed. Again, using the example above, an ad submitted with a duration of fifteen seconds would be allowed, whereas an ad submitted with an 18-second duration would be rejected.

### General Data Protection Regulation (GDPR)

GDPR is a data privacy law enacted by the European Union. The goal of GDPR is to provide more stringent data privacy and security measures and more user-friendly disclosures and reporting on data protection practices.

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `user.gdpr` | Optional | Object | Container object describing the GDPR settings. |
| `gdpr.consentrequired` | Optional | Boolean | Flag indicating if GDPR is in effect. |
| `gdpr.consentstring` | Optional | String | A string, comprised of a series of numbers, which identifies the consent status of an ad tech vendor. |

### Price granularity

| Parameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `precision` | Optional | Integer | If precision is omitted, it will default to. See [Prebid documentation](https://docs.prebid.org/adops/price-granularity.html#price-granularity-explained). |
| `ranges` | Optional | Object | Container object describing the price granularity range. |

### Price granularity ranges

| Patameter | Scope | Type | Description |
|:---|:---|:---|:---|
| `max` | Optional | Float | The maximum length of the range. |
| `increment` | Optional | Float | The amount to increment through the range. |

## Response

Demand partners returns a response to the ad pod bid request in JSON format.

### Ad pod

| Parameter | Type | Description |
|:---|:---|:---|
| `adpods` | Object | Container object describing the Prebid demand partner responses for each `ad pod` sent in the original request. |
| `adpods[...].podid` | Integer | The id of the corresponding `ad pod`. |
| `adpods[...].targeting` | Object | Container object describing the prebid demand partner bids for this pod translated into targeting keys. For more detail on the `adpods.targeting` object, see the [table](#ad-pod-targeting) below. |

### Ad pod targeting

| Parameter | Type | Description |
|:---|:---|:---|
| `hb_deal` | String | Deal code or external deal id from the associated bid. Omitted if this bid is not associated with a deal. |
| `hb_pb` | String | The price bucket targeting key. The price bucketing model is defined by the pricegranularity from the request and configuration. The price bucket targeting key-value represents the rounded bid price. |
| `hb_pb_cat_dur` | String | The value of this key represents the concatenation of three values, the price bucket (), the creative category code, and the duration of the video creative. <br>For example:<br>`adpods[...]targeting.hb_pb`<br><br>This would indicate a price bucket of $12.00 (if the currency was in US dollars), a category code of 135 (in the primary ad server's domain, such as Freewheel or Google Ad Manager), and a duration of thirty seconds.<br><br>**Note:** This key-value must be unique across all bids corresponding to its corresponding ad pod. If there are two identical `hb_pb_cat_dur` values, ImpBus will eliminate one of the bids. |
| `hb_cache_id` | String | The Prebid cache id. This value maps to the rendered video content.<br><br>**Note:**<br>This key-value must be unique across all bids across all pods in a single request. The actual creative cache key will be a concatenation of this value and `hb_pb_cat_dur`. Since `hb_pb_cat_dur` must be unique across all bids this guarantees that the actual creative cache key will be unique. The actual cache key will be created using macros, as illustrated below:<br>`${ hb_pb_cat_dur }_${ hb_cache_id }`<br><br>The `hb_cache_id` value will be the same for every entry in `targeting[...]` in a single response. |
| `hb_cache_host` | String | The host name of the cache where the creative associated with this bid is stored. |

## Example

### Code example

```
curl -X "POST" -H "Content-Type: application/json" -d 

{
   "podconfig":{
      "durationrangesec":[
         30
      ],
      "requireexactduration":false,
      "pods":[
         {
            "podid":1,
            "adpoddurationsec":60,
            "placementid":14997137
         }
      ]
   },
   "site":{
      "page":"https://www.foobar.com/1234.md"
   },
   "user":{
      "yob":1982,
      "gender":"M"
   },
   "device":{
      "ua":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13 (KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
      "ip":"123.145.167.10",
      "devicetype":1,
      "ifa":"AA000DFE74168477C70D291f574D344790E0BB11"
   },
   "includebrandcategory":{
      "primaryadserver":1
   },
   "video":{
      "w":640,
      "h":480,
      "mimes":[
         "video/mp4"
      ],
      "protocols":[
         2,
         3
      ]
   },
   "content":{
      "episode":6,
      "title":"episodeName",
      "series":"TvName",
      "season":"season3",
      "len":900,
      "livestream":false,
      "genre":"comedy",
      "program_type":"series",
      "contentrating":"GA",
      "id":"ABCDEF12345678",
      "language":"EN",
      "network":"XTV",
      "channel":"XandrTV",
      "airtime":1657827359,
      "album":"showads",
      "cat":[
         "IAB1-7",
         "IAB19-18"
      ],
      "context":1,
      "embeddable":false,
      "isrc":"USXND2100112",
      "keywords":"prizeworth=5000,gameshow,edu=true",
      "prodq":"prosumer",
      "qagmediarating":1,
      "sourcerelationship":true,
      "url":"https://tvname.xandrtv.com/overview",
      "userrating":"4/5 recommended",
      "producer":{
         "id":"xndtv5401",
         "name":"XandrTV",
         "cat":[
            "IAB1-7",
            "IAB19-18"
         ],
         "domain":"xandrtv.com"
      },
      "data":[
         {
            "id":"xandr",
            "name":"xndtv",
            "segment":[
               {
                  "id":"11854",
                  "name":"repeat viewers",
                  "value":"973"
               }
            ]
         }
      ]
   },
   "pricegranularity":{
      "precision":2,
      "ranges":[
         {
            "max":30.00,
            "increment":1.00
         }
      ]
   }
}
```

## Related topic

[PSP supported formats and integration paths](../monetize/prebid-server-premium-supported-formats-and-integration-paths.md)
