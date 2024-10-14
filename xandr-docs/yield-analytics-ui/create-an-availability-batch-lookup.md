---
title: Create an Availability Batch Lookup
description: The article describes how you can run multiple availability lookups as part of a single Availability report, by creating a batch lookup.
ms.date : 10/28/2023
ms.custom : yield-analytics-ui
---

# Create an availability batch lookup

You can run multiple availability lookups as part of a single availability report, by creating a batch lookup.

1. Set up a new lookup for availability based on a combination of targeting attributes or open an existing saved lookup. Then select **Add to Batch**. The **Availability Report** panel displays the available inventory based on your lookup criteria, excluding CPM, impressions, and capacity.
1. Modify the lookup criteria to set up a different set of targeting, and select **Add to Batch**. The **Availability Report** panel is updated with the available inventory based on your original lookup criteria and the new lookup criteria.
1. Repeat step 2 as needed. Then select **Run Batch**.
1. On the confirmation dialog that appears, note the batch lookup name, and then select **OK**.

> [!TIP]
> The lookup query that you set up on this screen will be broken out into multiple result rows that will appear in the Availability Report panel at the bottom of the screen once you select **Add to Batch**. The maximum number of rows is capped at 10,000 by default. That figure represents a reasonable limit, which is configurable at your request. Please contact your Client Services Manager if you feel that a higher ceiling is necessary.

## Related topics

- [Check Availability for a Combination of Targeting Attributes](check-availability-for-a-combination-of-targeting-attributes.md)
- [View Availability Batch Lookups](view-availability-batch-lookups.md)
- [Anatomy of the Availability Lookup Page](anatomy-of-the-availability-lookup-page.md)
