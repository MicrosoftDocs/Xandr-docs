---
title: Simulate Traffic on a TinyTag
description: Learn how When a TinyTag is created, the API returns its ID that is used to create the URL that simulates traffic on this TinyTag.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Simulate traffic on a TinyTag

When a TinyTag is created, the API returns its ID.

This ID is used to create the URL that simulates traffic on this TinyTag.

> [!NOTE]
> Which URL to call?
>
> If your bidder is set up in the test environment, use this template:  
> `https://ib-test.adnxs.com/ttj?id=(TINY_TAG_ID)&size=(WIDTHxHEIGHT)&debug_member=(YOUR_MEMBER_ID)`
>
> If your bidder in the test environment is only buying mobile inventory, use this template:
>
> `https://ib-test.adnxs.com/mob?st=mobile_app&id=(TINY_TAG_ID)&size=(WIDTHxHEIGHT)&debug_member=(YOUR_MEMBER_ID)`
>
> TT vs. TTJ
>
> The element in the auction URL, `/ttj` can also be set to `/tt`.
>
> `/ttj` denotes a JavaScript tinytag (placement or ad tag).
>
>`/tt` denotes an iFrame tinytag (placement or ad tag). 
>
> We recommend testing both `/tt` and `/ttj` to ensure your creatives

Assuming all of the API calls in this section run successfully, running the TinyTag populated with your ID should make a [Bid Request](outgoing-bid-request-to-bidders.md) from the selling member to all bidders, requesting a bid and a creative sized for the TinyTag's parameters.

Please run the debug auction URL from within a web browser. This will show you the output of the auction and can assist you with troubleshooting your bidder's responses to an auction.

If you want to run a full auction, to generate notification requests, remove the `debug_member=(YOUR_MEMBER_ID)` from the URL shown above. You will see a creative render in the browser and your bidder will receive notification requests to the `notify_uri` location you specified using the [Bidder Service](bidder-service.md).

> [!TIP]
> Set objects to active
>
> Make sure you've set your bidder object and bidder instance object to `active` (using the [Bidder Service](bidder-service.md) and [Bidder Instance Service](bidder-instance-service.md), respectively).
> Make sure your `ready_uri` is responding with a '1'.

Next step: [Processing the Bid Request](process-the-bid-request.md)
