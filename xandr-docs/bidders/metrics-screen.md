---
title: Metrics Screen
description: In this article, learn about the Metrics screen and gain a thorough understanding of its three main sections.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Metrics screen

Use the **Metrics** screen to monitor real time activity on your Xandr integration across all of our global data centers. Monitor the amount of traffic we send to your regional servers, or get data on bid rates and response times. Create your own graphs by selecting options in the three main sections of the metrics screen:

## Available metrics

### Bid requests

| Name | Definition |
|:---|:---|
| **Available** | Count of bid requests available for a bidder to bid on. Note that no bid requests have actually been sent when this is tallied, and only minimal filtering checks have been performed. |
| **Attempt** | Count of all bids requests sent to bidders in the auction prior to filtering logic and other checks being applied. |
| **Sent** | Count of valid bid requests actually sent to bidders after filtering logic has been applied. |
| **Profile filtered** | Count of bid requests that were not sent because they failed bidder profile filtering checks. |
| **Volume filtered** | Count of bid requests that the impbus throttled and did not send. Throttling is set via the `passthrough_percent` value in the profiles. |

### Bid responses

| Name | Definition |
|:---|:---|
| **Response received** | Count of valid bid responses the impbus received from the bidder. This metric is tallied after the response content is converted into JSON. If there is an error in the JSON parsing, this metric is not incremented. |
| **Partner impressions cleared** | Count of bids won on our SSPs. |
| **Platform impressions cleared** | Count of bids won on our Platform Inventory. |
| **Total impressions cleared** | Total count of bids won (from SSPs and Platform Inventory). |

### Notify requests

Notifications are set up by the bidder software that provide the results of an auction to bidders that have registered a notify URL. Notifications are JSON encoded responses that include information about the auction.

| Name | Definition |
|:---|:---|
| **Sent** | Total count of successfully sent notifies. |
| **Skipped**  | Count of notifies where the impbus did not send a notify request due to bidder configuration that turns off notifies, rather than because of an error. Notifies could be skipped because the bidder has them blocked, the bidder has not set a notify uri, or where the bidder has notifies explicitly turned off. |

### Pricing

Preemptive auctions occur when the impbus is participating in a third-party auction as a bidder. The impbus runs its own auction and passes the winning bid along to the third-party auction. The seller does not automatically display content for the winning bid because this winning bid is not guaranteed to win the final auction.

| Name | Definition |
|:---|:---|
| **Best bid price**<br>(platform) | Total amount of bids per number bids made, in USD for Platform inventory. |
| **Cleared price**<br>(platform) | Total amount of winning bids per total number of winning bids, in USD for Platform inventory. |
| **Best bid price**<br>(partner)* | Total best bid price averaged by count of best bids, in USD for SSP bids. |
| **Cleared bid price**<br>(partner)* | Average clear price for bids, in USD, that won the SSP auction. |

### Timing

| Name | Definition |
|:---|:---|
| **Avg response time** | Average response time per request, calculated by taking the sum of the response times reported for each bid and dividing them by the total valid responses received for each bid. |
| **Max response Time** | Maximum time to receive a bid response from a bidder in millils. |
| **Timeout %** | Percentage of bid requests the impbus sent that resulted in a timeout. |

### Other

| Name | Definition |
|:---|:---|
| **Client errors** | Total number of client errors. For a list of possible client errors, see the [Bid Error Codes](bid-error-codes.md) page. |
| **No connections** | Percent of bid requests sent that resulted in connection errors. Connection errors are indicated by the request status or by the request returning an HTTP status other than 200. Once this error is recorded, the impbus skips further bid processing steps and finishes processing that bid, recording the error. |
| **Mapped user imps** | Count of segment codes returned by data provider bidders. |

## Datacenter

Select the data center you would like to be included in the metrics graph:

| Name | Definition |
|:---|:---|
| **All** | Data from all global data centers will be included. |
| **New York** | US East coast data center. |
| **Los Angeles** | US West coast data center. |
| **Amsterdam** | Western Europe Data center. |
| **Singapore** | Asia and Australia Data Center. |
| **Frankfurt** | Eastern Europe Data Center. |

## Date range

Select the date range and time for the data to be displayed in the metrics graph. There are options to select both the date and the time.
