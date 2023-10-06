---
title: Microsoft Invest - How Guaranteed Outcomes Work
description: This article explains how guaranteed outcomes work. The outcome-based bids from the buyer are translated into impression-based CPM revenue for the seller.
---

# Microsoft Invest - How Guaranteed Outcomes work

The following overview describes the logic of Guaranteed Outcomes:

- Guaranteed Outcomes are possible because the Xandr Exchange automatically translates outcome-based bids (vCPM & CPCV) from the buyer into impression-based CPM revenue for the seller. This translation facilitates the transaction by bridging the currency gap between buyer and seller.
- Buyers who choose to buy with Guaranteed Outcomes enter an outcome-based bid (e.g. vCPM for Views and CPCV for Completes) as opposed to an impression-based CPM bid. Their bid will be converted and enter the seller's auction as an impression-based CPM bid, with normal auction mechanics applied.
- If the bid wins the auction, the seller is paid the impression-based CPM price. The buyer's creative is served, and the buyer is only charged if the desired outcome is measured on the impression.
- By default, Xandr uses the IAB definition of a viewable ad (50% of pixels in-view for 1 continuous second) and the Xandr measurement script to determine a view. However, we support additional viewability definitions and measurement technology vendors as well. See [Introduction to Viewability](./introduction-to-viewability.md) for more information about choosing these alternate measurements.
- For Guaranteed Completes, we always define a complete as a served video ad that reaches 100% of its duration.

## Related topics

- [Guaranteed Outcomes](./guaranteed-outcomes.md)
