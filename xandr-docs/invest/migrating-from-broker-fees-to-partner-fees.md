---
title: Microsoft Invest - Migrate from Broker Fees to Partner Fees
description: In this article, learn how to migrate from broker fees to partner fees, including reporting changes, transition periods, and affected reports.
ms.date: 10/28/2023
---

# Microsoft Invest - Migrate from broker fees to partner fees

> [!IMPORTANT]
> Partner Fees are an enhancement and replacement for [Broker Fees](broker-fees.md) for augmented line items (ALIs) and programmatic guaranteed line items (PGLIs).

If you're migrating from [Broker Fees](broker-fees.md), you'll find partner fees work differently in a few ways:

- Partner fees can be eligible for multiple advertisers and can be applied to multiple line items.
- A particular partner fee can be made required or optional for all an advertiser's augmented line items.
- Partner fees cannot be applied to insertion orders.

All serving fees on existing augmented line items have already been converted to partner fees. You can view them in the **Fees** section of the line item. If you have Member-level access, hover over your member name in the upper-right corner of the menu bar and click **Fees** to access the **Fees** screen.

## Changes in reports

With partner fees, several new metrics have been added to reports and there has been a standardization of how metrics are named and calculated across different reports. This resulted in the deprecation of some metrics and changes in the definitions of others.

Fields are now defined as follows for every report in which they appear:

- **Partner fees**: The total amount of third party costs, budgeted using Partner Fees, that have accrued on an augmented line item over the reported period of time.

- **Total cost**: All costs that are paid out to third parties. For buyers, total cost is all costs included in the budget, including media cost, data cost, partner fees, serving fees, and commissions. Total costs are calculated as follows:
  - **Total cost**: media costs + data cost + partner fees + commissions + serving fees OR publisher revenue
  - **Total cost eCPM**: (total cost/imps) * 1,000
  - **Total cost eCPC**: total cost/clicks
  - **Total cost eCPA**: total cost/conversions

- **Profit**: In the past, we have sometimes used "profit" to represent buyer profit and sometimes used it to represent Member profit. Going forward, it will always indicate buyer profit (booked revenue - total cost).

- **Member profit**: The sum of booked revenue and reseller revenue, minus total cost.

    Profit metrics based on including broker fees or data cost, but not including media cost, will be retired, in favor of the new definition of profit based on total cost. You will still be able to determine separate media and data costs.

## Transition period

The transition to partner fees was completed **November 12, 2019**. For reports and metrics related to ALIs prior to that date, some things to keep in mind:

- Reports which already had profit fields will continue to use the definitions they had used in the past.
- Logic was added to prevent double-counting third party costs (partner fees vs commissions & serving fees) in total cost metrics for ALIs.
- Commissions are no longer populated for augmented line items. These fees appear in the **partner fees** field.

## Affected reports

The changes for each report are summarized in the tables below.

[Buyer Segment Performance Report](buyer-segment-performance-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| Commissions | Commissions + equivalent partner fees<br> **Note:** Third-party fees will not be double-counted | $0.<br> Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br> **Note:** Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPM | (booked revenue - media cost) / imps * 1,000 | (booked revenue - total cost / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |

[Buyer Geo Analytics Report](buyer-geo-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPM | (booked revenue - total cost) / imps * 1,000 | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |

[Advertiser Analytics Report](advertiser-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| Commissions | Commissions + equivalent partner fees<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | $0.<br> Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | network revenue - network cost | booked revenue - total cost |
| Profit eCPM | (booked revenue - media cost / imps) * 1,000 | (booked revenue - total cost / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (network revenue - media cost) / network revenue | (booked revenue - total cost) / booked revenue |
| Total Revenue (net commissions) | total revenue - commissions | Deprecated. Returns error. |
| Revenue eCPM (net commissions) | ((cost / clicks) * 1,000) - commissions | Deprecated. Returns error. |
| Revenue eCPA (net commissions) | (cost / conversions) - commissions | Deprecated. Returns error. |

[Advertiser Video Analytics Report](advertiser-video-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Commissions | Commissions + equivalent partner fees<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | $0.<br>Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | ((booked revenue - total cost) / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - media cost) / booked revenue | (booked revenue - total cost) / booked revenue |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |

[Member Analytics Report](network-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| Commissions | Commissions + equivalent partner fees<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | $0.<br> Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br><br> **Note:** Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| RPM including Fees | ((revenue - fees) / imps) * 1,000 | Deprecated.<br>Returns error. |
| Profit (net commissions/gross serving fees) | profit - (serving fees + commissions) | Deprecated.<br>Returns error. |
| PPM including Fees | (profit / imps) * 1,000 | Deprecated.<br>Returns error. |
| CPM including Fees | (cost / imps) * 1,000 | Deprecated.<br>Returns error. |
| PPM | (profit / imps) * 1,000 | Deprecated.<br>Returns error. |

[Member Video Analytics Report](network-video-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | total network revenue - network cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | network profit per 1,000 impressions | Deprecated.<br>Returns error. |

[Creative Frequency and Recency Report](creative-frequency-and-recency-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | ((booked revenue - media cost) / imps) * 1,000 | Deprecated.<br>Returns error. |

[Member Site Domain Performance Report](network-site-domain-performance-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | ((booked revenue - total cost) / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |

[Site Domain Performance](site-domain-performance.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | (( booked revenue - total cost) / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |

[Carrier Analytics Report](carrier-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |

[Device Analytics Report](device-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|:---|:---|:---|
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | ((network revenue - network media cost) / imps) * 1,000 | Deprecated.<br>Returns error. |

## Log-level data

Partner fees are reported in the field `partner_fees` in the [Standard Feed](../log-level-data/standard-feed.md).
