---
title: Microsoft Monetize - Understanding Buyer Seat IDs
description: In this article, find information about buyer seat IDs and their advantages.
ms.date: 12/18/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Understanding buyer seat IDs

## Buyer seat IDs

Buyer seat IDs allow external DSPs to use their own proprietary buyer identifiers instead of Microsoft Monetize Member IDs. If a DSP or demand partner supports buyer seat IDs, you can choose whether to work with **member IDs** or **seat IDs** when using Microsoft Monetize.

Some external DSPs use identifiers that are internal to their bidder systems. This allows them to map activity directly to individual buyer seats without creating an intermediary Microsoft Monetize Member ID.

As a result, Microsoft Monetize surfaces both **Microsoft Monetize Member IDs** and a breakdown of individual **buyer seat IDs** for supported external DSPs.


## Seat ID characteristics

- Microsoft Monetize Member IDs typically contain 4–6 digits.
- Buyer seat IDs vary by DSP and don’t follow a standard format.
- Buyer seat IDs are **unique only within a DSP**. The same seat ID value may exist across multiple DSPs.


## Seat registration requirements

Before you can use a DSP’s buyer seat IDs in ad quality rules, deals, or reporting, the DSP must register those seat IDs with Microsoft.

DSPs can register buyer seat IDs in the following ways:

- **Manual registration**: DSPs can register new seats at any time by using the [Seat service](../bidders/seat-service.md).
- **Automatic registration**: When a new seat ID submits its first bid on inventory, Microsoft Monetize automatically registers it.

If a DSP hasn’t registered a seat ID and hasn’t submitted bids using that seat, the seat won’t appear when you configure ad quality rules or deals. If this occurs, contact the buyer and ask them to work with the DSP to register the seat with Microsoft Monetize.


## Deal eligibility

Some buyer seat IDs may be registered but not yet eligible for deal creation. To avoid issues, review the reference table in [External DSPs Using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md) before setting up a deal.



<!-- 

Buyer Seat IDs allow external DSPs to use proprietary buyer IDs for the buyers they manage, rather than using a Microsoft Advertising member ID. If a DSP has implemented this feature, you can choose between member and seat IDs when creating a deal and reporting on buyers.

Certain external DSPs have already set up Microsoft Advertising to use IDs internal to their bidder systems, so they can easily map activity to specific seats without creating an intermediary Microsoft Advertising ID. This means you can now see both Microsoft Advertising member IDs and a breakdown of individual seat IDs for external DSPs when you select from lists of buyers. While Microsoft Advertising member IDs are typically 4-6 digits, seat IDs can look different for every DSP. Seat IDs are only unique within a DSP. In other words, multiple DSPs might use the same seat ID.

Before you can set up deals with a DSP's buyer seats, the DSP needs to register the IDs with Microsoft Advertising. DSPs have several mechanisms for uploading new seats:

- DSPs can register new seats whenever they want using the [Seat service](../bidders/seat-service.md).
- The first time a new seat ID is used to bid on inventory, Microsoft Advertising registers it automatically.

If a DSP hasn't registered a seat or submitted bids with it before, you won't see the seat when you're trying to set up a deal. If you experience this problem, please reach out to the buyer and have them work with the DSP to get the seat registered with Microsoft Advertising.

You may encounter seat IDs that are not yet eligible for creating deals. To ensure a successful deal, check the reference table in [External DSPs Using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md).
-->
