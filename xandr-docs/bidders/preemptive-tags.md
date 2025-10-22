---
title: Preemptive Tags
description: In this article, learn about Preemptive tags and how they work.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Preemptive tags

Xandr offers two kinds of tags: [TinyTags](tinytags.md) and Preemptive tags.

Preemptive Tags are like TinyTags, but with a slightly different ad call procedure. They allow Xandr to hold an auction on the ad call and then pass the highest bid on to the publisher's ad server to decide how best to fill the impression. This solution gives sellers more transparency into market demand, more control over the bid process, and a greater array of advertiser demand.

## How it works

1. Create Xandr as an advertiser in your regular ad server and add the appropriate trafficking parameters. This allows the highest Xandr bid to be recognized by your ad server.

1. Either a preemptive tag is placed on the publisher's page or some other solution is reached, such as a CNAME redirect, in order to ping Xandr's impression bus as a first stop. See your Xandr contact for details.

1. An [auction](auction-overview.md) is held and a winning bidder is decided.

1. The impression bus passes the winning creative and the winning price on to the third-party ad server. Xandr appears as a bidder or a participant to that ad server.

1. That ad server decides whether to show the Xandr creative or to show another.

1. If it shows another ad, the call does NOT return to Xandr. If Xandr "wins", then the call passes back through the impression bus and the winning ad is served to the page.

## Related topics

- [TinyTags](tinytags.md)
- [Auction Overview](auction-overview.md)
