---
title: QPS FAQ
description: In this article, find information about QPS and how the final bid request traffic is calculated..
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# QPS FAQ

## Summary

QPS is defined as queries per second. For external bidders, QPS is used to describe the total number of bid requests that can be sent per second. The implementation of QPS is accomplished via the field `qps_limit`, on the `bidder_instance` object. This allows the external bidder to set a maximum traffic to be sent to per datacenter.

## Details

The purpose of QPS for external bidders is to ensure the bidder's servers do not receive more traffic than they can process. It is not meant to be the optimal amount of traffic. The bidder can receive traffic lower than the `qps_limit` value, based on the available inventory, how the bidder's profiles are configured, and their bidder's performance. For example, here's a bidder instance configuration:

```
{"id": 12345,
"active": true,
"datacenter_id": 6,
"port": 80,
"hostname": "dsp.goodstuff.com",
"qps_limit": 1000}
```

This instance is configured to receive a maximum of 1000 bid requests per second.

Let's look at the available traffic for this bidder:

**Figure 1**

:::image type="content" source="media/qps-faq-figure-a.png" alt-text="A graph of the traffic fluctuations of the Bid Requests available for a particular bidder.":::

Here's what's sent to this bidder:

**Figure 2**

:::image type="content" source="media/qps-faq-figure-b.png" alt-text="A graph of the traffic fluctuations of the Bid Requests sent to a particular bidder.":::

As the available inventory fluctuates (due to normal human web browsing behavior), the bid requests sent to the bidder will also fluctuate in a similar manner. Since this bidder has set the `qps_limit` value to 1000, the traffic is being limited to that value and this is reflected in Figure 2.

## Traffic calculation

Figure 1 shows the traffic fluctuates from a low of 50k to a high of 175k. Figure 2 shows the bidder has received from a low of 400 to a high of 1000 (the `qps_limit` value).

## How is this calculated

There are 7 key metrics used in determining the final bid requests sent. The following two tables detail these metrics and how they are utilized.

**Table 1**

| Bidder UI Metrics | Description |
|---|---|
| Bid requests - Attempt | Number of attempts to make a single bid request. |
| Bid requests - Available | Number of auctions that are available to a bidder, whether or not that bidder filters them |
| Bid requests - Profile filtered | Number of auctions that a bidder's profile filtered out |
| Bid requests - Sent | Number of attempts that a bid request succeeded to send |
| Bid requests - Volume filtered | Number of auctions that didn't send a bid request because of throttling |
| Other - Connection error pct | Percent of bid_requests that were aborted due to an inability to connect to the bidder. |
| Timing - Timeout % | Percent of bid_requests that timed out |

**Table 2**

| Metrics | When is it counted? |
|---|---|
| Bid requests - Attempt | After all filtering but before QPS filtering |
| Bid requests - Available | After sell-side filtering before bidder profiles applied |
| Bid requests - Profile filtered | After sell-side filtering and after bidder profiles excluded the auction |
| Bid requests - Sent | Once we've successfully sent the request to the bidder. |
| Bid requests - Volume filtered | After a bidder is eligible and its profiles include the auction, but the profiles have throttling set (passthrough_percent field) |
| Other - Connection error pct | Bidder is eligible to bid and fails to respond to a bid request because a connection could not be established. |
| Timing - Timeout % | Bidder is eligible to bid and fails to respond within the time limit |

Before calculating the Bid requests - Sent value, it is worth reviewing how we determine what bid requests are available.

Sellers have controls that can limit which bidders can receive traffic. When a seller blocks the buyer members of a bidder in the Ad Quality Rules, that bidder will not receive bid requests from that seller. Sellers can also use a visibility profile to block bid requests from being sent to a bidder.

The Timing – Timeout % metric consists of three components:

1. The bidder has sent a bid response, but the bid response was not received in time to be eligible for the auction.
1. The bidder has not sent a bid response to the auction.
1. The bidder has sent a bid response and is eligible for the auction, however, the bid response came in towards the end of the maximum allowed time. There are bid requests that have been waiting to be sent that will be timed out, since the adserver has determined the bidder cannot respond in time.

Here is an example of a bid request that was timed out on a given connection since only one bid request can be sent on a given connection at a time (using a default maximum allowed time of 100ms):

- Time 0ms: bid request 1 sent to your bidder
- Time 1ms: bid request 2 queued
- Time 1.5ms: bid request 3 queued
- Time 99ms: bid response 1 received
- Time 100ms: bid request 2 sent
- Time 102ms: bid request 3 timed out before the request was sent
