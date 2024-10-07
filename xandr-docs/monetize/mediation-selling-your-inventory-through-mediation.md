---
title: Selling Your Inventory Through Mediation
description: Learn how mediation works, and walks you through the process of using our system to set up mediation with external ad networks. 
ms.date: 10/28/2023
---

# Selling your inventory through mediation

> [!NOTE]
> Mediation is only available to Microsoft Monetize Ad Server customers.

## Microsoft Monetize Ad Server mediation

Microsoft Monetize Ad Server mediation allows demand from sources not integrated into the Monetize exchange or [Prebid Server Premium](prebid-server-premium.md) to compete for publisher inventory. Both known partners, such as Google, and custom networks are supported.

This page explains how mediation works and guides you through setting up mediation with external ad networks using Monetize.

### Getting started

To start selling inventory through mediation, customers must:

- Have access to the **Mediation** tab in the Monetize Ad Server account. Contact Microsoft Advertising if this is not already enabled.
- Add the relevant partners [as networks](mediation-networks.md).
- [Create Bids](mediation-bids.md) representing demand from the Networks.

### How mediation works

The high-level mediation workflow is as follows:

1. The publisher sends a bid request to Monetize.
1. Monetize evaluates the bid request against mediated Bids to determine eligibility based on the Bid’s targeting.
1. The Monetize Ad Server runs the auction for the impression, ranking bids from marketplace bidders and mediated bids. Mediated bids use a fixed CPM entered by the publisher, representing the amount they expect the network to pay.
1. If a mediated bid wins the auction, `mediation.js` is loaded on the page, which calls the ad tag previously entered by the publisher.
1. If the mediated Network partner bids, the ad is rendered. If they do not bid in time, the next highest bid from the Monetize auction is used.

For more detailed examples of the request and response process, refer to [Integrating for Mediation](mediation-integrating-for-mediation.md).

> [!NOTE]
> Mediated Networks are not connected directly to the Monetize exchange and do not submit bids into the auction in real-time. Publishers must regularly review reports from each Network and adjust Bid CPM values to ensure they represent a realistic price. Otherwise, an inaccurate mediated Bid could win auctions over higher bids from other sources.

## Related topics

- [Integrating for Mediation](mediation-integrating-for-mediation.md)
- [Mediation services](../digital-platform-api/mediation-services.md)
