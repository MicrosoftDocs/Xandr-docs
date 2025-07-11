---
title: Microsoft Monetize - Set Split Priority
description: Explore prioritizing programmable splits with unique priority numbers in Split Details grid for proper impression allocation.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set split priority

If an impression applies to multiple programmable splits, the impression is assigned to the split with the lowest priority number.

For example, if Split A (priority 1) is targeting "domain=cnn.com", Split B (priority 2) is targeting "city=Boston", and an impression is available from a user in Boston visiting cnn.com, then the impression will be assigned to Split A because it has a higher priority (lower priority number) than Split B.

1. Navigate to the Line item screen, select the **Programmable Splits** section. For more information on Line item, see [Working with Line Items](working-with-line-items.md)
1. Choose the number of splits and select **Start**
1. In the **Split Details** grid, set a priority number for each of your line item's splits.

   The same priority number can't be set for multiple splits.
