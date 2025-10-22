---
title: Real Time Integrations (Contextual Data Providers)
description: In this article, explore step-by-step real time integration instructions about contextual data providers with a detailed set of examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Real time integrations (contextual data providers)

For contextual data providers, the data is directly related to the inventory. This requires that we make a real time request to the data provider for each impression in order to gain information about brand safety and categorization data based on the referrer URL. When the referrer URL is passed to us for the auction (either server-side by an inventory partner or in the HTTP header), we pass that along to the contextual data providers, who respond with categories (which we call "segments") corresponding to the page's categorization, e.g., "News".

Also, see [Real Time Data Integration Instructions](real-time-data-integration-instructions.md).

## Process

:::image type="content" source="media/real-time-integrations-contextual-data-providers.png" alt-text="Diagram of a Real Time Data Provider Integration.":::

1. An impression comes into the impression bus either via a placement tag on the page or a server-side call from a supply partner. The impression must have a referrer URL either in the HTTP header, as a querystring parameter or from the default_referrer_url of the placement if the domain/url visibility in set to "hidden".
1. User data is looked up in the server-side cookie store using the UID in the user's browser cookie as the key for the look up.
1. User data is returned by the server-side cookie store. This data is attached to the auction as segment data and free-form user data JSON.
1. If there is a referrer URL, a request is sent to the contextual data provider containing the referrer URL as a querystring parameter.
1. The data provider returns a line-return separated list of segment codes (see the code field on the Segment service) corresponding to the categorization(s) for the page. These categorizations are attached to the auction as segment data.
    1. If no categorizations can be mapped to the referrer URL, a blank response with a new line character should be returned.
1. Bid requests are sent to our UI as well as other DSPs and Bidders. The auction data contains the segments associated with a given data provider only if the bidder or a member associated with that bidder has access to those segments.

    > [!TIP]
    > **Real Time vs Behavioral Segments**
    >
    > An important distinction between real time (contextual) and behavioral segments is that real time segments returned by a Real Time Data Provider only exist for the life of the impression and do not affect user segment membership. Behavioral segments are associated with the user, and exist as long as the user is associated with that segment.

1. DSPs, and Bidders return a response for each auction (either a bid or an indication that they do not wish to participate).
1. Lastly, for auctions where Xandr is the final decision maker, the winning creative is returned to the user's browser. If the impression was received via a server-side call from a supply partner, the winning creative and bid is returned to that supply partner for participation in another auction.

## Technical details

When an impression comes into the impression bus, an HTTP `GET` request is sent to an available data provider instance with the macros appended to the `bid_uri` parameter configured on the [Bidder Service](../bidders/bidder-service.md). The data provider instance should respond with a list of segment codes (not segment IDs - only segment codes will be accepted), separated by a new line (\n). The current timeout interval for data provider requests is 10 milliseconds.

> [!TIP]
> For a complete list of Xandr macros that can be appended to your `bid_uri`, see Xandr [Macros for Data Providers](xandr-macros-for-data-providers.md).

## Example request and response

### Request

```
GET /data_provider/get_categories?url=http://www.mikeonads.com/2009/10/18/rtb-serving-speed/
```

### Response

```
brand_safety_safe
brand_safety_not_adserver
brand_safety_general_audience
cat_computers
cat_real_time_bidding
cat_technology
```

## Setup

Data providers with real-time integrations are implemented as 'bidders' even though they are not actually placing bids. They set up [bidder instances](../bidders/bidder-instance-service.md) in each data center and interact directly with the impression bus. Each data provider using this integration method must have a single member associated with their bidder, and the segments will be housed within the member. We will configure the member for you and suggest that you do not modify this without first consulting with your technical contact at Xandr.

Since the timeout period of 10 milliseconds is so short and because requests are received directly from the impression bus, it is necessary to register a bidder instance in each data center that you wish to see requests in.

## Other considerations

- The data provider phase lasts 10 milliseconds, meaning that all data providers must respond with some kind of categorization within 10 milliseconds or less.
- A data provider will only be called if it has an instance in operation in the same data center that processes the impression. For example, if an impression comes into the Amsterdam data center, and the data provider has instances in the New York and LA data centers, they will not receive a request for categorization.
- Given the required response time of 10ms or less, real time data providers should consider co-locating within data centers used by Xandr to reduce latency and ensure the response times are 10ms or less.
- Real Time Data Provider integration usually takes multiple months to complete. We encourage prospective data providers to take that into account before starting integration with Xandr.
- In order to manage instances and the requests received, the data provider may use the bidder, bidder instance, and profile services in the impressions bus API.
