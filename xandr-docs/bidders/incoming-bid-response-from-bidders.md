---
title: Incoming Bid Response from Bidder
description: This article explains the process of implementing and receiving the bid response from bidder.
ms.date: 06/10/2025
---

# Incoming bid response from bidder

> [!WARNING]
> This describes the integration of the [OpenRTB 2.4 protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

A bidder will send a bid response after it receives a [Bid Request](./outgoing-bid-request-to-bidders.md) from the impression bus. The bid response will include the bidder's bid (`price`) and chosen creative (`creative_id` or `creative_code`). This creative will be served if the bid is ultimately accepted by the ad server. Multiple bids within the bid response are encouraged.

## Implementation

Refer to the following links to locate the objects that you need more information on.

[Bid response object](incoming-bid-response-from-bidders.md#bid-response-object) | [Seat Bid Object](incoming-bid-response-from-bidders.md#seat-bid-object)| [Bid Object](incoming-bid-response-from-bidders.md#bid-object) | [Bid Extension Object](incoming-bid-response-from-bidders.md#bid-extension-object) | [AppNexus Object](incoming-bid-response-from-bidders.md#appnexus-object)| [Custom Macro Object](incoming-bid-response-from-bidders.md#custom-macro-object)| [Bid Payment Type Object](incoming-bid-response-from-bidders.md#bid-payment-type-object)|

Xandr expects all calls to return HTTP code 200 except for an empty bid response (no bid), which will return HTTP code 204. We currently support the following fields in the bid response object.

### Bid response object

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | **Required**: The ID of the bid request to which this is a response. |
| `seatbid` | array of objects | **Required if a bid is made**: Used for identifying seatbid objects. See [Seat Bid Object](#seat-bid-object) for more information. |
|`bidid` | string | The bid response ID to assist tracking for bidders. This value is chosen by the bidder for cross-reference.<br><br> **Note**: This is used only to populate the macro `${AUCTION_BID_ID}`. We do not store this information. |
| `cur` | string | The bid currency using ISO-4217 alphabetic codes. If omitted, default is USD. Also used for the macro `${AUCTION_CURRENCY}` in the win notify URL and creative or pixel payload. |
| `ext` | string | Used for identifying platform-specific extensions to the OpenRTB bid response object.|

### Seat bid object

Xandr supports the following fields in the `seatbid` object, each of which represents a different bidder seat and contains one or more individual bids.

| Field | Type | Description |
|:---|:---|:---|
| `bid` | array of objects | **Required**: An array of bid objects; each bid object relates to an Impression Object in the [Bid Request](./outgoing-bid-request-to-bidders.md).<br><br>**Note**: If supported by an exchange, one Impression Object can have many bid objects. See [Bid Object](#bid-object) for more information. |
| `seat` | string | **Required**: The ID of the member whose creative is chosen by the bidder and corresponds to the Xandr `member_id`. Also used to populate the `${AUCTION_SEAT_ID}` macro in the win notify URL and creative or pixel payload.<br><br>**Note**: <br> - For DSPs migrated to Buyer Seat ID bidding, they can use buyer IDs native to their own systems. These identifiers will be registered as Seat Codes in Xandr systems.<br> - This feature is currently in Closed Beta. If you are interested in participating, reach out to your Xandr representative. |

### Bid object

| Field | Type | Description |
|:---|:---|:---|
| `id` | string | **Required**: The ID for the bid object; this is chosen by the bidder for tracking and debugging purposes. Useful when multiple bids are submitted for a single impression for a given seat. |
| `impid` | string | **Required**: The ID of the impression object to which this bid applies. Should match the `id` field from the bid request's impression object. Can be used to populate the `${AUCTION_IMP_ID}` macro. |
| `price` | float | **Required**: The bid price expressed in CPM. Also used to populate the `${AUCTION_PRICE}` macro.<br><br>If the `bid_payment_type` is not set to `"Impression"`, then price will be the eCPM price for the bid, and the `payment_type_price` will be used to populate the `${{AUCTION_PRICE} macro.PRICE}` macro.<br><br>**Note**: `bid_payment_type` is not enabled for all clients. Reach out to your account representative for this feature.<br><br>**Warning**: Although this value is a float, OpenRTB strongly suggests using integer math for accounting to avoid rounding errors. |
| `adid` | string | The Xandr creative ID, viewable via the API using the [Creative Service](./creative-service.md). This ID references the actual ad to be served if the bid wins. Can be used to populate the $`{AUCTION_AD_ID}` macro. If both `adid` and `crid` are passed, `adid` takes precedence. |
| `nurl` | string | The win notify URL, which is dropped as a pixel into the web browser or SDK. Our server pings this URL when it receives a client-side notification from the device, which indicates that we won the auction. Responses will be sent server side. This occurs at the same time when we record the impression. The max length is 2000 characters with macros expanded.<br><br>The following macros are supported in the notify URL:<br>`${AUCTION_ID}` - Xandr `auction_id_64`<br>`${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response<br>`${AUCTION_IMP_ID}` - ID of the impression, from the `impid` field in the bid object of the `seatbid` object<br>`${AUCTION_SEAT_ID}` - ID of the winning seat, from the `seat` field in the `seatbid` object<br>`${AUCTION_AD_ID}` - ID of the buyer's creative, from the `adid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_PRICE}` - Clearing price of the impression in the currency specified in the `cur` field in the bid response<br>`${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response<br>`${CREATIVE_CODE}` - The `code` field set on the `creative` object via the API when registering a creative<br>`${AN_PAYMENT_TYPE}` - ID of the payment type of bid specified in the `bid_payment_type` field of the bid response<br><br>**Note**: <br> - This macro is not enabled for all clients. Please reach out to your account representative for this feature.<br> - Only the macros in the preceding list can be used in the notify URL, no other macros are supported in the bid response. |
| `lurl` | string | **Warning**: This feature is currently in closed beta testing and is not available to all bidder integrations. If you would like to use this field in the bid response, please reach out to your account representative or file a support ticket at [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).<br><br>Loss notice URL called by Xandr when a bid is known to have been lost. Substitution macros may be included. Responses will be sent server side.<br><br>The following macros are supported in the loss notice URL.<br>`${AUCTION_ID}` - Xandr `auction_id_64`<br>`${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response<br>`${AUCTION_IMP_ID}` - ID of the impression, from the `impid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_SEAT_ID}` - ID of the winning seat, from the `seat` field in the `seatbid` object<br>`${AUCTION_AD_ID}` - ID of the buyer's creative, from the `adid` field in the `bid` object of the `seatbid` object<br>`${AUCTION_LOSS}` - Loss reason codes. For the full list of supported loss reason codes, see [Loss Reason Codes](./loss-reason-codes.md).<br>`${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cu`r field in the bid response<br>`${CREATIVE_CODE}` - The `code` field set on the `creative` object via the API when registering a creative.<br>`${AUCTION_MIN_TO_WIN}` - The lowest bid required to win the exchange’s auction, expressed in the same currency and units as the original bid. This feature requires separate enablement, contact your account representative or submit a support ticket if you're interested. |
| `crid` | string | The creative ID from the bidder's system. Used to reference a Xander creative based on the creative code as set via the [Creative Service](./creative-service.md). If both `adid` and `crid` are passed, `adid` takes precedence. |
| `cid` | string | The campaign ID from the bidder's system. Used for SSP reporting. |
| `dealid` | string | The deal ID from the `deal` object in the [Bid Request](./outgoing-bid-request-to-bidders.md), if this bid relates to a deal. |
| `ext` | object | Used for identifying platform-specific extensions to the OpenRTB bid response. See [Bid Extension Object](#bid-extension-object). |

### Bid extension object

We support the following fields in the `bid.ext` object:

| Field | Type | Description |
|:---|:---|:---|
| `dsa` | object | DSA object |

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

### AppNexus object

Xandr supports the following fields in the `appnexus` extension object.

| Field | Type | Description |
|:---|:---|:---|
| `custom_macros` | array of objects | Used for identifying `custom_macro` objects. See [Custom Macro Object](#custom-macro-object). |
| `min_price` | float | The minimum price to which the bid should be reduced in the second price auction. |
| `spend_protection_pixel_ids` | array of integers | **Deprecated**. |
| `custom_notify_data` | string | **Note**: This feature is not enabled by default. You must request to have this field enabled.<br><br>Use this field to pass information to the [Notify Request](./notify-request.md). The string is entered as freeform text and will be automatically URL- and/or cookie-encoded by ImpBus. |
| `click_url` | string | The click URL to be associated with the creative. This field should contain a redirect link. For example, [https://mydomain.com/abcd?redir=](https://mydomain.com/abcd?redir=) |
| `enable_bid_shading` | integer | **Note**: This field is in the process of being deprecated. It is set as **false** irrespective of the value sent in the bid response. |
| `bid_payment_type` | array of objects | **Note**: This feature is not enabled by default. You must request to have this field enabled.<br><br>Specifies the payment type for which the Bidder is bidding and will be billed. If omitted, then we will consider the payment type to be `'impression'`. |

### Custom macro object

Xandr supports the following fields in the `custom_macro` object of the `appnexus` extension object.

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | The name of the macro to be replaced in any of the creative's URLs (media, pixel, click, and so on). The name must be formatted as `${MACRO_NAME}` within the creative's URL or content.<br><br>**Note**: The custom macros are replaced AFTER system macros have been replaced. Refer to the [Creative Service](./creative-service.md) for more information. |
| `value` | string | The value used to replace the macro. Do not escape forward slashes. Even if the value is an integer, it must be placed within quotation marks (for example, `"42"`). The max length of the value is 550 characters. |

### Bid payment type object

Xandr supports the following fields in the `bid_payment_type` object of the `appnexus` extension object.

> [!NOTE]
> This feature is not enabled by default. You must request to have this field enabled.

| Field | Type | Description |
|:---|:---|:---|
| `payment_type` | integer | Specifies the payment type for which the Bidder is bidding and will be billed. If the payment type is not `'impression'`, then a billing notify URL must be set on the bid object. The currently supported values are -<br>`1`: Impression<br>`2`: Views - Standard Display<br>`6`: Views - Custom Display - 100pv1s<br>`8`: Views - Standard Video<br>`9`: Views - Custom Video - 100pv50pd<br><br>**Note**: Currently, for `"Viewable Impression"` bids, only USD bids are supported. |
| `price` | double | Specifies the bid price for the payment type. For the `'Viewable Impression'` payment type, the bid price will be vCPM. |

For more information, check the [Overview](./guaranteed-outcomes.md) page.

> [!NOTE]
> **Why we don't support the `adm` field?**
>
> Xandr works with members who care deeply about brand and reputation. For this reason, we are careful to ensure that the advertisements (creatives) that pass through our system are acceptable to all parties. For quality assurance, all creatives that serve on third-party inventory must be pre-registered using the [Creative Service](./creative-service.md).
>
> For these reasons, Xandr does not support the `adm` field (which allows bidders to pass in the actual ad markup). Instead, we construct the ad markup using the provided `adid` and `nurl` for win notification.

## Example for bid response

```
{
    "id": "4876290993254515176",
    "seatbid": [{
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "16",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}",
                "ext": {
                    "appnexus": {
                        "custom_macros": [{
                            "name": "dynamic_ad_markup",
                            "value": "dynamic.js"
                        }]
                    }
                }
            }

        ],
        "seat": "2739"
    }],
    "bidid": "1",
    "cur": "USD"
}
```

## Example for multi-bid response

```
Multi-bid response for one seat value
Option 1
{
    "id": "4876290993254515176",
    "seatbid": [{
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "16",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            },
            {
                "id": "2",
                "impid": "8278013996604245835",
                "price": 1,
                "adid": "22",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            },
            {
                "id": "3",
                "impid": "2345613996604245835",
                "price": 1,
                "adid": "23",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
        ],
        "seat": "2739"
    }],
    "bidid": "1",
    "cur": "USD"
}
Option 2
{
    "id": "4876290993254515176",
    "seatbid": [{
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "16",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            } 
        ],
        "seat": "2739"
    }],
    "seatbid": [{
        "bid": [ {
                "id": "2",
                "impid": "8278013996604245835",
                "price": 1,
                "adid": "22",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
        ],
        "seat": "2739"
    }],
    "seatbid": [{
       "bid": [ {
                "id": "3",
                "impid": "2345613996604245835",
                "price": 1,
                "adid": "23",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
        ],
        "seat": "2739"
    }],
    "bidid": "1",
    "cur": "USD"
}
Multi-bid response for multiple seat values
{
    "id": "4876290993254515176",
    "seatbid": [{
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "16",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
 
        ],
        "seat": "2739"
    },
    {
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "15",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
 
        ],
        "seat": "1234"
    },
    {
        "bid": [{
                "id": "1",
                "impid": "8278013996604217356",
                "price": 1,
                "adid": "22",
                "nurl": "https://68.67.148.76:10011/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}"
            }
 
        ],
        "seat": "9876"
    }],
    "bidid": "1",
    "cur": "USD"
}
```

## Win notification

For more information, see the definition of the `nurl` field above.

> [!NOTE]
> In certain auction types, a lost or pending notification may be generated prior to the win notification. Win notifications are always authoritative and override any other notifications previously received for that auction.

### Loss notification

If you opt for a loss notification, it will look something like this. The loss notification information appears at the end of the response.

```
{
    "notify_request": {
        "timestamp": "2016-03-17 06: 52: 40 ",
        "auction_timestamp": "2016 - 03 - 17 06: 52: 40 ",
        "user_id_64 ": 659854875312903738,
        "response_time_ms ": 40,
        "bid_info ": {
            "no_cookies": false,
            "payment_rule_id": 1772411,
            "no_flash": false,
            "browser": 7,
            "operating_system": 2,
            "operating_system_extended": 91,
            "operating_system_family": 5,
            "carrier": 1,
            "device_type": 1,
            "language": 1,
            "session_freq": 1,
            "pub_session_freq": 1,
            "country": "US",
            "within_iframe": false,
            "selling_member_id": 701,
            "publisher_id": 1483811,
            "user_id_64": 659214875312903738,
            "ip_address": "98.21.53.49",
            "user_agent": "Mozilla/5.0 (Windows NT 6.0; WOW64; rv: 44.0) Gecko / 20100101Firefox / 44.0 ",
            "region ": "PA ",
            "city ": "Ephrata",
            "postal_code ": "17522 ",
            "postal_code_id ": 12813,
            "dma ": 566,
            "time_zone ": "America / New_York ",
            "url ": "https: //www.example.com/",
            "domain": "example.com",
            "device_ids": {},
            "inventory_audits": [{
                "auditor_member_id": null,
                "intended_audience": "general",
                "inventory_attributes": [],
                "content_categories": [27, 8476]
            }],
            "userdata_json": "{\"uid\":\"5xb25EqcY3Hd9B\"}",
            "tpuids": [{
                "user_id": "5xc25EqcY3Hc9B"
            }],
            "segments": [{
                "id": 1,
                "member_id": 0,
                "code": "cookie_birthday",
                "provider": "Appnexus",
                "last_seen_min": 23767080
            }, {
                "id": 2087662,
                "member_id": 2636,
                "last_seen_min": 23959609
            }]
        },
        "tags": [{
            "id": 6123680,
            "auction_id_64": 4123382184097823951,
            "full_tag_info": {
                "auction_id_64": 4123382184097823951,
                "size": "300x250",
                "sizes": ["300x250"],
                "smaller_sizes_allowed": false,
                "position": "unknown",
                "tag_format": "iframe",
                "ad_profile_id": 114603,
                "visibility_profile_id": 625,
                "allowed_media_types": [1, 11],
                "media_subtypes": ["banner"],
                "predicted_view_rate": 0.1708,
                "estimated_clear_price": 9.00000,
                "estimated_average_price": 3.1630,
                "id": 6003680,
                "site_id": 1672260,
                "venue_id": 1299844
            },
            "payment_rule_id": 177245,
            "notify_type": "lost"
        }],
        "responses": [{
            "result": "error",
            "error": "Creative inactive, expired or not found by code;Member id: 1999,code: '537748'",
            "error_id ": 307
        }]
    }
}
```
