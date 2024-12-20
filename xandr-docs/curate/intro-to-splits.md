---
title: Microsoft Curate - Introduction to Splits
description: Learn how Supply Shaping refines targeting for curated deals using prioritized splits processed during ad calls.
ms.date: 11/14/2023
---

# Microsoft Curate - Introduction to splits

When using Supply Shaping you can define a series of splits for your curated deal. These splits will refine the targeting and behaviour of the deal line item they’re associated with.

Each split has a priority, its own targeting criteria and optional settings. The following steps describe how a deal line item and its splits are processed when the Microsoft Advertising platform receives an ad call:

1. The platform checks if the deal line item’s targeting criteria are met. If so, the platform starts checking the deal line item’s splits in ascending order of priority.

1. If a split’s targeting criteria are met, it is selected, and its settings are used to add the curated deal to the auction. If the split is configured with a custom margin, it will be used instead of the deal line item’s margin setting. Similarly, if the split has a custom floor it will be used instead of the deal line item’s floor.

1. The selected split’s its settings are used to add the curated deal to the auction. If the split is configured with a custom margin it will be used instead of the deal line item’s margin setting. Similarly if the split has a custom floor it will be used instead of the deal line item’s floor.

1. If a split’s targeting criteria are not met, the platform moves on to the next split.

1. If the platform has checked all splits but none of them have been selected:

    1. If the catch-all split is enabled, it will be selected. Like in **step 2**, its margin and floor settings will be used to add the curated deal to the auction. If the catch-all split disabled the curated deal will not be added to the auction.
    1. If the catch-all split disabled the curated deal will not be added to the auction.
    1. The platform prepares a bid request for the auction and sends it to buyers.

Some important things to remember:

- A split’s targeting can only be more restrictive than its deal line item’s targeting. For example, if the deal line item targets the United States and the split targets Canada, the split’s targeting criteria will never be met.
- If two splits have overlapping targeting, the split with the higher priority will always serve on the overlapping inventory. It’s best to create splits with non-overlapping targeting to make the deal line item easier to manage.

## Related topics

- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Curator Supply Shaping](curator-supply-shaping.md)
- [Create Splits](create-splits.md)
- [Monitor Splits](monitor-splits.md)
- [Report On Splits](report-on-splits.md)
