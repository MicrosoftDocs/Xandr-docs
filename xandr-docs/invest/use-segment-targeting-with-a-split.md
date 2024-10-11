---
title: Microsoft Invest - Use Segment Targeting with a Split
description: In this page, learn the criterias on the basis of which you can target splits, and the steps to do so. 
ms.date: 10/28/2023
---

# Microsoft Invest - Use segment targeting with a split

You can target splits based on segment presence/absence, age, or value.

> [!NOTE]
> A segment value of zero (0) is supported.

1. In the **Splits** table, select the pencil icon in the **Segment** column for the corresponding split.

    If you don't see the **Segment** column in **Splits** table, select the **Segments** checkbox from the **Audience** section within the **Select Targeting** menu.

   The **Edit Split** pane opens with the **Targeting** tab selected by default.

1. In the **Segments** section, select **and** or leave **or** selected.
1. Enter the segment ID in the search field, or select a segment from the menu that appears.
1. Select **include** :::image type="content" source="media/splits-include.png" alt-text="Screenshot of Include indicator."::: or **exclude** :::image type="content" source="media/splits-exclude.png" alt-text="Screenshot of Exclude indicator.":::.

1. Select outside the search field to exit the segment grouping.
1. Select the pencil icon to edit the segment's presence/absence, age, or value.
1. Select **Add Another Group** to add another segment grouping.
1. To change the relationship between segment groups, select outside the group and select **and** or **or**.

   > [!NOTE]
   > If splits belong to a retargeting line item, at least one retargeting segment (a segment not in the Data Marketplace) must be targeted at the line item level as well as the split level.
