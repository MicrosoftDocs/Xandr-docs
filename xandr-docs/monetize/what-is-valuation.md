---
title: What is Valuation?
description: Explore bid valuation, calculating success event bids. Advertisers gain when impressions cost less than successful actions' earnings.
ms.date: 10/28/2023
---

# What is Valuation?

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide ALI](optimization-guide-ali.md).

Valuation is the process by which our system determines a bid amount. In order to obtain one success event (i.e., a success event is an impression which leads to the user taking the action intended by the advertiser, such as a purchase), it is necessary to display a certain number of impressions to users. In order to earn a profit, the advertiser must pay less for the impressions displayed to obtain the success event than the money earned by the success event. There are several components which must be measured before the valuation formula can be applied:

- **P(success event):** This is the total number of clicks or conversions (depending on how a success event is defined) divided by the total impressions.
- **value(success):** This is the average value (as determined by the advertiser) that a single success event represents. For example, if a similar campaign run by this advertiser with similar conditions (creative size, location, site, etc.) generated 250 success events from which users made purchases totaling $1,000, the **value (success)** amount would be **$4**.
- **1000:** This is the factor used to adjust the cost to a **CPM** value.
- **Cadence:** This is a factor which increases or decreases the bid amount based on how many times and how recently the user has seen the creative.

## Valuation of a single impression

The valuation of a single impression is determined by the following formula:

**valuation = P(success event) X value(success) X 1000**

This formula shows that the valuation is the likelihood of a success event coming from a single impression (**P(success event)**) multiplied by the money earned from one success event (**value success**) multiplied by **1000** (to determine a **CPM** bid amount).

To account for the frequency (how many times a particular user has viewed a creative) and recency (how recently the user saw the creative), a **Cadence Modifier** is applied to the bid. The likelihood that a user will click on a creative changes based on the number of time they have seen it and how recently they have seen it, so this factor is applied to
the formula:

**bid = P(success event) X value(success) X 1000 X cadence**

For more detailed information, see [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md).

## Valuation in the Learn phase

In this phase, we have not yet seen enough clicks/conversions to accurately define how often they will occur on a specific node. Therefore, we supplement those clicks/conversions with additional historical data obtained from the **Bayes Funnel**. We take the data that is available from the current optimization node and combine it with data from the Bayes Funnel; specifically, the most granular level of the funnel in which at least five success events have occurred.

For more detailed information about the Bayes Funnel, see the **How Targeted Learn Leverages Historical Data** on the [Targeted Learn](targeted-learn.md) page.

> [!IMPORTANT]
> The data from the current optimization node could cause the learn rank to go up or down based on its performance relative to our prediction.

## Valuation on an Optimized node

Upon reaching the specified number of success events, a node is considered optimized. At this point, we can determine the likelihood of a success event for this node using the following formula:

**P(success event) = Total Clicks or Conversions / Total Impressions**

When we take this result and plug it into our bid formula (above), we get the total bid valuation for an optimized node:

**valuation = P(success event) X value(success) X 1000 = (Total Clicks or Conversions / Total Impressions) X value(success) X 1000**

## Related topics

- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Learn Budget](learn-budget.md)
- [Targeted Learn](targeted-learn.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Optimization Levers](optimization-levers.md)
- [Cadence Modifier and the Chaos Factor](cadence-modifier-and-the-chaos-factor.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
