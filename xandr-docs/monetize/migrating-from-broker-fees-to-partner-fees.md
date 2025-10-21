---
title: Microsoft Monetize - Migrating from Broker Fees to Partner Fees
description: Learn the different ways Partner Fees works while migrating from Broker Fees. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Migrating from broker fees to partner fees

> [!IMPORTANT]
> Partner Fees are an enhancement and replacement for [Broker Fees](broker-fees.md) for augmented line items (ALIs) and programmatic guaranteed line items (PGLIs).
>
> If you're migrating from [Broker Fees](broker-fees.md), you'll find partner fees work differently in a few ways:
>
> - Partner fees apply only to augmented line items (ALIs) and guaranteed delivery line items (GDLIs).
> - Partner fees can be eligible for multiple advertisers and can be applied to multiple line items.
> - A particular partner fee can be made required or optional for all an advertiser's augmented line items.
> - Partner fees cannot be applied to insertion orders.
  
All serving fees on existing augmented line items have already been converted to partner fees. You can view them in the **Fees** section of the line item. If you have Network-level access, hover over your member name in the upper-right corner of the menu bar and click **Fees** to access the **Fees** screen.

## Reporting changes

With partner fees, several new metrics have been added to reports and there has been a standardization of how metrics are named and calculated across different reports. This resulted in the deprecation of some metrics and changes in the definitions of others.

Fields are now defined as follows for every report in which they appear:

- **Partner fees**: The total amount of third party costs, budgeted using Partner Fees, that have accrued on an augmented line item over the reported period of time.

- **Total cost**: All costs that are paid out to third parties. For buyers, total cost is all costs included in the budget, including media cost, data cost, partner fees, serving fees, and commissions. For sellers, total cost is any publisher revenue paid out to publishers, whether as revshare or CPM. Total costs are calculated as follows:
  - **Total cost**: media costs + data cost + partner fees + commissions + serving fees OR publisher revenue
  - **Total cost eCPM**: (total cost/imps) \* 1,000
  - **Total cost eCPC**: total cost/clicks
  - **Total cost eCPA**: total cost/conversions

- **Profit**: In the past, we have sometimes used "profit" to represent buyer profit and sometimes used it to represent Network profit. Going forward, it will always indicate buyer profit (booked revenue - total cost).

- **Network profit**: The sum of booked revenue and reseller revenue, minus total cost.

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
|--|--|--|
| Commissions | Commissions + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted | $0 for ALI, commissions for standard line item.<br>Previous data will not be impacted. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | (booked revenue - media cost) / imps * 1,000 | (booked revenue - total cost / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Serving Fees | Serving fees + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, serving fees for standard line item.<br>Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Buyer Geo Analytics Report](buyer-geo-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | (booked revenue - total cost) / imps * 1,000 | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Advertiser Analytics Report](advertiser-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Commissions | Commissions + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, commissions for standard line item.<br>Previous data will not be impacted. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md) , that have accrued on an augmented line item over the reported period of time. | Same |
| Profit | network revenue - network cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | (booked revenue - media cost / imps) * 1,000 | (booked revenue - total cost / imps) * 1,000 |
| Profit Margin | (network revenue - media cost) / network revenue | (booked revenue - total cost) / booked revenue |
| Revenue eCPA (net commissions) | (cost / conversions) - commissions | Deprecated. Returns error. |
| Revenue eCPM (net commissions) | ((cost / clicks) * 1,000) - commissions | Deprecated. Returns error. |
| Serving Fees | Serving fees + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, serving fees for standard line item.<br>Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |
| Total Revenue (net commissions) | total revenue - commissions | Deprecated. Returns error. |

[Advertiser Video Analytics Report](advertiser-video-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Commissions | Commissions + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, commissions for standard line item.<br>Previous data will not be impacted. |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | ((booked revenue - total cost) / imps) * 1,000 |
| Profit Margin | (booked revenue - media cost) / booked revenue | (booked revenue - total cost) / booked revenue |
| Serving Fees | Serving fees + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, serving fees for standard line item.<br>Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Network Analytics Report](network-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Commissions | Commissions + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, commissions for standard line item.<br>Previous data will not be impacted. |
| CPM including Fees | (cost / imps) * 1,000 | Deprecated.<br>Returns error. |
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| PPM | (profit / imps) * 1,000 | Deprecated.<br>Returns error. |
| PPM including Fees | (profit / imps) * 1,000 | Deprecated.<br>Returns error. |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit (net commissions/gross serving fees) | profit - (serving fees + commissions) | Deprecated.<br>Returns error. |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| RPM including Fees | ((revenue - fees) / imps) * 1,000 | Deprecated.<br>Returns error. |
| Serving Fees | Serving fees + equivalent partner fees<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | $0 for ALI, serving fees for standard line item.<br>Previous data will not be impacted. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue<br>**Note**: Third-party fees will not be double-counted in the partner fees field. | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Publisher Analytics](publisher-analytics.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network PPM | (total network RPM - total publisher RPM) | Deprecated.<br>Returns error. |
| Network Profit | network revenue - publisher revenue | (booked revenue + reseller revenue) - total cost |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| Network ROI | network ROI | Deprecated.<br>Returns error. |
| Partner Fees | The total amount of third-party costs, budgeted using [Partner Fees](partner-fees.md), that have accrued on an augmented line item over the reported period of time. | Same |
| Profit | booked revenue - total cost | Same |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Network Video Analytics Report](network-video-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | network profit per 1,000 impressions | Deprecated.<br>Returns error. |
| Profit | total network revenue - network cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Publisher Video Analytics Report](publisher-video-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network PPM | network RPM - publisher RPM | Deprecated.<br>Returns error. |
| Network Profit | network revenue - network media cost | (booked revenue + reseller revenue) - total cost |
| Network Profit eCPA | (booked revenue + reseller revenue) - total cost / conversions | Same |
| Network Profit eCPC | (booked revenue + reseller revenue) - total cost / clicks | Same |
| Network Profit eCPM | ((booked revenue + reseller revenue) - total cost imps) * 1,000 | Same |
| Network Profit Margin | (booked revenue + reseller revenue) - total cost/ booked revenue + reseller revenue | Same |
| Network ROI | network ROI | Deprecated.<br>Returns error. |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Seller Brand Review Report](seller-brand-review-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | ((network revenue - network media cost) / imps) * 1,000 | Deprecated.<br>Returns error. |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Creative Frequency and Recency Report](creative-frequency-and-recency-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | ((booked revenue - media cost) / imps) * 1,000 | Deprecated.<br>Returns error. |
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Network Site Domain Performance Report](network-site-domain-performance-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | ((booked revenue - total cost) / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Site Domain Performance](site-domain-performance.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Profit | booked revenue - media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - media cost) / imps) * 1,000 | (( booked revenue - total cost) / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Carrier Analytics Report](carrier-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | Same |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

[Device Analytics Report](device-analytics-report.md)

| Metric | During the Transition Period | After the Transition Period |
|--|--|--|
| Network Profit | (booked revenue + reseller revenue) - total cost | Same |
| Network Profit eCPA | network profit / conversions | Same |
| Network Profit eCPC | network profit / clicks | Same |
| Network Profit eCPM | (network profit / imps) * 1,000 | Same |
| Network Profit Margin | network profit / booked revenue + reseller revenue | Same |
| PPM | ((network revenue - network media cost) / imps) * 1,000 | Deprecated.<br>Returns error. |
| Profit | network revenue - network media cost | booked revenue - total cost |
| Profit eCPA | (booked revenue - total cost) / conversions | Same |
| Profit eCPC | (booked revenue - total cost) / clicks | Same |
| Profit eCPM | ((booked revenue - total cost) / imps) * 1,000 | (profit / imps) * 1,000 |
| Profit Margin | (booked revenue - total cost) / booked revenue | Same |
| Total Cost | Media cost + data costs + partner fees + commissions + serving fees + publisher revenue | Same |
| Total Cost eCPA | total cost / conversions | Same |
| Total Cost eCPC | total cost / clicks | Same |
| Total Cost eCPM | (total cost / imps) * 1,000 | Same |

## Standard line items

If you still use standard line items, you must use [Broker Fees](broker-fees.md) to administer third-party fees for those. You can still apply broker fees on the insertion order, line item, or campaign; however, if the insertion order has both standard and augmented line items, the broker fees **will only apply to the standard line items**. You must create partner fees for augmented line items even if the parent insertion order has a broker fee applied.

## Log-Level data

Partner fees are reported in the field `partner_fees` in the [Standard Feed](../log-level-data/standard-feed.md).
