---
title: Optimized Bid Stream FAQ
description: In this article, explore answers to frequently asked questions (FAQs) about optimized bid stream.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Optimized Bid Stream FAQ

The Optimized Bid Stream is an adaptive bid stream sent to a bidder. The goal of this optimization is to tailor the bid stream before it is sent to you (as the bidder), so you only see inventory that you're interested in buying.

## How does Xandr determine which inventory to send?

The inventory sent to you is determined by your buying behavior.

## What if an inventory I don't bid on today becomes something I want to bid on tomorrow?

We pass on a sample percentage of requests for learning purpose. This provides a feedback loop that ensures a change in inventory that becomes relevant to you is taken into consideration going forward.

## Is my bidder profile taken into consideration?

Optimized Bid Stream does not negate profile filtering.

## How do I know if I'm getting Optimized Bid Stream?

You should have received a communication from Xandr if you're getting an Optimized Bid Stream. If you haven't received any communication but you're interested in Optimized Bid Stream, reach out to your Xandr representative to learn more.

## How can I increase my incoming QPS (queries per second)?

Increasing spend will expand the inventory that matches the key selection.

## Why did my QPS drop after Optimized Bid Stream was enabled?

With Optimized Bid Stream, you receive more bid requests for inventory you've been more likely to buy and fewer requests for inventory you've been less likely to buy. If you do not buy a segment of inventory, then we don't have information about your buying behavior on that inventory. In order to increase the QPS, you will have to start buying the inventory you're interested in.

## What changes have been made to the Optimized Bid Stream?

On September 5, 2018, we updated our OBS algorithm. Traffic will be maximized to meet your QPS cap. Low priority traffic that exceeds your QPS cap will not be sent. You may see an uptick in incoming traffic; however, your QPS cap will always be respected.

## What should I do if I have feedback or more questions on Optimized Bid Stream?

Optimized Bid Stream is an Alpha product still under development. Reach out to your Xandr representative to share your feedback with us or to learn more about Optimized Bid Stream.
