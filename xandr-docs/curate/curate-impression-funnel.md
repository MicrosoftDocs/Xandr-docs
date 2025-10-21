---
title: Microsoft Curate - Impression Funnel
description: In this article, explore detailed information about the Impression funnel and its various settings and metrics.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Impression funnel

The **Impression Funnel** provides detailed deal line item metric information in the form of graphs and charts. The **Impression Funnel** is available in the **Troubleshooting** window. For more information, see [Troubleshooting Line Items](curate-troubleshooting-line-items.md).

You can use the **Impression Funnel** to:

- View impressions matched, bids, bid requests, auctions won, and impressions rendered to understand the deal line item’s health.
- Monitor associated rates to keep track of deal line item performance, including: bid request rate, bid rate, win rate, and render rate.
- Learn recommended seller actions to manually remedy line item issues as well as buyer actions to suggest directly to the buyer.

The Impression Funnel includes the following settings and metrics:

- **Buyers** - The buyers associated with the line item. Select the **Edit** icon to change buyers.
  
  > [!NOTE]
  > Selecting a buyer filters the **Impression Funnel** issues and suggested actions to that specific buyer.

- **Scale** - The most useful way to display the line item metrics to for your situation: **Linear** or **Logarithmic**.
- **Metrics** - The available deal line item metrics that include:
  
  > [!NOTE]
  > You can select or deselect metrics to add or remove them from the bar graph for greater clarity.

  - **Imps Matched** - The count of available impressions matching the deal line item's targeting and buyer's acceptance status.
  - **Bids Requests** - The count of requests sent to the buyer with the deal included.
  - **Bids** - The count of deal auctions with a bid from the buyer. This metric represents the presence of a single bid per buyer, even if the buyer bids multiple times on the same auction.
  - **Auctions Won** - The count of bids that successfully won the Microsoft Advertising auction. This metric does not account for secondary auctions in the seller’s primary ad server.
  - **Imps Rendered** - The count of successful creative renders on the deal.
- **Time** - Use the **Time** drop-down to select the time frame in which to display the metrics. Choose from:
  - **10 Minutes**
  - **1 Hour**
  - **24 Hours**
- **Rates** - The following rates are displayed along with the number of **Issues and Actions** (if any). Select each rate to display a graphic of the results along with and a more detailed description of any issue and suggested seller and buyer actions:
  - **Bid Request Rate** - Calculated by dividing Bid Requests by Imps Matched.
  - **Bid Rate** - Calculated by dividing Bids by Bid Requests.
  - **Win Rate** - Calculated by dividing Auctions Won by Bids.
  - **Render Rate** - Calculated by dividing Imps Rendered by Auctions Won.

## Related topics

- [Monitor Line Items](monitor-line-items.md)
- [Troubleshooting Line Items](curate-troubleshooting-line-items.md)
