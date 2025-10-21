---
title: Guaranteed Delivery (GDALI)
description: In this article, learn about Guaranteed delivery augmented line items and the different delivery types that they have.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Guaranteed delivery (GDALI)

Guaranteed delivery line items help you meet delivery goals and serve budgets evenly and in full.

## New Guaranteed Delivery Augmented Line Item (GDALI)

Microsoft Advertising now offers a Guaranteed Delivery Augmented Line Item (GDALI) that is based on Microsoft Advertising's Augmented Line Item (ALI) and associated with the Seamless Insertion Order. The new GDALI offers similar features to the legacy guaranteed delivery line item (GDLI), but by consolidating onto the ALI framework, we have improved the feature set available for guaranteed delivery and provided a more intuitive workflow and user experience. For more information on the introduction of GDALIs, see [Guaranteed Delivery Line Item FAQ (GDALI)](guaranteed-delivery-line-item-faq-gdali.md).

For instructions on creating a GDALI, see [Create a Guaranteed Delivery Line Item (GDALI)](create-a-guaranteed-delivery-line-item-gdali.md).

## Guaranteed delivery

For direct-sold business, where sales has secured an insertion order from a buyer with a committed impression volume, the most important performance indicator is that the line item delivers its budget in full and evenly across its flight dates. We call this type of line item a Guaranteed Delivery (or "Guaranteed") Line Item, and it has the following properties:

- Delivers budget in full across its flight dates.
- Delivers budget evenly across its flight dates.
- Delivers on guaranteed goals while still (optionally) competing in the auction with other demand such as RTB, a feature made possible with Open Dynamic Allocation (for more information, see [Open Dynamic Allocation and Flexible Priorities](open-dynamic-allocation-and-flexible-priorities.md)).

## Delivery types

GDALIs have the following delivery types that determine how they will be prioritized in an auction:

- Impressions – GDALIs with this delivery type have impression-based goals, which they will attempt to meet while pacing evenly throughout the day (or daypart). They typically have priorities ranging from 11-17.
- Exclusive – GDALIs with this delivery type have percentage-based goals and have the highest priorities possible, typically ranging from 18-20. They will attempt to serve the scheduled percentage of total impressions where their targeting matches and they are eligible to serve.

For examples of how GDALIs with these delivery types behave in auctions, see [Guaranteed Delivery Auction Mechanics](guaranteed-delivery-auction-mechanics.md).

## Related topics

- [Create a Guaranteed Delivery Line Item (GDALI)](create-a-guaranteed-delivery-line-item-gdali.md)
- [Guaranteed Delivery Line Item FAQ (GDALI)](guaranteed-delivery-line-item-faq-gdali.md)
