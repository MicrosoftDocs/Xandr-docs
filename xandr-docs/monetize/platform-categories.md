---
title: Microsoft Monetize Platform Categories
description: Use this page to review available categories and their identifiers without calling the Category Service API.
ms.date: 9/4/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: v-garittar
ROBOTS: NOINDEX, NOFOLLOW
---

# Microsoft Monetize Platform Categories

The **Platform Category** page in Microsoft Monetize provides a read-only view of platform-defined categories used to classify brands and creatives. Use this page to review available categories and their identifiers without calling the Category Service API.

Platform categories are part of the platform taxonomy. Microsoft manages these categories centrally, so you can't create, edit, or delete them in Microsoft Monetize.

## View platform categories

1. Sign in to Microsoft Monetize.
2. In the upper-right corner, point to your user information.
3. Select **Platform Category**.

The page displays the platform categories available to your account.

## Category information

The category list includes the following columns:

| Column | Description |
|---|---|
| **Name** | The platform-defined category name. |
| **ID** | The unique identifier for the category. |

The values are system-defined and come from the Category Service.

## How platform categories are used

Microsoft Monetize uses platform categories to classify creatives and brands. This classification supports audit and enforcement workflows, including:

- Policy enforcement for sensitive categories.
- Creative serving eligibility.
- Allowlist and blocklist logic.
- Ad profile enforcement.
- Targeting and ad quality filtering.

Platform categories aren't associated with specific inventory objects.

## Category Service fields

The [Category Service](../digital-platform-api/category-service.md) provides read-only access to platform categories and their metadata. Category records can include the following fields:

| Field | Description |
|---|---|
| `id` | The unique category identifier. |
| `name` | The category name. |
| `is_sensitive` | Indicates whether the category is sensitive. |
| `requires_allowlist` | Indicates whether the category requires allowlisting. |
| `requires_allowlist_on_managed` | Indicates whether the category requires allowlisting on managed inventory. |
| `requires_allowlist_on_external` | Indicates whether the category requires allowlisting on external inventory. |
| `is_brand_eligible` | Indicates whether the category is eligible for brand classification. |
| `last_modified` | The date and time when the category was last modified. |

## Category taxonomy mapping

Microsoft Monetize maps its internal categories to IAB Content Taxonomy version 1. For the supported mappings, see [IAB Content Taxonomy Support](../bidders/iab-content-taxonomy-support.md).
