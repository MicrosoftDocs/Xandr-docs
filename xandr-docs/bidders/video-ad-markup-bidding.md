---
title: Video Ad Markup Bidding (ADM)
description: Learn how to submit raw video XML via ADM for bidding, simplifying creative registration and enabling dynamic ad delivery in OpenRTB.
ms.date: 10/28/2023
---

# Video Ad Markup bidding (ADM)

## Requirements for using video ADM  

Video Ad Markup Bidding (ADM) enables your bidder to submit video ad markup via the `adm` field in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, register only **one creative** per combination of:  

- **Unique ad campaign or brand** you represent
- **Unique supported language**
- **Video creative duration**  

> [!IMPORTANT]  
> The `adomain` field is required. The branding of the provided URL must match that of the content in the `adm` field and the registered creative.  
> [!NOTE]  
> It is highly recommended to use **BURL** for spend and impression tracking on the Monetize server side.

Additionally, your bidder must send **XML content** via the bidstream –NOT a wrapper URL to the content.

> [!NOTE]
> Custom macros and other required data must be prefilled within the XML content.  

The registered creative should have all supported MIME types for the brand. However, the dynamically passed XML should only include those MIME types supported in the bid request. For more details on required fields and supported MIME types, see the [Video Object](outgoing-bid-request-to-bidders.md#video-object-for-the-assets).

## Get started with video ADM  

Your bidder must be **enabled** to use this feature. If you're unsure whether your bidder is enabled, contact your Monetize account representative or submit a product support ticket.

Once enabled, follow these steps to buy inventory via ADM:  

1. **Register your individually branded creatives** – All creative assets associated with this brand will serve through this creative.  
2. **Bid with your creative assets dynamically**.  

## Register video creatives  

Register one creative per brand and language combination using the [Creative Service](creative-service.md). Consider the following when registering a creative:  

- The creative must represent one of the actual ads dynamically passed in the bid response for this brand.  
  - The specific ad chosen for registration does not matter.  
  - The creative must be eligible to serve on Monetize inventory.  
- The creative must undergo a platform audit.
- Only [Monetize macros](xandr-macros.md) are supported when registering a creative. OpenRTB macros (such as `${AUCTION_PRICE}`) are **not** expanded.  
- You do not need to specify the `brand_id` field; Monetize sets this during the audit.
- Bids must use the [OpenRTB protocol](bidding-protocol.md).
- Use **video creative template 6439**.  

## Bid with video ADM  

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
| `adm`   | string | Means of conveying ad markup in case the bid wins; supersedes the win notice if markup is included in both. Supports price macros such as `${AUCTION_PRICE}` and `${PRICE_PAID}`. |
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

- If the following macros are present and unencoded in `adm`, they are stripped out before serving the ad: `${AUCTION_PRICE}`. To use these macros, be sure to URL-encode them in pixels.

- We support both `seatbid.bid.nurl` and `seatbid.bid.burl` for server-side win notification. These must be submitted in the respective bid response field.

### Related topics

- [Ad markup (ADM) Bidding Overview](ad-markup-adm-bidding.md)
- [Bid with Native 1.2 Ad Markup (ADM)](native-ad-markup-bidding.md)
- [Banner Ad Markup (ADM) in Bid Responses](banner-ad-markup-bidding.md)
