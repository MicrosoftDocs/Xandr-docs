---
title: Yield Analytics 7.13
description: In this page, Learn how addition of Pre-Bid affects the Channel Management.  
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 7.13

## Channel management announcement

Channel Management is currently based on order lines. With the addition of Pre-Bid, we are now basing it on explicit product mappings. The following changes must be made:

- Product overlaps were applied based on overlaps that exist elsewhere in the system. Thus, they are less accurate than desired.
- With the explicit product mappings we can ensure that the reports are returning data to meet your specific needs.
- Order line based reporting will be deprecated. (This is why you see duplicate metrics at the moment. One is an order line metric, and the other is a product metric).

## Enhancements

Frequency Caps in Real Time Reservation - Real Time Reservations now support Frequency Capping, and return proper forecast results - based on this constraint.

## Fixes

Direct target attribute `attibute ! in`  is not functioning.

Detect if the user's session has changed -  If you have pages open in other tabs and get logged-out, you will see a message that says: “The current page has expired and was reloaded”.
