---
title: Prebid Server Premium Ad Quality
description: Prebid Server Premium (PSP) brings demand from other platforms to compete alongside bids from Microsoft Monetize's integrated bidders.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Prebid Server Premium ad quality

Prebid Server Premium (PSP) brings demand from other platforms to compete alongside bids from Microsoft Monetize's integrated bidders. The creative from other platforms, typically supply-side platforms (SSPs), is not registered in Microsoft Monetize the way creative from Monetize bidders is registered and audited, preventing most Monetize ad quality controls from being applied.

PSP publishers should use the ad quality controls in each demand partner's platform to ensure partners send bids with creative that is eligible to win and serve in the Microsoft Monetize auction.

## Microsoft Monetize controls

As a secondary level of control, publishers can choose to enable two Monetize settings on PSP demand via the [ad profile service](../digital-platform-api/ad-profile-service.md):
- **`apply_aq_on_psp`:** Determines if brand and category blocks in the [ad profile](../digital-platform-api/ad-profile-service.md) or `badv` or `bcat` fields of the bid request will apply to bids from Prebid Server Premium demand partners. Uses `seatbid.bid.adomain` field to infer brand.
- **`reject_unknown_adomain_on_psp`:** Related to `apply_aq_on_psp`. Determines if `seatbid.bid.adomain` values that have not yet been mapped to brands can be auctioned or blocked.

## Example

The example request below updates an existing ad profile to include PSP settings. To avoid having to include all of the content from the existing profile in the PUT request, include the `append=true` query string parameter.

```
{
    "ad-profiles": [
        {
            "apply_aq_on_psp": true,
            "reject_unknown_adomain_on_psp": false
        }
    ]
}
```

## Monitoring

Blocking bids through either or both of these settings can impact publisher revenue. Sellers are encouraged to test with a portion of their inventory (such as a specific publisher ID) via the ad profile and monitor revenue and blocked bids through:

- [Insights ad quality tab](monetize-insights-ad-quality.md)
- [Seller Bid Error report](seller-bid-error-report.md)

> [!NOTE]
> If you do not yet have access to Monetize APIs, please reach out to [Product Support](https://support.ads.microsoft.com/sign-in).

## Related topics

- [Ad profile service](../digital-platform-api/ad-profile-service.md)
- [Working with Ad quality](working-with-publisher-ad-quality.md)