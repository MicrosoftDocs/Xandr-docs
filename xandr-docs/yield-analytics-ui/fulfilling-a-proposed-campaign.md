---
title: Fulfilling a Proposed Campaign
description: In this article, learn the process of fulfilling a proposed campaign request in Yield Analytics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Fulfill a proposed campaign

Fulfilling a campaign is a core, and (usually) straightforward request in Yield Analytics. Determining what else can be offered when products are oversold is more complex. Yield Analytics can quantify overlaps and incremental inventory, but it usually takes a 'human touch' to find the right suggestion.

**High Level Path**:

1. Use reporting or check availability to understand available impression. This depends on the level of customization in the targeting.
1. Reporting may be more helpful if you want to see the various options based on priority and pipeline scenarios. Use Excel pivot tables to show the breakout of priority and status.
1. Use Analyze Overlaps to find more inventory in Sibling and Parent products, if requested products are oversold.

**Detailed Path**:

1. There are two ways to access availability data in Yield Analytics. The best path depends on if the proposed products are rate card or custom products. The same data for either scenario is available through the API, and through Yield Analytics’ various OMS plugin.
1. If the proposed products are rate card products (meaning they are predefined in Yield Analytics and have history), then it’s often easiest to pull a report from Analyzer. You would set:
   - Product as your primary dimension.
   - Available impressions as your primary metric.
   - Filter to inventory class of Guaranteed.
   - The time frame you need.
   - Select all the products desired in a product filter. Using product groups or product type can be a helpful shortcut.
1. Run the report.
1. If the proposed products are custom products (meaning they are custom permutations of target attributes that have not been predefined), then Availability lookup is the only way to query.
1. Go to the **Availability** tab \> **Check Availability**. Search for the necessary base product. You can then add additional custom attributes on, or simply build the product from scratch. For example, if you wanted to create a custom product of ROS – Wichita DMA, you can simply search for the ROS product that is already created (and has the requisite attribute expression). Then tack on the DMA value, rather than having to know the entire Boolean string of logic. You would set your dates, and select **Check Availability** (or add to batch for especially lengthy requests).
1. If there is not enough available inventory for your campaign, you could always choose to look at availability at an increased priority. This filter can be added in Analyzer and in Check Availability, to force YX to query avails at a specific priority, or you can look for similar products.
1. To find similar products, you can search for the product under “**products** \> **analyze overlaps**”. This is if you have the product already defined (a rate card or reporting product). Select your oversold product in question as the focus product, and YX will show you all the other products that overlap with that product, and to what extent.
1. A good way to find relevant product substitutions is to look for sibling or parent products under overlap type. Look for products that also have a sizeable amount of comparison non-overlapping impressions, which would be the incremental gain of targeting that product as well. You will probably already know what the parent products are. The sibling products can be more useful, as they will likely appear about as targeted as the focus product, but provide more inventory.
1. Alternatively, you can edit your inventory lookup in the Availability section. You could add more DMAs, or site sections and see how much more inventory you’d achieve based on those queries. For geo it’s often helpful to expand from DMA to state. For content, you can expand from a single site section to a parent section or multiple site sections.

## Related topic

[Common Journey Maps](common-journey-maps.md)
