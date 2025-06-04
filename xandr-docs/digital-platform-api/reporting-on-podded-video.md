---
title: Digital Platform API - Reporting on Podded Video
description: Explore the Pod Analytics report, which offers metrics for groups of ads delivered sequentially between segments of non-commercial video content.
ms.date: 06/04/2025
ms.custom: digital-platform-api
---

# Digital Platform API - Reporting on Podded video

> [!NOTE]
> This feature is currently in **Alpha**. It is still under development and may be subjected to changes without notice. Contact your Xandr Account Representative to get it enabled.

## Overview

The Pod analytics report provides metrics for groups of ads delivered sequentially in between segments of non-commercial video content. Podded video reporting has a fundamentally different way of optimising for yield due to the dimension of duration and the total number of ads (slots), as compared to display inventory where the reporting is optimised on variables such as price and fill rate.

## Reporting types

There are two reports that provide insight into how your podded video supply is performing on Xandr:

- Seller Slot Analytics Report
- Seller Pod Analytics Report

## Seller Pod Analytics

| Report Name | Description | Example Use Cases |
|:---|:---|:---|
| Seller Pod Analytics Report | This report provides an understanding on the effectiveness and monetization of your supply based on a particular ad break. You can report on the number of pods sent to xandr and the number of pods with at least 1 impression sold, so that you can analyze performance. This report enables reporting on the average number of impressions or revenue per pod to inform decisions on how to structure your inventory for optimal yield. All dimensions included in this report remain consistent across the entire ad break. | For a publisher, region or genre:<br>- Average pod fill rate in seconds per publisher.<br>- Average impression seconds sold per pod.<br>- Average impressions sold per pod.<br>- Average revenue per pod. |

## Seller Slot Analytics

| Report Name | Description | Example Use Cases |
|:---|:---|:---|
| Seller Slot Analytics Report | This report helps understanding delivery within your podded inventory, how individual slots within the pod are performing and how they are being sold across managed, deal and RTB channels. You can access metrics by the position of the slots and also differentiate bumpers from regular slots. The dimensions accessible inside this report are particular to the slot view such as purchaser, brand and creative length. | For a buyer, brand or line item:<br>- Impressions sold by pre, mid or post-roll.<br>- Average CPM by slot position.<br>- Average impression seconds sold by slot position. <br>- Which slot position(s) delivered impressions.<br>- How many impression seconds delivered in each slot. |

## Related topics

- [Seller Slot Analytics Service](seller-slot-analytics-report.md)
- [Seller Slot Analytics Report](../monetize/seller-slot-analytics-report.md)
