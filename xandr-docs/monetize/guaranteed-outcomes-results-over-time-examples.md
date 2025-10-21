---
title: Microsoft Monetize - Guaranteed Outcomes Results Over Time (Examples)
description: In this article, find information about the predicted outcome rate for Guaranteed Outcomes and its impact on the amount billed versus the amount paid with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Guaranteed outcomes results over time (Examples)

The auction mechanics for Guaranteed Outcomes create a short-term disconnect between how the buyer is charged and how the seller is paid. On average and over time, this disconnect is averaged out. In other words, for any single impression, it is likely that the seller is paid either significantly more or less than the buyer has been charged. Over many impressions, however, the difference between what is charged and what is paid should converge.

The key factor in this convergence is the accuracy of the predicted outcome rate; that is, the difference between the actual outcome rate and the predicted outcome rate. To illustrate the impact of prediction accuracy on the amount billed versus the amount paid, three different scenarios are described below - perfect prediction, under prediction, and over prediction. We've used Guaranteed Views for these examples, but the same holds true for Guaranteed Completes.

In the examples below:

- A buyer using Guaranteed Views bids $10 vCPM on supply with a 50% predicted viewability rate.
- The Exchange converts the vCPM bid to a $5 eCPM bid.
- The second-highest bid in the auction is a $4 CPM bid.
- It is a second price auction, so seller is paid $4.01 CPM.
- The buyer is charged $8.02 vCPM (that is, only if the impression is measured viewable).

## Perfect prediction

If the Exchange perfectly predicts the viewability rate for a given piece of inventory, then the aggregate amount charged to the vCPM buyer should match the aggregate amount paid the seller.

## Over-prediction

If the Exchange over-predicts the viewability of the inventory, then the aggregate amount charged to the vCPM buyer is less than the aggregate amount paid to the seller. In this example, the Exchange predicted a 50% viewability rate, but the inventory had only a 25% viewability rate. The Exchange is left with a negative balance.

## Under-prediction

If the Exchange under-predicts the viewability of the inventory, then the aggregate amount charged to the vCPM buyer is greater than the aggregate amount paid to the seller. In this example, the Exchange predicted a 50% viewability rate, but the inventory had a 75% viewability rate. The Exchange is left with a positive balance.

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [Guaranteed Delivery Auction Mechanics](guaranteed-delivery-auction-mechanics.md)
