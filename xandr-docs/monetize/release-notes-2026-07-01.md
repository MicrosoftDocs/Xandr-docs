---
title: Microsoft Monetize (January 7, 2026) Ad Quality - Enhanced bidder blocks (Closed Beta)
description: Learn about the new Enhanced bidder blocks in Microsoft Monetize
ms.topic: release-notes
ms.date: 01/07/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Ad Quality: Enhanced bidder blocks (Closed Beta)

**Release date:** January 7, 2026  
**Product:** Microsoft Monetize – Ad Quality: Enhanced bidder blocks 

## Overview
We’ve introduced enhancements to Ad Quality controls for Bidder Blocks, now available in Closed Beta. These updates improve visibility, hierarchy, and control when managing trust settings across bidders, members, and buyer seats.

## What’s new

### Unified hierarchy and improved visibility ###

- The Ad Quality UI now presents a clear hierarchy: Bidder → Member → Seat, making it easier to understand how trust settings are applied.
- You can set trust levels at the bidder level, with the ability to override settings at the member or seat level for more granular control.
- Across network and publisher rules, the system continues to apply the **most restrictive (conservative)** setting when conflicting rules exist.

### Support for buyer seat IDs

- The UI now indicates whether a bidder has **fully transitioned**, **partially transitioned**, or **not transitioned** to buyer seat IDs.
- This visibility helps you apply blocks at the correct level—bidder, member, or seat—for more precise enforcement.

### Best practices

- For global enforcement, apply blocks at the bidder level.
- For targeted control, use **member-level** or **seat-level** overrides as needed.
- Review your existing settings to ensure blocks are applied at the appropriate level.
- Use the **Seller Bid Error Report** to validate that blocks are enforced as expected.

### Important considerations

- If you previously configured bidder overrides during the Closed Beta, those settings were applied only to the bidder’s **default member**.
- If a bidder has **non-default members**, you must reapply the bidder trust level at the bidder level to ensure the setting applies to all members under that bidder.
