---
title: Microsoft Curate - Understand Buyer Seat IDs
description: Learn about Buyer Seat IDs, which let external DSPs use proprietary buyer IDs instead of Microsoft Advertising member IDs.
ms.date: 11/15/2023
---

# Microsoft Curate - Understand buyer seat IDs

Buyer Seat IDs allow external DSPs to use proprietary buyer IDs for the buyers they manage, rather than using a Microsoft Advertising member ID. If a DSP has implemented this feature, you can choose between member and seat IDs when creating a deal and reporting on buyers.

Certain external DSPs have already set up Microsoft Advertising to use IDs internal to their bidder systems, so they can easily map activity to specific seats without creating an intermediary Microsoft Advertising ID. This means you can now see both Microsoft Advertising member IDs and a breakdown of individual seat IDs for external DSPs when you select from lists of buyers. While Microsoft Advertising member IDs are typically 4-6 digits, seat IDs can look different for every DSP. Seat IDs are only unique within a DSP. In other words, multiple DSPs might use the same seat ID.

Before you can set up deals with a DSP's buyer seats, the DSP needs to register the IDs with Microsoft Advertising. DSPs have several mechanisms for uploading new seats:

- DSPs can register new seats whenever they want using the [Seat service](../bidders/seat-service.md).
- The first time a new seat ID is used to bid on inventory, Microsoft Advertising registers it automatically.

If a DSP hasn't registered a seat or submitted bids with it before, you won't see the seat when you're trying to set up a deal. If you experience this problem, reach out to the buyer and have them work with the DSP to get the seat registered with Microsoft Advertising.

You may encounter seat IDs that are not yet eligible for creating deals. To ensure a successful deal, check the reference table in [External DSPs Using Buyer Seat IDs](external-dsps-using-buyer-seat-ids.md).
