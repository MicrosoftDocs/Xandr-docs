---
title: Cadence Modifier and the Chaos Factor
description: Explore how Cadence Modifier shapes bids, factoring in frequency and recency for precise bid amount determination.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Cadence modifier and the chaos factor

## Overview

The Cadence Modifier adjusts the amount of a bid based on the **frequency** (the number of times the user has seen the creative) and **recency** (the amount of time that has passed since the user last saw the creative) of the user. Frequency and recency are two of many factors which influence the conversion likelihood. For example, if the bid in an
auction is $1, and the frequency and recency values indicate that this user is three times as likely to convert that impression, the system will increase the bid to $3. Conversely, if the frequency and recency values indicate that the user is only one-quarter as likely to convert that impression, the system will decrease the bid to $0.25.

The conversion likelihood, against which increased or decreased likelihood is measured, is the overall number of conversions divided by the overall number of impressions.

> [!IMPORTANT]
> The term conversion refers to the success event you have defined for the campaign. This can be a click or an acquisition.

For example, if there are a total of 100 impressions and 20 converted for an entire campaign regardless of frequency or recency, that equals a 20% conversion rate. If, of those impressions and conversions, 10 impressions and three (3) conversions occurred during a specific frequency/recency "bucket", that combination equals a 30% conversion
rate, which is 1.5 times greater than the overall rate. Therefore, the system will bid 1.5 times the normally-calculated bid amount in that auction. This is a cadence modifier value. Cadence modifier values are combined into a cadence model which is used to adjust bid amounts accordingly.

The table below is an example of the cadence modifiers for a specific advertiser:

| Frequency/Recency | 0-22 seconds | 21-44 seconds | 45-63 seconds |
|--|--|--|--|
| 0-2 times | 1.4 | 1.6 | 2.0 |
| 3-5 times | 2.0 | 2.0 | 0.6 |
| 6-8 times | 1.1 | 0.8 | 0.6 |
| 8-11 times | 0.3 | 0.2 | 0.1 |

In this instance, if the user has seen a creative between zero and two times, and last saw the creative between 21 and 44 seconds ago, the modifier applied would be **1.6** (the bid amount would be multiplied by a factor of 1.6). However, if that user saw that creative between three and five times, no more than 22 seconds ago, the modifier would change to **2.0**.

## How the table is populated

The initial data (frequency, recency, and conversion likelihood) which makes up this table comes from one of three sources, depending on cadence type and data sufficiency:

- **Advertiser** - The advertiser-level cadence type measures frequency and recency of how often a user has seen any creative from the advertiser. This cadence type is recommended when all creatives within an advertiser are similar.

- **Creative -** The creative-level cadence type measures frequency and recency of how often a user has seen the particular creative. This cadence type is recommended for generic creatives or when the creative is unlike other creatives under the advertiser.

- **Default** - If the model has insufficient conversion rate information (e.g., a brand new advertiser), the table is populated with default values from Microsoft Advertising. These default values are used in auctions until sufficient impressions and conversion data is obtained.

  Once initial data has been applied, the system can begin to bid on auctions. As impressions are won, the system gains additional information about when users convert impressions and adjusts the individual buckets accordingly. The borders of a bucket can shift based on statistical changes, as can the likelihood factor.

  > [!IMPORTANT]
  > The frequency/recency buckets are not of fixed size. The exact borders (e.g., frequency of 3-5, recency of 21-44 seconds) are determined by algorithms to be the most accurate statistically. Therefore, a bucket that started with a frequency of 3-5 and a recency of 21-44 seconds can change to a frequency of 2-4 and a recency of 30-40 seconds.

## Applying the chaos factor

Bidding is not an exact science. While Microsoft Advertising has tools that strive to determine the most effective bid amount for each auction, there is no guarantee that the bid is the best possible value. Therefore, after the bid is determined and the Cadence Modifier is applied, a final factor called the **Chaos Factor** is applied. This is a random calculation which can increase or decrease a bid up to the mean statistical variation of the frequency/recency bucket (which rarely exceeds 5%). In the event of similar campaigns that have very close bid amounts, the chaos factor ensures that neither campaign will win all of the auctions over the other. The chaos factor is used whenever the cadence modifier is applied, but cannot be applied to a bid amount independently.

## Other considerations

- Optimization automatically applies the cadence modifier.
- When you are bidding a base amount (e.g., you set a fixed bid for all auctions), the cadence modifier is not applied unless the setting **Enable Variable Pricing** is checked in Microsoft Monetize.
- If you restrict frequency and/or recency, you may be reducing the effectiveness of cadence modifier. If you set the frequency value to zero (0), the cadence modifier has no impact on the bid amount.

## Related topics

- [Optimization Guide](optimization-guide.md)
- [Optimization In-Depth](optimization-in-depth.md)
- [Optimization Buying Strategies](optimization-buying-strategies.md)
- [Targeted Learn](targeted-learn.md)
- [What is an Optimization Node?](what-is-an-optimization-node.md)
- [Learn Budget](learn-budget.md)
- [What is Valuation?](what-is-valuation.md)
- [Optimization Levers](optimization-levers.md)
- [Sell-Side Optimization](sell-side-optimization.md)
- [Dynamic Learn Percentage](dynamic-learn-percentage.md)
- [Give Up Price](give-up-price.md)
