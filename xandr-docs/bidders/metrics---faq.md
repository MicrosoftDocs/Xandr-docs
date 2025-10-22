---
title: Metrics - FAQ
description: In this article, explore answers to frequently asked questions about the metrics, their availability, and other related topics.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Metrics - FAQ

## Metrics availability

### Where can I find metrics on my bidder's performance?

Metrics are available for your bidder as part of the [bidder UI](https://bidder.xandr.com/). Use your bidder authentication credentials to access the UI.

## What do the following metrics mean?

### Bid requests available

This is the total number of requests that come into Xandr's platform. It is not the number of requests that meet your particular profile; it is all of the requests that, if you have no profile, you would be eligible to receive.

### Bid requests sent

This is not actually the number of requests that are sent to your bidder. It is the number of number of requests that are actually sent to your bidder minus the number of aborted bids. The following shows an example of an aborted bid on a given connection - since only one bid request can be out on a given connection at a time:

Time 0 ms: bid request 1 sent to your bidder

Time 1 ms: bid request 2 queued

Time 1.5 ms: bid request 3 queued

Time 99: bid response 1 received

Time 100: bid request 2 sent

Time 102: bid request 3 aborted because it timed out before the request was sent.

## Accessing the raw data for Metrics

For each graph in the Metrics section, you can download a text file with the raw data.

On the upper right corner of each graph, there is a button called 'Export Raw Data'. When this button is clicked, you will be prompted to save a file. This file will contain all the data points in the graph.

For example:

Bid requests - Available,1333306500,1333392900,300 | \[lots of data here\]

The format of the text file follows the below layout:

| **Selected Metric** | **Start time** | **End time** | **Time between data points (in seconds)** | **Data points** |

> [!NOTE]
> The Start and End times are in Unix time stamps.

## Related topic

[Bidder UI Metrics (for Data Providers)](metrics-screen.md)
