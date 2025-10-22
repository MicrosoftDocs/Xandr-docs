---
title: Banner Ad Markup Bidding (ADM)
description: In this article, find information about bidding with a banner ad markup and how to use this feature.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Banner Ad Markup bidding (ADM)

## Requirements for using banner ADM  

Banner Ad Markup Bidding (ADM) enables bidders to submit banner ad markup via `adm` in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, bidders must register only one creative per combination of the following:  

- **Unique ad campaign or brand** you represent
- **Unique supported language**  

> [!NOTE]
> The `adomain` field is required. The branding of the provided URL must match the content in the `adm` field and the registered creative.
> [!IMPORTANT]
> It is highly recommended to use **BURL** for spend and impression tracking on the Monetize server side.

## Get started with Banner ADM  

Your bidder must be **enabled** for this feature. If you're unsure whether your bidder is enabled, check with your Monetize account representative or open a product support ticket.  

Once enabled, follow these two steps to buy inventory via ADM:  

1. **Register individually branded creatives** – All creative assets associated with this brand will serve through this registered creative.  
2. **Bid with dynamic creative assets** – The ad markup submitted in the bid response should match the registered creative.  

## Register banner creatives  

Register one creative per brand and language combination using the [Creative Service](creative-service.md). Consider the following when registering a creative:  

- The creative must represent one of the actual ads dynamically passed in the bid response for this brand.  
  - The specific ad chosen for registration does not matter.  
  - The creative must be eligible to serve on Monetize inventory.  
- The creative must undergo a platform audit.  
- When registering a banner creative, several OpenRTB and Microsoft macros are supported. See the [Tracking Macros](#tracking-macros) section below for a list of macros supported in `adm`.
- You do not need to specify the `brand_id` field; Monetize sets this during the audit.
- Bids must use the [OpenRTB protocol](bidding-protocol.md).
- Include impression and click trackers when registering your creative. The ad markup in the bid response should use the same set of vendors (or fewer) that were registered with the creative.  

## Bid with banner ADM  

### Specifications  

- Banner creative markup must be passed as **HTML content** in the `seatbid.bid.adm` field.  
      - If the ad markup is not passed as valid HTML or is malformed, the bid is rejected.  

## Bid response’s bid object  

- Other bid response objects are not listed here. See the [bid response documentation](incoming-bid-response-from-bidders.md) for details.  
- Bidders should submit ad markup in the standard OpenRTB `seatbid.bid.adm` field.  
- The `crid`/`adid` sent must match that of the corresponding branded creative object.

> [!NOTE]
> You must include a registered creative ID in **one** of the two bid response fields listed below. The `crid` or `adid` sent must match the corresponding branded creative object.  

## Bid response fields  

| **Field**  | **Type**  | **Description**  |  
|------------|----------|----------------|  
| `adm`      | string   | Means of conveying ad markup in case the bid wins; supersedes the win notice if markup is included in both. Supports price macros such as `${AUCTION_PRICE}` and `${PRICE_PAID}`. |  
| `adomain`  | string   | **Required.** The URL representing the brand of the `adm` content in the bid response. |  
| `adid`     | string   | The registered Monetize creative ID. This can be viewed via the API using the **Creative Service**. |  
| `crid`     | string   | The creative ID from the bidder's system, used to reference a Monetize creative based on the creative code set via the **Creative Service**. <br> **Note**: If both `adid` and `crid` are sent, `adid` takes precedence, and `crid` is ignored. |

## Custom macros

When an enabled bidder submits ad markup, the `seatbid.bid.ext.appnexus.custom_macros` extension field is ignored.  

- If the ad markup field is not returned at all, the registered creative content will serve by default. In this case, `seatbid.bid.ext.appnexus.custom_macros` is supported as usual.

### Field details

| Field          | Type            | Description                            |
|---------------|----------------|----------------------------------------|
| `custom_macros` | Array of objects | Identifies `custom_macro` objects. |

## Inventory size

Bidders submit the creative dimensions in the `seatbid.bid.w` and `seatbid.bid.h` fields. These dimensions override the dimensions of the registered creative and are subject to standard size checks during the auction.

### Field details

| Field | Type    | Description                               |
|-------|--------|-------------------------------------------|
| `w`   | Integer | Exact width in device-independent pixels (DIPS). |
| `h`   | Integer | Exact height in device-independent pixels (DIPS). |

## Server-side impression tracking

Bidders submit the win notification URL in `seatbid.bid.nurl`. The bidder must include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro in this URL to receive win price information.

### Field details

| Field  | Type    | Description |
|--------|--------|-------------|
| `nurl` | String | The win notification URL, dropped as a pixel into the web browser or SDK. The server pings this URL upon receiving a client-side notification from the device indicating an auction win. The max length is 2000 characters with macros expanded. For bidders using banner adm, it is expected that the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro is included in this URL to receive win price information. Use `${AUCTION_ID}` in order to collate your nurl fire with the corresponding unique Monetize auction.|

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

## Audit events and macro expansion

Some publishers periodically audit creatives, which can generate false impression and click tracking events. When Xandr detects audit events:

- Any URL-encoded `${AUCTION_PRICE}` macro in `adm` expands to the string `"AUDIT"`.
- Any URL-encoded `${AN_IS_AUDIT}` macro expands to `1`.
- `nurl` is not called if it's present in the bid response.

> [!NOTE]
> The creative assets and technology vendors you bid with must match the brand and vendors of the creative asset you initially registered. If you registered an SSL creative, ad markup must also be SSL.

## Creative example  

This example uses the standard creative template **"HTML (Xandr Created)"** (ID 6).  
Any standard template for banner creatives may be used. See **Creative Service** for more details.  

## Adding a banner creative  

### Request Payload (`banner_creative.json`)  

```json
{
  "creative": {
    "allow_audit": true,
    "allow_ssl_audit": true,
    "description": "test description",
    "code": "test_code",
    "code2": "test_code2",
    "content": "...",
    "content_secure": "...",
    "width": 300,
    "height": 250,
    "status": {
      "user_ready": true
    },
    "template": {
      "id": 6
    }
  }
}
```

### cURL Command

```bash
curl -b cookies -c cookies -X POST -s @banner_creative.json 'https://api.adnxs.com/creative/123'

```

### Response example

```json
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
        "id": 6
      }
    },
    "dbg": { ... }
  }
}
```

### Bid reponse example

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
          "adm": "<a href=\"https://adserver.com/click?crid=54321...\"><img src=\"https://image.dspcdn.com/auction_id=123456789\"/></a>",
          "w": 728,
          "h": 90,
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


### Related topics

- [Ad markup (ADM) Bidding Overview](ad-markup-adm-bidding.md)
- [Bid with Native 1.2 Ad Markup (ADM)](native-ad-markup-bidding.md)
- [Video Ad Markup (ADM) in Bid Responses](video-ad-markup-bidding.md)
