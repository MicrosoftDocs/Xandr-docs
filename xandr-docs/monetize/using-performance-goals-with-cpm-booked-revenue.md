---
title: Using Performance Goals with CPM Booked Revenue
description: In this page learn why it is better to use performance goals on the line item rather than Optimize to a predicted CPC/CPA goal campaign buying strategies for line items using CPM booked revenue.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Using performance goals with CPM booked revenue

The purpose of this page is to illustrate how to best use Microsoft Advertising optimization when your client is paying you on a CPM basis but will measure results on a CPA, CPC or CTR basis.

In the past, Microsoft Advertising recommended setting up this scenario as a line item with CPM booked revenue and a campaign with the **Optimize to a predicted CPC/CPA goal** buying strategies.

With the release of enhanced Performance Goals section on the line item, we no longer recommend using campaign-based CPC/CPA goals in this case as performance goals will always be more efficient.

To understand why it is better to use performance goals on the line item rather than **Optimize to a predicted CPC/CPA goal** campaign buying strategies for line items using CPM booked revenue, consider the following scenario.

You are responsible for trafficking the following line item from an insertion order with the following specifications:

| Placement | Flight Dates | Rate Type | Rate | Units | Net Cost |
|--|--|--|--|--|--|
| Creative_ABC_RON | 5/1/14 - 5/31/14 | CPM | $1.00 | 10,000,000 | $10,000 |

Additional information:

- The agency issuing the insertion order has stated they would like to pay around $5 per conversion
- You would like to make as much margin as possible with this IO

Let's take a look at what this insertion order would look like if we trafficked it the old way using the **Optimize to a predicted CPA goal** campaign buying strategy.

## The old way: Optimize to a predicted CPA goal (no longer recommended)

### The setup

First, you would set up a line item with a budget of $10,000 and a $1.00 CPM booked revenue. Then you would set up a campaign and select the **Optimize to a predicted CPA goal** buying strategy, and enter the goal and caps to ensure your margin.

The setup would look something like this:

:::image type="content" source="media/optimize-to-cpa.png" alt-text="Screenshot to optimize to CPA.":::

### The results

After setting the campaign live, you may notice positive results. However, behind the scenes the algorithm is buying inventory that does not meet the client's goal.

To understand the sub-optimal results, consider the following breakdown of what is happening inside the optimization algorithm. A, B, C, and D below represent four sites that have become optimized on your campaign. For simplicity's sake, assume the conversion rates are constant and you can buy enough impressions to get one more conversion.

Let's take a look:

| Site | Conversion Rate | Bid Price (CPM) with max bid cap | Advertiser's Cost (CPM) | Imps bought | Network's eCPA | Advertiser's eCPA |
|--|--|--|--|--|--|--|
| A | 1 conversion per 2,500 imps | (1/2500) * 5 * 1000 = $2.00<br>=> $0.80 | $1.00 | 2,500 | $2.00 | $2.50 |
| B | 1 conversion per 5,000 imps | (1/5000) * 5 * 1000 = $1.00<br>=> $0.80 | $1.00 | 5,000 | $4.00 | $5.00 |
| C | 1 conversion per 7,500 imps | (1/7500) * 5 * 1000 = $0.67 | $1.00 | 7,500 | $5.00 | $7.50 |
| D | 1 conversion per 10,000 imps | (1/10000) * 5 * 1000 = $0.50 | $1.00 | 10,000 | $5.00 | $10.00 |
| **TOTAL** | **----------------** | **----------------** | **----------------** | **25,000** | **$4.00** | **$6.25** |

Looking at these four optimized sites, you may see some good things: for instance, you're making a 44% margin and, as far as you can tell, you are getting conversions at a $4.00 CPA.

However, two things are going very poorly:

1. You are **not hitting the advertiser's performance goal.** Instead of the $3.50 CPA that you're seeing based on your media cost, the advertiser will see a $6.25 CPA based on their media cost (your booked revenue).
1. You have delivered **nearly 3/4 of the budget here on inventory (C & D) that does not meet the advertiser's performance goals.**

The main issue is that the **Optimize to a predicted CPA goal** buying strategy prices inventory based on historical performance and **your cost, not the advertiser's**. As a result, you end up buying inventory that's cheap for you but disappointing to your advertiser.

A better strategy would find inventory that:

1. is priced cheaply enough to make your desired margin ($0.80 CPM in this example), and
1. still meets your advertiser's goal.

**Performance Goals** helps do just that.

Now let's take a look at our four optimized sites again, but this time buying with a CPA performance goal on the line item and an **Optimize to % a margin of booked revenue** buying strategy.

## The new way - Using performance goals (recommended)

### The setup

:::image type="content" source="media/optimize-to-margin.png" alt-text="Screenshot of optimize to revenue.":::

### The results

A, B, C, and D below represent the very same optimized sites, but this time we're buying using Performance Goals on the line item.

| Site | Conversion Rate | Advertiser eCPA | Performance Goals Bid/No Bid Decision | Bid |
|--|--|--|--|--|
| A | 1 conversion per 2,500 imps | $2.50 | Bid | $0.80 |
| B | 1 conversion per 5,000 imps | $5.00 | Bid | $0.80 |
| C | 1 conversion per 7,500 imps | $7.50 | No Bid | --- |
| D | 1 conversion per 10,000 imps | $10.00 | No Bid | --- |

The performance goals bid decisioning **prevents you from buying inventory that does not meet the advertiser's performance goal.**

The system can now allocate the budget from C & D towards buying more impressions from A & B and/or learning on other sites that may be likely to hit your performance goal.

## Further troubleshooting to improve delivery

If you find that you are still not on track to deliver the full budget for the advertiser, **performance goals give you a much greater degree of control by enabling you to adjust either performance or your margin to improve** **delivery.**

### Trade performance for delivery

With the two fields in the Performance Goals section of line item setup, you can easily increase your no-bid threshold while still tracking revenue at your client's stated CPA or CPC goal. In this scenario, you are making a strategic tradeoff between delivery and performance.

:::image type="content" source="media/performance-goals.png" alt-text="Screenshot of performance goals.":::

### Trade margin for delivery

Adjusting the **Optimize to a % margin of booked revenue** field on the campaign will allow you to increase and decrease your bid price, changing your margin and also controlling the price you're bidding for inventory.

> [!IMPORTANT]
> You will soon be able to adjust your margin centrally on the line item for all associated campaigns.

:::image type="content" source="media/margin.png" alt-text="Screenshot of Trade Margin for delivery.":::

By successfully managing tradeoffs between performance, margin and delivery, you can manage your line item to meet your clients' goals while also maximizing your margin.
