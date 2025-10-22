---
title: December 13, 2016 - Breaking Change to Replace sizes with format on Bid Requests
description: Explore transforming bid requests, replacing sizes with formats for a significant change in bid requests, aligning with OpenRTB standards.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# December 13, 2016 - Breaking change to replace sizes with format on bid requests

We have a new field for you: `imp.banner.format`. If you've used the `imp.banner.ext.appnexus.sizes` field, then you already know how to use the `format` field because it does the exact same thing. If you don't know what you'd use this field for, [take a look at the documentation](outgoing-bid-request-to-bidders.md). (Okay, here's a hint: it's an array of objects that represent the banner sizes permitted.)

We've made this change so we can follow the OpenRTB standard. Right now you can still use the `sizes` field, but you really should switch over because as of **February 17, 2017,** `sizes` will be deprecated and you'll wish you'd switched to `format`.

> [!NOTE]
> This change impacts only **External Bidders**.

As always, be sure to reach out to your account manager if you have questions or concerns.
