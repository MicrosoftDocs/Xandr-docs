---
title: Video Ad Markup Bidding (ADM)
description: Learn how to submit raw video XML via ADM for bidding, simplifying creative registration and enabling dynamic ad delivery in OpenRTB.
ms.date: 10/28/2023
---

# Video Ad Markup bidding (ADM)

## Requirements for using video ADM  

Video Ad Markup Bidding (ADM) enables your bidder to submit video ad markup via the `adm` field in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, register only **one creative** per combination of:  

- Unique ad campaign or brand  
- Unique supported language  
- Video creative duration  

> [!IMPORTANT]
> Use `burl` for **spend and impression tracking** server-side.  

Additionally, your bidder must send **XML content** via the bidstream.

> [!NOTE]
> Custom macros and other required data must be prefilled within the XML content.  
> [!NOTE]
> The `adomain` field is required. The branding of the provided URL must match the content in the `adm` field and the registered creative.  

The registered creative should have all supported MIME types for the brand. However, the dynamically passed XML should only include those MIME types supported in the bid request. For more details on required fields and supported MIME types, see the [Video Object](outgoing-bid-request-to-bidders.md#video-object-for-the-assets).

## Get started with video ADM  

Your bidder must be enabled for this feature. If you're unsure whether your bidder is enabled, **please contact your Monetize account representative or submit a product support ticket**.  

Once enabled, follow these steps to buy inventory via ADM:  

1. **Register** your branded creatives.  
   - All creative assets associated with the brand will serve through this creative.  

2. **Bid** dynamically with your creative assets.  

## Register video creatives  

Register **one creative per brand** using the [Creative Service](creative-service.md). Consider the following:  

- The creative must represent an actual ad dynamically passed in the bid response for this brand.  
  - The specific ad chosen for registration does not matter.  
  - The creative must be **eligible to serve** on Monetize inventory.  
- The creative must **pass a platform audit**. 
- When registering a creative, only OpenRTB macros are supported. [Monetize macros](xandr-macros.md) are not supported, and OpenRTB macros (such as ${AUCTION_PRICE}) will not be expanded.
- The `brand_id` field is set by Monetize during the audit.  
- Use **video creative template 6439**.  

## Bid with video ADM  

Your bids with a registered video creative become eligible once:  

- The creative is registered via the API.  
- The creative passes the Monetize platform audit.  
- Bids use the [OpenRTB protocol](bidding-protocol.md).  

### Specifications  

- Pass video creative assets via `seatbid.bid.adm`.  
  - These assets serve **instead of** the initially registered creative asset.  
- If you do not pass valid video creative assets, the **registered creative** serves by default.  

## Bid response’s bid object  

- The other bid response objects are not listed here. For more details, see our [bid response documentation](incoming-bid-response-from-bidders.md).  
- Bidders must submit ad markup in the standard OpenRTB `seatbid.bid.adm` field.  
- You must include a registered creative ID in one of the following bid response fields:  
- The `crid` or `adid` value must match the corresponding branded creative object

### Required fields  

| Field   | Type    | Description |
|---------|--------|-------------|
| `adm`   | string | The field expects XML. Supports macros like `${AUCTION_PRICE}` and `${PRICE_PAID}`. |
| `adomain` | string | **Required.** URL representing the brand of the `adm` content. |
| `adid`  | string | The registered Monetize creative ID, viewable via the API using the [Creative Service](creative-service.md). |
| `crid`  | string | The bidder's creative ID. Used to reference a Monetize creative based on the creative code set via the [Creative Service](creative-service.md).<br> **Note:** If both `adid` and `crid` are sent, `adid` takes precedence, and `crid` is ignored. |

## Custom macros  

When a bidder submits ad markup, the `seatbid.bid.ext.appnexus.custom_macros` field is **ignored**.  

### Custom macros Field  

| Field          | Type  | Description |
|---------------|-------|-------------|
| `custom_macros` | array | Identifies custom macro objects. |

## Inventory size  

Bidders submit creative dimensions in the `seatbid.bid.w` and `seatbid.bid.h` fields. These override the registered creative’s dimensions and are subject to standard size checks.  

| Field | Type    | Description |
|-------|--------|-------------|
| `w`   | integer | Exact width in device-independent pixels (DIPS). |
| `h`   | integer | Exact height in device-independent pixels (DIPS). |

## Server-side impression tracking  

Bidders submit the win notification URL in `seatbid.bid.nurl`. This URL must include the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro for win price information.  

The `nurl` field is used for win notifications and is required for server-side impression tracking. When the auction is won, the Monetize server pings this URL to confirm the win and track the impression.  

| Field  | Type   | Description |
|--------|--------|-------------|
| `nurl` | string | The win notification URL is dropped as a pixel into the web browser or SDK. When the device sends a client-side notification indicating that the auction was won, the server pings this URL. Responses are sent server-side while the impression is recorded. The maximum length of this URL is 2,000 characters with macros expanded. For bidders using Video ADM, the `${PRICE_PAID}` or `${AUCTION_PRICE}` macro must be included in this URL to receive win price information.|

## Tracking Macros  

Some publishers periodically audit creatives, which can generate false impression and click tracking events. When Xandr detects audit events:  

- Any URL-encoded `${AUCTION_PRICE}` macro in `adm` expands to the string `"AUDIT"`.
- If the `${AUCTION_PRICE}` macro is present and unencoded in `adm`, it is stripped out before the ad is served.

To use these macros, ensure they are URL-encoded in pixels as described in the previous section.

### Related topics

- [Ad markup (ADM) Bidding Overview](ad-markup-adm-bidding.md)
- [Bid with Native 1.2 Ad Markup (ADM)](native-ad-markup-bidding.md)
- [Banner Ad Markup (ADM) in Bid Responses](banner-ad-markup-bidding.md)
