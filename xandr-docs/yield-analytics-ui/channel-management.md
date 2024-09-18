---
title: Channel Management
description: Leverage Channel Management. Extract data, map via product-based approach. Dashboard, comparisons, detailed Channel Metrics for analysis.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Channel management

Channel Management uses a product-based approach to gather data. This data is extracted to create a mapping document. Explicit product mappings ensure that the reports are returning data to meet your specific needs. Thus, information is being directly ported into the system, as opposed to a crude distribution of how revenue is allocated to products.

## Dashboard

The Channels Dashboard gives you a quick overview of the breakdown and performance of your channels. It also allows you to compare the performance of these channels.

> [!TIP]
> The Channels Dashboard represents SSP data only. It does not include data from direct sales.

## Channel breakdown

The Channel Breakdown shows a visual pie-chart of your channels.  It can be **By Revenue** or **By Impressions**.

> [!TIP]
> This pie represents the percentages of your SSP channels. It does not represent your full revenue stack.

You also have the ability to change the date ranges by selecting **Last Week**.

## Channel comparison

The Channels Comparison compares channels over a period of time. It can be By eCPM, By Revenue, or **By Impressions**.

## Channel performance

You can view the performance of your channels either **By Advertiser** or **By Product**. This allows you to evaluate the performance of one SSP verses another, for a specific advertiser.

> [!TIP]
> When you select By Product, everything is going to map to a Total Network product by default.

Channel performance uses data from:

- Channel Advertiser - The advertisers Yield Analytics receives through your SSP integrations (if applicable).

> [!TIP]
> We do not always receive the advertiser information. (Just adding this as a reminder).

Channel - The SSP that the channel is associated with.

- Channel Consumed Impressions - This is how many impressions they are consuming.
- Channel Earned Revenue - This is how much revenue the channel is earning.
- Channel eCPM - This shows the eCPM (Effective Cost-Per-Thousand) for the channel.

## View all

Select **View All** to access the **Reports** screen.

## Reports

The Reports screen allows you to evaluate and analyze the data that we have access to. Essentially, this is the data we give you for your SSP reporting. You have the ability to filter, sort, and add additional filters. Within the configuration are filters and dimensions related to channels.

The Analyzer functionality is also available on this page.

> [!TIP]
> There are specific filters related to each SSP integration. Yield Analytics will work with the data that you allow us to access and evaluate.

## Product/Customer dimensions related to channels

There are two specific metrics that relate to channel management:

- Under Product Dimensions > Channel
- Under Customer Dimensions > Channel Advertiser

## Channel metrics

There are also specific metrics for Channel Management, and they are all pre-fixed by the word Channel.

> [!TIP]
> All reporting is product-based. These metrics apply only to product and target, and not to order-lines dimensions.

Here are the definitions of the metrics in Channel Reporting:

| Metric | Definition |
|---|---|
| Channel Received Impressions | The number of impressions that the channel received, as recorded by the channel. (Capacity Impressions for non-SSP products/targets)<br>Basically, received impressions are the impressions that the ad server has made available to the SSP. The ad server has given the SSP the ability to make a request. |
| Channel Consumed Impressions | The number of impressions that were filled or consumed by the channel. |
| Channel Consumed Clicks | The number of clicks consumed or delivered by the channel. |
| Channel Earned Revenue | The total revenue earned by the channel. |
| Channel CTR % | The Click Through Ratio percent metric based on the preceding Channel Consumed Impressions and Clicks. |
| Channel eCPM | The computed eCPM (Effective Cost-Per-Thousand) for the channel. |
| Channel rCPM | Channel `real` CPM using the Channel Received Impressions instead of the Channel Consumed Impressions. |
| Channel Fill % | Utilization rate of the channel (Sell Through % for non-SSP products/targets. Consider the fact that only guaranteed consumed impressions are taken into account). |

## Best practices to switch to a product-based system

Channel Management is currently based on order lines. With the addition of Pre-Bid, we are now basing it on explicit product mappings. The following changes must be made:

- Product overlaps were applied based on overlaps that exist elsewhere in the system. Thus, they are less accurate than desired.
- With the explicit product mappings we can ensure that the reports are returning data to meet your specific needs
- Order line based reporting will be deprecated. (This is why you see duplicate metrics at the moment. One is an order line metric, and one is a product metric).

When Yield Analytics integrates a client, the following general steps are taken:

1. The clients pick which SSPs they want to integrate with.
1. Yield Analytics sets up an integration with the API for that SSP.
1. We pull in the appropriate ad server data.
1. We map that data back to the revenue that comes out of the SSP API.
1. We then apply it together in the Channels Dashboard. This gives you insight into your SSP Management.

Now that we are mapping to products, the Channels Dashboard allows you to evaluate how your revenue compares on a product-by-product basis. (Including or not including SSP data).

> [!TIP]
> We are happy to show whatever data the publisher deems valuable. By sharing details at a product level, or matching product mappings - it helps us to better work with the publisher to expose that data.

## Related topic

[Working with Channel Metrics](working-with-channel-metrics.md)
