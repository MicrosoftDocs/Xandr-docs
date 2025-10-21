---
title: Deals
description: This page provides an overview on Deals in Monetize and FAQs on Bid Rejections in UI dashboard.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Deals

In **Monetize Insights, Deals** tab specifies the most significant bid rejections by a deal. The **Deals** tab:

- sorts by total bid value, absolute and percentage changes.
- shows the inventory the blocks are occurring on, and the overall rejection history.

## Bid rejections in UI dashboard

**What is it?**

Dedicated UI dashboard giving you the access to bid rejection revenue impact data across Ad Quality, Floors, Deals, and Demand Issues categories.

**How does it help customers?**

You can now easily identify and visualize top impacting bid rejection reasons and access supplementary data to evaluate the opportunity for settings adjustments.

**Is it differentiated in market? How is it so?**

Guided flows remove the need to configure reporting dashboards like in Index, OpenX and Yahoo SSP. You do not need to pull reports to access quick, high-level information about their inventory any more.

## Filter

Clicking on **Filter** next to **Bid Rejections** will open a window with the following fields:

| Filter | Description |
|--|--|
| Bid rejection type | The classification of the bid rejection. Possible values are Brand, Category, Tech, and Language. |
| Bidder | Also known as DSP. It is the demand partner platform submitting the bid. |
| Buyer | The Microsoft Advertising member seat that submitted the bid. |
| Deal | The most significant bid rejections by deal. |
| Media type | Native, Banner or Video creative. |
| Name | The specific name of the block. For example, brand name, category name or technical attribute name that has been blocked. |
| Placement group | Is part of the inventory structure and can be used to group placements within a publisher. |
| Publisher | An object within our system to group inventory, normally by publication. |

Steps to make changes in the graph and the table that follows it:

1. The filter has features specific to Bid Rejections.
1. Clicking on **Apply** updates the graph and the table that appears after that.
1. The graph is configurable so you can choose what you want to plot on the graph, whether it is blocked bid opportunity, Error count or Avg CPM.
1. You can group the data on the basis of Publisher, Media Type, Placement group, Buyer, Bid Rejection or Bidder.
1. You can also select how you want the chart to be displayed whether as a Bar chart or a time series Area chart.
1. Hovering on the chart will give you information on the chart at that position.
1. The chart helps you quickly examine issues in aggregate to decide where to focus.

## Overview

Under **Overview** there are three dropdowns. Selection of fields in these dropdowns will decide the appearance of the chart.

| Dropdown | Description |
|--|--|
| Compare relative scale and observe trends | View as Bar chart to compare how the metrics compare between the grouping you have selected. You can also view as Area chart to see how the groupings changed over time. It specifies if there are spikes or consistent behaviour. |
| How you want the data grouped | Focusing on how you want the data to be grouped. Grouping can be done on the basis of the Publisher, Media type, Placement group, Buyer, Bid rejection or Bidder. |
| Which metric is of interest | To get the metric of interest, choose between Blocked bid opportunity, Error count and Avg CPM. |

## Bid rejections

**Bid Rejections** shows the issues with the biggest impacting blocks and how much this is changing week over week. The Bid Rejections table have the columns listed in the table below.

| Field | Description |
|--|--|
| **% Δ Blocked Bid Opportunity** | The percent change in the total value of blocked bids over the selected time range. |
| **Avg CPM** | The average [CPM](../industry-reference/online-advertising-and-ad-tech-glossary.md#cpm) of the bid rejections. |
| **Bidder** | Also known as the DSP, it is the demand partner platform submitting the bid. Buyers are associated with one bidder at a time. |
| **Blocked Bid Opportunity** | The total value of blocked bids within the selected time range. |
| **Buyer** | The Microsoft Advertising member seat that submitted the bid. |
| **Deal** | This is the negotiated deal between the seller and the buyer. |
| **Error Count** | The total number of bid rejections resulting from Ad Quality Rules. |
| **Name** | The specific name of the block. For example, brand name, category name or technical attribute name that has been blocked. |
| **Type** | The classification of the bid rejection. Possible values are Brand, Category, Tech, and Language |
| **Δ Blocked Bid Opportunity** | The change in the total value of blocked bids over the selected time range. |

> [!NOTE]
> Click on any row to zoom into more contextual details on the block.

## Issue resolution summary

This is the context on how the issue could be resolved.

## Creative preview

This shows 5 sample creatives for easy ability to preview.

## History chart

Using History chart you can see the trends for Blocked Bid Opportunity, Error Count and CPM.
