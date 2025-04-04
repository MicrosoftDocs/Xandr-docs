---
title: Microsoft Monetize - November 26, 2024 - Household Attribution
description: Learn about the enhanced Blocked Bid Value metric in Microsoft Monetize Insight, helping identify impactful bid rejections to increase revenue.
ms.date: 11/26/2024
ms.topic: release-notes
---

# Microsoft Monetize - November 26, 2024: Enhanced blocked bid value metric

## Overview

The Blocked Bid Value metric in Microsoft Monetize Insight for the Bid Rejection pages (Ad Quality, Deals, YM Floors, and Buyer Issues) is upgraded to help you more precisely identify the rejections that, if unblocked, are more likely to help drive increases in revenue.

## Key updates

1. As per the enhancement, the **Blocked Bid Value** is now calculated as the difference between the blocked bid price and the transacted impression price, instead of summing all bid prices per impression.
   For example, consider the following scenario:

    **Scenario 1**:

     - Bid A: $4.5 CPM, rejected 1,000,000 times over the course of a week due to Ad Quality.
     - Bid B: $4.00 CPM, won the impression.
     - **Blocked bid impact**: $500 (0.5/1,000 * 1,000,000).
  
    **Scenario 2**:

    - Bid A: $4.00 CPM, rejected 1,000,000 times.
    - Bid B: $4.5 CPM, won the impression.
    - **Blocked Bid impact**: $0.
  
1. If the bid rejection occurred on an impression that did not deliver, the bid rejection is not counted.
1. If the bid is from a PG deal or GDALI that bids on a CPM, the bid rejection is not counted.
1. This is an **Indicative Metric** of impact, not a revenue prediction. Factors such as buyer frequency caps can influence bidding behavior after enabling blocked demand, which are not accounted for.

## FAQ

**Has the Seller Bid Error report changed?**

No, the Seller Bid Error report has not been changed. This is still the best place to see the full spectrum of errors, regardless of their likely revenue impact.

**How is impact calculated on non-transacting impressions?**

The blocked impact only looks at rejections on transacted impressions.

**How are pCPM line items and PG deals considered?**

As pCPM bids do not reflect the revenue of the line item, bids from PG Deals and GDALIs are not included in the blocked impact dataset.

### Related topics

- [Monetize Insights Ad Quality](monetize-insights-ad-quality.md)
- [Monetize Insights Deals](monetize-insights-deals.md)
- [Monetize Insights Demand Issues](monetize-insights-demand-issues.md)
- [Monetize Insights Floor Rules](monetize-insights-floor-rules.md)
- [Monetize Insights for Publishers](monetize-insights-for-publishers.md)
- [Monetize Insights Total Revenue](monetize-insights-total-revenue.md)