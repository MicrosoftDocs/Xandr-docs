---
title: Prebid Server Premium Data Passthrough
description: In this article, find information about the data passthrough feature of Prebid Server Premium (PSP).
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Prebid Server Premium data passthrough

## SupplyChain object

Per the IAB, the SupplyChain (schain) object, along with sellers.json, identifies all of the intermediaries in the flow of money from the buying platform back to the publisher. It does not include an intermediary that does not participate in the money flow or systems that are paid a fee for their services but do not pay upstream sellers.

Prebid Server Premium (PSP) acts as a pass-through for requests and responses and although it incurs a fee for the publisher, PSP is not a financial entity in the chain. For this reason, the appnexus (Microsoft Advertising) node is not appended to the schain when requests are sent from PSP to external demand partners (SSPs). Those SSPs apply their node to the schain when they send the request on to DSPs.

More information on the SupplyChain object can be found [here](https://iabtechlab.com/wp-content/uploads/2019/07/FAQ-for-sellers.json_supplychain-object.pdf).

## Floors

When a publisher includes reserved price or price in the request to Microsoft Advertising, PSP passes the value on to demand partners. PSP does not pass yield management floors to demand partners. For more information on yield management, see [Working with Yield Management](working-with-yield-management.md).

## Global Placement ID (GPID)

The Global Placement ID (GPID) is passed by PSP to demand partners for publishers using these endpoints:

- `/openrtb2/prebid`
- `/ut/v3/prebid`
- `/ptv`
- `/ssptv`

We are working to support the remaining PSP endpoints.

More information on GPID via Prebid can be found [here](https://docs.prebid.org/features/pbAdSlot.html).
