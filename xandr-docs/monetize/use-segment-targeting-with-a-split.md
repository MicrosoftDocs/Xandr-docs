---
title: Microsoft Monetize - Use Segment Targeting with a Split
description: This page is a step-by-step guide to target splits based on segment presence/absence, age, or value.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Use Segment Targeting with a Split

You can target splits based on segment presence/absence, age, or value.

> [!NOTE]
> A segment value of zero (0) is supported.

1. In the **Splits** table, click the pencil icon in the **Segment** column for the corresponding split.

    If you don't see the **Segment** column in **Splits** table, select the **Segments** checkbox from the **Audience** section within the **Select Targeting** menu.

    The **Edit Split** pane opens with the **Targeting** tab selected by default.
1. In the **Segments** section, select **and** or leave **or** selected.
1. Enter the segment ID in the search field, or select a segment from the menu that appears.
1. Select **include**:::image type="content" source="media/splits-include.png" alt-text="Screenshot of splits include."::: or **exclude**
   :::image type="content" source="media/splits-exclude.png" alt-text="Screenshot of splits exclude.":::.
1. Click outside the search field to exit the segment grouping.
1. Click the pencil icon to edit the segment's presence/absence, age, or value.
1. Click **Add Another Group** to add another segment grouping.
1. To change the relationship between segment groups, click outside the group and select **and** or **or**.

    > [!NOTE]
    > If splits belong to a retargeting line item, at least one retargeting segment (a segment not in the Data Marketplace) must be targeted at the line item level as well as the split level.