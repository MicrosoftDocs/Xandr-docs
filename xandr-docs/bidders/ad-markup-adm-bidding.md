---
title: Overview - ADM Bidding
description: Learn how to target specific content categories to optimize ad campaigns and improve reach accuracy.
ms.date: 10/28/2023
---

# Overview - ADM Bidding

## What is Ad Markup (ADM) bidding?

Ad markup (ADM) bidding simplifies the creative registration workflow. Instead of registering all creatives individually, you register only representative creatives. The content is allocated dynamically at bid time, allowing all creative assets for a brand to be passed via ad markup in the bid response.

### Requirements for using ADM

ADM enables your bidder to submit content via the `adm` field in the OpenRTB bid response. Instead of registering every creative with Microsoft Monetize, you must register only a single creative per combination of the following:

- **Unique ad campaign or brand** you represent
- **Unique supported language**  

> [!IMPORTANT]  
> The `adomain` field is required. The branding of the provided URL must match that of the content in the `adm` field and the registered creative.  

> [!IMPORTANT]
> Effective September 2025: Declare via the `bid.cat` field in OpenRTB whether your dynamic ad is intended for political advertising. Learn more about upcoming updates to [Monetize Creative Standards regarding political ads](../monetize/creative-standards.md). Learn more about how [political advertising](https://help.ads.microsoft.com/#apex/ads/en/60380/-1) is defined.

> [!NOTE]  
> It is highly recommended to use **BURL** for spend and impression tracking on the Monetize server side.  

## Get started with ADM

Your bidder must be **enabled** to use this feature for every supported media type: **native, banner, and video**. If you're unsure whether your bidder is enabled, contact your Monetize account representative or submit a product support ticket.

Once enabled, complete the following steps to buy inventory via ADM:

1. **Register your individually branded creatives** – All creative assets associated with this brand will serve through this creative.  
2. **Bid with your creative assets dynamically**.  

> [!NOTE]  
> Audio media type is not currently supported for ADM.

## Register creatives

Register one creative per brand and language combination using the [Creative Service](creative-service.md). Consider the following when registering a creative:

- The creative must represent one of the actual ads that will be dynamically passed in the bid response for this brand.
  - The specific ad chosen to register does not matter.
  - The creative must be eligible to serve on Monetize inventory.
- The creative must be submitted for a platform audit.
- When registering a creative, several OpenRTB and Microsoft macros are supported.
- You do not need to specify the `brand_id` field; Monetize sets this during the audit.
- Bids must use the [OpenRTB protocol](bidding-protocol.md).

## FAQ

### What are creative templates?

Creative templates define the structure and format of creatives used in ADM bidding. They ensure consistency and compliance with Monetize platform requirements while allowing for dynamic asset allocation at bid time.

A creative template typically includes:

- Ad format specifications – Defines supported ad types (banner, video, or native).
- Supported macros – Lists available macros for tracking and content insertion.
- Branding requirements – Ensures alignment with Monetize audit policies.
- Technical constraints – Specifies file size limits, supported file types, and other restrictions.

For more details, see [Creative Template Service](creative-template-service.md).

### Why do I have to register a creative for each brand I represent?

- Monetize policy prohibits brand rotation on creatives. This is enforced through the creative audit.
- Monetize ensures that each creative complies with audit policies by performing an initial audit and periodically scanning the creative content that your bidder dynamically passes in the bid response.
- If there is a misalignment between the registered creative and the bid response (for example, images and text for a different brand), the registered creative will be reaudited and may be rejected.

For more details, see [Creative Audit Feedback](creative-audit-feedback.md).

### Will I be charged creative audit fees for periodically reaudited creative ad markup?

No. Creative audit fees apply only during your creative's initial audit.

### What happens if my creative passes the initial audit but fails a subsequent reaudit?

- Your creative will not be permitted to serve.
- The audit failure may be due to rotating brands.
- If you believe your creative was incorrectly failed or have other questions, contact customer support and select the category **Creative Audit**.

> [!NOTE]  
> Frequent creative audit rejections due to rotating brands may result in revoked access to the ADM feature.

### Where do I go for more help?

If you have additional questions, contact your account representative or customer support.

### Related topics

- [Bid with Native 1.2 Ad Markup (ADM)](native-ad-markup-bidding.md)
- [Banner Ad Markup (ADM) in Bid Responses](banner-ad-markup-bidding.md)
- [Video Ad Markup (ADM) in Bid Responses](video-ad-markup-bidding.md)
