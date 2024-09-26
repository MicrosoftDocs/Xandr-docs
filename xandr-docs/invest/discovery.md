---
title: Microsoft Invest - Discovery 
description: In this article, understand what Discovery is and how it helps in optimization by prioritizing the inventory that is most likely to perform.
ms.date: 10/28/2023
---

# Microsoft Invest - Discovery

Discovery is an optimization component that helps line items meet their goals as quickly as possible by spending on inventory that performs well and quickly cutting inventory that doesn't meet the goal.

> [!TIP]
> Discovery does not apply to line items with CPA retargeting or with vCPM, CPCV, or VCR goals.

Because the pool of inventory that a line item can serve on is huge - even oceanic - even moderately targeted line items run the risk of "boiling the ocean" or trying to test everything. Boiling the ocean not only wastes money, but also time - it may take a while to accrue enough meaningful data to call something "good" or "bad." Sometimes cutting bad inventory takes so much time that traders resort to allowlists of the best domains and placements instead. This might help performance in the short term, but it also prevents the line item from discovering any new performant inventory sources in the long term.

Discovery solves this problem by breaking inventory down into different sections, ranking the sections based on historical data, and testing the sections most likely to perform well first.

As a result:

- Advertiser dollars go farther because less money is spent in testing.
- Traders spend less time making manual optimizations, resulting in more time for higher impact tasks or wider campaign management scope.
- Traders spend less time making allocation decisions about inventory that is working well.
- Line items achieve their goals faster with less human effort.

## Discovery workflow

This is how Discovery works:

1. When we see that an impression is eligible for a line item's targeting, we sort it into a ranked testing list - kind of like an allowlist, but dynamically generated and custom to each line item. Inventory that's most likely to achieve the line item's goal rises to the top of the list, while inventory that's least likely to achieve the goal falls to the bottom, or isn't added at all.
1. Discovery starts testing at the top of the list, passing and failing inventory as the line item spends money, a process we call "axing".
1. When inventory is failed for not meeting the goal, Discovery dynamically adds what's next up on the list.

> [!NOTE]
> If you change your line item goals, Discovery uses the line item's existing data to re-evaluate inventory against the new goal.

## Process of ranking

The sections of inventory that Discovery tests are called "Discovery nodes". A node is defined by a combination of tag + inventory URL, except for CPA prospecting, where a node is defined by inventory URL only. As soon as we see that a single impression has been served against a Discovery node, we look up that Discovery node in our ranking system so we can determine whether the line item should keep testing it.

Because performance depends on the line item setup, Discovery also filters historical data by the line item's ad type (banner, native, or video) and the line item's targeted country.

From there we rank RTB inventory into five buckets: super good, good, less good, bad, and unknown. (Managed inventory is never ranked.) The ranking is based on CPC for line items with CPC and post-click CPA goals and on CTR for line items with CTR goals. For CPA  prospecting, nodes are ranked based on "user overlap", or how similar their user traffic is to the traffic for nodes that have historically produced a high volume of converting users. If both nodes have similar user traffic overall, we assume they will have similar conversion rates.

- **Super good** - Everything in this bucket gets added to the pool of inventory to test as soon as the line item starts.
- **Good** - When we need to add more nodes to the test pool, we take eligible nodes from this bucket first.
- **Less good** - If we still need to add more nodes to test and the first two buckets have been exhausted, we add from this bucket next.
- **Bad** - These will never be allowed to test.
- **Unknown** - Long tail nodes. We only add nodes to test from this bucket if the line item has exhausted all of the inventory from the good or less good buckets.

If the current line item hasn't purchased any impressions in a node, the node is considered "explore inventory". A line item will always serve on a minimum of 1% explore inventory in order to discover new, potentially performant inventory sources and to feed our eligibility list. We will increase that percentage if the line item is not meeting its delivery goal.

## Process of axing

"Axing" is the term we use to describe the process of eliminating Discovery nodes as nonperformant. Axing decisions are based on a combination of:

- Fail criterion
- Pass criterion
- Interaction with goal priorities
- A false positives check

## Fail criterion

In order to cut inventory that's not working, we first need to determine the line item's fail criterion, or the threshold at which we consider the inventory to be bad. We use a very straightforward benchmark: the line item's CPC goal for click-based goals or its CPA goal for CPA prospecting. In other words, if the line item has a goal of $1.00, it should be getting one click per every dollar spent on a slice of inventory in order to achieve the goal. If we see that a Discovery node has not achieved any clicks, but the line item has reached its fail criterion ($1.00), the node will be immediately failed. For managed nodes, the fail criterion is higher because the inventory is known and therefore presents less risk.

|Type of Nodes | Click-based Goals (CPC, CTR, Post-Click CPA) | CPA Prospecting |
|---|---|---|
| RTB Nodes | 1x line item's CPC goal | 1x line item's CPA goal |
| Managed Nodes | 1.8x line item's CPC goal | 1x line item's CPA goal |

For CPM, Cost Plus, dynamic CPM, and viewable CPM booked revenue types, we axe based on booked revenue dollars. For the CPC revenue type because booked revenue is less predictable, we axe based on media cost dollars.

## Pass criterion

As mentioned above, if a line item has a $1.00 CPC goal, spends $1.00 on a slice of inventory, and achieves 0 clicks, then failing the inventory is straightforward. For CPA prospecting, passing the inventory is just as straightforward: if a conversion occurs after that $1 of spend, the node passes; if no conversion occurs, the node fails.

For click-based goals, passing the inventory is a little more complicated. For example, if the inventory has spent $1.00 and achieved 1 click, we can tell that the inventory is achieving the goal right now — but we don't know if the inventory will achieve the goal consistently in the future.

In order to account for this risk, a Discovery node's pass criterion changes depending on the number of clicks it has.

If a node has one click at or below $1 of spend, the pass criterion increases to $2. If a node has two clicks at or below $2 of spend, the pass criterion increases to $3. If the node has 3 clicks at or below $3 spend, the node passes, unless the line item's CPC goal change.(In that case, as with any changes to the goal, Discovery will automatically reevaluate nodes against the new criteria.)

## Interaction between axing and goal priorities

On the line item, you choose a goal priority: delivery, performance, or margin. When you choose **Performance** (the default), axing uses the default pass and fail criteria described above. When you choose **Delivery**, we implement a dynamic fail criterion calculation and also modify the criterion with an [Adaptive Pacing](adaptive-pacing.md) modifier, which can go up to 2.0. In other words, if a line item is not meeting its delivery goal, then Discovery will keep incrementally increasing the fail criterion threshold until it does.

| Goal Priority | Fail Criterion |
|---|---|
| Performance (the default) | 1x the line item's goal |
| Delivery | Up to 10x the line item's goal (x Adaptive Pacing modifier) |
| Margin | 1x the line item's goal |

## False positives check

False positives are Discovery nodes that have passed (achieved three or more clicks at or below the line item's CPC goal), but now have a cumulative CPC far above the goal. In other words, these are nodes that once performed well but do not perform well anymore. Our valuation algorithm may eliminate some of these nodes by devaluing them, but that tends to take a while, which can hurt the line item's overall performance.

To help line items with click-based goals weed out poor performing inventory and achieve their goals faster, Discovery axes inventory with CPCs two or more times greater than the goal. For CPA prospecting, it's a little more complicated: Discovery axes inventory based on the following formula:

Booked revenue on the node > 2 (fail criterion) * (conversions + 1)

## Optimization override service

Clients with sophisticated optimization needs can disable discovery or adjust the Discovery fail criterion on line items with CPC or post-click CPA goals by using the [Optimization Override Service](../digital-platform-api/optimization-override-service.md).
