---
title: Yield Analytics 7.13
description: Learn how addition of Pre-Bid has changed the basing of Channel Management from order lines to explicit product mappings. 
ms.date: 10/28/2023
ms.custom: yield-analytics-ui

---


# Yield analytics 7.13

## Channel management announcement

Channel Management is currently based on order lines. With the addition
of Pre-Bid, we are now basing it on explicit product mappings. The
following changes must be made:

- Product overlaps were applied based on overlaps that exist elsewhere
  in the system. Thus, they are less accurate than desired.
- With the explicit product mappings we can ensure that the reports are
  returning data to meet your specific needs.
- Order line based reporting will be deprecated. (This is why you see
  duplicate metrics at the moment. One is an order line metric, and the
  other is a product metric).

## Enhancements

Frequency Caps in Real Time Reservation - Real Time Reservations now
support Frequency Capping, and return proper forecast results - based on
this constraint.

## Fixes

Direct target attribute `attibute ! in`  is not functioning.

Detect if the user's session has changed -  If you have pages open in
other tabs and get logged-out, you will see a message that says: “The
current page has expired and was reloaded”.








