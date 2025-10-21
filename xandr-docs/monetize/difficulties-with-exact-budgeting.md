---
title: Difficulties with Exact Budgeting
description: In this page, learn why it can be difficult to spend exactly as much as you budgeted, so you can make allowances for such variations. Learn how Microsoft Advertising deals with these issues.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Difficulties with exact budgeting

Establishing a budget for a campaign or line item can appear to be a straightforward exercise. However, there is a degree of complexity that makes it difficult to make a campaign or line item hit a budget exactly. This page explains why it can be difficult to spend exactly as much as you budgeted, so you can make allowances for such variations.

> [!TIP]
> The goal of accurate budgeting is to get the amount of actual impressions, clicks or acquisitions purchased to be as close to the quantity specified by the advertiser. However, details such as cadence modification, second price auctions, and the time delay inherent in the bidding process can make that difficult to achieve precisely. Therefore, when you set your budget to purchase a certain number of impressions or spend a specific currency amount, there will generally be some small amount of over or underspend.

It is important to remember that the issues described below affect each other (i.e., the problem of Speed and Volume is compounded by and related to the Number of Bidders).

> [!NOTE]
> **In-flight adjustments to budgets:** Although most in-flight changes to budget settings will change how the bidder responds within 5 minutes, due to the complexity of the backend systems involved, in isolated cases, it can take up to 4 hours for the bidder to modify its behavior in reaction to in-flight budget setting changes.

## Speed and volume

Microsoft Advertising sees over 700 billion impressions every day (as of mid-2022), or more than 8 million impressions each second. Our standard auction timeout is currently 200 milliseconds. Therefore, during the course of an auction, it is possible for us to see 1.6 million impressions. These massive numbers mean that we are likely bidding on a second, third, or fourth impression before we know whether or not we won the first impression, creating a situation where we will always be making budgeting decisions without the most recent spend information. Therefore, the campaign stops spending when it reaches the exact budget amount, but the auctions that are still in progress will come in after that time, resulting in a small amount of overspend.

The following topics are additional aspects of overspend:

## Number of bidders

There can be hundreds of bidders working to win impressions for a single campaign. The total activity across these bidders cannot be recorded and acted upon in real-time; in the time it takes one auction to execute, numerous other auctions have been completed. Therefore, the budget available when an auction begins is different than when it ends.

> [!TIP]
> An analogy would be if you tried to provide second-by-second updates of the location of 10 people by calling each of them on the phone separately. It would be impossible to remain current.

## Small budgets or the budget ends

Campaigns with small budgets can serve their entire budgets so quickly that the sheer quantity of bidders can exceed the budgeted amount before any current auction data can be analyzed. This also occurs when campaigns with larger budgets reach the end of their budget; however, since the amount of overspend is represented as a percentage of the total budget, the overspend percentage for smaller budgets will be much greater than the percentage of overspend for larger budgets. For example, consider two campaigns targeting inventory with a similar cost. If one campaign has a budget of $100, and one campaign has a budget of $10,000, and both overspend by $1, the smaller-budget campaign has a 1% overspend, while the larger-budget campaign has an overspend of .01%. While the overspend amount is the same, the impact on the smaller campaign is more significant.

## A closer look at budget size and overspend

In general, campaigns with smaller budgets are more likely to overspend. This leads us to several questions:

- What is a small budget?

- Is the overspend proportional to the budget size?

- Do small budgets make up most of the overspend?

  To answer these questions, we gathered data over several weeks and analyzed over two million budget objects. Overspend is roughly proportional to the budget, regardless of budget size; therefore, small budgets do not count for a disproportionally large amount of overspend.

  Although the proportion of overspend is not a function of budget size, are smaller budgets more likely to overspend in general? Using the same dataset as before, we determined the probability of overspend by budget size for multiple thresholds. This is graphed below:

:::image type="content" source="media/overspend-probability-graph-a.png" alt-text="Screenshot of budget Size and overspend.":::

:::image type="content" source="media/overspend-probability-graph-b.png" alt-text="Screenshot of overspend graph.":::

  The X-axis shows the **Budget Size** (log axis) and the Y-axis shows the **Probability of Overspend**. Each of the lines represents a different threshold of overspend. What do the charts tell us? **As budget size decreases, the likelihood of overspending increases.** Budgets less than $30 are more at risk to overspend, at 10% chance of overspend. A $1 budget has around a 45% chance of overspending, and a 12% chance of overspending by more than 30% of its daily budget.

## Multiple geography and distribution

If you want to target multiple geographic locations (e.g., United States and Europe), we recommend creating separate campaigns for each geography. Otherwise, you will not be able to control how your budget is spent across geographies (since each geographic location is agnostic of the other, each will try to spend the entire budget and will not stop until the campaign or line item budget threshold is reached).

## How does Microsoft Advertising combat these issues?

We realize that these inherent fluctuations in budgeting can cause problems for our clients regardless of their overall advertising budget. To combat this concern, we apply the concept of [Daily Pacing](daily-pacing.md). By tracking metrics such as the number of bids per impression cleared (also known as the **win rate**), the average time between bids, the budget impact of each impression cleared, and the number of milliseconds to wait between bids for optimal delivery, we know how often to bid on an impression and how often to pass on an opportunity to bid. This procedure greatly smooths the bumps in your spend curve and gives you greater confidence that your campaigns will spend as close as possible to your budget.

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Why Use Budgeting?](why-use-budgeting.md)
- [Daily Pacing](daily-pacing.md)
- [Key Budgeting and Pacing Concepts](key-budgeting-and-pacing-concepts.md)