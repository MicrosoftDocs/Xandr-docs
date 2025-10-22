---
title: Debugging - FAQ
description: Explore valuable debugging insights in FAQs for common issues and solutions, providing useful information for effective problem-solving.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Debugging - FAQ

## Connection quality

**How can I get stats on technical data like timeouts, no_connections, and so on?**

This is available in the [Bidder UI](https://bidder.xandr.com/login) in the **Metrics** tab. Click edit and choose which metrics you would like graphed. Relevant metrics include No connections, Mapped user imps, Avg response time, Max  response time, and Timeout %.

## Traffic

**Why is my bidder not receiving any traffic?**

There are several reasons why a bidder may not be getting traffic. The following are the most common explanations. Please also see [Getting Started - FAQ](getting-started---faq.md).

- The bidder is not active. You can check your bidder's status with the [Bidder Service](bidder-service.md).
- You have not set up any bidder instances. You can set up a bidder instance with the [Bidder Instance Service](bidder-instance-service.md).
- Your bidder instances are not active. You must have at least one bidder instance active in the data center from which you would like to receive traffic.
- No active bidder instances are responding to the [Ready Request](ready-request.md). In order to receive traffic, a bidder instance must respond with a `1` to ready requests.
- You have no active, ready bidder instances in the data center to which you are sending traffic. If your bidder instances are all in the east coast, but you are sending traffic to the west coast data center, you will not receive any impressions.
- No member is active for your bidder. This can be change with the [Member Service](member-service.md).
