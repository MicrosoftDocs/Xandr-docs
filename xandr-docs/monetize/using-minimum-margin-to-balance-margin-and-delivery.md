---
title: Using Minimum Margin to Balance Margin and Delivery
description: Learn how using minimum margin you can attain right balance between delivery and margin. This page explores steps to set up the line item so that you make as much margin as possible.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Using minimum margin to balance margin and delivery

This page illustrates how you can use Minimum Margin to better manage your margins and find the right balance between margin and delivery for your line items.

With Minimum Margin, you have the ability to **manage your margin from a central location on the line item.** This easy to use lever, allows you to find the **right balance between delivery and margin**. To understand how Minimum Margin can help you, consider the following scenario.

You are responsible for trafficking the following line item from an insertion order with the following specifications:

| Placement | Flight Dates | Rate Type | Rate | Units | Net Cost |
|--|--|--|--|--|--|
| Creative_ABC_RON | 5/1/14 - 5/31/14 | CPM | $5.00 | 50,000,000 | $10,000 |

Your number one goal, first and foremost, is to deliver the budget in full. However, you want to make as much margin as possible from this line item. Let's take a look how you would set up this line item.

## The setup

First, you set up a line item with a budget of $10,000 and a $5.00 CPM booked revenue. Not wanting to impact the initial delivery of the line item, you begin with a conservative minimum margin of 5%.

:::image type="content" source="media/min-margin.png" alt-text="Screenshot of Min margin.":::

The minimum margin % on the line item ensures that all child campaigns are bidding at or below the minimum margin % for 3rd party inventory. Let's look at how it works behind the scenes.

## In action

For this example line item, consider two children campaigns, A & B, buying 3rd party inventory. The minimum margin of 5% essentially caps the bids of all the campaigns.

| Campaign A | Campaign B |  |
|--|--|--|
| Bid | $5.00 * (1-.20) = $4.00 | $5.00 |
| Buying Strategy | Prospecting campaign <br>Optimize to 20% of Booked Revenue | Re-targeting campaign <br>Bid a base of $5.00 |
| **Final Bid with Min Margin of 5%** | **$4.00** | **$4.75** |
| **Min Margin Cap** | **$5.00 * (1-.05) = $4.75** | **$5.00 * (1-.05) = $4.75** |

After some time, you notice the budget is on pace and are making a healthy margin of 18% with the two campaigns. You now want to see if you can make more, so you adjust the minimum margin to 25% to ensure an even greater margin.

| Campaign A | Campaign B |  |
|--|--|--|
| Bid | $5.00 * (1-.20) = $4.00 | $5.00 |
| Buying Strategy | Prospecting campaign <br>Optimize to 20% of Booked Revenue | Re-targeting campaign <br>Bid a base of $5.00 |
| **Final Bid with Min Margin of 25%** | **$3.75** | **$3.75** |
| **Min Margin Cap** | **$5.00 * (1-.25) = $3.75** | **$5.00 * (1-.25) = $3.75** |

However after raising the minimum margin to 25% you start to see delivery on the line item start to suffer and readjust downwards to 20% So on and so forth until you find the right balance.

|  | Campaign A | Campaign B |
|--|--|--|
| Bid | $4.00 | $5.00 |
| Buying Strategy | Prospecting campaign <br>Optimize to 20% of Booked Revenue | Re-targeting campaign <br>Bid a base of $5.00 |
| **Final Bid with Min Margin of 20%** | **$4.00** | **$4.00** |
| **Min Margin Cap** | **$5.00 * (1-.20) = $4.00** | **$5.00 * (1-.20) = $4.00** |

**Minimum Margin is a single, easy to use lever to lower your overall margin to improve delivery (and vice versa if delivery is strong).**

## Campaigns targeting direct inventory

For campaigns targeting direct publishers in your network, you enable margin controls at the network level. This is a network-wide setting and should be enabled when when you have made a business decision to prioritize margin for your line items over fill on your direct inventory.

If the network setting is enabled, the direct campaign will only serve on direct inventory where the minimum margin is met. Let's take our previous example and add a third campaign targeting three direct publishers.

Line item: $5.00 CPM booked revenue and minimum margin of 20%

|  | Campaign A | Campaign B | Campaign C |
|--|--|--|--|
| Bid | $4.00 | $5.00 | $5.00 |
| Buying Strategy | Prospecting campaign <br>Optimize to 20% of Booked Revenue | Re-targeting campaign <br>Bid a base of $5.00 | Direct Inventory<br>Targeting: Publishers X, Y & Z |
| Final Bid with Min Margin of 20% | $4.00 | $4.00 | --- |

Let's see what happens when this Campaign C bids on the three publishers.

:::image type="content" source="media/min-margin-on-direct.png" alt-text="Screenshot of Campaign C biding on the three publishers.":::

Minimum Margin ensures that the direct campaign only serves on publishers where you will meet your minimum margin %.
