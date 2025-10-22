---
title: Ready Requests
description: In this article, learn what the Ready Request is and how to receive and respond to ready requests.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Ready requests

The Ready Request asks your bidder if it is ready to receive requests. If an instance fails to respond to three subsequent requests, or responds that it is not ready on any request, it will be taken out of rotation and no further requests (bid, click, etc.) will be sent to this instance until it responds that it is ready.

## Receiving ready requests

To receive ready requests, set the `ready_uri` field of the [Bidder Service](bidder-service.md) to the URI at which you want to receive these requests.

## Responding to ready requests

To indicate readiness, respond with the character `1` in the response. This can be in any form - JSON, free text, etc. - as long as a `1` is present.

> [!WARNING]
> Do not use the character `1` anywhere in your not-ready response. If you do, your not-ready response will communicate readiness. For example, a not-ready response such as `ready: "false (version 1.1)"` would be misinterpreted because of the presence of the character `1`.

## Related topics

- [Bidder Service](bidder-service.md)
- [Bidder Instance - FAQ](bidder-instance---faq.md)
