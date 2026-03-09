---
title: Microsoft Monetize (March 6, 2026) Deal sync status visibility and filtering
description: Learn about Deal sync status visibility and filtering
ms.topic: release-notes
ms.date: 03/06/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rbaruah
---

# Deal sync status visibility and filtering

**Release date:** March 6, 2025  
**Product:** Microsoft Monetize  
**Area:** Deals  
**Status:** General Availability (GA)

## Overview

Microsoft Monetize now provides visibility into **deal synchronization status with DSP buyers**. This update allows users to view the current sync state of a deal directly in the **Deals screen** and track whether buyers have accepted, targeted, or declined the deal.

This feature helps sellers quickly understand whether a deal has successfully synced to buyers and whether it is actively being targeted.

---

## Checking deal sync status

You can view a deal’s sync status in the **Deals screen** under the **Buyer** column.

- For **single-buyer deals**, the sync status is displayed directly in the deals grid.
- For **multi-buyer deals**, buyer-specific sync information is available in the **Settings side pane**.
- Sync status is **not displayed** for deals targeted to the entire DSP.

---

## Sync status labels

The following sync statuses may appear:

| Status | Description |
|------|-------------|
| **Syncing** | The deal is queued to sync in the next hourly batch. |
| **Syncing Error** | The deal attempted to sync but an error occurred. The system will retry in the next batch. |
| **Pending** | The deal was successfully sent to the DSP and is awaiting buyer acceptance. |
| **Accepted** | The buyer has accepted the deal in their DSP. |
| **Targeted** | The buyer is actively targeting the deal with at least one line item. |
| **Archived** | The buyer archived the deal in the DSP and can no longer buy it. |
| **Declined** | The buyer declined the deal. Contact the buyer for additional details. |

---

## Filtering by sync status

You can filter deals based on their sync status using the **Filters** located at the top of the **Deals screen**, next to the search bar.

This allows you to quickly identify deals that are:

- Awaiting buyer acceptance
- Experiencing synchronization issues
- Actively targeted by buyers

## Related topics

- [Explore and manage deals](explore-and-manage-deals.md)
- [View deal details](view-deal-details.md)
