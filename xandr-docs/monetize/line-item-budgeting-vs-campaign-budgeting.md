---
title: Line Item Budgeting vs Campaign Budgeting
description: In this article, find information about the different methods of setting budgets along with examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Line item budgeting vs Campaign budgeting

You can set budgets at the line item level, the campaign level, or both, depending on your needs. Each level uses a different methodology when determining how a budget is spent; therefore, when you are planning how to budget, you must consider these different methods. This page will explain the details of these settings and provide some best-practice examples of how to set your budget.

Campaigns are children of line items; the primary impact of this relationship is that when a budget amount is reached or exceeded at the line item level, all campaigns that belong to that line item stop bidding. When a campaign reaches or exceeds its budget amount (if it has one), it stops bidding but has no impact on its parent line item or on any other campaigns under that line item.

> [!NOTE]
> The goal of proper budgeting is to earn the exact amount earmarked by the client and spend an amount that makes the greatest profit for you. However, aspects such as cadence modification, second price auctions, and the time delay inherent in the bidding process make that very difficult. Therefore, when we indicate that you will serve a certain number of impressions or meet a specific budget goal, we mean that you are getting as close as can reasonably be expected.

## Booked revenue vs cost

The line item level uses **booked revenue**, which is the dollar amount the advertiser pays the network. The campaign level uses **cost**, which is the dollar amount that the network spends to purchase impressions. Because these are calculated differently, if you do not recognize the inherent difference between them, you can get into an over- or underspend situation, or you can even lose money on a campaign.

Both the line item level and the campaign level can use **impressions** to count a budget; instead of counting dollars spent or dollars earned, this counts the quantity of impressions without considering cost or revenue. This is the measurement of the number of times that a creative appears to a user.

### Revenue (line item)

Revenue or booked revenue is the budgeting method by which you record the money that the advertiser has given you (the network) to purchase advertising inventory on websites. When line items are created, they are budgeted in this manner because the advertiser has indicated their goals and how much money they will give you to achieve those goals, but it is up to you to determine how to meet those goals.

There are five booked revenue types:

- **CPM** - CPM means cost per mille (thousand), so if you have a revenue budget of $100 and track revenue at a $1 CPM, the budget will be hit once 100,000 impressions are served.
- **CPC** - If you have a revenue budget of $100 and enter a $2 CPC revenue type, the budget will be reached once there has been 50 clicks regardless of the amount of impressions you had to buy to generate those clicks.
- **CPA** - This functions in the same way as CPC but instead of clicks it is based on conversions. You will set a different value for post-view and post-click conversions, and every time one of these events happen that value will be deducted from your budget until there is no budget left. Again, this is based only on those events and does not regard the number of impressions you had to buy to generate those events.
- **Cost Plus** - This adds a margin to total media cost of a campaign via either a flat CPM or a % margin. For example, if you have a 20% Cost Plus margin and a $120 revenue budget, this budget will be hit once the campaign has spent $100 ($100 + 20% = $120)
- **Fixed Fee** - This type of revenue does not require any kind of budgeting, as it represents a one time payment on a certain date and nothing more.

> [!NOTE]
> When working with CPM booked revenue on the line item, setting a performance goal can help prevent you from buying inventory that does not meet the advertiser's performance goal, and gives you a greater degree of control by enabling you to adjust either campaign performance or margin to improve delivery. For more information, see [Understanding Performance Goals](understanding-performance-goals.md) and [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md). To learn about setting up performance goals, see [Add a Performance Goal to a Line Item](add-a-performance-goal-to-a-line-item.md).

Refer to the **Set the booked revenue** section on the [Create a Standard Line Item](create-a-standard-line-item.md) page for more information.

### Cost (campaign)

Cost is the budgeting method by which you record the money that you spend to purchase inventory on websites. When campaigns are created, they are budgeted in this manner because you (as the network) wish to see how much you are spending to purchase inventory compared to how much the client has given you to execute their campaign. The greater the difference, the greater your profit. Therefore, the primary reason for you to establish a cost budget is to control the amount you spend in a campaign. There are four cost types:

- **Optimize to a % of Booked Revenue** - This allows you to set the margin you would like to be left with. For example, if you have a revenue budget of $100 and are tracking on a $1 CPM as in the previous example with your campaign set to optimize to 20% of booked revenue, the campaign budget will be reached once $80 has been spent (80,000 impressions have served).
- **Bid a Base CPM** - If your cost budget is $100 and you are bidding a base of $1 CPM, your cost budget will be reached at 100,000 impressions bought.
- **Optimize to a CPC/CPA Goal** - This will function in the same manner as Bid a Base CPM in regards to your budget with the difference being you will have varying CPM bids.
- **Bid via ECP or EAP** - As above, this will function in the same manner as Bid a Base CPM in regards to your budget however you will have varying CPM bids.

> [!NOTE]
> **Combining CPM booked revenue and CPC/CPA buying strategies**
>
> - When your line item booked revenue is CPM but you want your campaign to optimize to a CPC or CPA goal, we no longer recommend using the Optimize to a CPC/CPA Goal buying strategy. For best results, use the **Performance Goals** section on your line item (from **Create New Line Item**, select **Basic Settings** and go to **Performance Goals** or from **Edit Line Item**, go to **Basic Settings** and select **Performance Goals**) to set a CPC or CPA performance goal.
> - In addition, the ability to combine CPM booked revenue with either the **Pay on a Per-click (CPC) Basis** or the **Pay on a Per-conversion (CPA) Basis** buying strategy is being deprecated. Although this combination will remain functional for existing campaigns, you will no longer be able to use it on new campaigns or when duplicating existing campaigns. For best results, use the **Performance Goals** section on your line item (from **Create New Line Item**, select **Basic Settings** and go to **Performance Goals** or from **Edit Line Item**, go to **Basic Settings** and select **Performance Goals**) to set a CPC or CPA performance goal. Then use **Optimize to a % Margin of Booked Revenue** as your campaign buying strategy.
>
> For more information, see [Using Performance Goals with CPM Booked Revenue](using-performance-goals-with-cpm-booked-revenue.md).
>
> To learn about setting up **Performance Goals**, see Step 6 of [Create a Standard Line Item](create-a-standard-line-item.md).

Review the [Buying Strategies](buying-strategies.md) page for more information.

### Impressions

This is the budgeting method by which you count the number of impressions served instead of money booked or spent. This method can be selected at the line item or campaign level.

## Best practices

The number of possible setting combinations between the line item and the campaign create numerous budgeting scenarios. While it is feasible (and sometimes beneficial) to apply a budget to both levels, we recommend that you first attempt to apply a budget at only one level. If you do apply a budget amount at both levels, you should consider how the different calculation methods (cost vs. revenue) can impact the situation. The following examples show how setting both budget levels can lead to problems, when setting at one level would have achieved the desired goal.

### Example 1

In this example, a client is setting a $10,000 revenue (line item) budget, allocating $5,000 cost (campaign) budget to each of the two campaigns under that line item. Since these budgets are based on different calculations, the assumption that two $5,000 cost-based budgets equals one $10,000 revenue-based budget is incorrect. Therefore, depending on the revenue per impression versus how much it cost to win the impression, you might reach your campaign budgets before you reach your line item budget, or vice versa. Budgeting at one level only will avoid this issue.

### Example 2

In this example, a client is setting two budgets based on CPM, so setting a budget at both levels is not necessary. You can choose to budget based on revenue (line item level) and not budget at the campaign level, or cost (campaign level) and not budget at the line item level. With budgeting set at only one level, there is no concern about reaching one budget threshold before another. Since there is no priority between budgets, whenever any budget threshold is reached, the campaign stops spending immediately. Therefore, if an advertiser is paying you (as the network) $10,000 and you want to retain 20% of that as your fee, there are two ways to do this:

- Set a revenue (line item based) budget of $10,000 and choose the buying strategy **Optimize to a % Margin of Booked Revenue** set to **20%** at the campaign level when defining the buying strategy.
- Set a cost (campaign based) budget of $8,000 to ensure you don't spend more than this and thereby retain the difference between what the advertiser paid you and what you spent to win the impressions.

> [!IMPORTANT]
> You can set buying strategies on both line item and campaign levels even if you only set a budget on one level.

### Example 3

In this example, you are being paid in a non-guaranteed manner (CPC or CPA), so it can be beneficial to budget at both levels. Since your revenue type is based on a click (CPC) or conversion (CPA), you should set a revenue (line item level) budget that will stop bidding once a certain number of clicks or conversions have happened (using the average revenue for each success event). However, to avoid buying impressions without getting the clicks/conversions (which would cause you to spend more than desired) you can also set a cost (campaign level) budget to cap your spend. Since bidding stops when either budget threshold is reached, you are assured that you will not overspend on the campaign even if you do not get the desired click/conversion performance.

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Why Use Budgeting?](why-use-budgeting.md)
- [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)
- [Daily Pacing](daily-pacing.md)
- [Line Item Pacing vs. Campaign Pacing](line-item-pacing-vs-campaign-pacing.md)
- [Key Budgeting and Pacing Concepts](key-budgeting-and-pacing-concepts.md)
