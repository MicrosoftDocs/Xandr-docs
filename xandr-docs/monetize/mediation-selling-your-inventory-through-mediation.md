---
title: Selling Your Inventory Through Mediation
description: This page explains how mediation works, and walks you through the process of using our system to set up mediation with external ad networks. 
ms.date: 10/28/2023
---


# Selling your inventory through mediation

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

Mediation is a process by which you allocate inventory to buyers that are not directly integrated with our exchange. This is necessary in order to get access to certain demand sources (mobile ad networks in particular). We help you manage your mediation efforts by providing the following features:

- See the performance of all of the networks you work with in one place
- Built-in support for integrating with popular networks
- Support for custom network integrations

This page explains how mediation works and walks you through the process of using our system to set up mediation with external ad networks. The focus is on networks we support, but you can create custom networks to perform any kind of integration you want.

## Getting started

To start selling your inventory through mediation, you must:

1. Have the **Mediation** tab enabled for your Microsoft Advertising Monetize Ad Server account. You'll need to contact your Microsoft Advertising representative.
1. From the list of supported networks in the **Mediation** tab, add the networks for which you have accounts. For instructions, see [Mediation Networks](mediation-networks.md).
1. Once you've created your networks, switch to the bids page and begin creating bids. For instructions, see [Mediation Bids](mediation-bids.md).
1. Activate your bids to start selling.

## How mediation works

At a high level, here's how mediation works:

1. You [Mediation Networks](mediation-networks.md) to our system that represents a mediated ad network.
1. You [Mediation Bids](mediation-bids.md) which is used to rank that network in auctions for your inventory. The bid should represent the amount you think the network is likely to pay for your inventory.
1. The auction is run, with the bid price you set used to rank the mediated bid against other bids coming in from the exchange in real-time.
1. The mediated network either returns an ad or not. If no ad is returned or the network does not respond in time, we move on to the next highest bid in the auction.

Because the mediated networks are not connected directly to the exchange, they are not submitting bids in real time. Therefore it's very important for the bids you create to be kept as accurate and up-to-date as possible. Otherwise, an inaccurate mediated bid could win auctions over other, higher bids that would make you more money.

To illustrate this point, the diagram below represents an auction with three bids. The top bid (marked in green) is a mediated bid for $2.00 from a network called CoolAds. Because the CoolAds bid is higher than the other bids coming in, it wins the auction. However, CoolAds may not actually be paying you $2.00, and you won't find out until well after the auction when you check the daily totals from the CoolAds servers.

> [!NOTE]
> For more information about how mediated bids interact with the other demand types in auctions, see [How Auctions Work for Sellers](mediation-how-auctions-work-for-sellers.md).

:::image type="content" source="media/ssp-auction-example-a.png" alt-text="Screenshot of an auction with three bids.":::

## Related topics

- [How Auctions Work for Sellers](mediation-how-auctions-work-for-sellers.md)
- [Integrating for Mediation](mediation-integrating-for-mediation.md)
- [Mediation FAQs](mediation-faqs.md)