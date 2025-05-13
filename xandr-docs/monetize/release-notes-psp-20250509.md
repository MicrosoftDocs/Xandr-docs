---
title: May 09, 2025 - Prebid Server Premium Brand Blocks
description: Explore the May 09, 2025 release, delving into Prebid Server Premium Brand Blocks
ms.date: 05/09/2025
ms.topic: release-notes
ms.author: rupambaruah
---

# January 09, 2025 - Prebid Server Premium Brand Blocks

Prebid Server Premium (PSP) publishers historically have, and still should, use ad quality controls in PSP demand partners' platforms so those partners send eligible bids to the Monetize auction. Publishers can now choose to enable two supplemental Monetize settings on PSP demand via the [ad profile service](../digital-platform-api/ad-profile-service.md):
 

1. apply_aq_on_psp: Checks bids from PSP demand partners against brand and category blocks in the ad profile or badv / bcat fields of the bid request. Uses seatbid.bid.adomain field to infer brand. Unknown adomains are allowed to serve unless reject_unknown_adomain_on_psp setting is enabled.
reject_unknown_adomain_on_psp: Rejects bids from PSP demand partners where seatbid.bid.adomain values are missing or have not yet been mapped to brands.

1. Blocking bids through these settings can impact publisher revenue. Publishers are encouraged to test a portion of their inventory with the apply_aq_on_psp setting (such as a specific publisher ID) via the ad profile and monitor revenue and blocked bids through:

 

- [Insights ad quality tab](monetize-insights-ad-quality.md)
- [Seller Bid Error report](seller-bid-error-report.md)
 

Once enabled, Publishers should work with demand partners driving high block rates to update ad quality settings in the relevant platforms. PSP documentation is available [here](prebid-server-premium-ad-quality.md).


