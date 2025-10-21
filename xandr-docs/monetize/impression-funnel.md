---
title: Microsoft Monetize - Impression Funnel
description: In this article, find information about the Impression Funnel and details about the metrics associated with it.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Impression funnel

The Impression Funnel provides detailed line item metric information in the form of graphs and charts.

> [!IMPORTANT]
> The Microsoft Monetize Monitoring feature is in **Open Beta** and currently only supports deal line items, augmented line items (ALI), and guaranteed delivery augmented line items (GDALI). It is subject to change without notice and is only available to select clients.

The **Impression Funnel** is available in the **Troubleshooting** window. For more information, see [Troubleshoot Line Items](troubleshoot-line-items.md). You can use the Impression Funnel to:

- View impressions matched, bids, bid requests, auctions won, and impressions rendered to understand the line item’s health.
- Monitor associated rates to keep track of line item performance, including: bid request rate, bid rate, win rate, and render rate.
- Learn recommended seller actions to manually remedy line item issues as well as buyer actions to suggest directly to the buyer.

The Impression Funnel includes the following settings and metrics:

- **Buyers** - the buyers associated with the line item. Click the edit icon to change buyers. For more information, see [Set Up Multi-Buyer Deals](set-up-multi-buyer-deals.md).
  
  > [!NOTE]
  > Selecting a buyer filters the Impression Funnel issues and suggested actions to that specific buyer.

- **Scale** - select the most useful way to display the line item metrics to for your situation: **Linear** or **Logarithmic**.
- **Metrics** - the available line item metrics include:

  > [!NOTE]
  > You can select or deselect metrics to add or remove them from the bar graph for greater clarity.

  - **Imps Matched** - the count of available impressions matching the line item's targeting and buyer's acceptance status.
  - **Bids Requests** - the count of requests sent to the buyer with the deal included.
  - **Bids** - the count of deal auctions with a bid from the buyer. This metric represents the presence of a single bid per buyer, even if the buyer bids multiple times on the same auction.
  - **Auctions Won** - the count of bids that successfully won the Microsoft Advertising auction. This metric does not account for secondary auctions.
  - **Imps Rendered** - the count of successful creative renders on the deal.
- **Time** - use the **Time** drop-down to select the time frame in which to display the metrics. Choose from:
  - **10 Minutes**
  - **1 Hour**
  - **24 Hours**
- **Rates** - the following rates are displayed along with the number of **Issues and Actions** (if any). Select each rate to display a graphic of the results along with and a more detailed description of any issue and suggested seller and buyer actions:
  - **Bid Request Rate** - calculated by dividing Bid Requests by Imps Matched.
  - **Bid Rate** - calculated by dividing Bids by Bid Requests.
  - **Win Rate** - calculated by dividing Auctions Won by Bids
  - **Render Rate** - calculated by dividing Imps Rendered by Auctions Won.

## Related topics

- [Monitor Line Items](monitor-line-items.md)
- [Troubleshoot Line Items](troubleshoot-line-items.md)
