---
title: Microsoft Monetize - Set Spend Allocation and Capping on a Split
description: Explore daily budget, cap settings, and manage conflicts in spending allocation versus line item delivery goals.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set spend allocation and capping on a split

Spend allocation is the percentage of the line item daily budget assigned to a split, and capping determines how a split handles conflicts between the spend allocation and line item delivery goals.

1. From the **Split Details** view, select **Use Spend Allocation** to set spend allocation for your splits.
1. Enter a percentage for each split in the **Spend Allocation** column.

   Spend allocation can be between 1% and 99%. The sum of all spend allocations is 100%, which includes the line item default. The **Line Item Default** row at the bottom of the **Split Details** view grid shows you the percentage of the line item that has not been allocated to a split. It acts as a catch-all for impressions that pass ALI targeting but doesn't meet any split targeting requirements.

1. Set capping settings on the **Setup** tab in the **Edit Split** pane:

    - **Uncapped**: Uncapped splits prioritize delivery over spend allocation. When uncapped splits are underdelivering, they are permitted to exceed the spend allocation goal to reach the line item delivery goal. That is, if the line item cannot reach the delivery goal, Microsoft Advertising will ignore spend allocation goals and maximize spend on every split until the line item reaches the delivery goal. If the line item delivery goal is being met, then spend allocation goals will be met. If a spend allocation goal isn't met, this implies that the particular split does not have enough inventory to reach its spend allocation goals. By default, splits are uncapped.
    - **Capped**: Capped splits prioritize spend allocation over delivery. Even when line items are underdelivering, capped splits are not permitted to exceed the spend allocation goal to help the line item reach its delivery goal. This will prevent overspend on a split, but may cause the line item to underdeliver.

   > [!NOTE]
   > If you use the **Inherit weights from splits** creative rotation strategy, the spend allocation will determine how the creatives are weighted. For more information, see [Creative Rotation (ALI)](creative-rotation-ali.md).
