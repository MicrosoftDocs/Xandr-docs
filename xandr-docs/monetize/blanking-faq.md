---
title: Blanking FAQ
description: This page covers concepts related to Blanking, like what is Blanking, why it is served, why it is charged, where to see it, how to avoid it and how it will appear on your invoice.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Blanking FAQ

## What is "blanking"?

*Blanking* is when we serve a blank creative, resulting in an empty space where the ad would have been. It is technically the delivery of a `200 OK` response.

## What scenarios cause a blank to be served?

- **An auction is held but there is no demand**: In this scenario, the default creative or PSA for that size is not available, so a blank is served. The client can choose for a blank to serve rather than a PSA. To do so, set the parameter `PSA = no` in the ad tag.
  
  > [!NOTE]
  >  This is the only blanking scenario where you are billed and the blank is logged.

- **The Impbus fails for some reason**: In this case, no auction is held and a blank is served. Not billed or logged.
- **An excluded impression of some sort (either URL or User IP) on a blocklist**: In this case, no auction is held and a blank is served. Not billed or logged.

## Why do we charge for blanks?

Because it costs Microsoft Advertising, money to run an auction and serve a blank, and our clients have the option of turning blanks on or off, we charge for the blanks the same as we would for a creative or PSA.

## Where can I see blank activity?

You can see blank activity in Monetize reporting. From the reports tab, you will have the option to see blanks only or among other impression types. You can also see this on a publisher specific level to be sure you can pass along the costs to the publisher if necessary.

## How can I avoid blanks?

1. See [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md).
1. Set up defaults for uncommon placement sizes.
1. Consider contracts with publishers to pass along that cost.

## How will blanking charges show up on the invoice?

The blank charges will be rolled up into the line item **Managed Ad Serving Fee**. The difference in revenue for one month for most clients will be insignificant and thus, unnoticeable.
