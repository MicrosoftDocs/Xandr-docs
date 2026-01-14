---
title: Microsoft Monetize - Set up multi-buyer deals with DV360 buyers
description: In this page, learn how to setup multi-buyer deals with DV360 buyers
ms.date: 1/14/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupmabaruah
---

# Set up multi-buyer deals with DV360 buyers

Although the buyer targeting selection in Monetize allows you to select only a single DV360 buyer, you can create a deal that is accessible to **multiple DV360 buyers** by targeting a **Central Partner ID**.

This article explains how DV360 buyer structures work and how to correctly configure both **single-buyer** and **multi-buyer** deals.

---

## Understand DV360 buyer structure

DV360 buyers are integrated using **seats**, which allows you to target DV360 buyer IDs directly in Monetize.

There are two types of buyer IDs in DV360:

- **Partner IDs**  
  Represent individual DV360 buyers.

- **Central Partner IDs**  
  Act as umbrella seats that group multiple Partner IDs under a single financial entity.

A Central Partner ID does not actively bid. Instead, it enables all Partner IDs under it to access the same deal when the deal is synced with the Central Partner ID.

Based on this structure, there are two ways to configure deals:

- **Single-buyer deal**  
  Target a **Partner ID**. The deal is shared with one specific DV360 buyer.

- **Multi-buyer deal**  
  Target a **Central Partner ID**. The deal is available to all Partner IDs grouped under that Central Partner ID.

When you target a Central Partner ID, you should expect bids from multiple buyers.

---

## Set up a multi-buyer deal

The deal configuration process remains the same as for a single-buyer deal. The only difference is the buyer selected in the **Buyer** section.

To set up a multi-buyer deal:

1. Create a new deal.
2. In the **Buyer** section, select a **Central Partner ID** instead of a Partner ID.
3. Complete the remaining deal settings as required.
4. Save the deal.

Deals targeted to a Central Partner ID are accessible to all Partner IDs that fall under the same umbrella seat.

A deal can target only **one Central Partner ID**. However, you can also include additional buyers from other DSPs within the same deal.

> [!NOTE]
> A Central Partner ID often includes the term *Central Partner ID* in its name, but this is not guaranteed. You are responsible for confirming with the buyer whether the provided ID is a Partner ID or a Central Partner ID.

---

## When a Central Partner ID is not available in buyer selection

If a DV360 buyer provides a Central Partner ID that does not appear in the buyer selection list, the ID has not yet been registered in the system.

To resolve this issue:

1. Open a **Support Ticket**.
2. Request registration of the new buyer ID.
3. Clearly specify that the ID is a **Central Partner ID** to ensure it is registered correctly.

Once registered, the Central Partner ID will be available for deal targeting.

---

## Monitoring and reporting

The actual buyers bidding on a multi-buyer deal are visible in most reports.

For reporting:

- Select **Buyer Seat Name** and **Buyer Seat Code** as dimensions to identify bidding buyers.
- The **Seller Deal Metrics** report displays the **Central Partner ID** targeted in the deal.
- To view individual buyer activity, use the **Multi-Buyer Seller Deal Metrics** report, which provides a breakdown of all buyers purchasing under the deal.

For detailed buyer-level analysis, include **Buyer Seat Name** and **Buyer Seat Code** as dimensions in the report.
