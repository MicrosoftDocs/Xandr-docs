---
title: StackAdpt DSP Buying Guide
description: In partnership with StackAdpt DSP, Microsoft has created this guide to help Microsoft Monetize publishers and curators communicate with their buyers about accessing and targeting Monetize’s publisher inventory using StackAdpt as their DSP.
ms.date: 05/12/2026
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# StackAdpt DSP buying guide

In partnership with StackAdpt DSP, Microsoft has created this guide to help Microsoft Monetize publishers and curators communicate with their buyers about accessing and targeting Monetize’s publisher inventory using StackAdpt as their DSP. This information has been created in collaboration with and approved by the StackAdpt team. Please note that the platforms can and will change regularly. We will do our best to update this guide as needed.

## Overview

This document guides you to correctly route traffic to StackAdapt. Upon successfully routing the traffic, clients will add the deal into their account via the ‘BYOD’ feature and initiate campaigns. The instructions provided apply to both Private-Marketplace (PMP) and Programmatic Guaranteed (PG) deals. 

### Bringing deals to StackAdapt

> [!NOTE]
> StackAdapt does not support account-specific seat IDs. You should send the deal to StackAdapt through a generic (any buyer) seat ID. Please read below for more details on how to identify the correct seat ID.

Once you curate the deal, the client should provide the Microsoft-specific seat ID. This seat ID is the same across all StackAdapt clients as the client will attach the deal directly to their own account on the platform. 

See below for Microsoft-specific instructions.

| **SSP** | **Seat ID** | ** Instructions** |
| --- | --- | --- |
| Microsoft Monetize | 3350 | Search for StackAdapt (3550) in either “Buyer” or “DSPs” (both will work) and choose the correct result. The successful selection will be confirmed by a green checkmark appearing in the selected view.|

> [!NOTE]
> PG Seat ID default to PMP Seat ID unless specified otherwise.

## Troubleshooting deals

- **You are not receiving any avails on the StackAdapt platform.**
Ensure that the seat ID is not the client account ID - the seat ID should be SSP specific, and can be found above. 
You should also ensure that the correct SSP is selected and that the deal_id information is inputted correctly. If you are still not receiving any avails, provide a sample bid request in a .txt file for StackAdapt’s inventory team to investigate further.

- **You are receiving avails but not bidding**
You should look at your campaign’s drop-off-funnel to troubleshoot why the campaign is not bidding. Campaign targeting preferences like geo-targeting, audience-targeting, or other goals may be limiting bids. If you target additional inventory and bid high enough for other inventory, but not for this specific deal, you may not see any issues in the drop-off funnel. 

- **You are bidding but not winning**
If you are bidding and not winning, StackAdapt has no insight into why bids are lost. The publisher and/or the SSP should be able to provide more insights on why bids are lost

- **You are seeing minimal spend on the deal**
If there are no technical issues with the deal but you are seeing minimal spend, try to send more avails to see how pacing metrics improve. You may be running on other inventory lines and are preferring other inventory over the publisher’s / SSP’s. 
