---
title: Native 1.2 Ad Markup Bidding (ADM)
description: This page explains the native ad markup bidding feature, how to enable it, and supported fields, with creative examples.
ms.date: 10/28/2023
---

# Native 1.2 Ad Markup bidding (ADM)

## Requirements for using Native 1.2 ADM

Native Ad Markup Bidding (ADM) enables your bidder to submit native ad markup via the `adm` field in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, register one creative for each of the following combinations:

- **Unique ad campaign or brand** you represent
- **Unique supported language**  

> [!IMPORTANT]  
> The `adomain` field is required. The branding of the provided URL must match that of the content in the `adm` field and the registered creative.  
> [!NOTE]  
> It is highly recommended to use **BURL** for spend and impression tracking on the Monetize server side.

## Get started with Native ADM  

Your bidder must be **enabled** for this feature. If you're unsure whether your bidder is enabled, check with your Monetize account representative or open a product support ticket.  

Once enabled, follow these two steps to buy inventory via ADM:  

1. **Register individually branded creatives** – All creative assets associated with this brand will serve through this registered creative.  
2. **Bid with dynamic creative assets** – The ad markup submitted in the bid response should match the registered creative.  

> [!NOTE]
> This feature does not support bidding with native video ad markup. Only non-video native ad markup is accepted.

## Register Native creatives  

Register one creative per brand and language combination using the [Creative Service](creative-service.md). Consider the following when registering a creative:  

- The creative must represent one of the actual ads dynamically passed in the bid response for this brand.  
  - The specific ad chosen for registration does not matter.  
  - The creative must be eligible to serve on Monetize inventory.  
- The creative must undergo a platform audit.  
- When registering a native creative, several OpenRTB and Microsoft macros are supported. See the [Tracking Macros](#tracking-macros) section below for a list of macros supported in `adm`.
- You do not need to specify the `brand_id` field; Monetize sets this during the audit.
- Bids must use the [OpenRTB protocol](bidding-protocol.md).
- Include impression and click trackers when registering your creative. The ad markup in the bid response should use the same set of vendors (or fewer) that were registered with the creative.  

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
- You must include a registered creative ID in one of the following bid response fields (`adid`, `crid`).
- The `crid` or `adid` value must match the corresponding branded creative object.
  
### Bid response fields

| Field  | Type   | Description  |
|--------|--------|-------------|
| `adm`  | string | Means of conveying ad markup in case the bid wins; supersedes the win notice if markup is included in both. Format should be a JSON-encoded string. |
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

| Field   | Type    | Description  |
|---------|---------|-------------|
| `event`  | integer | Type of event to track. Supported types:  <br> 1. **Impression** – Impression tracking  <br> 2. **Viewable-mrc50** – Visible impression using MRC definition (50% in view for 1 second)  <br> 3. **Viewable-mrc100** – 100% in view for 1 second  <br> 4. **Viewable-video50** – Visible impression for video using MRC definition (50% in view for 2 seconds) |
| `method` | integer | Type of tracking requested:  <br> 1. **`img`** – Image-pixel tracking (URL provided will be inserted as a 1x1 pixel at the time of the event)  <br> 2. **`js`** – JavaScript-based tracking (URL provided will be inserted as a JS tag at the time of the event)  |
| `url`    | string  | The URL for the image or JS tracker. <br> The following OpenRTB macros are supported in this field:  <br> - `${AUCTION_ID}` – Monetize auction_id_64.  <br> - `${AUCTION_BID_ID}` – ID of the bid specified in the `bidid` field in the bid response.  <br> - `${AUCTION_IMP_ID}` – ID of the impression, from the `impid` field in the bid object of the `seatbid` object.  <br> - `${AUCTION_SEAT_ID}` – ID of the winning seat, from the `seat` field in the `seatbid` object.  <br> - `${AUCTION_AD_ID}` – ID of the buyer's creative, from the `adid` field in the bid object of the seatbid object.  <br> - `${AUCTION_CURRENCY}` – Currency of the clearing price, as specified in the `cur` field in the bid response.  |

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

We support all data asset types found in the [IAB OpenRTB Native Ads Specification 1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf).  

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

For bidders using **native ADM**, submit the win notification URL in `seatbid.bid.nurl`. It is expected that the bidder will include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro in this URL to receive win price information.  

### Field definitions

| Field       | Type    | Description  |  
|------------|--------|--------------|  
| `nurl` / `burl` | integer | The win notify URL, which is dropped as a pixel into the web browser or SDK. Our server pings this URL when it receives a client-side notification from the device, indicating that we won the auction. Responses will be sent server-side. This occurs concurrently while we record the impression. The max length is `2000` characters with macros expanded. <br> For bidders using native `adm`, it is expected that the bidder will include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro in this URL to receive win price information.|

## Tracking macros  

Some publishers periodically audit creatives, which can generate false impression and click tracking events. When Microsoft detects audit events:  

- Any URL-encoded `${AUCTION_PRICE}` macro in `adm` expands to the string `"AUDIT"`.  
- Any URL-encoded `${AN_IS_AUDIT}` macro expands to `1`.  

The following macros support impression and click tracking. See ADM macros example below for usage details.

### Macro reference  

| Macro | Description |
|-------|------------|
| `${AN_IMP_URL}` | Expands to a Microsoft impression tracking URL and is intended to prepend the bidder's impression tracking pixel. When the ad is rendered, the expanded URL redirects to the bidder's pixel and correctly expands the `${AUCTION_PRICE}` macro. All macros in the bidder's pixel must be URL-encoded in `adm`. |
| `${AN_CLICK_URL}` | Expands to a Microsoft click tracking URL and is intended to prepend the bidder's click tracking pixel. When the ad is clicked, the expanded URL redirects to the bidder's pixel and correctly expands the `${AUCTION_PRICE}` macro. The bidder's pixel and `${AUCTION_PRICE}` must be URL-encoded in `adm`. |
| `${AN_IS_AUDIT}` | Expands to `1` when audit events (impressions and clicks) occur, expands to `0` otherwise. Must be URL-encoded when included in a URL following `${AN_IMP_URL}` or `${AN_CLICK_URL}`. |
| `${AUCTION_ID}` | Represents the unique identifier for the auction (`auction_id_64`). |
| `${AUCTION_BID_ID}` | Represents the unique identifier for the bid specified in the `bidid` field in the bid response. |
| `${AUCTION_IMP_ID}` | Represents the unique identifier for the impression from the `impid` field in the bid object of the `seatbid` object. |
| `${AUCTION_SEAT_ID}` | Represents the unique identifier for the winning seat from the `seat` field in the `seatbid` object. |
| `${AUCTION_AD_ID}` | Represents the unique identifier for the buyer’s creative from the `adid` field in the bid object of the `seatbid` object. |
| `${AUCTION_PRICE}` | Represents the clearing price of the impression in the currency specified in the `cur` field in the bid response. |
| `${AUCTION_PRICE:HMAC-SHA1-XOR}` | Represents a secure version of the auction price. The clearing price of the impression in the currency specified in the `cur` field in the bid response. |
| `${AUCTION_CURRENCY}` | Represents the currency of the clearing price as specified in the `cur` field in the bid response. |
| `${CREATIVE_CODE}` | Represents the `code` field set on the creative object via the API when registering a creative. |
| `${AN_PAYMENT_TYPE}` | Represents the ID of the payment type of the bid, specified in the `bid_payment_type` field of the bid response. |
| `${AUCTION_LOSS}` | Represents the loss reason code of the auction. For a full list of supported loss reason codes, see [Loss reason codes](../bidders/loss-reason-codes.md). |
| `${AN_SOURCE_FD}` | Represents the entity responsible for the final impression sale decision:<br> - `0`: Exchange (default). Microsoft Monetize holds the final auction.<br> - `1`: Upstream source. The bid is passed along to a header bidding auction or external supply. |

### Encoding and notification  

All OpenRTB macros must be URL-encoded. To use these macros, ensure they are properly encoded in pixels as described above.  

Microsoft supports both `seatbid.bid.nurl` and `seatbid.bid.burl` for server-side win notification. These must be submitted in the respective bid response field.  
  
## Creative example

This example uses four data assets and two image assets, but you can choose to use a different combination depending on the assets you want to register. (Remember, you must have at least one asset of each type.) For more details on native creative assets, see the [Creative Service](creative-service.md).

### Related topics

- [Ad markup (ADM) Bidding Overview](ad-markup-adm-bidding.md)
- [Banner Ad Markup (ADM) in Bid Responses](banner-ad-markup-bidding.md)
- [Video Ad Markup (ADM) in Bid Responses](video-ad-markup-bidding.md)
