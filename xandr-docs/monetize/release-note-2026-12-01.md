---
title: Microsoft Monetize (January 12, 2026) Seller Monitoring Workflow (SMW) UI Modernization (Fluent UI)
description: Learn about the new Enhanced Seller Monitoring Workflow (SMW) UI
ms.topic: release-notes
ms.date: 01/12/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Seller Monitoring Workflow (SMW) UI Modernization (Fluent UI)

**Release date:** January 12, 2026  
**Product:** Microsoft Monetize
<br>**Area**: Seller Monitoring Workflow (SMW)
<br>**Status**: Phased rollout

## Overview
Microsoft Monetize is modernizing the Seller Monitoring Workflow (SMW) by migrating the user interface from anxreact to Fluent UI. This update improves accessibility, aligns Monetize with Microsoft-wide UI standards, and lays the foundation for future enhancements.

The rollout is being delivered in phases, starting with the Advertisers experience. This update:

- Ensures compliance with Microsoft accessibility standards (WCAG)
- Consolidates Monetize on a single, supported UI framework
- Reduces technical debt from legacy components
- Enables faster, more consistent UI improvements going forward

## What’s new

### Advertisers (Phase 1)

- Updated Advertisers UI built on Fluent UI
- Improved accessibility, including:
    - Enhanced keyboard navigation
    - Improved screen reader support
- Modernized table layout with clearer hierarchy and spacing
- Consistent interaction patterns aligned with other Microsoft applications

### Availability

**Alpha**: January 7, 2026 (subset of Ad Server clients)

**General Availability (GA)**: January 12, 2026

## What’s coming next

- **Insertion Orders**: Fluent UI update planned shortly after Advertisers GA
- **Line Items**: Final phase of the SMW migration, following a similar rollout model

Each phase will progress from alpha to GA to ensure stability and usability.

## What remains unchanged

- Core SMW functionality and workflows
- Advertiser, Insertion Order, and Line Item management behavior
- Data integrity, permissions, and reporting logic
- Users can continue managing their inventory and delivery without workflow disruption.

## Known limitations

At initial GA, the following limitations may apply:

- **Quick filters**: Some quick filtering capabilities may be temporarily unavailable. Inclusion is targeted for the release where possible.
- **Saved views**: Saved views are not available at GA and are planned as a fast-follow update.

These limitations **do not** block primary SMW workflows.

## Related topics
- [Working with advertisers](working-with-advertisers.md)
- [View advertiser details](view-advertiser-details.md)
