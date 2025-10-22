---
title: Supply Stream Efficiency
description: In this article, explore information about Supply Stream Efficiency and its various key features.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Supply Stream Efficiency

This page provides details about the Supply Stream Efficiency feature, supported by the Microsoft Advertising platform.

## Overview

Programmatic bidders are increasingly focused on the efficiency of the traffic they receive from SSPs, prioritizing performance and high-quality inventory. Each bidder might have their own criteria for measuring efficiency, but common among them is the expectation that SSPs deliver traffic they are likely to buy and minimize unwanted traffic. To address this, our platform provides Supply Stream Efficiency, Microsoft Monetize's automatic traffic shaping solution for bidders.

## Key features

This section highlights the key features of the Supply Stream Efficiency system.

### Improved traffic shaping

The Supply Stream Efficiency system shapes all the traffic sent by Microsoft Monetize. This benefits any bidder conscious of SSP efficiency and actively managing QPS.

### Dual-level shaping

Microsoft Monetize's traffic shaping operates at two levels:

- **Supply Stream Efficiency**: Automatically discards low-scoring traffic, as determined by the bidder's bidding and buying history, across the full spectrum of supply for that bidder.
- **QPS Caps**: As a bidder approaches their QPS cap, Microsoft Monetize uses that bidder's buying history to intelligently filter out low-value traffic, ensuring that only the most valuable traffic is retained.

### Optimize bidder traffic

Supply Stream Efficiency leverages each bidder’s unique buying patterns to deliver the most relevant traffic, optimizing the flow of high-value traffic. This ensures that bidders receive a more targeted stream of valuable opportunities. New and low-scoring traffic is sent in controlled amounts, enabling bidders to explore new opportunities and begin buying inventory they may not have bought before. Bidders might notice a decrease in traffic volume, especially if they are not regularly hitting QPS caps, as low-scoring traffic will be actively filtered out. 

## Related topic

[Optimized Bid Stream FAQ](./optimized-bid-stream-faq.md)