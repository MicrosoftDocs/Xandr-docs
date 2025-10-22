---
title: Dealing with Campaign Under-Delivery
description: The article discusses diagnosing and fixing under-delivery issues in different scenarios, exploring root causes and noting how political obstacles complicate solutions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Deal with campaign under-delivery

Diagnosing and solving under-delivery concerns can be a complex task. This is because there are often a number of possible root causes and barriers that make it difficult to make decisions strictly based on revenue.Unlike ad server reports, Yield Analytics can provide a tremendous amount of transparency into all the competing campaigns. Depending on the business concerns a publisher must satisfy in order to make a decision, it can sometimes be a lengthy path to gather all the necessary intel.

**High level path**:

1. Diagnose the problem by using Order Line Visibility. This to look at competing order lines, and the projected delivery trends for the order line.

1. Use Product Visibility to look at capacity trends. Understand if there is an organic or technical issue in play.

1. Pull reporting by order line. Specify the priority to a product with Analyzer, to understand the impact of priority changes.

**Detailed path**:

1. To understand why a campaign is under-­delivering, we have to understand if the problem is on the supply side (has there been a sudden drop in capacity?), demand side (has there been a sudden increase in demand?), or both.

1. Since there are a few causes to the problem, there are a few ways to start to diagnose it. If we assume the problem is on the demand side, the recommended starting point is by looking up the order line in question. We do this by going to the Orders tab, and searching for the Order Line ID.

1. Select on the desired order line, and use the performance details screen to understand when the delivery issue surfaced, and if it is expected to get better or worse.

1. If it is determined the problem will persist through the life of the order line, then look at the competing order lines in the bottom section, and which order lines are competing most. Yield Analytics will complete a number of useful metrics.
   - To show how many impressions any one order line is demanding from the same product
   - What percentage of the competition it represents.
   - If that order line is on schedule or not.
   - By looking at the start/end dates of the highest competing order lines, you can identify if a large order line in competition with the focus order line matches - when the focus order line delivery started to fall below quota. If there are order lines that have a high degree of competition and are delivering to their quota at the same rate as the focus product, the product itself is likely oversold.

1. Even though it may have been identified why something is under-­delivering, if it is suspected the product itself is oversold, select on the **Trafficked As** product in the Order Line details. (You could have also started from here to diagnose the problem).

1. Look at the Allocated Inventory section on the Product Visibility screen to identify how the product capacity and demand is trending in aggregate. You can see:
   - If capacity has recently fallen. This could represent organic traffic trends, or in extreme cases a technical problem. (Tags being removed from the page or otherwise corrupted by a publisher’s technical teams). If it has fallen, by how much and when?
   - What percentage of the product is contained to that inventory? (It must deliver to that inventory pool).
   - What percentage is indirectly reliant on the inventory?

1. Regardless of supply or demand, it should now be identified as to why the order line is under-delivering. There is more competition for the inventory (and we should know exactly what that competition is), and/or, there is less traffic to fulfill the demand (and we should know when the shift in traffic occurred and have an inclination if it was organic or not).

1. The root cause of the problem determines what action should be taken.
   - If the traffic has evaporated, the solution could be to promote that area of the site with paid traffic or editorial attention.
   - If the demand has increased, it can be determined if you want to increase the priority of the order line or not based on the specific campaigns that are competing, and if it is paying more or less than that competition.
   - Strategic factors may plan in as well: Is a struggling order line to a high revenue client even if they aren't a high yield client?  The answer may be that we would rather under-deliver the focus order line than its competition, depending on the circumstance.

1. An alternative solution would be to stagger the priority of the competing order lines, based on their end-date. This is so that you prioritize full delivery on campaigns ending soonest.  In this case, we could pull a report from Analyzer.

1. The report we pull should have:
   - Order line as it’s primary dimension.
   - Consumed impressions as it’s primary metric
   - include priority and consumption date as an additional dimension.
   - In addition: Other helpful elements such as order, order ID, advertiser, salesperson, etc.
   - You also want to filter this report to the trafficked - as product our order line is running against.

1. If you pull this report and then pivot it with priority as a row label, consumption date as a column label, with consumed impressions as the values - you can see the demand against our product by priority. Also, how much inventory is available in each tier. This gives a sense of how much inventory can be taken (and from which order lines) with a priority increase. For example: There are **3.1MM** impressions available to a particular product on a specific day, and **1**.5MM are running to order lines booked at priority 15 or higher. That means if you move the problem order line (which needs **150K imps**) from priority 16 to priority 14, we can guarantee full delivery - potentially at the expense of the order lines at priority **15** and up. If most of those are indirectly consuming the inventory, the net impact of the change cannot be realized of the without running a scenario. A smart contact at the publisher that has a feel for the inventory will likely know if the net impact is positive or negative. This is by knowing what the indirect targets are, and if those targets tend to be sold out or not. (Example: If most of the indirect demand is ROS, and ROS is never more than **50%** sold, those order lines will be fine).

1. As a publisher, you have to determine if this makes sense or not. Extracting this data from **YX** gives you full transparency into what will happen.
