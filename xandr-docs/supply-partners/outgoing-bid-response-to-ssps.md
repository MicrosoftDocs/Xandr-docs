---
title: Outgoing Bid Response to SSPs
description: Learn about different fields like Native object, Bid object, Asset object, that Xandr supports in the bid response object. 
ms.date: 10/28/2023
---

# Outgoing bid response to SSPs

> [!NOTE]
> This describes the Xandr integration of the
> [OpenRTB 2.4 protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

Xandr will send a Bid Response after it receives a [Bid Request](incoming-bid-request-from-ssps.md) from an SSP. The Bid Response will include the bidder's bid (`price`) and chosen creative (`creative_id`). This creative will be served if the bid is ultimately accepted by the ad server. Multiple bids within the Bid Response are supported.

## Implementation

Xandr currently supports the following fields in the bid response object:

**Bid response object**

| Field | Type | Description |
|--|--|--|
| `bidid` | string | The bid response ID to assist tracking for bidders. This value is chosen by the bidder for cross-reference. <br> **Note**: This is used only to populate the macro `${AUCTION_BID_ID}`. We do not store this information. |
| `cur` | string | The bid currency using ISO-4217 alphabetic codes. If omitted, default is USD. Also used for the macro `${AUCTION_CURRENCY}` in the win notify URL and creative or pixel payload. |
| `id` | string | **Required**: The ID of the bid request to which this is a response. |
| `seatbid` | array of objects |Required if a bid is made: Used for identifying seatbid objects. See [Seat Bid Object](#seat-bid-object) for more information. |
| `ext` |  |Used for identifying platform-specific extensions to OpenRTB for the bid response object. |

### Seat bid object

By default, Xandr will return a single `seatbid` object in the bid response. Xandr can also return multiple `seatbid` objects (multiple bids). Please contact your account representative for more details.

Xandr supports the following fields in the `seatbid` object:

> [!NOTE]
> We will not group bids by their seat ids. For example, if there are three bids from the same seat, we will send three seatbid objects.

| Field | Type | Description |
|--|--|--|
| `bid` | array of objects | An array of bid objects; each bid object relates to an Impression Object in the [Bid Request](incoming-bid-request-from-ssps.md). Note that one Impression Object can have many bid objects. See [Bid Object](#bid-object) for more information. |
| `seat` | string | Either the `seat_id` passed in the bid request query string (if one was provided) or the Xandr buyer `member_id`. |

### Bid object

| Field | Type | Description |
|--|--|--|
| `adid` | string | The Xandr creative ID, viewable via the API using the [Creative Service](../bidders/creative-service.md). This ID references the actual ad to be served if the bid wins. |
| `adm` | string | The rendered creative markup to be delivered. Native creatives are returned in this field as a JSON-encoded string. See [Native Object](#native-object) below.<br>**Note**: SSPs can opt to have markup delivered to the win notification (nurl) instead by `specifying` "markup_delivery": 1 in the bid request. |
| `adomain` | array of strings | A list of URLs associated with the brand of the creative in the bid. |
| `attr` | array of integers | Set of attributes describing the creative. Refer to section 5.3 of the IAB specification for a list of attributes. |
| `cat` | array of strings | IAB content categories of the creative. Refer to section 5.1 of the IAB specification for a list of content categories. |
| `cid` | string | The Xandr buyer's member ID. |
| `crid` | string | The Xandr creative ID, viewable via the API using the [Creative Service](../bidders/creative-service.md). This ID references the actual ad to be served if the bid wins. |
| `dealid` | string | The seller's deal ID (Xandr deal code) from the deal object in the [Bid Request](incoming-bid-request-from-ssps.md), if this bid relates to a deal.<br>If the deal does not have a Xandr deal code then we will omit this field. |
| `ext` | object | Used for identifying Xandr-specific extensions to the OpenRTB bid response. See [Extension Object](#extension-object) below. |
| `h` | integer | The height of the creative, in pixels. |
| `id` | string | The unique ID for the bid object; this is chosen by Xandr for tracking and debugging purposes. |
| `impid` | string | The ID of the impression object to which this bid applies. Will match the `id` field from the bid request's `impression` object. |
| `iurl` | string | A preview URL for the creative in the bid. |
| `price` | float | The bid price expressed in CPM.<br>**Note**: Although this value is a float, OpenRTB strongly suggests using integer math for accounting to avoid rounding errors. |
| `w` | integer | The width of the creative, in pixels. |

### Bid extension object

We support the following fields in the `bid.ext` object:

| Field | Type | Description |
|--|--|--|
| `dsa` | object | Extension for DSA transparency information.|

### DSA extension object

| Attribute | Type | Description |
|:---|:---|:---|
| `behalf` | string  | Advertiser Transparency: Free UNICODE text string with a name of whose behalf the ad is displayed. Maximum 100 characters. |
| `paid` | string | Advertiser Transparency: Free UNICODE text string of who paid for the ad. Must always be included even if it's the same as what is listed in the behalf attribute. Maximum 100 characters.|
|transparency| array of object|Array of objects of the entities that applied user parameters and the parameters they applied. |
|adrender |integer |Flag to indicate that buyer/advertiser will render their own DSA transparency information inside the creative. <br> `0` = buyer/advertiser will not render<br> `1` = buyer/advertiser will render.|

### Object: Transparency

| Attribute | Type | Description |
|:---|:---|:---|
| `domain` | string  | Domain of the entity that applied user parameters.|
| `params` | array of integer | Array of buy-side applied user parameter targeting (using [the list provided by DSA Transparency Taskforce](https://github.com/InteractiveAdvertisingBureau/openrtb/diffs/0?base_sha=7751c1fc24cee4f81633dc687c41b5bd26cb9bbb&branch=1e1d5ad36c07bc8a41c97ac5e8113df91d3f95ca&head_user=lamrowena&name=1e1d5ad36c07bc8a41c97ac5e8113df91d3f95ca&pull_number=152&qualified_name=1e1d5ad36c07bc8a41c97ac5e8113df91d3f95ca&sha1=7751c1fc24cee4f81633dc687c41b5bd26cb9bbb&sha2=1e1d5ad36c07bc8a41c97ac5e8113df91d3f95ca&short_path=5ab9e62&unchanged=expanded&w=false#user_parameters)). Include support for multiple vendors who may add their own user-targeting parameters. |

Sample  OpenRTB 2.6 Bid Response with DSA transparency:

```
{ 
    "id": "1234567890", 
    "bidid": "abc1123", 
    "seatbid": [ 
        { 
            "seat": "512", 
            "bid": [ 
                { 
                    "id": "1", 

                    "nurl": "http://adserver.com/winnotice?impid=102", 
                    "iurl": "http://adserver.com/pathtosampleimage", 
                    "adomain": [ 
                        "advertiserdomain.com" 
                    ], 
                    "ext": { 
                        "dsa": { 
                            "behalf": "Advertiser", 
                            "paid": "Advertiser", 
                            "transparency": { 
                                "domain": "dsp1domain.com", 
                                "params": [ 
                                    1, 
                                    2 
                                ] 
                            }, 
                            "adrender": 1 
                        } 
                    } 
                } 
            ] 
        } 
    ] 
} 
```

### Native object

Xandr supports the following fields to define a native object to be included as a JSON-encoded string in the `adm` field of the `bid` object. Refer to [Example Native Creative Bid Response](#native-creative-bid-response) for an example of formatting this string.

| Field | Type | Description |
|--|--|--|
| `assets` | array of objects | (Required) List of the native ad's assets. See [Asset Object](#asset-object) below.<br> |
| `imptrackers` | array of strings | Array of impression-tracking URLs expected to return a 1x1 image or HTTP 204 (No Content) response. This is typically passed only when using third-party trackers.<br>**Note**: This field is only returned for Native version 1.1. |
| `jstracker` | string | Optional JavaScript impression tracker. This is a valid HTML , Javascript is already wrapped in `script` tags. It should be executed at impression time where it can be supported.<br>**Note**: This field is only returned for Native version 1.1. |
| `link` | object | (Required) The default destination link for the native ad. Each individual asset can have its own link object, which applies if that asset is clicked. If an individual asset link does not have a link object, the parent link object is used. See [Link Object](#link-object) below. |
| `privacy` | string | If support was indicated in the request, URL of a page informing the user about the buyer’s targeting activity. |
| `ver` | integer | The version of the Native Markup in use. This is only returned for Native version 1.2 and later. |

### Asset object

Xandr supports the following fields to define one or more native `asset` objects to be included as a JSON-encoded string as part of the `native` object in the `adm` field of the `bid` object. Refer to [Example Native Creative Bid Response](#native-creative-bid-response) for an example of formatting this string.

| Field | Type | Description |
|--|--|--|
| `data` | object | The data object, for data assets, such as ratings, prices, and so on. See [Data Object](#data-object) below. |
| `id` | integer | (Required) The unique asset ID. Must match an asset ID in the request. |
| `img` | object | The image object, for image assets. See [Image Object](#image-object) below. |
| `link` | object | The link object for individual assets, which applies if that asset is clicked. If there is no link object for an asset, the parent link object is used. See [Link Object](#link-object) below. |
| `required` | integer | Set to 1 if bidder requires asset to be displayed.<br> |
| `title` | object | The title object, for title assets. See [Title Object](#title-object) below. |
| `video` | object | The video object, for video assets. Note that in-stream video ads are not part of native objects. Native ads may be contain a video as the creative itself. See [Video Object](#video-object) below. |

### Title object

Used to define a title asset in a native object.

| Field | Type | Description |
|--|--|--|
| `text` | string | (Required) The text for a title element. |

### Image object

Used to define a image asset in a native object. Used for all image elements of the native ad, such as icons, main image, and so on.

| Field | Type | Description |
|--|--|--|
| `h` | integer | (Recommended) The height of the image, in pixels. |
| `url` | string | (Required) The URL of the image asset. |
| `w` | integer | (Recommended) The width of the image, in pixels. |

### Data object

Used to define a data asset in a native object. Used for all miscellaneous elements in a native ad, such as ratings, price, review count, downloads, and so on.

| Field | Type | Description |
|--|--|--|
| `label` | string | An optional formatting string name of the data type. |
| `value` | string | The formatted string of data to be displayed (such as `"5 stars"` or `"$10"`). |

### Video Object

Used to define a video asset. Contains the value of a conforming VAST tag.

| Field | Type | Description |
|--|--|--|
| `vasttag` | string | (Required) The VAST XML for this asset. |

### Link object

Used to define the link for a native asset. When clicked, the user is taken to the location of the link. Can be defined for individual assets as well as for the parent native object, which is used as the default for assets when no unique asset link is defined.

| Field | Type | Description |
|--|--|--|
| `clicktrackers` | Array of strings | Array of third-party tracking URLs to be fired when the link is clicked. |
| `fallback` | string | A fallback URL to be used if the URL is not supported by the device. |
| `url` | string | (Required) The landing URL for the clickable link. |

### Event trackers response object

Xandr supports the following fields in the `event trackers response` object (Native 1.2 only):

| Field | Type | Description |
|--|--|--|
| `event` | integer | Type of event available for tracking. Supported values are:<br>` 1: impression` - Impression<br>`2: viewable-mrc50` - Viewable impression using MRC definition at 50% in view for 1 second<br>`3: viewable-mrc100` - Viewable impression using MRC definition at 100% in view for 1 second (ie GroupM standard)<br>`4: viewable-video50` - Viewable impression for video using MRC definition at 50% in view for 2 seconds |
| `method` | integer | Type of tracking requested for the given event.<br>Supported values are:<br>`1: img` - Img-pixel tracking - URL provided will be inserted as a 1x1 pixel at the time of the event<br>`2: js` - Javascript-based tracking - URL provided will be inserted as a js tag at the time of the event |
| `url` | string | The URL of the `img` or `js`. |

### Extension Object

Xandr supports a single object in the `ext` object to support Xandr-specific extensions:

| Field | Type | Description |
|--|--|--|
| `appnexus` | object | Specifies the Xandr-specific extensions to the OpenRTB bid response. See [AppNexus Object](#appnexus-object) below. |

### AppNexus Object

Xandr supports the following fields in the `appnexus` extension object:

| Field | Type | Description |
|--|--|--|
| `auction_id` | integer | Specifies the Xandr auction ID. |
| `bid_ad_type` | int | Specifies the ad type of the winning bid. Possible values:<br>- 0: banner<br>- 1: video<br>- 2: audio<br>- 3: native |
| `bidder_id` | integer | Specifies the Xandr ID that corresponds to the winning bid's bidder (sometimes referred to as a DSP). |
| `brand_id` | integer | Specifies the Xandr brand ID. |
| `exclusive` | boolean | Indicates whether the bid is exclusive depending on the priority.<br>- If 0, then bid is not exclusive<br>- If 1, then bid is exclusive<br>**Note**: This field is only enabled for specific clients. Please reach out to your account representative for this feature. |
| `ranking_price` | double | Specifies the pCPM bid value for GDLI bids.<br>**Note**: This field is only enabled for specific clients. Please reach out to your account representative for this feature. |

## Examples

### Banner creative bid response

``` 
 {
    "id": "rELYJA1ynf",
    "seatbid": [{
            "bid": [{
                "id": "1122797001398827907",
                "impid": "rELYJA1ynf",
                "price": 1.443626,
                "adid": "41112643",
                "adm": "<a href=\"https://nym1.ib.adnxs.com/click?rA8o_BZ9z-sDyj8Fxn3PwJAAAAAAAPA_rA8o_BcZ9z-sDy8Fxn3PxK8gLrAPTk9oPSfTXFhkVBk_7xWAAAAAPIYXwAMDQAADA0AAAIAAABDVHMCEM8NAAAAAQBVU0QAVVNEACwB-gA_WQAAiLABAQMAAQAJAKkAhCGkZgAAAAA./cnd=%21NQkicgj8x9UFEMOozRMYkJ43IAQoiobAmgE./referrer=ebay.com/clickenc=https%3A%2F%2Fwww.appnexus.com\" target=\"_blank\"><img width=\"300\" height=\"250\" style=\"border-style: none\" src=\"https://dummyimage.com/300x250/363534/FF8700&text=Banner%20Ad\"/></a><script>!function(){function e(e,t){return\"function\"==typeof __an_obj_extend_thunk?__an_obj_extend_thunk(e,t):e}function t(e,t){\"function\"==typeof __an_err_thunk&&__an_err_thunk(e,t)}function n(e){\"function\"==typeof __an_redirect_thunk?__an_redirect_thunk(e):document.write('<script language=\"javascript\" src=\"'+e+'\"></scr'+'ipt>')};var r=function(e){this.rdParams=e};r.prototype={constructor:r,walkAncestors:function(e){try{if(!window.location.ancestorOrigins)return;for(var t=0,n=window.location.ancestorOrigins.length;n>t;t++)e.call(null,window.location.ancestorOrigins[t],t)}catch(r){\"undefined\"!=typeof console}return[]},walkUpWindows:function(e){var t,n=[];do try{t=t?t.parent:window,e.call(null,t,n)}catch(r){return\"undefined\"!=typeof console,n.push({referrer:null,location:null,isTop:!1}),n}while(t!==window.top);return n},getPubUrlStack:function(e){var n,r=[],o=null,i=null,c=null,d=null,a=null,s=null,u=null;for(n=e.length-1;n>=0;n--){try{c=e[n].location}catch(l){\"undefined\"!=typeof console,t(l,\"AnRDModule::getPubUrlStack:: location\")}if(c)i=encodeURIComponent(c),r.push(i),u||(u=i);else if(0!==n){d=e[n-1];try{a=d.referrer,s=d.ancestor}catch(l){\"undefined\"!=typeof console,t(l,\"AnRDModule::getPubUrlStack:: prevFrame\")}a?(i=encodeURIComponent(a),r.push(i),u||(u=i)):s?(i=encodeURIComponent(s),r.push(i),u||(u=i)):r.push(o)}else r.push(o)}return{stack:r,detectUrl:u}},getLevels:function(){var e=this.walkUpWindows(function(e,n){try{n.push({referrer:e.document.referrer||null,location:e.location.href||null,isTop:e===window.top})}catch(r){n.push({referrer:null,location:null,isTop:e===window.top}),\"undefined\"!=typeof console,t(r,\"AnRDModule::getLevels\")}});return this.walkAncestors(function(t,n){e[n].ancestor=t}),e},getRefererInfo:function(){var e=\"\";try{var n=this.getLevels(),r=n.length-1,o=null!==n[r].location||r>0&&null!==n[r-1].referrer,i=this.getPubUrlStack(n);e=this.rdParams.rdRef+\"=\"+i.detectUrl+\"&\"+this.rdParams.rdTop+\"=\"+o+\"&\"+this.rdParams.rdIfs+\"=\"+r+\"&\"+this.rdParams.rdStk+\"=\"+i.stack+\"&\"+this.rdParams.rdQs}catch(c){e=\"\",\"undefined\"!=typeof console,t(c,\"AnRDModule::getRefererInfo\")}return e}};var o=function(n){var o=\"\";try{n=e(n,0);var i=e(new r(n),1);return i.getRefererInfo()}catch(c){o=\"\",\"undefined\"!=typeof console,t(c,\"AnRDModule::executeRD\")}return o};;var s=\"https://nym1.ib.adnxs.com/rd_log?e=wqT_3QKvBPBCJgIAAAIA1gAFCOT-87UFEJL4gtSLuM-cPRig6f_slK7YyFAgASotCawPKPwXGfc_EawPKPwXGfc_GQAAAAAAAPA_IRESACkRCagw8rH8AjiMGkCMGkgCUMOozRNYkJ43YABov7IBeIjhAoABAYoBA1VTRJIBAQbwUpgBrAKgAfoBqAEBsAEAuAEBwAEDyAEA0AEJ2AEA4AEB8AEAigI6dWYoJ2EnLCA3OTk1MTksIDE0NTUyMjY3MjQpO3VmKCdyJywgNDExMTI2NDMsMh4A8GaSAq0BIU1DdUNtQWo4eDlVRkVNT296Uk1ZQUNDUW5qY3dBRGdBUUFSSWpCcFE4ckg4QWxnQVlQX19fXzhQYUFCd0FYZ0JnQUVCaUFFQmtBRUJtQUVCb0FFQnFBRURzQUVBdVFFQUFBAQPIRHdQOEVCckE4b19CY1o5el9KQWM3QW9yNDNoZkFfMlFIdERiNHdtU3JtUC1BQkFQVUJBATdgSmdDaW9iQW1nR2dBZ0EumgIlIU5Ra2ljZzawABxrSjQzSUFRbwks8HRFLtgCnEPgAtvyJeoCCGViYXkuY29tgAMAiAMBkAMAmAMUoAMBqgMAsAMAuAMAwAOsAsgDANgDpg7gAwDoAwD4AwOABACSBAkvb3BlbnJ0YjKYBACiBA8yMDcuMjM3LjE1MC4yNDaoBACyBAYIABAAGAC4BAA.&s=f3c3b6704b20f2baa8e488269a5810b3cc0ae6f1&referrer=ebay.com\";s+=\"&\"+o({rdRef:\"bdref\",rdTop:\"bdtop\",rdIfs:\"bdifs\",rdStk:\"bstk\",rdQs:\"\"}),n(s)}();</script><script type=\"application/javascript\">;document.write('<div lnttag=\"v;tv=view5-1;d=300x250;s=1770882;samp=1;vc=iab;url=ebay.com;cb=' + encodeURIComponent('https://nym1.ib.adnxs.com/vevent?e=wqT_3QKvBPBCJgIAAAIA1gAFCOT-87UFEJL4gtSLuM-cPRig6f_slK7YyFAgASotCawPKPwXGfc_EawPKPwXGfc_GQAAAAAAAPA_IRESACkRCagw8rH8AjiMGkCMGkgCUMOozRNYkJ43YABov7IBeIjhAoABAYoBA1VTRJIBAQbwUpgBrAKgAfoBqAEBsAEAuAEBwAEDyAEA0AEJ2AEA4AEB8AEAigI6dWYoJ2EnLCA3OTk1MTksIDE0NTUyMjY3MjQpO3VmKCdyJywgNDExMTI2NDMsMh4A8GaSAq0BIU1DdUNtQWo4eDlVRkVNT296Uk1ZQUNDUW5qY3dBRGdBUUFSSWpCcFE4ckg4QWxnQVlQX19fXzhQYUFCd0FYZ0JnQUVCaUFFQmtBRUJtQUVCb0FFQnFBRURzQUVBdVFFQUFBAQPIRHdQOEVCckE4b19CY1o5el9KQWM3QW9yNDNoZkFfMlFIdERiNHdtU3JtUC1BQkFQVUJBATdgSmdDaW9iQW1nR2dBZ0EumgIlIU5Ra2ljZzawABxrSjQzSUFRbwks8HRFLtgCnEPgAtvyJeoCCGViYXkuY29tgAMAiAMBkAMAmAMUoAMBqgMAsAMAuAMAwAOsAsgDANgDpg7gAwDoAwD4AwOABACSBAkvb3BlbnJ0YjKYBACiBA8yMDcuMjM3LjE1MC4yNDaoBACyBAYIABAAGAC4BAA.&s=f3c3b6704b20f2baa8e488269a5810b3cc0ae6f1&referrer=ebay.com') + '\" style=\"display:none\"><\\/div><sc' + 'ript type=\"text/javascript\" async=\"true\" src=\"https://cdn.adnxs.com/v/s/33/trk.js\"><\\/scr' + 'ipt>');</script><img src=\"https://nym1.ib.adnxs.com/openrtb_win?e=wqT_3QKvBPBCJgIAAAIA1gAFCOT-87UFEJL4gtSLuM-cPRig6f_slK7YyFAgASotCawPKPwXGfc_EawPKPwXGfc_GQAAAAAAAPA_IRESACkRCagw8rH8AjiMGkCMGkgCUMOozRNYkJ43YABov7IBeIjhAoABAYoBA1VTRJIBAQbwUpgBrAKgAfoBqAEBsAEAuAEBwAEDyAEA0AEJ2AEA4AEB8AEAigI6dWYoJ2EnLCA3OTk1MTksIDE0NTUyMjY3MjQpO3VmKCdyJywgNDExMTI2NDMsMh4A8GaSAq0BIU1DdUNtQWo4eDlVRkVNT296Uk1ZQUNDUW5qY3dBRGdBUUFSSWpCcFE4ckg4QWxnQVlQX19fXzhQYUFCd0FYZ0JnQUVCaUFFQmtBRUJtQUVCb0FFQnFBRURzQUVBdVFFQUFBAQPIRHdQOEVCckE4b19CY1o5el9KQWM3QW9yNDNoZkFfMlFIdERiNHdtU3JtUC1BQkFQVUJBATdgSmdDaW9iQW1nR2dBZ0EumgIlIU5Ra2ljZzawABxrSjQzSUFRbwks8HRFLtgCnEPgAtvyJeoCCGViYXkuY29tgAMAiAMBkAMAmAMUoAMBqgMAsAMAuAMAwAOsAsgDANgDpg7gAwDoAwD4AwOABACSBAkvb3BlbnJ0YjKYBACiBA8yMDcuMjM3LjE1MC4yNDaoBACyBAYIABAAGAC4BAA.&s=f3c3b6704b20f2baa8e488269a5810b3cc0ae6f1&referrer=ebay.com&pp=${AUCTION_PRICE}\" width=\"1\" height=\"1\" border=\"0\">",
                "iurl": "https://nym1.ib.adnxs.com/cr?id=41112643",
                "cid": "3140",
                "crid": "41116499",
                "h": 250,
                "w": 300,
                "ext": {
                    "appnexus": {
                        "brand_id": 1,
                        "auction_id": 2211625207958125586
                    }
                }
            }],
            "seat": "3344"
        }
    ],
    "bidid": "2134167541719148457",
    "cur": "USD"
}
```

### VAST creative bid response

``` 
 {
    "id": "993af0d9-4ecb-4ac7-ac99-6bac442d9774",
    "seatbid": [{
        "bid": [{
            "cid": "362",
            "iurl": "https://nym1-ib.adnxs.com/cr?id=115601913",
            "adomain": [
                "ca.com"
            ],
                        "adm": "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><VAST version=\"3.0\"><Ad id=\"115601913\"><Wrapper>...</Wrapper></Ad></VAST>",
            "adid": "115601913",
            "ext": {
                "appnexus": {
                    "brand_id": 29148,
                    "auction_id": 4072930007301496300,
                    "bidder_id": 2,
                    "bid_ad_type": 1,
                    "prebid_server_bid": false
                }
            },
            "w": 1,
            "h": 1,
            "cat": [
                "IAB19-9",
                "IAB19-11",
                "IAB19-12",
                "IAB10-6",
                "IAB19-29",
                "IAB19-28",
                "IAB19-5",
                "IAB19-17",
                "IAB19-10",
                "IAB19"
            ],
            "crid": "115601913",
            "id": "1255325421669335693",
            "impid": "1",
            "price": 1.743896
        }],
        "seat": "362"
    }],
    "bidid": "3718090108021111485",
    "cur": "USD"
}
```

### Native creative bid response

``` 
{
        "bidid": "7056250063591570777",
        "cur": "USD",
        "id": "124476071019177977",
        "seatbid": [{
                "bid": [{
                        "adid": "49717777",
                        "adm": "{\"assets\":[{\"id\": 2,\"img\":{\"url\":\"https://cdn.adnxs.com/p/75/e7/9c/15/75e79c15d07b3548651ac638f7c87444.jpg\",\"w\": 800,\"h\": 800}},{\"id\": 1,\"title\":{\"text\":\"Still in search?\"}},{\"id\": 3,\"data\":{\"value\":\"Native\"}},{\"id\": 4,\"data\":{\"value\":\"Future is now!\"}}],\"link\":{\"url\":\"https://nym1-ib.adnxs.com/click?x8bGxsbGEkDsUbgehesPQOxRuB6F6w9AAAAAAAAAEUAAAAAAAAAUQHigAarFkkkWG3fXpZUyLXO3g0pZAAAAALiXsADtHwAAcgMAAAIAAADuofYClRgUAAAAAABVU0QAVVNEAAEAAQDzZQAAAAABAgUCAQAAALUAyCASkfAAAAA./pp=${AUCTION_PRICE}//cnd=%21XgmbpwjIyZoIEO7D2hcYlbFQIAAoADoJTllNMjoyOTQ5/bn=61950/test=1/referrer=https%3A%2F%2Fwww.example.com%2Fnl-nl%2F/clickenc=https%3A%2F%2Fwww.appnexus.com\"},\"imptrackers\":[\"https://nym1-ib.adnxs.com/openrtb_win?e=wqT_3QLlBfBM5QIAAAMA1gAFAQi3h6rKBRD4wIbQ2tjkpBYYm-7drtrSzJZzIAEqLQnHxsbGxsYSQBHsUbgehesPQBnsUbgehesPQCEAAAAAAAARQCkFCLAAFEAwuK_CBTjtP0DyBkgCUO7D2hdYlbFQYABo88tpeP7jA4ABAYoBA1VTRJIFBvBOmAEBoAEBqAEBsAEAuAECwAEFyAEC0AEJ2AEA4AEB8AEAigI5dWYoJ2EnLCA2MTA3MSwgMTQ5ODA1NTYwNyk7dWYoJ3InLCA0OTcxNzc0MjYeAPCHkgLtASFBQzVQaXdqSXlab0lFTzdEMmhjWUFDQ1ZzVkF3QURnQVFBQkk4Z1pRdUtfQ0JWZ0FZTE1EYUFCd0FIZ0FnQUVBaUFFQWtBRUJtQUVCb0FFQnFBRURzQUVBdVFIenJXcWtBQUFVUU1FQjg2MXFwQUFBRkVESkFRQUFBQUFBQVBBXzJRRQkMKEFEd1AtQUJBUFVCBREoSmdDQUtBQ0FMVUMFEARMMAkI8EZNQUNBTWdDQU9BQ0FPZ0NBUGdDQUlBREFaQURBSmdEQWFnRHlNbWFDTG9EQ1U1WlRUSTZNamswT0EuLpoCLSFYZ21icHdqSS7wAPD6bGJGUUlBQW9BRG9KVGxsTk1qb3lPVFE02AIA4AKO2z7qAh1odHRwOi8vd3d3LmV4YW1wbGUuY29tL25sLW5sL4ADAIgDAZADAJgDFKADAaoDAMADkBzIAwDYAwDgAwDoAwH4AwOABACSBAkvb3BlbnJ0YjKYBACiBAw3MS4yNDAuMTk5LjCoBOT8DbIECggAEAAYACAAMAC4BADABADIBADSBAlOWU0yOjI5NDjaBAIIAOAEAPAE7sPaF4gFAZgFBKAF____________AaoFEjEyNDQ3NjA3MTAxOTE3Nzk3OMAFAMkFAAAAAAAA8D_SCQkJAAAAAAAAAAA.&s=249717074fb86b5ca693d6607d76a0eb3477660e&referrer=https%3A%2F%2Fwww.example.com%2Fnl-nl%2F&pp=${AUCTION_PRICE}&\"]}",
                        "adomain": [
                                "appnexus.com"
                        ],
                        "cat": [
                                "IAB3-1"
                        ],
                        "cid": "882",
                        "crid": "49717777",
                        "ext": {
                                "appnexus": {
                                        "auction_id": 1605976119792738444,
                                        "bidder_id": 2,
                                        "brand_id": 86444
                                }
                        },
                        "id": "1633865541179659394",
                        "impid": "1",
                        "iurl": "https://nym1-ib.adnxs.com/cr?id=49717777",
                        "price": 3.99
                }],
                "seat": "882"
        }]
}
```
