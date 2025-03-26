---
title: Microsoft Monetize - Universal ID Support
description: This article provides summary of the Universal IDs that are supported by Microsoft Monetize.
ms.date: 03/04/2025
ms.author: shsrinivasan
---

# Microsoft Monetize - Universal ID support 

This page summarizes the Universal IDs supported by Microsoft Monetize. All integrations are with a Universal ID solution provider (not facilitated by Microsoft), and Microsoft Publisher Enablement is not necessary. Universal IDs supported by our SSP are passed to DSP bidders by default.

## Supported Universal IDs

| ID Solution |Source Name |Supported Endpoint | Support level |Frequency Capping Capabilities  |Audience Onboarding/Activation Capabilities |
|:---|:---|:---|:---|:---|:---|
|Criteo|[criteo.com](https://www.criteo.com/)| AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** |No |No|
|Unified ID 1.0 (aka TradeDesk ID, TTID) |[adserver.org](https://adserver.org)|AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** |
|NetID |[netid.de](https://netid.de)|AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Full support (SSP + DSP support)* |Yes |Yes |
|LiveRamp RampID |[liveramp. com](https://liveramp.com/) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Full support (SSP + DSP support)* | Yes | Yes |
|UID2.0 |[uidapi.com](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)**  |No |No |
|UID2.0 via LiveRamp <br><br>**Note**: Reach out to a Microsoft Monetize representative to enable UID2.0 via Liveramp.|[uidapi.com](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0)  | AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)**  | No  | No |
|HadronID (Audigent) |[audigent. com](https://audigent.com/) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** | No  |No |
|Publink (Epsilon) |[epsilon.com](https://www.epsilon.com/apac) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** |No |No  |
|ID5 |[id5-sync. com](https://id5.io/) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap  | Passthrough (SSP support Only)**  |No |No |
|sharedID |[pubcid.org](https://docs.prebid.org/dev-docs/modules/pubCommonId.html) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** |No |No |
|EUID |[euid.eu](https://partner.thetradedesk.com/v3/portal/euid/overview) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** | No |  No |
|Yahoo Connect |[yahoo.com](https://www.yahoo.com/) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)** |No |No |
|Utiq |[utiq.com](https://utiq.com/) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap | Passthrough (SSP support Only)**  |No  |No  |
|Panorama ID |[crwdcntrl.net](https://crwdcntrl.net) |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap |Passthrough SSP support only**  |No |No |
|Utiq MartechPass |`utiq-mtp.com` |AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap |*This ID is used as a publisher first-party ID, not as a cross-publisher universal ID. Monetize member approval and enablement is required to use this ID. Please reach out to your Monetize account manager if interested.* |*Requires enablement*  |*Requires enablement*  |
|LinkedIn ID|[linkedin.com](https://linkedin.com/)|AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap|Passthrough (SSP support only)**|No|No  |
|First ID|[first-id.fr](https://first-id.fr/)|AST (ut/v3), prebid.js (ut/v3/prebid), openrtb, ptv, ssptv, vmap, ssvmap|This ID is used as a publisher first-party ID, not as a cross-publisher universal ID. Monetize member approval and enablement is required to use this ID. Please reach out to your Monetize account manager if interested.|No|No|
|LiveIntent - Index Exchange ID | `liveintent.indexexchange.com` | Index Exchange ID | Passthrough for Prebid Server Premium | No | No |
|LiveIntent - Triplelift ID | `liveintent.triplelift.com`| Triplelift SSP ID | Passthrough for Prebid Server Premium | No | No |
|LiveIntent - Rubicon ID | [rubiconproject.com](rubiconproject.com)| Rubicon SSP ID | Passthrough for Prebid Server Premium | No | No |
|LiveIntent - Openx ID | [openx.net](openx.net)| OpenX SSP ID | Passthrough for Prebid Server Premium | No | No |
|LiveIntent - Pubmatic ID | [pubmatic.com](pubmatic.com)| PubMatic SSP ID | Passthrough for Prebid Server Premium | No | No |

> [!NOTE]
>
> - Email your ID solution provider and Microsoft Representative to enable Universal IDs, such as RampID, in LLD.
>
> - *Full support (SSP + DSP support): The ID is supported in both Microsoft Monetize and Microsoft Invest. This means Microsoft Invest buyers can use the ID for audience segments, frequency and recency caps, and attribution.
>
> - **Passthrough (SSP support Only): The ID is only supported in Microsoft Monetize. This means that the identifier is not used by Microsoft Invest for frequency/recency capping, segments, and attribution, but the identifier is passed on to third-party Bidders/DSPs that may support these capabilities.
