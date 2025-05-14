---
title: Demand Issues
description: Learn how Demand Issues show the bid rejections caused by buyer behavior, like native creative does not match title, creative does not support required video protocol, the accept URL is too long and creative id was not found.    
ms.date: 10/14/2024
---

# Demand issues

**Demand Issues** show the bid rejections caused by buyer behavior. Some of the common examples include:

- native creative does not match title or data asset requirements
- creative does not support required video protocol
- the accept URL is too long
- creative id was not found

Drill down of this feature includes issue resolution help, timeseries chart, and creative preview.

## Navigation

In **Monetize Insight** dashboard, click on **Open Exchange** tab next to **Total Revenue** and **Deals** and then click **Demand Issues**.

## Filter

Clicking on **Filter** next to **Demand Issues**, opens a small window with the following fields:

| Filter | Description |
|--|--|
| Buyer | The Microsoft Advertising member seat that submitted the bid. |
| Demand Issue | Bid rejections caused by buyer behavior. |
| Media type | Native, Banner or Video creative. |
| Placement group | Is part of the inventory structure and can be used to group placements within a publisher. |
| Publisher | An object within our system to group inventory, normally by publication. |

Steps to make changes in the graph and the table that follows it:

- The filter has features specific to Demand Issues.
- Clicking on **Apply** updates the graph and the table that appears after that.
- The graph is configurable so you can choose what you want to plot on the graph, whether it is blocked bid opportunity, Error count or Avg CPM.
- You can group the data on the basis of Publisher, Buyer, Issue, Media type or Placement group.
- You can also select how you want the graph to be displayed whether as a Bar chart or a time series Area chart.
- Hovering on the chart will give you information on the chart at that position.
- The chart helps you quickly examine issues in aggregate to decide where to focus.

## Overview

There are three dropdowns under **Overview**. The selection of fields in these dropdowns will decide how the chart will appear below.

| Dropdown | Description |
|--|--|
| Compare relative scale and observe trends | View as a bar chart to compare how the metrics compare between the grouping you have selected. You can also view as Area chart to see how the groupings changed over time. It specifies if there are spikes or consistent behaviour. |
| How you want the data grouped | Focuses on how you want the data to be grouped. Grouping can be done on the basis of the Publisher, Buyer, Issue, Media type or Placement group. |
| Which metric is of interest | To get the metric of interest, choose between Blocked bid opportunity, Error count and Avg CPM. |

## Demand issues

**Demand Issues** table show the issues with the biggest impacting blocks and how much this is changing week over week. The table below list the columns that appear in the table.

| Field | Description |
|--|--|
| % Δ Blocked Bid Opportunity | The percentage change in the total value of blocked bids over the selected time range. |
| Avg CPM | The average [CPM](../industry-reference/online-advertising-and-ad-tech-glossary.md#cpm) of the bid rejections. |
| Blocked Bid Opportunity | The total value of blocked bids within the selected time range. |
| Buyer | The Microsoft Advertising member seat that submitted the bid. |
| Error Count | The total number of bid rejections resulting from Ad Quality Rules. |
| Issue | Issues for a buyer on specific publishers. |
| Publisher | An object within our system to group inventory, normally by publication. |
| Δ Blocked Bid Opportunity | The change in the total value of blocked bids over the selected time range. |

> [!NOTE]
> Click on any row to zoom into more contextual details on the block.

## Issue resolution summary

On clicking anywhere in **Demand Issues** Table, it will take you to a screen. This is the screen which shows the context on how the issue could be resolved.

## History chart

Below the **Issue Resolution Summary** is the **History Chart**. Here you can see the Blocked Bid Opportunity, Error Count and [CPM](../industry-reference/online-advertising-and-ad-tech-glossary.md#cpm).

## Creative preview

Here you can see 5 sample creatives for easy ability to preview.
