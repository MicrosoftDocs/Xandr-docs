---
title: Network Revenue and Billing Your Clients
description: The article guides readers in comprehending Network Revenue, media cost, network profit, and client billing processes.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Network revenue and billing your clients

## Overview

Networks use Microsoft Monetize to buy inventory on behalf of their advertisers. This inventory may be:

- **3rd-party**: inventory sold by other networks/exchanges on the platform
- **Managed**: inventory purchased directly from managed publishers with whom the network has proprietary relationships

To succeed in their role as financial intermediaries, networks must be able to easily and accurately invoice their advertisers and pay their publishers for **all activity**, as well as have the tools to make sure they maintain an appropriate profit margin.

:::image type="content" source="media/activity-diagram.png" alt-text="Diagram that explains how the networks is able to easily and accurately invoice their advertisers.":::

## Pulling billing reports

The Billing Report tool of Microsoft Monetize allows you to easily manage internal invoicing for your publishers and advertisers across all activity, both managed and 3rd-party buying and selling. To access this tool, go **Network**  >  **Reporting** and select "Billing Report" from the **Type** drop-down. You now have a new set of metrics and dimensions available which simplify your in-house invoice development process.

## Booked revenue: How advertisers pay networks?

Advertisers make all kinds of financial deals with networks, based on CPMs, CPAs or other models. Within Microsoft Monetize, networks can input their "booked revenue," or the revenue they will receive from advertisers.

- CPM: A flat payment per thousand impressions
- CPC: A flat payment per click
- CPA: A flat payment per conversion
- Cost Plus (CPM): Your total cost (whatever you, the buyer, spend on inventory including data costs cleared through AppNexus plus any serving fees and commissions) plus an additional flat payment per thousand impressions
- Cost Plus (Margin): Your total cost, plus a margin (total cost \*  (1+X%))
- Fixed Fee: A flat payment on a specified allocation date

Booked Revenue is set at the line item level. Setting these values allows the system to report back against how you should be billing your advertisers.

Although defining your revenue values at the Line Item level is technically optional, please note that not entering your revenue values limits to a great degree the amount of information we can present in the billing reporting tools.

## Media Cost: How networks pay publishers?

Networks can buy from real-time publishers, or they can buy from their own, managed publishers. Real-time publishers are paid on a CPM basis. Networks and other Microsoft Monetize users can use bidding strategies to optimize their bids based on events other than impressions, such as [Buying Strategies](buying-strategies.md), but ultimately the bids themselves are made using CPMs.

For managed publishers, networks can set their pricing models as:

- **CPM**: Publisher is paid a flat fee per thousand ads served
- **Revenue share**: Publisher is paid a percentage of booked revenue received from the advertiser

When you apply a pricing model to a publisher in Microsoft Monetize, this is for reporting purposes only and will not affect **actual** publisher payout. Networks pay their publishers directly, rather than through Microsoft Monetize.

## Network profit

The Network's profit is then Booked Revenue - Media Cost. For booked revenue that is dependent on an event (CPC or CPA), there will be a waiting period before networks can bill advertisers and consequently pay publishers.

## Example

Let's say an advertiser, Prostarr Sportswear, will pay a $1 CPM to Network A, and will pay a maximum of $10,000 over the next month. The money is not dependent on performance, but there are certain restrictions. They want users between 20 and 40 who live in the major U.S. metropolitan regions where Prostarr has stores, and they have different creatives for men and women. They want to show their ads on sports sites, news sites, and Facebook.

For this example, Network A is buying only 3rd party inventory and not from its own managed publishers.

Network A enters the $1 CPM and $10,000 budget into the Line Item. Within that line item, they create one campaign that targets women, and one that targets men, each with the appropriate creative. Within each campaign they target the advertiser's desired inventory and regions.

Now they have to decide how much profit they need to make from this transaction. Let's say they want to spend a $.50 CPM, and make a $.50 profit. So they bid $.50.

Now when they go to bill the advertiser, they run a report on booked revenue, and that is the amount they bill advertisers. A report on media cost tells them how much they owe the Microsoft Advertising platform.

They can also run reports on revenue to easily see the difference between what they spent and what they made.
