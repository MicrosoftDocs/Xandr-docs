---
title: Guaranteed Delivery Pacing
description: In this article, find information about the pacing algorithm that governs how Guaranteed Delivery line items meet their budgets.
ms.date: 10/28/2023
---

# Guaranteed delivery pacing

> [!IMPORTANT]
> This option is available only to Xandr Ad Server customers.

[Guaranteed Delivery](guaranteed-delivery.md) line items are designed to deliver their budgets in full and evenly across their flight dates. How guaranteed line items pace determines how well they meet the requirements of those budgets.

This page describes the pacing algorithm that governs how Guaranteed Delivery line items meet their budgets.

> [!NOTE]
> The descriptions of our guaranteed pacing algorithm on this page apply to version 1.0. Over the coming months, we plan to roll out a version 2.0 with a number of improvements.

## The ideal delivery curve

For a guaranteed line item with a delivery goal of 1 million impressions over a 60-day flight that is set to the default pacing value of 105%, the ideal delivery curve looks like this:

:::image type="content" source="media/ideal-delivery-curve.png" alt-text="A graph of days against daily delivery goal that shows the ideal delivery curve.":::

To achieve the ideal delivery curve, we have to control the delivery rate across a distributed system of bidders over the entire length of the flight. Broadly speaking, there are two ways to control the delivery rate:

1. Raising or lowering the bid price
1. Deciding whether to bid or not

### The challenge

Due to physical constraints (such as how fast information propagates across networks), it's impossible to adjust bid prices and bid/no-bid decisions in real-time across our distributed system of bidders to precisely match bid request rates and win rates. Instead, information can only be propagated across systems at slower-than-realtime speeds.

Furthermore, even if it were possible to adjust bid decisions in real-time, the request rates and win rates across a slice of inventory are often extremely volatile, as shown in the graphs below. Due to the fact that budgets are distributed across our many bidders and any real-time calculations have to occur locally at the bidder level, were we to attempt to adjust bid decisioning in response to this information, each bidder would have either a very outdated estimate of the request and win rate (due to slower-than-real-time updates), or a very noisy one (thanks to the volatility of the graphs).

To give you some idea of the volatility involved, here are the bid requests per minute across one randomly selected slice of inventory on the Xandr platform over a 24-hour period in early 2015:

:::image type="content" source="media/request-rate.png" alt-text="A graph of minutes against bid requests per minute for one random inventory over a 24-hour period.":::

Here is the win rate of a $0.10 CPM bid for a similar randomly selected slice of inventory graphed over a 24-hour period in early 2015:

:::image type="content" source="media/win-rate.png" alt-text="A graph of minutes against win rate for one random inventory over a 24-hour period.":::

### Our solution

Given these challenges, and the requirement that we maintain the even delivery rate required by sellers, we forego attempting to update bidders in real-time and instead dynamically estimate the request rates and win rates algorithmically, based on a statistical analysis of sample data. Specifically, we use a [Logistic regression](https://simple.wikipedia.org/wiki/Logistic_regression), which is a fancy way of saying that we use a mathematical model to guess the probability of an event given some other data.

In addition to mathematical modeling of request rates and win rates, we do a few other things to make sure that guaranteed line items meet publisher commitments:

- Set the pCPM bid price slightly higher than strictly necessary to ensure robust win rates.
- Cap the delivery rate to avoid over-delivery by having individual bidders go to sleep (i.e., stop bidding) when ahead of even delivery by a certain percentage.
- Set the daily budget goal at 105% of even lifetime delivery by default to ensure goals are met.
- Ensure that when guaranteed line items compete for the same impression, we select one based on a weighted average of their target win rates. In other words, most of the time, we choose the guaranteed line item that is further from meeting its delivery goals to serve on eligible impressions.

For more information about pCPM and how competition between guaranteed line items works, see [Guaranteed Delivery Auction Mechanics](guaranteed-delivery-auction-mechanics.md).

## Behavior at the start of the campaign

At the start of the campaign, guaranteed line items will attempt to "front-load" slightly to ensure that budgets are delivered (assuming that the line item pacing is set to the default of 105%). This, combined with the settings described above, should cause the delivery curve to look like the graph in [The Ideal Delivery Curve](#the-ideal-delivery-curve) section.

## Behavior at the end of the campaign

Currently there is no special behavior that takes place during the final hours of the line item's flight. Line items continue to pace according to the algorithm described here until the flight ends.

## Timing of budget updates

Unlike some other systems that only recalculate pacing goals every hour or eight hours, the pCPM values that allow guaranteed line items to compete with RTB bids are recalculated locally by the bidder every few minutes. This is supplemented by the global budget update that goes out to all bidders, which happens approximately every 15 minutes.

## Underdelivery and how we catch up

### Catch up examples

The way we try to catch up underdelivering line items is by having the line item try to purchase enough impressions to bring it back to even delivery within a 24-hour period after underdelivery is detected.

For example, if a guaranteed line item is behind by 100,000 impressions and has a daily delivery goal of 20,000 impressions, it will attempt to serve 120,000 impressions during the current 24-hour period.

Here's another example that follows a 7-day campaign with a budget of 700,000 imps throughout its flight:

1. Day 1: Line item delivers 102,000 imps, and is on pace.
1. Day 2: Line item is paused early in the day.
1. Days 3, 4, and 5: Line item remains paused.
1. Day 6: Line item is enabled to serve and starts trying to catch up the underdelivery. Since it is behind by approximately 400,000 impressions, it will attempt to serve 500,000 impressions on day 6: 100,000 for each of the days it was paused, and 100,000 to fulfill the current day's budget.
1. Day 7: If the line item was able to catch up fully on day 6, it delivers normally (approximately 100,000 impressions) on day 7. If the line item wasn't able to catch up, it will once again try to catch up however many impressions it's still behind, plus 100,000 to fulfill the delivery goal for day 7.

### How the daily budgeting process works

For any given line item, the daily budgeting process will run once per day at midnight in the timezone of the line item. The basic steps of this process are:

1. Calculate the delivery amount needed to catch up in full by the end of the coming day.
1. Calculate the historical rate of underdelivery, looking back over the past 4 days.
1. Divide the delivery amount calculated in the first step (#1 above) by the average underdelivery rate (#2 above) to account for persistent underdelivery. This value is used as our daily delivery goal.

## Related topics

- [Guaranteed Delivery](guaranteed-delivery.md)
- [Guaranteed Delivery Auction Mechanics](guaranteed-delivery-auction-mechanics.md)
- [Using Multiple Campaigns with a Guaranteed Line Item](using-multiple-campaigns-with-a-guaranteed-line-item.md)
- [Create a Guaranteed Delivery Line Item](create-a-guaranteed-delivery-line-item.md)
