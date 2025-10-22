---
title: Data Cost Calculation
description: Learn about key steps in assessing data cost. This page illustrates segment targeting using *AND* and *OR* boolean along with examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Data cost calculation

A buyer is only charged for a segment if that segment is used in a winning bid for an impression. Whether the buyer is charged for the segment is further determined by the *AND/OR* boolean logic that the buyer has selected.

The diagram below illustrates this process. In this process, a relevant segment is a segment that has a match with one or more parameters within an ad request. If a campaign is targeting 3rd party segments and there are no relevant segments then no bid is made. A used segment is a segment that is used to bid in the auction. The difference between a relevant segment and a used segment is that not all relevant segments are required to be used for a campaign to bid in the auction. Note that many other factors besides segment targeting influence the decision on whether a bid is made on an impression in the auction such as inventory or geo targeting.

:::image type="content" source="media/data-cost-calculation.png" alt-text="Screenshot of Data Cost Calculation.":::

Key steps in assessing data cost:

1. A list of relevant segments is provided in the bid request
1. Used segments are determined based upon the segments which caused Xandr to submit a bid. The list of relevant segments, the buyer's targeted segments and boolean *AND/OR* decisioning logic the buyer has selected are all determining factors (see [Segments selected in the auction](#segments-selected-in-the-auction) below).
1. The auction is run and the impression is won by the campaign (see [Win the auction](#win-the-auction) below).
1. Data costs for used segments are determined based on a pricing methodologies (see [Pricing methodologies](#pricing-methodologies) below).

The examples below illustrate in more detail how this process works.

## Segments selected in the auction

> [!NOTE]
> In the examples below, a green box indicates a relevant segment for a single impression, a red box indicates that it is not a relevant segment for a single impression.

## Single segment targeted

In the simplest scenario, the campaign is targeting just a single segment. The presence of the user's unique identifier (a parameter in the auction) determines whether the demographic segment is relevant. For campaigns targeting one segment, if a segment is relevant, then the segment is used to bid in the auction.

:::image type="content" source="media/simple-segment-targeted.png" alt-text="Screenshot of Single Segment Targeted.":::

## Multiple segments targeted

If multiple segments are targeted with a campaign, the boolean *AND/OR* logic that the buyer has selected determines whether the ad request matches the required targeting criteria.

- If the segments are ANDed, only an ad request that is relevant to ALL segments generates a bid.
- If the segments are ORed, an ad request that is relevant to ANY of the targeted segments generates a bid.

### When the segments are targeted using the *AND* boolean

#### If the ad request is relevant in ALL targeted segments, a bid is made

:::image type="content" source="media/ad-request-a.png" alt-text="Screenshot of when a bid will be made.":::

#### If the ad request isn't relevant in multiple targeted segments, then no bid is made

:::image type="content" source="media/ad-request-b.png" alt-text="Screenshot of when an ad request is not relevant to one or many of the targeted segment.":::

:::image type="content" source="media/ad-request-c.png" alt-text="Screenshot of when no bid will be made.":::

> [!NOTE]
> Since the ad request is required to be relevant for ALL targeted segments using the AND boolean, the buyer is charged for the use of ALL segments if the impression is won.

### When the segments are targeted using the *OR* boolean

#### If the ad request is relevant to ANY segment, a bid is made using the relevant segment

:::image type="content" source="media/ad-request-d.png" alt-text="Screenshot of when the ad request is relevant to ANY segment, a bid will be made.":::

:::image type="content" source="media/ad-request-e.png" alt-text="Screenshot of when a bid will be made using the relevant segment.":::

#### If an ad request is relevant to multiple segments (overlaps), Xandr uses the lowest-priced segment for bidding in the auction

:::image type="content" source="media/ad-request-f.png" alt-text="Screenshot of ad request when it is relevant to more than one segment.":::

#### If the ad request is NOT relevant to any targeted segment, then no bid is made

:::image type="content" source="media/ad-request-g.png" alt-text="Screenshot of ad request when it is NOT relevant to any targeted segment.":::

## Multiple groups of segments targeted

Buyers can create multiple segments groups (using the boolean AND/OR operators described above) and those groups can apply either the AND or OR boolean operator. The same process described above is used to determine whether a bid is made. However, due to the complexity of the
tiering of boolean operations (e.g., an AND within an ORed group) the calculation needs to be performed multiple times to determine whether the campaign bids in the auction or not.

### AND targeting using segment groups

:::image type="content" source="media/multiple-groups-of-segments-targeted-a.png" alt-text="Screenshot of AND Targeting using Segment Groups.":::

When using the AND boolean against segment groups, the boolean within each group is set to OR. OR pricing logic described in the section above is used to determine which segments to use in each group. Then a second calculation is done to verify that at least one segment is relevant in each group. At least one segment from each group is used to bid on the auction.

### OR targeting using segment groups

:::image type="content" source="media/multiple-groups-of-segments-targeted-b.png" alt-text="Screenshot of When the segment groups have been ORed.":::

When using the OR boolean against segment groups, the boolean within each group is set to AND. As such, each segment group is evaluated using the AND pricing logic described in the section above to calculate the prices for each group. Then a second calculation is done to evaluate each group using the OR pricing logic described above. All segments within one segment group is used to bid on the auction.

### When the segments are negatively targeted (exclusion targeting)

- If a parameter in the ad request is included in the negatively targeted segment, then no bid is made.  
- If a parameter in the ad request is not included in the negatively targeted segment, then a bid is made.

## Win the auction

Data costs are only charged on impressions that are won by the campaign.

- **When the segments are positively targeted (inclusion targeting)** - The buyer is charged for all segments that were used to win the bid. The group of used segments is passed through the data provider's pricing methodology to determine a bundled price (see next section).

- **When the segments are negatively targeted (exclusion targeting)** - The buyer is charged for exclusion targeted segments when an impression is won. For further clarity, this means that the buyer is charged when parameters for an ad request does not belong to the segment.

## Pricing methodologies

Pricing of segments is determined by the following pricing methodologies. We offer a variety of methodologies to support a wide range of business models. The pricing methodology used for your segments is selected by you and Xandr in your Xandr Data Provider agreement and can only be changed through amending that agreement.

> [!NOTE]
> The price set for each category is mutually determined by you and Xandr by rate cards that you have submitted and that Xandr have accepted. Xandr does not set prices without your knowledge or consent.

### Pricing methodology 2

|  |  |
|--|--|
| Summary | When multiple segments are used under this pricing methodology, Xandr will charge the highest CPM segment across all publishers. |

|  |  |
|--|--|
| Diagram | :::image type="content" source="media/pricing-methodology-a.png" alt-text="Screenshot of Pricing Methodology 2."::: |

|  |  |
|--|--|
| Example | Final Price: $1.50 CPM<br>:::image type="content" source="media/pricing-methodology-b.png" alt-text="Screenshot showing the bundled price for all four segments."::: <br> - Four segments were used to win the impression and the buyer will be charged for the usage of all segments <br> - The bundled price for all four segments is $1.50 CPM (the highest CPM category) |

### Pricing methodology 3

|  |  |
|--|--|
| Summary | When multiple segments are used under this pricing methodology, Xandr will charge for all categories. |

|  |  |
|--|--|
| Diagram | :::image type="content" source="media/pricing-methodology-c.png" alt-text="Screenshot of Pricing Methodology 3."::: |

|  |  |
|--|--|
| Example | Final Price: $1.25 CPM <br>:::image type="content" source="media/pricing-methodology-d.png" alt-text="Screenshot of Pricing Methodology when the bundled price is $1.25 CPM."::: <br> - Seven segments were used to win the impression and the buyer will be charged for the usage of all segments <br> - The bundled price will be determined by adding the price of each that category is used <br> - The bundled price is $1.25 CPM = $0.10 + $0.20 + $0.25 + $0.30 + $0.40 |

### Pricing methodology 4

|  |  |
|--|--|
| Summary | When multiple segments are used under this pricing methodology, Xandr will charge for the highest CPM category. |

|  |  |
|--|--|
| Diagram | :::image type="content" source="media/pricing-methodology-e.png" alt-text="Screenshot of Pricing Methodology 4."::: |

|  |  |
|--|--|
| Example | Final Price: $0.40 CPM <br>:::image type="content" source="media/pricing-methodology-f.png" alt-text="Screenshot of Pricing Methodology when the bundled price is $0.40 CPM."::: <br> - Seven segments were used to win the impression and the buyer will be charged for the usage of all segments <br> - The bundled price will be determined by the highest CPM price of the categories used <br> - The bundled price is $0.40 CPM |

## Glossary

- Segments - Segments available through the Data Marketplace.
- Relevant Segment - A segment (targeted by the buyer) that matches against one or more parameters of the ad request. A relevant segment is eligible for being used by Xandr to bid on the campaign.
- Used Segment - A segment that is used by Xandr to bid on the auction. If the campaign wins the auction, then all used segments is charged to the buyer. The segment(s) used for each auction is determined by Xandr.
- Bundled Price - The price for a group of segments determined by the data provider via their chosen pricing methodology.
- Exclusion Targeted Segment - A segment that is negatively targeted by the buyer. The buyer is choosing not to bid on auctions where one or more parameters of the ad request fall into an exclusion targeted segment.
