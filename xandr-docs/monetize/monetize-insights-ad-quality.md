---
title: Ad Quality
description: In this page, learn what is an Ad Quality and how it gets configured when the client joins our platform.
ms.date: 10/14/2024
---

# Ad quality

**Ad Quality** shows revenue-impacting blocks to help identify and evaluate opportunities to adjust ad quality settings. They are settings that the publisher has for brand safety. It gets configured when the client joins our platform and then may not be re-evaluated frequently. In the **Ad Quality** tab:

- **Creative Preview** lives directly in the side panel for quick review.
- there are direct links to rule management settings.

> [!NOTE]
> As an organization, we recommend you to regularly view your Ad Quality settings (at least quarterly) to make sure that are appropriate and consistent with settings configured in the other SSPs (that you may also be using to monetize inventory). Generally, the blocked bid opportunity overestimates potential revenue impact and is influenced by the price and frequency of the bids that have been blocked.
>
> If an Ad Quality (AQ) is set as `default_brand_status:banned` but the parent brand is set as `status:trusted`, the child brand overrides the setting in `default_brand_status` and it will be able to serve unless it is explicitly banned in the Ad Profile's brand override list.

## Ad quality summary

The value mentioned on **Ad Quality** tab is the blocked bid opportunity. A $5.8M of blocked bid opportunity in last 7 days, up 11% compared to prior week does not provide a direct revenue number but can be used directionally to assess opportunities.

## Filter

Clicking on **Filter** next to **Ad Quality** will display a small window with following fields:

| Filter | Definition |
|--|--|
| Ad profile | Is the object that contains the targeting for the ad quality rule. |
| Ad quality rule | Is the configuration for demand blocks, for example to enforce brand safety. |
| Bid rejection type | The classification of the bid rejection. Possible values are Brand, Category, Tech, and Language. |
| Media type | Native, Banner or Video creative. |
| Name | The specific name of the block. For example, brand name, category name or technical attribute name that has been blocked. |
| Placement Group | Is part of the inventory structure and can be used to group placements within a publisher. |
| Publisher | An object within our system to group inventory, normally by publication. |

Steps to make changes in the graph and the table that follows it:

1. The filter has features specific to Ad Quality.
1. Clicking on **Apply** updates the graph and the table that appears after that.
1. The graph is configurable so you can choose what you want to plot on the graph, whether it is Blocked Bid Opportunity, Error Count or Avg CPM.
1. You can group the data on the basis of Publisher, Ad Quality Rule, Rejection Type, Bid Rejection, Media Type or Placement Group.
1. You can also select how you want the graph to be displayed whether as a Bar chart or a time series Area chart.
1. Hovering on the chart will give you information on the chart at that position.

## Quickly get a sense of relative impact and trends

The chart helps you to quickly examine issues in aggregate to decide where to focus.

## Overview

There are three dropdowns which decide how your chart appears depending on your selection:

| Field | Description |
|--|--|
| Compare relative scale and observe trends | View as a bar chart to compare how the metrics compare between the grouping you have selected. You can also view as an area chart to see how the groupings changed over time. It specifies if there are spikes or consistent behaviour. |
| How you want the data grouped | Focuses on how you want the data to be grouped. Grouping can be done on the basis of Publisher, Ad quality rule, Rejection type, Bid rejection, Media type or Placement group. |
| Which metric is of interest | To get the metric of interest, choose between Blocked bid opportunity, Error count and Avg CPM. |

## Bid rejections table

The table contains rejections that are grouped according to different publishers. Below are the different columns that appear on the table:

| Field | Description |
|--|--|
| % Δ Blocked Bid Opportunity | The percentage change of the blocked bid opportunity week over week. Sort by this value to see the biggest relative changes between time periods. |
| Ad Quality Rule | What type of creative is it, and where is it being blocked within your inventory. |
| Avg CPM | The average bid price of the rejections. |
| Bid Rejection Name | This is the specific block reason. For example, if brand Fizzy Drinks is blocked due to its brand, the name of the brand will show here. |
| Bid Rejection Type | The general reason for the block, such as Technical Attribute, Category or Brand. |
| Blocked Bid Opportunity | The sum of all bid prices. Directional to gauge potential impact. Incremental bid value to existing revenue and multiple bids not accounted for. |
| Error Count | The total number of bid rejections resulting from Ad Quality Rules. |
| Media Type | Native, Banner or Video creative. |
| Publisher | An object within our system to group inventory, normally by publication. |
| Δ Blocked Bid Opportunity | The change in dollars of the Blocked Bid Opportunity in the last 7 days compared to 7 days prior to it. Sort by this value to see the biggest changes between time periods. |

> [!NOTE]
> Click on any row to zoom into more contextual details on the block.

## Creative preview

You can view 5 example creatives observing this block. On expanding **Show creative** metadata, you can get the actual id of that creative, Media Type, Audit Status, Brand ID and Brand.

## Ad quality rule info

This is where the block appears. You can quickly review the ad quality rule and profile information.

> [!NOTE]
> Edit the Ad Quality Rule Info (pencil icon) is not clickable and is currently under development.

## History chart

The chart shows how the rejection has developed over time. For example, is it a one-off spike or sustained block which could be more indicative of an opportunity.

## Buyers

Refers who are the buyers most affected by this block. Also speaks if there is an opportunity to create a deal with them that permits this category.
