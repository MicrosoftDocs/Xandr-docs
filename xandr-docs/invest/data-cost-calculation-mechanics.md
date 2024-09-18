---
title: Microsoft Invest - Data Cost Calculation Mechanics
description: In this article, find information about how buyers are billed for the segments they acquire through Data Marketplace.
ms.date: 10/28/2023
---

# Microsoft Invest - Data cost calculation mechanics

The Data Cost Calculations Mechanics outlines how buyers are billed for the segments they acquire through the data marketplace.

The costs of these segments are displayed during the following scenarios:

- With a CPM price point.
- When the segment is chosen during targeting in line items.
- Aggregated on the relevant items, also appearing in the corresponding reports.
- Consolidated into your invoice totals and presented as an aggregated data cost.

> [!NOTE]
> The expenses for segments for which the prices were not provided by the data provider, are presently not included in the overall cleared totals. For usage reports and the associated costs of such segments, you must coordinate with the data providers as billing for these segments will be handled separately by the Data Provider.

A buyer will only be charged for a segment from the data marketplace if that segment is used in a winning bid for an impression. Whether the buyer is charged for the segment is further determined by the AND/OR boolean logic that the buyer has selected.

The diagram below illustrates this process. In this process, a relevant segment is a segment that has a match with one or more parameters within an ad request. If a line item is targeting 3rd party segments and there are no relevant segments then no bid is made. A used segment is a segment that is used to bid in the auction. The difference between a relevant segment and a used segment is that not all relevant segments are required to be used for a line item to bid in the auction. Note that many other factors besides segment targeting influence the decision on whether a bid is made on an impression in the auction such as inventory or geo targeting.

Key steps in assessing data cost:

1. A list of relevant segments is provided in the bid request
1. Used segments are determined based upon the segments which caused Microsoft Invest to submit a bid. The list of relevant segments, the buyer's targeted segments and boolean AND/OR decisioning logic the buyer has selected are all determining factors.
1. The auction is run and the impression is won by the line item (see [Win the Auction](#win-the-auction)).
1. Data costs for used segments are determined based on each data provider's rate cards and pricing rules.

## Costs incurred for selected segments

The examples below illustrate in more detail how this general process works.

> [!NOTE]
> In the examples below, a green box indicates a relevant segment for a single impression, a red box indicates that it is not a relevant segment for a single impression.

### Target single segment

In the simplest scenario, the line item or campaign is targeting just a single segment. The presence of the user's unique identifier (a parameter in the auction) determines whether the demographic segment is relevant. For line item or campaign targeting one segment if a segment is relevant, then the segment will be used to bid in the auction.

:::image type="content" source="media/basic.png" alt-text="Screenshot of a single segment targeted.":::

### Target multiple segments

If multiple segments are targeted with a line item or campaign, the boolean AND/ OR logic that the buyer has selected will determine whether the ad request matches the required targeting criteria.

- If the segments are ANDed, only an ad request that is relevant to ALL segments will generate a bid.
- If the the segments are ORed, an ad request that is relevant to ANY of the targeted segments will generate a bid.

#### Target segments using the AND boolean

- If the ad request is relevant in ALL targeted segments, a bid will be made.

    :::image type="content" source="media/advanced-and-a.png" alt-text="Screenshot of a bid when the ad is relevant to all targeted segments.":::

- If the ad request is not relevant to one or many of the targeted segments, then no bid will be made.

    :::image type="content" source="media/advanced-and-b.png" alt-text="Screenshot of a bid when the ad is not relevant to one of the targeted segments.":::

    :::image type="content" source="media/advanced-and-c.png" alt-text="Screenshot of a bid when the ad is not relevant to any of the targeted segments.":::
  
  > [!NOTE]
  > Since the ad request is required to be relevant for ALL targeted segments using the AND boolean, the buyer will be charged for the use of ALL segments if the impression is won.

#### Target segments using the OR boolean

- If the ad request is relevant to ANY segment, a bid will be made using the relevant segment.

    :::image type="content" source="media/advanced-or-a.png" alt-text="Screenshot of a bid when the ad is relevant to any targeted segment.":::

    :::image type="content" source="media/advanced-or-b.png" alt-text="Screenshot of a bid when the ad is relevant to any of the targeted segments.":::

- If the ad request is relevant to more than one segment (overlaps), Microsoft Advertising will use the lowest priced segment to bid on the auction.

    :::image type="content" source="media/advanced-or-c.png" alt-text="Screenshot of a bid when the ad is relevant to more than one targeted segment.":::

- If the ad request is NOT relevant to any targeted segment, then no bid will be made.

    :::image type="content" source="media/advanced-or-d.png" alt-text="Screenshot of a bid when the ad is not relevant to any targeted segment.":::

### Target multiple groups of segments

Buyers can create multiple segments groups (using the boolean AND/OR operators described above) and those groups can apply either the AND or OR boolean operator. The same process described above is used to determine whether a bid is made. However, due to the complexity of the tiering of boolean operations (e.g., an AND within an ORed group) the calculation needs to be performed multiple times to determine whether the line item or campaign bids in the auction or not.

#### Target segment groups using AND logic

:::image type="content" source="media/advanced-and.png" alt-text="Screenshot of a bid when the ad is relevant to all targeted segment groups.":::

When using the AND boolean against segment groups, the boolean within each group will be set to OR. OR pricing logic described in the section above will be used to determine which segments to use in each group. Then a second calculation is done to verify that at least one segment is relevant in each group. At least one segment from each group will be used to bid on the auction.

#### Target segment groups using OR logic

:::image type="content" source="media/advanced-or.png" alt-text="Screenshot of a bid when the ad is relevant to any targeted segment groups.":::

When using the OR boolean against segment groups, the boolean within each group will be set to AND. As such, each segment group will be evaluated using the AND pricing logic described in the section above to calculate the prices for each group. Then a second calculation is done to evaluate each group using the OR pricing logic described above. All segments within one segment group will be used to bid on the auction.

#### Target segments negatively (exclusion targeting)

- If a parameter in the ad request is included in the negatively targeted segment, then no bid is made.
- If a parameter in the ad request is not included in the negatively targeted segment, then a bid is made.

> [!NOTE]
>
> - Data costs are only charged on impressions that are won by the line item
> - The buyer will be charged for all inclusive targeted segments that were used to win the bid. The group of used segments will be passed through the data provider's pricing methodology as described in the provider's rate cards to determine a bundled price. Contact your Microsoft representative or data provider for segment pricing information.
> - The buyer will be charged for exclusion targeted segments when an impression is won. For further clarity, this means that the buyer will be charged when parameters for an ad request does not belong to the segment.

## Win the auction

Data costs are only charged on impressions that are won by the line item or campaign.

### Positive targeting of segments (inclusion targeting)

The buyer will be charged for all segments that were used to win the bid. The group of used segments will be passed through the data provider's pricing methodology as described in the provider's rate cards to determine a bundled price. Contact your Microsoft Advertising representative or data provider for segment pricing information.

### Negative targeting of segments (exclusion targeting)

The buyer will be charged for exclusion targeted segments when an impression is won. For further clarity, this means that the buyer will be charged when parameters for an ad request does not belong to the segment.

## Related topic

[Data Marketplace Overview](data-marketplace-overview.md)
