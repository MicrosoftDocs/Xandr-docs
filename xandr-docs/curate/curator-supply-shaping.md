---
title: Microsoft Curate - Curator Supply Shaping
description: Learn about Supply Shaping to target inventory and audiences with splits, set custom margins, floors, and allocations for better results.
ms.date: 11/14/2023
---

# Microsoft Curate - Curator supply shaping

## Overview

Supply Shaping enables advertisers to customize the behavior of curated deals in auctions. Supply Shaping allows advertisers to optimize curated deals by customizing margins, floor prices, and spend allocations for specific inventory and audience segments.

> [!NOTE]
> To use Supply Shaping, contact your Microsoft Advertising account representative.

When you create a curated deal, you configure the inventory and the audiences you want to target. When the Microsoft Advertising platform receives an ad call, the platform add's it to the auction and sent to the buyer so they can bid on it.

By default, curated deals respond uniformly to every ad call. If the targeting criteria for a curated deal are met, the platform includes it in the auction. If you have configured a floor or margin on your curated deal, these same settings are used in the auction.

There are scenarios where you might want your curated deal to behave differently for certain ad calls. For example:

- Certain tranches of inventory or certain audience segments may be driving better performance for your buyer’s campaign. If you take a margin, you may want to reduce it on these tranches or segments to drive more delivery.  
- Alternatively, to further drive delivery on inventory and audiences performing well for your buyer, you might wish to send them different bidding guidance by using a higher floor price.  
- Certain publishers might be sending a larger volume of ad calls than others, meaning they have a larger representation within the curated deal’s delivery. For certain publishers, even if they meet the curated deal’s targeting criteria, you might want to curate only a portion of their auctions to ensure a more even representation across publishers.

**Supply Shaping** is designed to address these scenarios. It allows you to create splits that target inventory and audiences in a granular way and define custom margins, floors, and spend allocations for each split.

To get started, see the [Introduction to Splits](intro-to-splits.md) page.

## Related topics

- [Curated Deal Floors](curated-deal-floors.md)
- [Curator Margins](curator-margins.md)
- [Introduction to Splits](intro-to-splits.md)
- [Create Splits](create-splits.md)
- [Monitor Splits](monitor-splits.md)
- [Split Report Details](report-on-splits.md)
