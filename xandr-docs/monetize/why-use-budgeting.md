---
title: Why Use Budgeting?
description: The article explains budget that is client's spend or impressions goal for insertion order, line item, or campaign. 
ms.date: 10/28/2023
---

# Why use budgeting?

A budget is the amount of money or the number of impressions that a client wants to spend for a specific insertion order, line item or campaign. Ideally, this budget amount is based on the specific business needs or goals of the client.
Once the budget for a campaign (or its parent line item) has been met, the campaign will no longer bid on inventory, and no creatives will be served. Budgets can be established on a daily basis, for the lifetime of the campaign, or for both. It is neither necessary nor required to set a budget for each campaign; however, not doing so can create very risky
scenarios.

Budgets can also be created for insertion orders and line items. An insertion order is a parent to one or more line items, and a line item is a parent to one or more campaigns. When a parent entity (e.g., an insertion order) reaches its budget amount, any children of that parent are also restricted from serving creatives. Therefore, if a budget is
established for an insertion order, and it is reached, all line items belonging to that insertion order (regardless of their budget amount) cease activity. Subsequently, all campaigns under those lines items stop serving creatives (again, regardless of their budget amount). This is one way to reduce the potential of spending a great deal more than
desired (also known as overspend).

When a client sets a budget, that client has determined that they need to spend a specified amount to get a specific message across and, either immediately or in the future, recognize a benefit from the campaign (e.g., larger mailing lists, increased product sales, etc.).

## Types of budgeting

There are many different ways to apply a budget. You can determine whether your budget is counted in revenue, cost, or in the number of impressions served. The choice of which to use is up to you, but once you make a selection, you must count the budget in that manner through the life of the insertion order, line item or campaign.

You can apply a budget to an **Insertion Order**, a **Line Item**, or a **Campaign**:

| Object Type | Budget Type | Description |
|---|---|---|
| Insertion Order | Revenue-based | The system measures the booked revenue (in advertiser-selected currency) against the entire insertion order. You would select this option to reach a set goal of dollars earned by the insertion order. This would not necessarily take the amount of dollars spent into account, but there are other methods at work to ensure that you do not spend more money than you earn. |
| Insertion Order | Impression-based | The system measures the number of impressions served against that entire insertion order. You would select this option to serve a specific number of impressions by the insertion order (with the assumption that you know or have a good estimate of the rate and value of impressions). |
| Line Item | Revenue-based | The system measures the booked revenue (in advertiser-selected currency) against the entire line item. You would select this option to reach a set goal of dollars earned by the line item. This would not necessarily take the amount of dollars spent into account, but there are other methods at work to ensure that you do not spend more money than you earn. |
| Line Item | Impression-based | The system measures the number of impressions served against that entire line item. You would select this option to serve a specific number of impressions by the campaign (with the assumption that you know or have a good estimate of the rate and value of impressions). |
| Campaign | Cost-based | The system measures the dollars spent in the campaign. You would select this option to stay within a set amount of dollars spent, regardless of how much income the campaign may or may not generate. |
| Campaign | Impression-based | The system measures the number of impressions served against the campaign. You would select this option to serve a specific number of impressions by the campaign (with the assumption that you know or have a good estimate of the rate and value of success events). |

## Budget caps

The buy-side objects to which you can associate a budget (**Insertion Order**, a **Line Item**, or a **Campaign**) are hierarchical:

- **Insertion Orders** contain **Line Items**
- **Line Items** contain **Campaigns**

If a parent item has a budget assigned to it, and that budget is reached, all children under that parent will stop bidding on inventory, regardless of whether or not they have reached their individual budgets. Therefore, if one campaign in a line item spikes and exhausts the parent line item's budget, all campaigns under that line item will stop bidding, even though they haven't reached their specific budget amounts.

## Risks of not budgeting

Budgeting acts as a control feature, maintaining an upper limit that the campaign, line item, or insertion order cannot exceed. Without a budget, your campaign could continue to win bids and spend money until you deactivate it. Even in a short time, a campaign can easily spend tens of thousands of dollars. Therefore, it is strongly recommended that you set
lifetime budgets on your campaigns (daily budgets are also recommended). It is also recommended that you set both lifetime and daily budgets for your parent line items and insertion orders. These practices will help you avoid overspend.

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)
- [Daily Pacing](daily-pacing.md)
- [Key Budgeting and Pacing Concepts](key-budgeting-and-pacing-concepts.md)
