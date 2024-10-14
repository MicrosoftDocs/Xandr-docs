---
title: Yield Analytics UI Glossary
description: In this article, explore the glossary containing definitions of frequently used terms throughout the application.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Yield Analytics UI Glossary

The following glossary provides definitions of commonly used terms across the application. Click a letter to skip to its section.

## A

### Adjustment type

Determines types of changes that can affect forecasting for a product.

- Direct Seasonal – Product is a seasonal product.
- Indirect Seasonal – Product is influenced by a seasonal product (parent or child of the seasonal product).
- Direct Manual – Product has a manual adjustment.
- Indirect Manual – Product is influenced by a product that has a manual adjustment (parent or child of the manually adjusted product).

### Attribute

See Target attribute/Targeting characteristics.

### Available impressions

The available impressions for a target. Also referred to as availability.

Formula: Impression capacity – Consumed impressions

> [!NOTE]
> This is a dynamic calculation. The set of consuming order lines can be filtered, which will affect the availability accordingly.

### Available revenue (@ Rate card)

A measure of the revenue that remains to be "captured" for a product based on the available impressions, and rate card value of the product.

Formula: \[(Impression capacity - Consumed impressions) / 1000 x Rate card value of the target\] – Earned revenue of "unconsumed" impressions

> [!NOTE]
> This is a dynamic calculation. The set of consuming order lines can be filtered, which will affect the utilization accordingly.

### Average frequency (daily)

Average number of times a user was exposed to a defined set of inventory per day.

Formula: Average (Total Views per day / Total Uniques per day)

### Average uniques (daily) when report is run with order line dimensions

Average of the daily order line weighted unique counts for the Order Line's lifetime.

Formula: Sum (Order Line Consumption / Product Capacity) \* Total uniques) / Total number of days

### Average uniques (daily) when report is run with product dimensions

Average of the per-day unique counts for the time period selected.

Formula: Total uniques per day / Total number of days

## C

### Capacity

Maximum impressions that can be delivered by an order line.

### Channel consumed impressions

The number of impressions that were filled or consumed by the channel. In the case of secondary channels, this is the impressions filled by the channel.

### Channel received impressions

The number of impressions that the channel received as recorded by the channel. In the case of the Direct Sales channel, the Channel Received Impressions will equal Capacity Impressions.

### Channel earned revenue

The total revenue earned by the channel.

### Channel eCPM

The computed eCPM for the channel.

Formula: Channel Earned Revenue / (Channel Consumed Impressions/1000)

### Channel rCPM

Channel "real" CPM. This is a measure of how well a channel is monetizing the opportunity that it is presented with. It is useful for comparing the value brought by various partners. rCPM uses the "Channel Received Impressions" instead of Channel Consumed Impressions when determining value.

Formula: Channel Earned Revenue / (Channel Received Impressions/1000)

### Channel fill %

A measure of the utilization rate of the channel. In the case of the Direct Sales Channel, the Channel Fill % will equal the Sell Through % (calculated based on the consumed impressions associated to the Direct channel).

Formula: Channel Consumed Impressions/Channel Received Impressions \* 100

### Click pacing

A measure of the total clicks scheduled in the ad server for CPC order lines subtracted from the number of clicks - that have either delivered in the past or are forecast to deliver in the future - based on the date range selected in Yield Analytics. This value can be positive or negative with over- or under-delivery. This metric is available for order line and product dimensions.

Formula: Consumed clicks - Scheduled clicks

### Click pacing (lifetime)

A measure of the total clicks scheduled in the ad server for CPC order lines subtracted from the number of clicks delivered and forecasted for a CPC order line, based on the entire lifetime of the order line. This value can be positive or negative with over-or under-delivery. This metric is available only for order line dimensions.

Formula: Consumed clicks (Lifetime) - Scheduled clicks (Lifetime)

### Close date

Date on which the order/deal was closed.

### Consumed value (@ Rate card)

A measure of the monetary value of the consumed impressions based on the rate card value of the product.

Formula: Consumed impressions / 1000 x Rate card value of the product

### Consumption

Impressions consumed for an order line.

### Consumption date

Date of consumption for the order line (i.e., date on which the order line is scheduled to consume impressions from inventory).

### Consumed clicks

A measure of clicks that have either delivered in the past or are forecast to deliver in the future.

### Consumed clicks (3rd party)

The number of clicks that have been consumed in the past, as measured by the associated third party. Currently, no future consumption is forecast.

### Consumed clicks (lifetime)

The number of clicks that have been delivered and forecasted for a CPC order line. This metric is available only for order line dimensions.

### Consumed impressions

The number of impressions that have been consumed in the past - or are forecast to be consumed in the future.

### Consumed impressions (3rd party)

The number of impressions that have been consumed in the past, as measured by the associated third party. Currently, no future consumption is forecast.

### Consumption type

Describes the way inventory is being consumed by the order lines flighting on that inventory. The consumption-type relationship is always defined in the context of a specific order line, to a specific inventory product (also called focus product):

- Direct – Indicates order lines that have been targeted to exactly the same targeting attributes as the focus product.
- Contained – Indicates order lines that have been targeted to a set of attributes that are entirely contained within the focus product.
- Indirect – Indicates order lines that have been targeted to a set of attributes that partially overlap with the focus product.

For example, if you have three products that overlap in the following ways:

:::image type="content" source="media/hh.png" alt-text="Diagram of the three products.":::

And three order lines that are targeted as follows:

- "Nike" order line targeted to Section=Sports.
- "Champion" order line targeted to Section=Football.
- "Times" order line targeted to Geo=New York.

Then the consumption types for the order lines can be represented as follows:

- Direct – The Nike order line is "direct" to the Sports product, since it is directly targeted to the Sports product.
- Contained – The Champion order line is "contained" to the Sports product, since it is directly targeted to the Football section which is entirely contained within the Sports section.
- Indirect – The Times order line is "indirect" to the Sports product, since it is directly targeted to Geo=New York. This partially overlaps with the Sports section.

### Consumption-to-schedule percentage

A measure of pacing per schedule. For future time periods, this number takes into account the expected consumption based on the allocation forecast. Guaranteed order lines with pricing types CPM, CPD, and CPC are subject to this calculation.

C:S % is event agnostic, meaning that clicks and impressions are used interchangeably, determined by order line pricing type.

Formula: (Consumed events / Scheduled events) x 100

C:S % is calculated for CPM campaigns in the following way:

Formula: (Consumed impressions / Scheduled impressions) x 100

This metric is also calculated for cost-per-click (CPC) order lines:

Formula: (Delivered clicks / Scheduled clicks) x 100

### Consumption-to-schedule percentage (lifetime)

This is the same as the Consumption-to-schedule percentage metric, except that this metric aggregates over the lifetime of all order lines and is not bound by the time period. When the lifetime metric is used, the time period filter is only used to filter to order lines delivering in the selected time period.

This metric is only available for order line dimensions.

Formula: (Consumed events / Scheduled events) x 100

### Contract type

Contract type or ad type per the ad server (Example: standard, exclusive, sponsorship, weight-based, etc.).

### Contracted clicks

The number of clicks contractually obligated for a CPC order line based on the date range selected in Yield Analytics. This metric is available for order line and product dimensions.

### Contracted clicks (lifetime)

The number of clicks contractually obligated for a CPC order line, based on the entire lifetime of the order line. This metric is available only for order line dimensions.

### Contracted CPD

Contracted CPD rate for the order line. When aggregated as a metric, this is the weighted average of the Contracted CPD for the selected order lines.

Metric formula: Contracted revenue / Number of days in the campaign

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Contracted CPM

Contracted CPM rate for the order line.

When aggregated as a metric, this is the weighted average of the Contracted CPM for the selected order lines.

Metric formula: Contracted revenue / Contracted impressions x 1000

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Contracted impressions

The total contracted impressions per the order management system, prorated evenly over time. Order lines that do not have an impression goal (Example: sponsorships) will not have contracted impressions.

> [!NOTE]
> Proposed order lines are not included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Contracted impressions (lifetime)

This is the same as the Contracted impressions metric. The exception is that this metric aggregates over the lifetime of all order lines, and is not bound by the time period. When the lifetime metric is used, the time period filter is only used to filter to order lines contracted in the selected time period. This metric is only available for order line dimensions.

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Contracted revenue

The total contracted revenue per the order management system prorated evenly over time.

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Contracted revenue (lifetime)

This is the same as the Contracted revenue metric. The exception is that this metric aggregates over the lifetime of all order lines and is not bound by time period. When the lifetime metric is used, the time period filter is only used to filter to order lines contracted in the selected time period. This metric is only available for order line dimensions.

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### CTR %

Click-through rate percentage. This is a measure of the click frequency for ads.

Formula: Delivered clicks / Consumed impressions x 100

### CTR (3rd party)

Click-through rate percentage. This is a measure of click frequency as measured using third party data.

Formula: Consumed clicks (3rd party) x 100 / Consumed impressions (3rd
party)

## D

### Days to delivery

A measure of the amount of time that has elapsed between the close of the deal and the delivery of its order lines. This metric is useful for performing booking curve analysis.

Formula: Consumption date – Close date

### Delivered clicks

No longer in use. See Consumed clicks.

### Delivery system

Indicates the actual ad serving system. This is the delivery system in which the order is currently delivering or will eventually deliver. This should only contain actual ad serving systems like DFP, OAS, Freewheel, etc.

### Dimensions

Dimensions describe the data about your customers, orders, products, or sales teams. For example: Advertiser, Order, Product, and Salesperson are all dimensions. Dimensions are used for primary analysis and filtering data.

The following types of dimensions exist:

- Order line dimensions – Refer to either the order line itself or its attributes. For example: Order, Salesperson, or Advertiser.
- Product dimensions – Refer to either the inventory product itself or its attributes. For example, Product Group.

Order line and product dimensions have different behaviors in terms of the analysis that can be performed. For example: Certain metrics such as Available Impressions and Impression Capacity are only relevant for inventory Products. They do not make sense in the case of order line dimensions, such as Advertiser or Salesperson.

Because overlapping inventory will result in double counting, certain Product dimensions cannot be used as the primary analysis dimension (For example, Product Group), but can be used as filters.

### Direct target attribute

An attribute that is directly targeted by an order line.

> [!NOTE]
> When applying a Direct Target Attribute metric filter, it will not filter based on the order line's current targeting expression. Rather, it will provide data for your selected reporting dimension, based on consumption to a target that contains the Direct Target Attribute filter. For example: If you have an order line that is currently targeting "country=canada" and it just started targeting that attribute value yesterday - when running a report for the last 30 days and filtering your report to this direct target attribute, only yesterday's data will be included in the report.

### Discount %

A measure of the discount offered relative to the order line's "list" price.

When dimensioning by product, the metric accounts for the difference between the contracted rate of order lines allocating to the product - versus the rate card value of the product.

When dimensioning by order line, the metric reflects the difference between the contracted rate of the order line versus the rate card value of the order line's Sold As product. This metric is capped so it will not reflect premiums (i.e., negative discount).

Formula: 1 − (Contracted rate/Rate card CPM)

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Discrepancy % (3rd party)

The difference in the impression consumption as reported by the local ad server and the third party ad server.

## E

### Earned revenue

A measure of the monetary value earned or expected to be earned in the future, taking into account underdelivery. Earned Revenue is capped over the lifetime of the order line, so that it does not ever exceed the Contracted Revenue.

Formula for CPC order lines: Consumed clicks x Contracted CPC

Formula for CPD order lines: Number of days in the campaign with Consumed impressions \> 0 x Contracted CPD

Formula for CPM order lines: Consumed impressions / 1000 x Contracted CPM

### eCPM

Effective cost per mille, a measure of the effectiveness of the inventory being sold.

Formula: Earned revenue / Consumed impressions x 1000

### Effective discount % (@ Rate card)

A measure of the percent of a product's value not captured due to discounting.

> [!NOTE]
> Effective Discount % is different from Sales Discount % in that it uses the product's rate card value versus the order line's rate card value. Premiums (i.e., sale at a value higher than rate card) are not displayed.

Formula: 1 – \[Earned revenue / Consumed value (@Rate card) x 100\]

### Effective discount value (@ Rate card)

A measure of the total value not captured due to discounting relative to the product's rate card value. Premiums (i.e., sale at a value higher than rate card) are not displayed.

Formula: Consumed value (@Rate card) – Earned revenue

## I

### Impression capacity

The total inventory projected in the future or realized historically for the product.

### Industry

Name of industry that is mapped to the advertiser for an order line.

### Inventory class

Indicates whether an order line is sold as guaranteed or pre-emptible, based on the business rules defined for guaranteed versus pre-emptible.

## M

### Metrics

Metrics represent the quantifiable aspects of your business that you want to measure and track. For example, Earned Revenue and eCPM are metrics that you may want to track over time. Metrics can be aggregated for dimensions. For example, Earned Revenue can be aggregated by Advertiser, Salesperson, or Target.

Certain metrics are considered "dynamic" metrics. These include:

- Available impressions
- Available revenue (@Rate card)
- Utilization %
- Yield %

For dynamic metrics, you can control the definition of the metric by using the metric filters to define what is being considered "consumed." For example: To determine what inventory is available at a priority greater than 10, the priority metric filter should be set for the range of 1-10 so that all order lines within the range are considered "consumed", and therefore not available.

## N

### Network status

Indicates whether Yield Analytics processes log files to analyze the underlying impression details for a product:

- Analyzed Network – Indicates products (or associated order lines) for which Yield Analytics receives and processes impression-level log files.
- Non-analyzed Network – Indicates products (or associated order lines) for which Yield Analytics does not receive and process impression-level log files.

## O

### Order

Name of the order associated with an order line.

### Order external ID or Order ID

The unique identifier of the order from the order management system or ad server.

### Order line

Name of the order line.

### Order line external ID or Order line ID

The unique identifier of the order line from the order management system or ad server.

### Order line "Sold As" product

Name of the product from the product catalog that is associated with an order line. This represents the product that has been sold, which may be different from how the order line has been trafficked.

### Order line status

The state of an order line, which determines whether inventory can be allocated to the line, and whether it contributes to earned revenue.

### Order line target

The target against which the order line is directly trafficked in the ad server.

### Order line target expression

The combination of attribute/value pairs that uniquely describes the order line target.

### Order line target external ID

The unique identifier of the order line "Trafficked As" target from the order management system, or other externally managed product catalog.

### Order line target Yield Analytics ID

The unique identifier for the order line target in Yield Analytics.

### Origin system

Indicates the original source of the data. This is the system where the order was first input such as DSM, Operative, Salesforce etc.

### Overbooked impressions

A measure of unmet demand for a product. This metric should be used to identify "hotspot" areas in your network where demand exceeds supply. For example: Assume your entire network consists of two sections, Sports, and News - with the capacities as listed below. If a user books 600 K to Sports, then the Scheduled and Overbooked impressions will roll-up as follows:

| Hotspot areas  | Capacity | Scheduled impressions | Overbooked impressions |
|:---|:---|:---|:---|
| ROS | 1,000,000 | 600,000 | 0 |
| Sports | 500,000 | 600,000 | 100,000 |
| News | 500,000 | 0 | 0 |

Only guaranteed order lines with impressions goals are included in this calculation. In addition, since this metric is only available for products, only those order lines that are direct or contained to the product are included in the computation.

Formula: Scheduled impressions − Capacity

### Overlap type

This is the hierarchical relationship between products that determines how order lines overlap.

### Oversold

A measure of the amount of delivery available for a specific product, when displacement and indirect order line distribution is taken into consideration.

Oversold = total sold impressions - direct capacity

Total sold impressions = direct/contained contracted impressions + sum(indirect sold impressions \* cohesion, for all overlaps)

Cohesion Factor is a measure of the similarity of two products based on their physical overlap and the two capacities.

If there is no overlap, the cohesion is 0. If the products are identical, the cohesion is 1. All cohesion values are between 0 and 1. Randomly chosen product pairs typically have very tiny cohesion.

Indirect sold impressions:

For goal-based order lines: scheduled impressions

For non-goal-based order lines: base consumption

## P

### Pacing

A measure of the risk of an order line under delivering or over delivering. This metric includes both underdelivery and overdelivery, and should be used to measure both.

When dimensioning by product, only those order lines that are direct or contained to the product are included in the computation. This metric is calculated only for CPM order lines.

Formula: Consumed impressions – Scheduled impressions

### Pacing (lifetime)

This is the same as the Pacing metric. The exception is that this metric aggregates over the lifetime of the order line, and is not bound by the time period. When the lifetime metric is used, the time period filter is only used to filter to order lines delivering in the selected time period. This metric is only available for order line dimensions, and is calculated only for CPM order lines.

Formula: Consumed impressions (Lifetime) – Scheduled impressions (Lifetime)

### Package ID

The unique identifier of the package from the order management system or ad server.

### Parent product

The product that is at the top of a hierarchical product tree. The Parent Product can be applied as a filter to view products that are
children (i.e., entirely contained) within the specified product.

> [!NOTE]
> Parent Product is available only as a dimension filter and cannot be used as a primary analysis dimension.

### Pricing type

Pricing method for the order line such as CPM, CPD, or CPC.

### Priority

Priority of the order line in the ad server.

### Product

Products are a way to represent inventory within a structure that carries pricing and/or reporting metadata. Products are given targeting characteristics that define the ad server implementation of the Product in terms of what inventory it captures. A product's targeting characteristics can be changed using the Edit Product window, and the Product will maintain a continuous history across all previous versions of its targeting characteristics.

### Product external ID

The unique identifier of the product from the order management system or other externally managed product catalog.

### Product group

Collection or logical grouping of products.

> [!NOTE]
> Product Group is available only as a dimension filter and cannot be used as a primary analysis dimension.

### Product status

Indicates the state of a product. This is determined by the type of product and how the product was created.

### Product Yield Analytics ID

The unique identifier for the product in Yield Analytics.

## R

### Revenue against goal

A measure of the revenue that is at risk of underdelivering. This metric includes both underdelivery and overdelivery, and should be used to measure both. When dimensioning by product, only those order lines that are direct or contained to the product are included in the computation.

Formula: Earned revenue - Contracted revenue

### Revenue against goal (lifetime)

This is the same as the Revenue Against Goal metric. The exception is that this metric aggregates over the lifetime of all order lines, and is not bound by the time period. When the lifetime metric is used, the time period filter is only used to filter to order lines delivering in the selected time period. This metric is only available for order line dimensions for all pricing types.

### Revenue capacity (@ Rate card)

A measure of the potential revenue for a product, based on the impression capacity and rate card value.

Formula: Impression capacity / 1000 x Rate card value of the target

## S

### Sales team member

Name of all sales team members that are associated with a deal. When Sales Team Member is the dimension, all revenue and impression numbers are weighted based on the team members split percentage.

> [!NOTE]
> When the Salesperson dimension is used, all revenue is attributed to the primary salesperson.

### Scheduled clicks

The total clicks scheduled in the ad server for CPC order lines based on the date range specified in Yield Analytics. This metric is available for all order line and product dimensions.

### Scheduled clicks (lifetime)

The total clicks scheduled in the ad server for CPC order lines based on the entire lifetime of the order line. This metric is available only for order line dimensions.

### Scheduled impressions

The total impressions that have been scheduled in the ad server based on the order line's flighting policy. Order lines that do not have an impression goal (Example: sponsorships) will not have scheduled impressions.

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Scheduled impressions (lifetime)

This is the same as the Scheduled Impressions metric The exception is that this metric aggregates over the lifetime of all order lines, and is not bound by the time period. When the lifetime metric is used, the time period filter is only used to filter to order lines scheduled in the selected time period. This metric is only available for order line dimensions.

> [!NOTE]
> Proposed order lines are included in the calculations.
>
> When dimensioning by product, only direct and contained order lines are included in the calculation.

### Sell through

Sell-through rate: The percentage of available impressions that have been sold, based on the impressions consumed versus impression capacity.

Formula: Consumed impressions / Impression capacity

> [!NOTE]
> This is a dynamic calculation. The set of consuming order lines can be filtered, which will affect the utilization accordingly.

### Source system

Indicates the current source of the data. This is the system from which Yield Analytics is currently pulling the order data. This could be an ad server or any other system in the chain.

### SOV

Share of voice: This represents the percentage of inventory available to a particular product or order line.

## T

### Target

Unique order line targeting expression that is used by the system to provide forecasting, reporting and other functionality. Targets can be defined at any level of granularity (Example: site, section, sub-section, or even the most granular combination of behavioral/audience segments).

### Target attribute/targeting characteristics

Specific attribute that is contained within the targeting expression of a target (Example: size, site, DMA, etc.).

> [!NOTE]
> Target Attribute is available only as a dimension filter and cannot be used as a primary analysis dimension.

### Target expression

The combination of attribute/value pairs that uniquely describes the product.

### Third party

The name of the third party ad server used to measure the clicks and impressions for the campaign.

### Uniques (lifetime)

Projection of the total number of unique visitors that an order line will reach over its lifetime. This metric is only available when Order Line is the dimension.

Formula: Average Uniques (Daily) \* (1 + turnoverPerDay \* (daysLifetime -1))

### Utilization %

A measure of how well a product is being utilized (Example: sell-through) based on the impressions consumed versus impression capacity.

Formula: Consumed impressions / Impression capacity

> [!NOTE]
> This is a dynamic calculation. The set of consuming order lines can be filtered, which will affect the utilization accordingly.

### Viewability metrics

The following metrics are supported for clients for whom we maintain an integration with DFP Active View. They are all date-range specific, with collected data used to support historical reporting and for future projections.

- Consumed Measurable Impressions
  - This is the total number of measurable impressions.
  - This is a metric designed to:
    - Help users to diagnose viewability setup issues.
    - Support and validate the viewable rate calculation.
- Measurable Capacity
  - This metric is particularly useful for site redesign work and to explain why viewable impressions volume could be low.
- Measurable Rate
  - This metric is helpful when analyzing falloff; to compare changes between measurable and viewable rates.
  - Formula: (consumed measurable impressions/consumed eligible impressions) × 100
- Consumed Viewable Impressions
- vCPM
  - Formula: (Earned Revenue/Consumed Viewable Impressions) x 1000
- Viewable Capacity
- Viewable Multiplier
  - This metric makes it easier for users to determine how much inventory to schedule to reach a specific viewability goal, and how to adjust pricing accordingly.
    - It is exclusive to the Check Availability task interface.
  - Formula: total consumed impressions/viewable consumed impressions
- Viewable Rate
  - This is the percentage of viewable impressions out of all measurable impressions.
  - Formula: (consumed viewable impressions/consumed measurable impressions) x 100

## Y

### Yield % (@ Rate card)

A measure of how well a product is being monetized, based on the revenue earned versus revenue capacity.

Formula: Earned revenue / Revenue capacity (@Rate card)

> [!NOTE]
> This is a dynamic calculation. The set of consuming order lines can be filtered, which will affect the yield accordingly.
