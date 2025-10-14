---
title: Bidstream Creative Registration (BCR) 
description: Bidstream Creative Registration (BCR) is a feature in Microsoft Moentize platform that enables external bidder clients to register creatives in real time directly through the bidstream
ms.date: 10/14/2025
ms.author: shsrinivasan
---

# Bidstream Creative Registration (BCR) 

> [!NOTE]
> This product is currently in Beta and may change without notice. To inquire whether BCR may be right for your bidder, please contact your Microsoft Advertising Account Representative.

## Overview

Bidstream Creative Registration (BCR) is a feature in Microsoft Moentize platform that enables external bidder clients to register creatives in real time directly through the bidstream. With BCR, clients don’t need to pre-register creatives or maintain an integration with Microsoft Creative APIs. This provides a streamlined alternative approach for bidders who cannot or prefer not to integrate with Microsoft [Creative Service APIs](creative-service.md). 

## BCR workflow

BCR registers creatives within the Microsoft Monetize platform in real time on behalf of the bidder and routes them through the standard audit workflow. It does not replace existing creative registration APIs or workflows. Instead, it provides an alternate path for eligible bidders and real-time creative onboarding.

The workflow is as follows:

- When a BCR-enabled bidder submits a bid with a creative that is not yet registered in the Microsoft Monetize platform (that is, it has no creative ID (**crid**)), BCR identifies it as unregistered.
- If the **crid** does not exist in the system, the bid is rejected. BCR then attempts to register the creative with a new crid using the creative content passed in the bid request.
- After successful registration, the creative receives a **pending audit** status and enters the standard Microsoft audit review process.
- We recommend configuring your member settings (using the [Member Service](member-service.md)) to receive email notifications when:
    - A creative completes audit (`audit_notify_email`)
    - Sherlock scans a creative (`sherlock_notify_email`)

> [!IMPORTANT]
> This solution assumes that the bidder continues submitting bids with unregistered creatives. These bids are rejected until the creative is successfully registered.
> - If the publisher allows supply of unaudited creatives, the bid is accepted as soon as the creative is registered (with an audit status of pending).
> - If the publisher requires audited creatives, the bid continues to be rejected until the creative passes audit and is approved.

## Implementation of BCR 

- **Contact your Microsoft Advertising Account Representative:** To enable this feature, contact your Microsoft Advertising Account Representative
- **Prepare your bid logic:** 
    - Include the required fields in each bid response (see the [Requirements](#required-fields-by-media-type) section for details)
        - `adm` (ad markup)
        - `adomain` (advertiser domain)
        - `crid` (creative ID)
    - For native creatives, also include:
        - `ver` (version)
        - `link` (destination URL)
- **Start bidding with unregistered creatives**
    - Send bids that include creatives not yet registered on the Microsoft Monetize platform.
    - Continue submitting these bids until BCR samples and registers them.
- **Monitor registration and audit status**
    - Track creative status through the audit pipeline
    - If your configuration allows **unaudited creatives**, you can begin serving them once they are registered with a **pending audit** status
- **Handle errors and rejections**
    - Review error messages returned in bid responses and resolve issues such as:
        - Invalid or unsupported `adm` markup
        - URLs exceeding character limits
        - Missing or invalid `crid` values 
- **Ramp up registration**
    - After you validate your implementation, increase BCR usage gradually. For example:
        - Start at 1% of traffic
        - Increase to 15%, then 50%
        - Move to 100% once stable
- **Review and update documentation to maintain integration:** Review product updates regularly and update your integration and documentation to stay compliant with BCR requirements.


## Requirements for using BCR 
You must meet the following requirements to use Bidstream Creative Registration (BCR). For media-type–specific field requirements, see the sections below:

- **Bid with adm:** Include valid ad markup information in the `adm` field for every bid. 
- **Bid with adomain:** The adomain field is required; the branding of the provided URL must match both the content in the `adm` field and the final registered creative. 
- **Creative ID (crid):** Assign a unique crid for each creative. 
    - You may reuse the same `crid` across media types. 
    - If you pass `media_type`, the system appends it to the crid to create the final creative code.
    - If you do not pass `media_type`, BCR determines it from the `adm` field.
- **Continued bidding until registration completes:** Your bidding logic must allow unregistered creatives to continue bidding until BCR registers them. 

## Required fields by media type 
Mandatory fields vary by creative media type. Please see below for more information: 

### Banner creatives 

| Media type | Field | Type | Description |
|:---|:---|:---|:---|
| Banner | **crid** | string | The bidder's creative ID. Used to reference a Monetize creative based on the creative code set via the [Creative Service](creative-service.md). <br> **Note:** If both `adid` and `crid` are sent, `adid` takes precedence, and `crid` is ignored. |
| Banner | **adm** | string | It conveys ad markup information for banner creatives. For more information, please see [Banner Ad Markup bidding (ADM)](banner-ad-markup-bidding.md). |
| Banner | **adomain** | string | The URL representing the brand of the `adm` content sent in the bid response.   |

### Video creatives
| Media type | Field | Type | Description |
|:---|:---|:---|:---|
| Video | **crid** | string | The bidder's creative ID. Used to reference a Monetize creative based on the creative code set via the [Creative Service](creative-service.md). <br> **Note:** If both `adid` and `crid` are sent, `adid` takes precedence, and `crid` is ignored. |
| Video | **adm** | string | It conveys ad markup information for video creatives. For more information, please see [Video Ad Markup bidding (ADM)](video-ad-markup-bidding.md). |
| Video | **adomain** | string | The URL representing the brand of the `adm` content sent in the bid response. |

### Native creatives
| Media type | Field | Type | Description |
|:---|:---|:---|:---|
| Native | **crid** | string | The bidder's creative ID. Used to reference a Monetize creative based on the creative code set via the [Creative Service](creative-service.md). <br> **Note:** If both `adid` and `crid` are sent, `adid` takes precedence, and `crid` is ignored. |
| Native | **ver** | string | Specifies the version of the native ad specification in use. Only native version 1.2 is supported. |
| Native | **link** | object | The URLs associated with the native creative. The URLs must not exceed 2048 characters. For more information, see [Creative Service](creative-service.md). |
| Native | **adm** | string | It conveys ad markup information for native creatives. For more information, please see [Native 1.2 Ad Markup bidding (ADM)](native-ad-markup-bidding.md). |
| Native | **addomain** | string | The URL representing the brand of the `adm` content sent in the bid response. |

## Error responses
You may encounter the following errors during creative registration or audit. Use the recommended resolutions to troubleshoot issues.

| Error | Description | Resolution |
|:---|:---|:---|
| Creative not registered | The bid is rejected because the creative has not been sampled or the `crid` is missing or invalid. | Continue bidding until the creative is sampled and registered. Verify that the `crid` follows the correct format. |
| Creative audit pending | The creative is registered but is still under audit review. | If your supply allows unaudited creatives, bidding can proceed. Otherwise, wait for audit approval. |
| Invalid `adm` field | The `adm` (ad markup) field is missing or incorrectly formatted | Provide valid and complete ad markup in the `adm` field. |
| Missing `crid` | The `crid` field is missing in the bid response. | Assign and include a unique `crid` for each creative. |
| URL too long | A URL exceeds the 2048-character limit. | Shorten the URL before submitting the bid. |


## Related topics
- [Creative API services](creative-api-services.md)
- [Bidders - Creative service](creative-service.md)
- [Submit Auditable Dynamic Creatives](submit-auditable-dynamic-creatives.md)
- [Xandr macros](xandr-macros.md)
