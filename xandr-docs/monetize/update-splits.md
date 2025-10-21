---
title: Microsoft Monetize - Update Splits
description: This page provides an overview to update splits. Learn to edit, activate/deactivate, delete and remove all splits in this page.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Update splits

## Edit a split

Navigate to the Line item screen, select the **Programmable Splits** section. For more information on Line item, see [Working with Line Items](working-with-line-items.md). Expand the **Programmable Splits** section. Select a split from the Splits table or click on the pencil icon next to the split name.

## Duplicate a split

1. Select the split(s) you'd like to duplicate and click **Actions** \> **Duplicate Selected**.
1. By default, the new splits have the same names as the original splits but with "COPY" as a prefix. If necessary, update the names for the new splits.

Once you duplicate a split, you will need to manually readjust allocations and priorities.

## Activate/Deactivate a split

Select the split(s) you'd like to activate or deactivate and click **Actions** \> **Activate Selected** or **Actions** \> **Deactivate Selected**.

When you activate a split:

- It will automatically receive the lowest priority, which you can adjust at will.
- It is allocated 0% of the line item budget. You will need to adjust allocations manually.

When you deactivate a split:

- Priorities will readjust automatically.
- The split allocation is reassigned to the line item remainder.

For more information, see [Create an Augmented Line Item](create-an-augmented-line-item-ali.md).

## Delete a split

Select the split(s) you'd like to activate or deactivate and click **Actions** \> **Delete Selected**.

> [!NOTE]
> You cannot recreate a deleted split. Deleted splits will still appear in reporting.

## Remove all splits

Select the split(s) you'd like to activate or deactivate and click **Actions** \> **Remove All Splits**.

> [!NOTE]
> You cannot recreate a deleted split. Deleted splits will still appear in reporting.

## Related topics

- [Configure a Programmable Split](configure-a-programmable-split.md)
- [Understanding Splits](understanding-splits.md)
- [Import or Export Split CSVs](import-or-export-split-csvs.md)
- [Explore Splits](explore-splits.md)