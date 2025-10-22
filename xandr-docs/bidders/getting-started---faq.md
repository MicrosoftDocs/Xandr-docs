---
title: Getting Started - FAQ
description: This article provides answers to the frequently asked questions on how to get started with Bidder.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Getting started - FAQ

## Connection errors

### I'm not getting notify requests

You will only get notify requests if you win the auction or if you you lose because of an error. If you lose because you didn't bid the highest price, or because you no-bid, you won't get a notify request. Debug auctions will not send notify requests if you are running tags that have the parameter `&debug=1`. Finally, you must have the `"notify_uri"` set in for your bidder. Make sure that this is not a blank string, and that it points to your notify handler.

### I'm not getting traffic from my tag to my bidder

To run a debug tag in the sandbox run: `https://ib-test.adnxs.com/tt?id=YOUR_DEBUG_TAG_ID&debug=1`. This will print the output of the debug tag. You can look up your bidder ID to determine whether an impression was sent to your bidder. If the impression wasn't sent to your bidder, you will find the explanation next to your bidder ID. Common problems include:

1. [Pool isn't available](#pool-isnt-available).
1. Bidder does not accept unaudited URLs - change the `"send_unaudited"` flag on your bidder to `"true"`.
1. Member doesn't have a contract - reach out to your technical and account contacts at Xandr.

### Pool isn't available

When running a debugging session for your tinytag, if you see "Skipping bidder x because pool isn't available," this means that the impbus isn't able to connect to any of your instances. To debug this, you must make sure that:

1. Your bidder is active.
1. Your member is active.
1. You have registered bidder instances for your bidder, and that the bidder instances are active.
1. You are running a debug in a datacenter in which you have an active bidder instance. For example, if you only have a bidder instance in New York, but you are physically in LA, you will be routed to the LA datacenter and will not have any active bidder instances. To force an auction at a particular datacenter, you can run `ib.nym1.adnxs.com`. Currently the Test environment is only in NYM so ensure you have a bidder instance registered in our NYM datacenter.
1. Your bidder instances are responding to ready requests with a `1` (is there a firewall blocking outside IPs?).

## General settings

### Are there any settings that you recommend?

Yes. Make sure that the `send_class_2`, `send_class_3`, and `send_unaudited` are all set to `true` in the bidder service. These are artifacts of a legacy system and it is not recommended that you use them.
