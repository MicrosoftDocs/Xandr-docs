---
title: Industry ID Support Matrix for Sellers
description: This article provides summary of the kind of Industry IDs and handlers that are supported.
ms.date: 10/28/2023
---

# Industry ID support matrix for sellers

This page provides a summary of the Industry IDs and handlers that are supported by Xandr.

| ID Solution |Source Name |Endpoint Supported |Regional Availability of Solution |Frequent Capping Capabilities  |Audience Onboarding/Activation Capabilities |Attribution Capabilities |Publisher Setup |Xandr Publisher Enablement |External Bidder Enablement |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
|Criteo|[criteo.com](https://www.criteo.com/)|ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global |No |No| No |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Xandr sends bids to all bidders after consent and bidder profile checks. Consent check is based on privacy checks, while TCF string and CCPA are checked for cookies and other IDs. Bidder profile check determines eligibility for bid request.|
|Unified ID 1.0 (aka TradeDesk ID, TTID) ||ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap, ttj |Global |No | No |No |Integration with ID solution provider (not facilitated by Xandr)|Not needed|Not needed. Xandr sends it to all bidders after consent and bidder profile checks. |
|NetID ||ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap | Germany |Yes |Yes | Yes |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Xandr sends it to all bidders after consent and bidder profile checks. |
|LiveRamp RampID |[liveramp. com](https://liveramp.com/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap | Global | Yes | Yes |Yes |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Xandr sends it to all bidders after consent and bidder profile checks. |
|UID2.0 |[uidapi.com](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global  |No |No  |No |Integration with ID solution provider (not facilitated by Xandr)  | Not needed |Not needed. Xandr sends it to all bidders after consent and bidder profile checks. |
|UID2.0 via LiveRamp |[uidapi.com](https://www.thetradedesk.com/us/about-us/industry-initiatives/unified-id-solution-2-0)  | ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |US only  | No  | No  | No  |Integration with ID solution provider (not facilitated by Xandr)<br><br>Publisher needs to work with LiveRamp to enable this option in SideCar| Needs to be enabled for LiveRamp. |Needs to be enabled for LiveRamp. |
|HadronID (Audigent) |[audigent. com](https://audigent.com/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap | Global | No  |No |No |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Controlled by Audigent and only enabled for Audigent RTDP instance and PSP. |
|Publink (Epsilon) |[epsilon.com](https://www.epsilon.com/apac) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global |No |No  |No  |Integration with ID solution provider (not facilitated by Xandr)    |Not needed |Not needed. Controlled by Epsilon and only enabled for Epsilon bidder instance and PSP. |
|ID5 |[id5-sync. com](https://id5-sync.com/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap  |Global  |No |No | No |Integration with ID solution provider (not facilitated by Xandr) |Not needed  |Not needed. Currently controlled by ID5 and only enabled for TTD, Amobe, Adform, DeepIntent, Active Agent, Patform 161, Travel Audience bidders, and PSP. |
|sharedID |[pubcid.org](https://pubcid.org/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global |No |No  | No  |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Enabled for Epsilon, Active   Agent, Criteo, Quantcast, RTB House, bidder, and PSP. |
|EUID |[euid.eu](https://euid.eu/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap    |Global    |No    |  No | No |Integration with ID solution provider (not facilitated by Xandr)    |Not needed    |Not needed. Only enabled for TTD currently.|
|Yahoo Connect |[yahoo.com](https://www.yahoo.com/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global |No |No |No |Integration with ID solution provider (not facilitated by Xandr) |Not needed |Not needed. Controlled by Yahoo and enabled for Yahoo bidder and PSP only. |
|Utiq |[utiq.com](https://utiq.com/) |ut, openrtb2, ptv, prebid, ssvmap, ssptv, vmap |Global  |No  |No  |No |  Integration with ID solution provider (not facilitated by Xandr) |Not needed |Enabled for Adform. Criteo is the only DSP currently supporting utiq. |
