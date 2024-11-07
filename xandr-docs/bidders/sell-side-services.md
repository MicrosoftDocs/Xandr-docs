---
title: Bidders - Services (Sell-Side)
description: Learn how publishers use ad tags on their pages. Some will keep preexisting ad while others will use new Xandr tags. Also, this page covers two main implementations for selling inventory through Xandr.   
ms.date: 10/28/2024

---


# Bidders - Services (Sell-Side)

At Xandr, some publishers will keep preexisting ad tags on their pages; others will use new Xandr tags. It depends on their original ad serving solution and the ways in which they wish to modify that solution with Xandr services.

## Implementation

There are two main implementations for selling inventory through Xandr:

1. [TinyTags.](tinytags.md) TinyTags are the most straightforward solution. A TinyTag is placed on a publisher's page. The most basic form of a TinyTag is: `ib.adnexus.com/tt?id=123`.

1. [Preemptive Tags.](preemptive-tags.md) PriceCheck is used in conjunction with another ad solution, usually an exchange. PriceCheck can either refer to a modified TinyTag or to keeping a preexisting tag.

TinyTag and PriceCheck tags are associated with unique IDs that map to tag data stored server side. This means that once tags are in place, you can modify them without having to re-tag the page. Simply add or change information within Xandr storage.
