---
title: Bid with Native 1.2 Ad Markup (ADM)
description: This page explains the native ad markup bidding feature, how to enable it, and supported fields, with creative examples.
ms.date: 10/28/2023
---

# Bid with native 1.2 Ad Markup (ADM)

> [!NOTE]
> This feature does not support bidding with native video ad markup. Only non-video native ad markup is accepted.

## Requirements for using Native 1.2 ADM

Native Ad Markup Bidding (ADM) enables your bidder to submit native ad markup via the `adm` field in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, register one creative for each of the following combinations:

- Unique ad campaign or brand you represent  
- Unique supported language  

> [!IMPORTANT]
> It is highly recommended to use **BURL** for spend and impression tracking on the Monetize server side.
> [!NOTE]
> The `adomain` field is required. The branding of the provided URL must match that of the content in the `adm` field and that of the registered creative.

## Bid with native ADM

### Specifications

> [!NOTE]
> See the [Native v1.2 IAB specifications](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf).

### Considerations

- Use native creative template `39461`.
- Native creative assets must be passed via the `seatbid.bid.adm` object.
  - Include image assets, data assets, and event trackers.
  - These assets will serve instead of the creative asset you initially registered.

### Bid response’s bid object

- The other bid response objects are not listed here. For more information, see our [bid response documentation](incoming-bid-response-from-bidders.md).
- Bidders should submit ad markup in the standard OpenRTB `seatbid.bid.adm` field.
- You must include a registered creative ID in one of the following bid response fields (adid, cridd).
- The `crid` or `adid` value must match the corresponding branded creative object.
  
### Fields

| Field  | Type   | Description  |
|--------|--------|-------------|
| `adm`  | string | The field is expected to be XML, and supports PRICE macros like `${AUCTION_PRICE}` and `${PRICE_PAID}`. |
| `adomain` | string | **Required**: URL representing the brand of the `adm` content sent in the bid response. |
| `adid`  | string | The registered Monetize creative ID, viewable via the API using the [Creative Service](creative-service.md). |
| `crid`  | string | The creative ID from the bidder's system. Used to reference a Monetize creative based on the creative code as set via the [Creative Service](creative-service.md). <br> **Note**: If both values are sent, the `adid` takes precedence over `crid`, and the `crid` is ignored. |

## ADM object

| Field         | Type              | Description |
|--------------|------------------|-------------|
| `assets`     | array of objects | **Required**: List of the native ad's assets. See Asset Object below. |
| `link`       | object           | **Required**: The default destination link for the native ad. Each individual asset can have its own link object. If an asset link does not have a link object, the parent link object is used. See Link Object below. |
| `eventtrackers` | array of objects | Array of tracking objects. See Event Trackers Response Object. |
| `privacy`    | string           | If support was indicated in the request, URL of a page informing the user about the buyer’s targeting activity. |
| `ext`        | object           | Used for identifying Monetize-specific extensions to the OpenRTB bid response. |
| `ver`        | string           | Native version. Only `1.2` is supported. |

## Event trackers response object

| Field  | Type    | Description  |
|--------|--------|-------------|
| `event` | integer | Type of event to track. Supported types: <br> 1. Impression <br> &nbsp;&nbsp;&nbsp; - Impression tracking <br> 2. Viewable-mrc50 <br> &nbsp;&nbsp;&nbsp; - Visible impression using MRC definition at 50% in view for 1 second) <br> 3. Viewable-mcr100 <br> &nbsp;&nbsp;&nbsp; - 100% in view for 1 second <br> 4. Viewable-video50 <br> &nbsp;&nbsp;&nbsp; - Visible impression for video using MRC definition at 50% in view for 2 seconds <br> 5. 500+) Exchange-specific |
| `method` | integer | Type of tracking requested: <br> 1) `img` <br> &nbsp;&nbsp;&nbsp;  - Image-pixel tracking - URL provided will be inserted as a 1x1 pixel at the time of the event.  <br> 2) `js` <br> &nbsp;&nbsp;&nbsp; - Javascript-based tracking – URL provided will be inserted as a JS tag at the time of the event. <br> 500+) exchange-specific <br> &nbsp;&nbsp;&nbsp; - Could include custom measurement companies such as moat, doubleverify, IAS etc – in this case addition elements will often be passed.|
| `url` | string | The URL for the image or JS tracker. <br> The following OpenRTB macros are supported in this field: <br> - `${AUCTION_ID}` - Monetize auction_id_64. <br> - `${AUCTION_BID_ID}` - ID of the bid specified in the bidid field in the bid response. <br> - `${AUCTION_IMP_ID}` - ID of the impression, from the impid field in the bid object of the seatbid object. <br> - `${AUCTION_SEAT_ID}` - ID of the winning seat, from the seat field in the seatbid object. <br> - `${AUCTION_AD_ID}` - ID of the buyer's creative, from the adid field in the bid object of the seatbid object. <br> - `${AUCTION_CURRENCY}` - Currency of the clearing price, as specified in the `cur` field in the bid response. |

## Native `ext` object

Monetize supports a single native ext object for Monetize-specific extensions.

### Field definitions

| Field      | Type   | Description |
|------------|--------|-------------|
| `appnexus` | object | Specifies Monetize-specific (formerly AppNexus) extensions to the OpenRTB bid response. |

## Asset object

Monetize supports the following fields to define one or more native asset objects, which are included as a JSON-encoded string in the `adm` field of the bid object.

### Field definitions

| Field     | Type             | Description  |
|-----------|-----------------|--------------|
| `id`      | integer         | **Required**: The unique asset ID. Must match an asset ID in the request. |
| `required` | integer         | Set to `1` if the bidder requires the asset to be displayed. |
| `title`   | object          | The title object for title assets. See [Title Object](native-ad-markup-bidding.md#title-object)below. |
| `img`     | object          | The image object for image assets. See [Image Object](native-ad-markup-bidding.md#image-object) below. |
| `data`    | object          | The data object for data assets such as ratings and prices. See [Data Object](native-ad-markup-bidding.md#data-object) below. |

### Title object

Defines a title asset in a native `adm` object.

| Field  | Type   | Description  |
|--------|--------|-------------|
| `text` | string | **Required**: The text for a title element. |
| `len`  | integer | The length of the title being provided. |

### Image object

| Field  | Type    | Description  |
|--------|--------|-------------|
| `url`  | string | **Required**: The URL of the image asset. |
| `w`    | integer | **Recommended**: Width of the image in pixels. |
| `h`    | integer | **Recommended**: Height of the image in pixels. |
| `ext`  | object | Used for identifying Monetize-specific extensions to the OpenRTB bid response. |

## Image `ext` Object  

Monetize supports a single native `ext` object for Monetize-specific (formerly AppNexus) extensions.  

### Field definitions

| Field     | Type   | Description  |  
|-----------|--------|--------------|  
| `appnexus` | object | Specifies the Monetize-specific (formerly AppNexus) extensions to the OpenRTB bid response. |  

## Image `ext` AppNexus object  

Monetize supports the following fields in the `appnexus` extension object:  

| Field         | Type    | Description  |  
|--------------|---------|--------------|  
| `prevent_crop` | boolean | Allows the buyer to specify whether the image can be cropped: <br> **Note**: This can be applied to icon and main image. <br> - If set to `1`, the image **cannot** be cropped (fill).<br> - If set to `0`, the image **can** be cropped (fit). <br> - If flag is not passed in pr the **Default behavior**: `0`. Images are assumed to allow modifications unless explicitly indicated otherwise. |  

## Data object  

Defines a data asset in `adm` object. Used for miscellaneous elements in a native ad, such as ratings, prices, review counts, downloads, etc.  

### Field definitions  

| Field  | Type    | Description  |  
|--------|---------|--------------|  
| `type` | integer | Supported types: <br> - `1`: **Sponsored** <br> &nbsp;&nbsp; - Sponsored by message. |  
| `value` | string  | The formatted string of data to be displayed (e.g., `"5 stars"` or `"$10"`). |  

## Link object  

Defines the link for a native asset. When clicked, the user is directed to the specified URL. This object can only be defined on the parent `adm` object.  

### Field definitions

| Field          | Type              | Description  |  
|---------------|-------------------|--------------|  
| `url`         | string            | **(Required)** The landing URL for the clickable link. **Macros are not supported.** |  
| `clicktrackers` | Array of strings | An array of third-party tracking URLs triggered when the link is clicked. |  
| `fallback`    | string            | A fallback URL if the primary URL is not supported by the device. |  

## Custom macros  

When an enabled bidder submits ad markup, the `seatbid.bid.ext.appnexus.custom_macros` extension field is ignored.  

- If the `admarkup` field is not returned at all, the registered creative content will serve by default. In this case, `seatbid.bid.ext.appnexus.custom_macros` is supported as usual.  

### Field definitions

| Field          | Type              | Description  |  
|---------------|-------------------|--------------|  
| `custom_macros` | array of objects | Identifies custom macro objects. |  

## Bid response example  

```json
{
  "seatbid": [
    {
      "bid": [
        {
          "nurl": "https://rtb-fakeurl.com/lax/wintrk=CwE&wp=${AUCTION_PRICE}&curr=${AUCTION_CURRENCY}&aid=${AUCTION_AD_ID}",
          "adid": "12345",
          "crid": "test_code",
          "price": 2.50,
          "adm": {
            "link": {
              "url": "https://rtb-fakeurl.com"
            },
            "ver": "1.2",
            "assets": [
              {
                "id": 1,
                "img": {
                  "w": 1200,
                  "h": 627,
                  "url": "https://rtb-fake-image-url.com",
                  "ext": {
                    "appnexus": {
                      "prevent_crop": 1
                    }
                  }
                }
              },
              {
                "id": 2,
                "title": {
                  "text": "AD"
                }
              },
              {
                "id": 3,
                "data": {
                  "value": "abc.com"
                }
              }
            ],
            "privacy": "https://rtb-fake-privacy-url.com",
            "eventtrackers": [
              {
                "event": 1,
                "method": 1,
                "url": "https://rtb-fakeurl.com/price=${AUCTION_PRICE}"
              }
            ]
          },
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

```

## Server-side impression tracking  

Bidders submit the win notification URL in `seatbid.bid.nurl`. It is expected that the bidder will include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro in this URL to receive win price information.  

### Field definitions

| Field       | Type    | Description  |  
|------------|--------|--------------|  
| `nurl` / `burl` | integer | The win notify URL, which is dropped as a pixel into the web browser or SDK. Our server pings this URL when it receives a client-side notification from the device, indicating that we won the auction. Responses will be sent server-side. This occurs concurrently while we record the impression. The max length is 2000 characters with macros expanded. <br> For bidders using video `adm`, it is expected that the bidder will include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro in this URL to receive win price information.|

## Creative example

This example uses four data assets and two image assets, but you can choose to use a different combination depending on the assets you want to register. (Remember, you must have at least one asset of each type.) For more details on native creative assets, see the [Creative Service](creative-service.md).

### Related topics

- [Ad markup (ADM) Bidding Overview](ad-markup-adm-bidding.md)
- [Banner Ad Markup (ADM) in Bid Responses](banner-ad-markup-bidding.md)
- [Video Ad Markup (ADM) in Bid Responses](video-ad-markup-bidding.md)
