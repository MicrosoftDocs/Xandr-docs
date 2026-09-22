---
title: Video Ad Pods
description: Learn how structured and dynamic video ad pods work in Microsoft Monetize and what publishers, supply partners, and bidders need to support them.
ms.date: 09/22/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Video ad pods

An ad pod is a commercial break: a sequence of video ads that play back-to-back inside one break, most often in connected TV and other streaming content. OpenRTB 2.6 pod bidding allows the break to be offered as a related set of opportunities instead of unrelated single ad slots.

Microsoft Monetize supports both structured and dynamic video ad pods. Supply-side support and buy-side enablement are separate. A supply partner can send OpenRTB 2.6 pod fields by using the 2.6 version header, but a bidder must be enabled for OpenRTB 2.6 to receive dynamic pod fields.

## Structured and dynamic pods

A **structured pod** has slots whose positions and acceptable durations are predetermined by the seller. Buyers bid against those known opportunities.

A **dynamic pod** specifies the total duration that buyers may fill and the maximum number of ads, but doesn't predetermine the exact number or duration of every ad. Microsoft Monetize assembles the winning sequence from eligible bid responses within those limits. A pod identifier groups opportunities into the same break, but a pod identifier by itself doesn't make a pod dynamic.

For field-level requirements, see:

- [Integration with OpenRTB 2.6 protocol for supply partners](../supply-partners/integration-with-openrtb-2-6.md#video-ad-pods)
- [Integration with OpenRTB 2.6 protocol for bidders](../bidders/integration-with-openrtb-2-6.md#video-ad-pods)
- [IAB Tech Lab OpenRTB 2.6 specification, September 2026 release](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md)

## Frequently asked questions

### What is an ad pod, and how is it different from a single video ad?

A single video ad fills one impression opportunity. An ad pod represents one commercial break that can contain multiple ads played in sequence. Pod signals let sellers and buyers treat those ads as parts of the same break and apply limits across the sequence.

### What is the difference between a structured pod and a dynamic pod?

In a structured pod, the seller defines each slot, including its position or acceptable duration, before the auction. In a dynamic pod, the seller defines the total fillable duration and maximum number of ads. The eligible bids determine the final number and duration of ads.

### Does Microsoft Monetize support dynamic ad pods today, and on which side of the platform?

Yes. Supply partners can send dynamic pods to Microsoft Monetize with OpenRTB 2.6. Microsoft Monetize can pass dynamic pod requests to bidders that are enabled for OpenRTB 2.6 and can process their multi-ad responses. Support on the supply side doesn't automatically enable a bidder on the buy side.

### What do I need to do as a publisher or SSP to send ad pods?

Send the OpenRTB version header with a value of `2.6`, describe the break with the supported pod fields, and make sure your ad server can consume a response containing multiple ads. For a dynamic pod, provide both the total fillable duration and the maximum number of ads. No separate supply-side enablement is required.

### What do I need to do as a bidder to buy them?

Ask your Microsoft account representative or support contact to enable OpenRTB 2.6. Your integration must read the pod constraints, return multiple bids when offering multiple creatives, and state each creative's duration. Return a guaranteed pod position only when the seller offered one.

### Why am I not seeing podded traffic even though I am integrated on OpenRTB 2.6?

OpenRTB 2.6 support alone doesn't create podded traffic. A seller must send pod inventory, dynamic pods must include the dynamic constraints, and the bidder must be enabled on the buy side. Inventory availability, targeting, auction eligibility, and demand can also affect whether a bidder receives or wins pod opportunities.

### How are the winning ads chosen and put in order?

Microsoft Monetize evaluates eligible bids and assembles a sequence whose creative durations fit within the seller's total duration and ad-count limits. If the seller guarantees a pod position, bids for that position are considered according to that constraint. Otherwise, the platform determines the final sequence from the eligible bids.

### What happens if the bids do not fill the whole pod duration?

The limits describe the maximum fillable duration and number of ads, not a requirement to fill every second or position. Microsoft Monetize can return a shorter sequence when the eligible bids don't fill the entire break. The seller's ad server or player controls how any remaining time is handled.
