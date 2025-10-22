---
title: Identify Impression and Spending Rules - FAQ
description: This article provides answers to the frequently asked questions on how to identify impression and spending rules.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Identify impression and spending rules - FAQ

Most discrepancies exist because different systems use different rules to count impressions or spend. The following are some things to look for as you try to resolve discrepancies related to impression counting and spend.

## When are impressions counted?

To evaluate impressions counting, review when an impression is recorded in your system and compare that to when impressions are recorded by Xandr. The following is a list of when impressions might be recorded:

1. At the time the creative is completely received by the user device.
1. At the "win notification" or "nurl" call reception time.
1. At the creative call time.
1. At the creative display on the publisher page or app time.
1. At an imp tracking pixel call time contained in the creative code.
1. At an imp tracking pixel call time integrated as third-party pixel of the creative object. If an imp tracking pixel is used, note whether it is JS or IMG type.
1. At the redirection time, from the imp tracking tech to the creative call.
1. At the redirection time, from the imp tracking tech to an imp tracking pixel contained in the creative code.
1. At the redirection time, from the imp tracking tech to an imp tracking pixel integrated as a third-party pixel object of the Xandr creative object.
1. Another custom time unique to your system.

## How are impressions counted?

In addition to *when* an impression is counted, you'll want to note *how* impressions are counted. Here are some possibilities:

1. Is imp tracking tech using a blocklist based on IP Address (blocklisting invalid traffic, robots, spiders)? Is this list IAB compliant?
1. Is imp tracking tech counting the impressions for cookieless users?
1. What is the user match rate you detect between Xandr and your imp tracking tech?
1. Bid request can come with multiple impressions, are you able to handle those multiple impressions in the bid request? Try to confirm that you implemented the logic that handles the different impressions using different IDs and that you're not mixing impression counts.

## Where are impressions counted?

After evaluating *when* and *how*, you should look at *where* impression-counting is happening. Possible locations include:

- A specific creative
- Seller
- Hour
- Geo
- Browser
- Carrier
- Device
- Third-party brand safety
- Creative swapping
- Third-party viewability or third-party tracking vendors used by adding pixels into creatives

## Spend rules

If you're having spend discrepancies, note how you're getting your spend:

- Macro `${AUCTION_PRICE}` in nurl
- Macro `${PRICE_PAID}` in a tracking pixel
- Macro `${PRICE_PAID}` in the creative code call
- Macro `${PRICE_PAID}` in the redirecting URL of the creative URL call
