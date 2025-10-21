---
title: Daily Pacing
description: Learn when enabled how Daily Pacing helps campaigns spend their budgets fairly evenly over the day. This page also addresses some common questions related to pacing.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Daily pacing

When you set a daily budget for a campaign, you have the option to enable **Daily Pacing**. When it is enabled, Daily Pacing helps campaigns spend their budgets fairly evenly over the day. Without pacing, campaigns purchase as much inventory as possible between budget updates. If you have a campaign with a small budget or a high win rate and pacing is not enabled, you can easily overspend your budget. While you can take certain steps to ensure that you get the maximum benefit from Daily Pacing, the calculations are done by the system automatically during the day without human interaction.

> [!NOTE]
> **In-flight adjustments to budgets:** Although most user-initiated in-flight changes to budget settings will change how the bidder responds within 5 minutes, due to the complexity of the backend systems involved, in isolated cases, it can take up to 4 hours for the bidder to modify its behavior in reaction to manual in-flight budget setting changes.

Daily Pacing allows us to calculate a pacing lever which modifies the rate at which bids are submitted, slowing the buy rate over time and delivering the budget more evenly over the day. The pacing lever adjusts automatically throughout the day based on the performance of the campaign to that point in an attempt to maintain an even budget delivery.

Microsoft Advertising recommends that you enable pacing for most campaigns.

## How the system reduces over- or underspend

When a campaign serves too many or too few impressions in a day, it is called **overspend** or **underspend** (respectively). In order to avoid either of these conditions, the system uses the following information to determine the pacing lever:

- **The total number of minutes in the day during which your ad can serve** If you have not placed any restrictions regarding the time of day during which your ad can serve (daypart restrictions), this value is **1,440** (the number of minutes in a standard day). If you have determined that your ad can serve only from 6 - 11 a.m. and from 3 - 8 p.m. every day (called daypart restrictions), then this value is **600** (10 hours per day).
- **The number of minutes remaining in the day during which your ad can serve** At any given point during the day, there are only so many minutes remaining during which your ad can serve. For example, if you have no daypart restrictions in place, at 10 a.m. there are **1,080** minutes remaining for that ad to serve. If you have daypart restrictions in place indicating that your ad can serve only from 6 - 11 a.m. and from 3 - 8 p.m. every day, at 10 a.m. there are **360** minutes remaining for that ad to serve (one available hour until 11 a.m., and then five available hours from 3 - 8 p.m.).
- **The budget spent up to the most recent time stamp** The system must know how much of the budget has been spent at a given point in time in order to determine if it is necessary to change the daily pacing lever.
- **The budget spent during the last budget update** In order to determine a trend, the system must know how much of the budget has been spent in the period between the two most recent time stamps.
- **The daily budget** This is the amount of the budget that should serve on the current day.

> [!NOTE]
> When referring to the budget spent, you can use quantity (i.e., 156 ads served) or dollar amounts (i.e., $1,850 of ads served). However, you must use the same value for all calculations. Budgets set in dollar amounts are set against booked revenue at the line item level, and against media cost at the campaign level.

The system periodically checks this information (approximately every 15 minutes) and determines if the pacing lever needs to be adjusted.

## Example

- You have a campaign with a daily budget of **2,000** impressions (i.e., must be met by 12 a.m. midnight).
- As of 8 p.m. (the most recent time stamp), the system had served **1,200** impressions for the day.
- As of 7:45 p.m., the system had served **1,175** impressions for the day.
- There are no daypart restrictions.

In order to reach your budget of **2,000** impressions, we must serve **800** more impressions in four hours. Since we served an average of **25** impressions in the previous 15-minute period, we will likely only serve another **400** impressions before the end of the day. This will represent a budget underspend. Therefore, in order to meet the daily budget amount, the system increases the bid rate enough so that it will win an additional **400** impressions by midnight.

## How the system moderates the pacing settings

When the system modifies the daily pacing to account for daily over- or underspend, it can be in danger of generating a spend spike. For example, the process described in the example above is unable to consider that this ad wins a great number of bids between 11:30 p.m. and midnight; if the daily pacing lever is adjusted without considering this, the system is likely to drastically overspend in the last 30 minutes of the day (generating a "spike" in successful bids) and exceeding the budget amount significantly. It is also possible to perform this in reverse (reduce a bid so drastically that it falls well below the budget amount).

To combat this, the system uses the three most-recently completed pacing values (which includes the over- or undespend pacing value) to determine the pacing value for the coming period. This more-closely aligns the bidder to the correct bid rate, and also moderates the pacing value.

## How you can ensure proper pacing for your campaign

Due to the complexity of bidding in real time, it is extremely difficult to provide exact pacing. Our system must rely on certain assumptions about earlier performance in order to maintain a steady and even rate of delivery for the remainder of the day. Campaigns that do not conform to these assumptions will have a greater difficulty pacing evenly compared to campaigns that do. Therefore, the more you comply with the following guidelines, the greater the likelihood that your campaign will enjoy smooth delivery.

- **Limit intra-day changes to inventory, bids, or targeting** Since we can't predict how much inventory a campaign will win in real time, we rely on recent delivery as an indicator of future delivery. If you increase these values, you will change the rate of won impressions; however, we could continue pacing based on the delivery rate before the change for up to two budget cycles (20-40 minutes). If the difference between delivery rates is great enough, the budget will overspend or deliver faster than anticipated, before pacing can account for the new win rate. Therefore, try to perform as few of these in-flight changes as possible.
- **Keep your budgets consistent** Budgets set at the campaign level have no knowledge of budgets set at the line item level, and vice-versa, so if one campaign has used all of its allotted budget, the other will not adjust the rate at which it is pacing to compensate. Therefore, you should make sure that campaign level budgets and line item daily budgets do not restrict each other.
- **The smaller your budget, the greater the margin for error** In order to spend a budget, a portion of it must be allocated to each bidder. Considering the number of individual bidders within Microsoft Advertising (thousands), it becomes more difficult to allocate that amount accurately. This leads to us delivering budgets much faster than expected. To combat this situation, you can do one of the following:
  - **Increase the budget:** This gives pacing a chance to work.
  - **Decrease the win rate:** The most effective way to do this is to reduce your bid amount.
  - **Decrease the pool of available inventory:** You can do this by adding targeting, limiting delivery to certain high-quality buyers, or both.
- **Ensure that your Learn Budget amount does not restrict your Daily Pacing amount** When using optimization, if you set a learn budget amount that is less than the daily pacing amount, new campaigns (with no optimized inventory) will stop serving when the learn budget amount is reached. For more information, see [Learn Budget](learn-budget.md).

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Why Use Budgeting?](why-use-budgeting.md)
- [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)
- [Key Budgeting and Pacing Concepts](key-budgeting-and-pacing-concepts.md)