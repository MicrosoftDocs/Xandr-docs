---
title: Native Ad Markup Bidding
description: In this article, learn about the native ad markup bidding feature, steps to enable the feature, its creative examples, and supported fields.
ms.date: 10/28/2023
---

# Native ad markup bidding

Native Ad Markup Bidding enables your bidder to submit native ad markup via `adm` in the OpenRTB bid response. Instead of registering every native creative asset you have with Xandr, you are required to register only a single creative for each ad campaign or brand you represent; all native creative assets for that brand can be passed dynamically via ad markup in the bid response. This page explains how to use this feature.

> [!NOTE]
> This feature does not currently support bidding with native video ad markup. Only non-video native ad markup is accepted.

## Getting started

Your bidder must be enabled to use this feature. If you are not sure whether your bidder is enabled, then check with your Xandr account representative.

Once enabled, there are two steps required to buy Native inventory via Ad Markup Bidding:

1. Register your creative. For each brand that you represent, you must register a single creative that represents that brand. Your creative must pass platform audit. All native creative assets associated with this brand within your bidder will serve through this creative. For details, see [Register native creatives](#register-native-creatives) below.
1. Bid with your creative assets on native inventory. For details, see [Bid with native ad markup](#bid-with-native-ad-markup) below.

## Register native creatives

For each brand that you represent, you must register a single creative that represents that brand. This is done using the [Creative Service](creative-service.md). When registering a Native Creative, there are a few considerations to keep in mind:

- The creative must represent one of the actual native ads that you will dynamically pass on the bid response for this brand. The specific ad you choose to register does not matter, but the creative must contain at least one image asset and one data asset consistent with an ad you would actually serve on native inventory.
- When registering a creative, only [Xandr Macros](xandr-macros.md) are supported. OpenRTB macros (such as `${AUCTION_PRICE}`) will not be expanded.
- The creative must be submitted for platform audit.
- You do not need to specify the `brand_id` field; this will be set by Xandr during audit.
- Be sure to include impression and click trackers when registering your creative. The ad markup submitted in the bid response should use the same set of vendors (or fewer) that were registered with this creative.
- Be sure to use native creative template 39461.

The following section provides an example of defining and registering a Native Creative.

## Creative example

This example uses four data assets and two image assets, but you can choose to use a different combination depending on the assets you want to register. (Remember, you must have at least one asset of each type.) For more details on native creative assets, see the [Creative Service](creative-service.md).

### Adding a native creative

```
$ cat native_creative.json
 
{
  "creative": {
    "description": "test description",
    "code": "test_code",
    "code2": "test_code2",
    "allow_audit": 1,
    "template": {
      "id": 39461
    },
    "native_attribute": {
      "link": {
        "url": "https://www.landingpage.com",
        "fallback_url": "https://fallback.com",
        "trackers": [{
          "url": "http://url.com",
          "url_secure": "https://secureurl.com"
        }]
      },
      "data_assets": [
        {
          "data_type": "title",
          "value": "Test Title"
        },
        {
          "data_type": "sponsored_by",
          "value": "Test Sponsor"
        },
        {
          "data_type": "description",
          "value": "Test description."
        },
        {
          "data_type": "call_to_action",
          "value": "Test CTA!"
        }
      ],
      "image_assets": [
        {
          "image_type": "main_image",
          "creative_asset_image": {
            "url": "http://url.com/main_img.png",
            "url_secure": "https://secureurl.com/main_img.png",
            "height": 1200,
            "width": 628
          }
        },
        {
          "image_type": "icon_image",
          "creative_asset_image": {
            "url": "http://url.com/icon_img.png",
            "url_secure": "https://secureurl.com/icon_img.png",
            "height": 150,
            "width": 150
          }
        }
      ],
      "image_trackers": [{
        "url": "http://url.com",
        "url_secure": "https://secureurl.com"
      }],
      "javascript_trackers": [{
        "url": "http://url.com",
        "url_secure": "https://secureurl.com"
      }]
    }
  }
}
 
$ curl -b cookies -c cookies -X POST -s @native_creative.json 'https://api..com/creative/123'
 
{
  "response": {
    "status": "OK",
    "id": 12345,
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "creative": {
      "id": 12345,
      "active": true,
      "member_id": 123,
      "description": "test description",
      "code": "test_code",
      "code2": "test_code2",
      "audit_status": "pending",
      "allow_audit": true,
      "ssl_status": "pending",
      "allow_ssl_audit": true,
      "template": {
        "id": 39461
      },
      "native_attribute": {
        ...
      },
      ...
    },
    "dbg": {
      ...
  }
}
```

## Bid with native ad markup

> [!NOTE]
> This feature does not currently support bidding with native video ad markup. Only non-video native ad markup is accepted.

Once you have registered a Native Creative and it has passed platform audit, you can begin bidding with that creative using the [OpenRTB protocol](bidding-protocol.md).

> [!NOTE]
> Xandr supports v1.1 of the [OpenRTB Dynamic Native Ads API](https://iabtechlab.com/specifications-guidelines/openrtb-native/).

Some considerations:

- Either the `crid` or `adid` field must be included in the bid response to identify the creative that was registered. The `crid` value must match the creative's `code;` `adid` must match the creative's `id`.
- Native creative assets must be passed via the `seatbid.bid.adm.native` object. Be sure to include image assets, data assets, impression trackers, and click trackers. These assets will serve instead of the creative asset you initially registered.
  
    > [!NOTE]
    > The creative assets you bid with must belong to the same brand as the creative asset you initially registered. Xandr periodically scans and reviews ad markup creative content to ensure this content is consistent with the registered creative. If there is a discrepancy, your creative can be rejected by platform audit. Frequent creative audit rejections due to rotating brands can result in revoked access to the Ad Markup Bidding with Native feature.

- If you do not pass native creative assets in your bid response, or the assets are malformed, the registered creative content will serve by default.

## Bid response supported fields

> [!NOTE]
>
> - The `ver` field is ignored in the bid response.  
> - The `adomain` field may be checked occasionally to verify that the ad’s brand aligns with publisher preferences.  

### Bid object

| Field | Type | Description |
|:---|:---|:---|
| `adm` | string | Conveys ad markup in case the bid wins. The `native` object (described below) should be passed in as a JSON-encoded string. |

### Native object

| Field | Type | Description |
|---|---|---|
| `assets` | array of objects | (Required) List of the native ad's assets. See [Asset Object](#asset-object) below.<br>  |
| `link` | object | (Required) The default destination link for the native ad. Each individual asset can have its own link object, which applies if that asset is clicked. If an individual asset link does not have a link object, the parent link object is used. See [Link Object](#link-object) below. |
| `imptrackers` | array of strings | Array of impression-tracking URLs expected to return a 1x1 image or HTTP 204 (No Content) response. This is typically passed only when using third-party trackers.<br>The following OpenRTB macros are supported in this field:<br> - `${AUCTION_ID}` - Xandr `auction_id_64`.<br> - `${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response.<br> - `${AUCTION_IMP_ID}` - ID of the impression, from the `impid` field in the `bid` object of the `seatbid` object.<br> - `${AUCTION_SEAT_ID}` - ID of the winning seat, from the `seat` field in the `seatbid` object.<br> - `${AUCTION_AD_ID}` - ID of the buyer's creative, from the `adid` field in the `bid` object of the `seatbid` object.<br> - `${AUCTION_PRICE}` - Clearing price of the impression in the currency specified in the `cur` field in the bid response.<br> - `${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response. |
| `jstracker` | string | Optional JavaScript impression tracker. This should be wrapped in `<script>` tags.<br>The following OpenRTB macros are supported in this field:<br> - `${AUCTION_ID}` - Xandr `auction_id_64`.<br> - `${AUCTION_BID_ID}` - ID of the bid specified in the `bidid` field in the bid response.<br> - `${AUCTION_IMP_ID}` - ID of the impression, from the `impid` field in the `bid` object of the `seatbid` object.<br> - `${AUCTION_SEAT_ID}` - ID of the winning seat, from the `seat` field in the `seatbid` object.<br> - `${AUCTION_AD_ID}` - ID of the buyer's creative, from the `adid` field in the bid object of the `seatbid` object.<br> - `${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response. |
| `privacy` | string | If support was indicated in the request, URL of a page informing the user about the buyer’s targeting activity. |
| `ext` | object | Used for identifying Xandr-specific extensions to the OpenRTB bid response. |

### Native ext object

Xandr supports a single object in the native ext object to support Xandr-specific extensions:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the Xandr-specific (formerly AppNexus) extensions to the OpenRTB bid response.  |

### Native ext AppNexus object

Xandr supports the following fields in the `appnexus` extension object:

| Field | Type | Description |
|:---|:---|:---|
| `third_party_imptrackers` | array of strings | Array of impression-tracking URLs expected to return a 1x1 image or HTTP 204 (No Content) response. The following OpenRTB macros will be expanded as empty strings:<br> - `${AUCTION_PRICE}` - Clearing price of the impression in the currency specified in the `cur` field in the bid response.<br> - `${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response.<br>All other OpenRTB macros will expand normally. |

### Asset object

Xandr supports the following fields to define one or more native `asset` objects to be included as a JSON-encoded string as part of the `native` object in the `adm` field of the `bid` object.

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | (Required) The unique asset ID. Must match an asset ID in the request. |
| `required` | integer | Set to `1` if bidder requires asset to be displayed. |
| `title` | object | The title object, for title assets. See [Title Object](#title-object) below. |
| `img` | object | The image object, for image assets. See [Image Object](#image-object) below. |
| `data` | object | The data object, for data assets such as ratings, prices, and so on. See [Data Object](#data-object) below. |
| `link` | object | This object is not supported in our native implementation. |

### Title object

Used to define a title asset in a native object.

| Field | Type | Description |
|:---|:---|:---|
| `text` | string | (Required) The text for a title element. |

### Image object

Used to define an image asset in a native object. Used for all image elements of the native ad, such as icons, main image, and so on.

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | (Required) The URL of the image asset. |
| `w` | integer | (Recommended) The width of the image, in pixels. |
| `h` | integer | (Recommended) The height of the image, in pixels. |
| `ext` | object | Used for identifying Xandr-specific (formerly AppNexus) extensions to the OpenRTB bid response. |

### Image ext object

Xandr supports a single object in the native ext object to support Xandr-specific (formerly AppNexus) extensions:

| Field | Type | Description |
|:---|:---|:---|
| `appnexus` | object | Specifies the Xandr-specific (formerly AppNexus) extensions to the OpenRTB bid response.  |

### Image ext AppNexus object

Xandr supports the following fields in the `appnexus` extension object:

| Field | Type | Description |
|:---|:---|:---|
| `prevent_crop` | boolean | Allows the buyer to indicate whether the image can be cropped or not. This can be applied to icon and main image.<br> - If flag is set to 1, the image can not be cropped (fill).<br> - If flag is set to 0, the image can be cropped (fit).<br> - If flag is not passed in/default behavior: 0; images are assumed to allow modifications unless explicitly indicated otherwise. |

### Data object

Used to define a data asset in a native object. Used for all miscellaneous elements in a native ad, such as ratings, price, review count, downloads, and so on.

| Field | Type | Description |
|:---|:---|:---|
| `label` | string | An optional formatting string name of the data type. |
| `value` | string | The formatted string of data to be displayed (such as `"5 stars"` or `"$10"`). |

### Link object

Used to define the link for a native asset. When clicked, the user is taken to the location of the link. Can only be defined on the parent native object.

| Field | Type | Description |
|:---|:---|:---|
| `url` | string | (Required) The landing URL for the clickable link.<br>**Macros cannot be used in this field.** |
| `clicktrackers` | Array of strings | Array of third-party tracking URLs to be fired when the link is clicked. |
| `fallback` | string | A fallback URL to be used if the URL is not supported by the device. |

## Bid response example

```
{
    "seatbid": [
        {
            "bid": [
                {
                    "nurl": "https://rtb-fakeurl.com/lax/wintrk=CwE&wp=${AUCTION_PRICE}&curr=${AUCTION_CURRENCY}&aid=${AUCTION_AD_ID}",
                    "adid": "12345",
                    "crid": "test_code",
                    "price": 2.50,
                    "adm": "{\"assets\":[{\"id\":1,\"img\":{\"url\":\"https://url.com/dynamic_main_img.jpg\",\"w\":1200,\"h\":628}},{\"id\":2,\"title\":{\"text\":\"Dynamic Title\"}},{\"id\":3,\"data\":{\"value\":\"Dynamic Description\"}},{\"id\":4,\"data\":{\"value\":\"Dynamic Sponsor\"}}],\"link\":{\"url\":\"https://www.landingpage.com\",\"clicktrackers\":[\"https://thirdparty-clicktracker-1.com\",\"https://thirdparty-clicktracker-2.com\"],\"fallback\":\"https://fallback-url.com\"},\"imptrackers\":[\"https://imptracker.com\"]}",
                    "impid": "3226285750417000001",
                    "id": "6ab34155-c960-1111-abcd-52b7321adbbb"
                }
            ],
            "seat": "123"
        }
    ],
    "id": "3",
    "cur": "USD"
        }
    ]
}
```

## FAQs

### Why do I have to register a creative for each brand I represent?

Xandr policy prohibits brand rotation on creatives. By registering a creative for each brand you work with, your creative will be able to pass Xandr's audit. This will maximize the native inventory on which it can serve. Xandr ensures that each creative complies with our audit policies by performing an initial audit and then periodically scanning the creative content that your bidder dynamically passes in its bid responses. If the dynamic content served by your bidder differs substantially from the registered creative (i.e. images and text for a different brand) it will be reaudited and may be rejected.

### Will I be charged creative audit fees for periodically reaudited creative ad markup?

No. Creative audit fees will apply only during your creative's initial audit.

### What happens if my Native Creative passes initial audit but fails a subsequent reaudit?

Your creative will not be permitted to serve. The audit failure may be due to rotating brands. If you believe your creative has been failed incorrectly or have other questions contact customer support and select the Category "Creative Audit".

> [!NOTE]
> The frequent creative audit rejections due to rotating brands may result in revoked access to the Ad Markup Bidding with Native feature.

### Where do I go for more help?

If you have additional questions, contact your account representative or [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## Related topic

[Smart Image Adjustments page](smart-image-adjustments-for-native-creatives---bidders.md)
