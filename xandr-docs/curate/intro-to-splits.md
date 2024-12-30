---
title: Microsoft Curate - Introduction to Splits
description: Learn how Supply Shaping refines targeting for curated deals using prioritized splits processed during ad calls.
ms.date: 11/14/2023
---

# Microsoft Curate - Introduction to splits

When using Supply Shaping, you can define a series of splits for your curated deal. These splits refine the targeting and behaviour of the deal line item they’re associated with.

Each split has a priority, its own targeting criteria, and optional settings. The following steps describe how a deal line item and its splits are processed when the Microsoft Advertising platform receives an ad call:

1. The platform checks if the deal line item’s targeting criteria are met. If they are, the platform starts checking the deal line item’s splits in ascending order of priority.

1. If a split’s targeting criteria are met, the platform selects it, and its settings are used to add the curated deal to the auction.
    - If the split is configured with a custom margin, it will be used instead of the deal line item’s margin setting.
    - Similarly, if the split has a custom floor, it will be used instead of the deal line item’s floor.
    - The selected split’s settings are used to add the curated deal to the auction. If the split is configured with a custom margin it will be used instead of the deal line item’s margin setting. Similarly if the split has a custom floor it will be used instead of the deal line item’s floor.

1. If a split’s targeting criteria are not met, the platform moves on to the next split.

1. If the platform has checked all splits but none of them have been selected:

    - If the catch-all split is enabled, it will be selected. As in **step 2**, its margin and floor settings are used to add the curated deal to the auction. If the catch-all split disabled the curated deal will not be added to the auction.
    - If the catch-all split is disabled, the curated deal will not be added to the auction.
1. The platform prepares a bid request for the auction and sends it to buyers.

Some important things to remember:

- A split’s targeting must be more restrictive than its deal line item’s targeting. For example, if the deal line item targets the United States and the split targets Canada, the split’s targeting criteria will never be met.
- If two splits have overlapping targeting, the split with the higher priority will always serve on the overlapping inventory. Create splits with non-overlapping targeting to simplify deal line item management.

## Related topics

- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Curator Supply Shaping](curator-supply-shaping.md)
- [Create Splits](create-splits.md)
- [Monitor Splits](monitor-splits.md)
- [Report On Splits](report-on-splits.md)
